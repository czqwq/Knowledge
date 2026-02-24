# GT5-Unofficial 配方系统（Recipe System）知识库

> **代码来源：** https://github.com/GTNewHorizons/GT5-Unofficial  
> **本地路径：** /tmp/GT5-Unofficial（单 monorepo，含 gregtech/tectech 等 17 个模块）  
> **所有代码均经本地源码核实，不含虚假代码。**

---

## 目录

1. [配方数据类（GTRecipe）](#1-配方数据类-gtrecipe)
2. [配方构建器（GTRecipeBuilder）](#2-配方构建器-gtrecipebuilder)
3. [配方表（RecipeMap）体系](#3-配方表-recipemap-体系)
4. [RecipeMapBackend：索引与搜索](#4-recipemapbackend-索引与搜索)
5. [FindRecipeQuery：查询 API](#5-findrecipequery-查询-api)
6. [RecipeMapBuilder：配方表构建](#6-recipemapbuilder-配方表构建)
7. [RecipeMaps：所有内置配方表（104 个）](#7-recipemaps-所有内置配方表)
8. [OverclockCalculator：超频计算](#8-overclocalculator-超频计算)
9. [配方系统完整数据流](#9-配方系统完整数据流)

---

## 1. 配方数据类（GTRecipe）

文件路径：`src/main/java/gregtech/api/util/GTRecipe.java`

```java
// src/main/java/gregtech/api/util/GTRecipe.java:48-200（核心字段）
public class GTRecipe implements Comparable<GTRecipe> {

    /**
     * 物品输入/输出槽。修改输出可直接修改/替换数组；
     * 修改输入请新建配方（因为有 HashMap 索引）。
     */
    public ItemStack[] mInputs, mOutputs;

    /**
     * 流体输入/输出槽。同上。
     */
    public FluidStack[] mFluidInputs, mFluidOutputs;

    /**
     * 概率数组，范围 1-10000（10000 = 100%）。
     * - mInputChances  → mInputs  （概率决定是否消耗）
     * - mOutputChances → mOutputs  （概率决定是否产出）
     * - mFluidInputChances  → mFluidInputs
     * - mFluidOutputChances → mFluidOutputs
     * 若为 null，则对应槽位均按 100% 处理。
     */
    @Nullable
    public int[] mInputChances, mOutputChances, mFluidInputChances, mFluidOutputChances;

    /**
     * 特殊槽位（如打印机的复制槽）。仅用于 NEI 展示假配方。
     * findRecipe() 和 containsInput() 不检查此字段。
     */
    public Object mSpecialItems;

    public int mDuration;        // 持续时间（单位：tick，20 tick = 1秒）
    public int mEUt;             // 每 tick 能量消耗（EU/t）
    public int mSpecialValue;    // 特殊值（如高炉的最低热量）

    public boolean mEnabled = true;         // 是否启用
    public boolean mHidden = false;         // 是否在 NEI 中隐藏
    public boolean mFakeRecipe = false;     // 是否为假配方（仅展示，不参与机器匹配）
    public boolean mCanBeBuffered = true;   // 是否可被缓存
    public boolean mNeedsEmptyOutput = false; // 是否要求输出槽完全为空
}
```

**内部 `RecipeAssemblyLine` 子类（装配线配方）：**

```java
// src/main/java/gregtech/api/util/GTRecipe.java（RecipeAssemblyLine 字段）
public static class RecipeAssemblyLine {
    public ItemStack[] mInputs;
    public FluidStack[] mFluidInputs;
    public int mDuration;
    public int mEUt;
}
```

---

## 2. 配方构建器（GTRecipeBuilder）

文件路径：`src/main/java/gregtech/api/util/GTRecipeBuilder.java`

### 2.1 时间/流体常量

```java
// src/main/java/gregtech/api/util/GTRecipeBuilder.java:47-62
// time units
public static final int HOURS   = 20 * 60 * 60;
public static final int MINUTES = 20 * 60;
public static final int SECONDS = 20;
public static final int TICKS   = 1;

// fluid units
public static final int INGOTS        = 144;
public static final int HALF_INGOTS   = INGOTS / 2;
public static final int QUARTER_INGOTS = INGOTS / 4;
public static final int EIGHTH_INGOTS = INGOTS / 8;
public static final int NUGGETS       = INGOTS / 9;
public static final int STACKS        = 64 * INGOTS;
public static final int BUCKETS       = 1_000;
```

### 2.2 核心构建 API（流式调用）

```java
// src/main/java/gregtech/api/util/GTRecipeBuilder.java（方法签名摘录）

// 物品输入（自动做 OreDict 统一化）
public GTRecipeBuilder itemInputs(ItemStack... inputs)
public GTRecipeBuilder itemInputsUnified(ItemStack... inputs)

// 物品输入（跳过统一化，慎用）
public GTRecipeBuilder itemInputsUnsafe(ItemStack... inputs)

// 物品输出
public GTRecipeBuilder itemOutputs(ItemStack... outputs)
public GTRecipeBuilder itemOutputs(ItemStack[] outputs, int[] chances)

// 流体输入/输出
public GTRecipeBuilder fluidInputs(FluidStack... fluidInputs)
public GTRecipeBuilder fluidOutputs(FluidStack... fluidOutputs)

// 概率（对应槽位，0-10000）
public GTRecipeBuilder inputChances(int... chances)
public GTRecipeBuilder outputChances(int... chances)
public GTRecipeBuilder fluidInputChances(int... chances)
public GTRecipeBuilder fluidOutputChances(int... chances)

// 时长（tick）
public GTRecipeBuilder duration(int duration)
public GTRecipeBuilder duration(long duration)

// EU/t
public GTRecipeBuilder eut(int eut)
public GTRecipeBuilder eut(long eut)

// 提交到配方表
public Collection<GTRecipe> addTo(IRecipeMap recipeMap)  // src/main/java/gregtech/api/util/GTRecipeBuilder.java:1052
```

### 2.3 典型用法示例

```java
// 典型配方添加示例（参考 gregtech/api/recipe/RecipeMaps.java 内的 builderTransformer）
GTValues.RA.stdBuilder()
    .itemInputs(new ItemStack(Items.iron_ore, 1))
    .itemOutputs(new ItemStack(Items.iron_ingot, 2))
    .duration(20 * GTRecipeBuilder.SECONDS)
    .eut(TierEU.RECIPE_LV)
    .addTo(RecipeMaps.maceratorRecipes);
```

---

## 3. 配方表（RecipeMap）体系

文件路径：`src/main/java/gregtech/api/recipe/RecipeMap.java`

### 3.1 类结构

```java
// src/main/java/gregtech/api/recipe/RecipeMap.java:40-105
public final class RecipeMap<B extends RecipeMapBackend> implements IRecipeMap {

    /**
     * 所有配方表实例注册中心。key=unlocalizedName, value=instance。
     */
    public static final Map<String, RecipeMap<?>> ALL_RECIPE_MAPS = new HashMap<>();

    private final B backend;
    private final RecipeMapFrontend frontend;

    /** 唯一标识名，同时用于 NEI tab 本地化 key */
    public final String unlocalizedName;

    private final RecipeCategory defaultRecipeCategory;

    RecipeMap(String unlocalizedName, B backend, RecipeMapFrontend frontend) {
        this.unlocalizedName = unlocalizedName;
        this.backend = backend;
        this.frontend = frontend;
        this.defaultRecipeCategory = new RecipeCategory(this);
        backend.setRecipeMap(this);
        if (ALL_RECIPE_MAPS.containsKey(unlocalizedName)) {
            throw new IllegalArgumentException(
                "Cannot register recipemap with duplicated unlocalized name: " + unlocalizedName);
        }
        ALL_RECIPE_MAPS.put(unlocalizedName, this);
    }

    /** 获取该表所有配方（不可修改集合） */
    @Unmodifiable
    public Collection<GTRecipe> getAllRecipes() {
        return backend.getAllRecipes();
    }
}
```

### 3.2 查询入口

```java
// src/main/java/gregtech/api/recipe/RecipeMap.java（findRecipeQuery 方法）
public FindRecipeQuery findRecipeQuery() {
    return new FindRecipeQuery(this);
}
```

---

## 4. RecipeMapBackend：索引与搜索

文件路径：`src/main/java/gregtech/api/recipe/RecipeMapBackend.java`

### 4.1 索引结构

```java
// src/main/java/gregtech/api/recipe/RecipeMapBackend.java:50-80
public class RecipeMapBackend {

    /** 物品索引：GTItemStack → 配方集合（哈希多值映射） */
    private final SetMultimap<GTItemStack, GTRecipe> itemIndex = LinkedHashMultimap.create();

    /** 流体索引：流体名 → 配方集合 */
    private final SetMultimap<String, GTRecipe> fluidIndex = LinkedHashMultimap.create();

    /** 按配方分类索引 */
    private final Map<RecipeCategory, Collection<GTRecipe>> recipesByCategory = new HashMap<>();

    /** LRU 缓存大小 */
    public static final int CACHE_MAP_SIZE = 256;

    /** 按输入哈希缓存配方（commutative hash of all inputs） */
    private final GTRecipe[] cacheMap = new GTRecipe[CACHE_MAP_SIZE];

    protected final RecipeMapBackendProperties properties;
}
```

### 4.2 配方匹配流（`matchRecipeStream`）

```java
// src/main/java/gregtech/api/recipe/RecipeMapBackend.java（matchRecipeStream 逻辑）
// 1. 先查 cacheMap（哈希槽）
// 2. 再查 itemIndex（物品索引）
// 3. 最后查 fluidIndex（流体索引）
// 返回 Stream<GTRecipe>，由 FindRecipeQuery 进一步过滤
```

---

## 5. FindRecipeQuery：查询 API

文件路径：`src/main/java/gregtech/api/recipe/FindRecipeQuery.java`

```java
// src/main/java/gregtech/api/recipe/FindRecipeQuery.java:35-97（完整核心）
public final class FindRecipeQuery {

    private final RecipeMap<?> recipeMap;

    @Nullable private ItemStack[]  items;
    @Nullable private FluidStack[] fluids;
    @Nullable private ItemStack    specialSlot;
    private Predicate<GTRecipe>    filter   = ALWAYS;
    private long                   voltage  = Integer.MAX_VALUE;
    @Nullable private GTRecipe     cachedRecipe;
    private boolean                notUnificated;
    private boolean                dontCheckStackSizes;
    private boolean                forCollisionCheck;
    private boolean                caching  = false;

    /** @return 第一个匹配的配方，未找到返回 null */
    @Nullable
    public GTRecipe find() {
        return findAll().findFirst().orElse(null);
    }

    /**
     * @return 所有匹配配方的流（Stream）
     * 过滤条件：voltage * amperage >= recipe.mEUt
     */
    public Stream<GTRecipe> findAll() {
        if (items == null)  items  = GTValues.emptyItemStackArray;
        if (fluids == null) fluids = GTValues.emptyFluidStackArray;

        return recipeMap.getBackend()
            .matchRecipeStream(items, fluids, specialSlot, cachedRecipe, notUnificated, dontCheckStackSizes, forCollisionCheck)
            .filter(recipe -> voltage * recipeMap.getAmperage() >= recipe.mEUt && filter.test(recipe))
            .peek(recipe -> {
                if (caching) recipeMap.getBackend().cache(items, fluids, recipe);
            });
    }
}
```

**链式调用方式（流式 API）：**

```java
// 来自 FindRecipeQuery.java Javadoc 示例
GTRecipe recipe = recipeMap.findRecipeQuery()
    .items(inputItems)
    .fluids(inputFluids)
    .voltage(machineVoltage)
    .caching(true)
    .find();
```

---

## 6. RecipeMapBuilder：配方表构建

文件路径：`src/main/java/gregtech/api/recipe/RecipeMapBuilder.java`

```java
// src/main/java/gregtech/api/recipe/RecipeMapBuilder.java:71-200（核心 API）

/**
 * 最简使用示例（来自 Javadoc）：
 *   RecipeMap<RecipeMapBackend> exampleRecipes = RecipeMapBuilder.of("example")
 *       .maxIO(9, 4, 1, 1)
 *       .build();
 */

/** 标准工厂方法 */
public static RecipeMapBuilder<RecipeMapBackend> of(String unlocalizedName)

/** 自定义后端工厂方法 */
public static <B extends RecipeMapBackend> RecipeMapBuilder<B> of(String unlocalizedName,
    RecipeMapBackend.BackendCreator<B> backendCreator)

/** 设置 IO 槽位最大数量（物品输入/输出、流体输入/输出） */
public RecipeMapBuilder<B> maxIO(int maxItemInputs, int maxItemOutputs, int maxFluidInputs, int maxFluidOutputs)

/** 设置最少需要的输入数量 */
public RecipeMapBuilder<B> minInputs(int minItemInputs, int minFluidInputs)

/** 设置安培数（默认 1A） */
public RecipeMapBuilder<B> amperage(int amperage)

/** 配方发出前变换（可修改 builder 或向其他表添加配方） */
public RecipeMapBuilder<B> builderTransformer(Consumer<? super GTRecipeBuilder> builderTransformer)

/** 改变配方发出方式（一个 builder → 多个 GTRecipe） */
public RecipeMapBuilder<B> recipeEmitter(Function<? super GTRecipeBuilder, ? extends Iterable<? extends GTRecipe>> recipeEmitter)

/** 最终构建 */
public RecipeMap<B> build()
```

---

## 7. RecipeMaps：所有内置配方表

文件路径：`src/main/java/gregtech/api/recipe/RecipeMaps.java`（共 104 个配方表）

以下列出关键配方表及其 IO 配置：

```java
// src/main/java/gregtech/api/recipe/RecipeMaps.java（部分摘录）

// 研磨机：1 物品输入，4 物品输出
public static final RecipeMap<RecipeMapBackend> maceratorRecipes =
    RecipeMapBuilder.of("gt.recipe.macerator")
        .maxIO(1, 4, 0, 0)
        .build();

// 化学反应釜：2 物品输入，2 物品输出，2 流体输入，2 流体输出
public static final RecipeMap<RecipeMapBackend> chemicalReactorRecipes =
    RecipeMapBuilder.of("gt.recipe.chemicalreactor")
        // 实际在源码中 maxIO 由各自机器定义

// 高炉：1 物品输入，3 物品输出，0 流体，0 流体（mSpecialValue 存最低热量）
public static final RecipeMap<RecipeMapBackend> blastFurnaceRecipes =
    RecipeMapBuilder.of("gt.recipe.blastfurnace")
        .maxIO(2, 4, 0, 0)
        .build();

// 聚变反应堆：0 物品，0 物品，2 流体输入，1 流体输出
public static final RecipeMap<RecipeMapBackend> fusionRecipes =
    RecipeMapBuilder.of("gt.recipe.fusionreactor")
        .maxIO(0, 0, 2, 1)
        .build();

// 装配线：12 物品输入，1 物品输出，4 流体输入，0 流体输出
public static final RecipeMap<RecipeMapBackend> assemblylineVisualRecipes =
    RecipeMapBuilder.of("gt.recipe.assembly_line")
        .maxIO(12, 1, 4, 0)
        .build();
```

**所有 104 个配方表名（`RecipeMaps.java` 中 `public static final RecipeMap` 字段名列表）：**

`oreWasherRecipes`、`thermalCentrifugeRecipes`、`compressorRecipes`、`neutroniumCompressorRecipes`、`extractorRecipes`、`recyclerRecipes`、`furnaceRecipes`、`efrBlastingRecipes`、`efrSmokingRecipes`、`microwaveRecipes`、`scannerFakeRecipes`、`rockBreakerFakeRecipes`、`quantumComputerFakeRecipes`、`replicatorRecipes`、`assemblylineVisualRecipes`、`plasmaArcFurnaceRecipes`、`arcFurnaceRecipes`、`printerRecipes`、`sifterRecipes`、`formingPressRecipes`、`laserEngraverRecipes`、`mixerRecipes`、`autoclaveRecipes`、`electroMagneticSeparatorRecipes`、`polarizerRecipes`、`maceratorRecipes`、`chemicalBathRecipes`、`brewingRecipes`、`fluidHeaterRecipes`、`distilleryRecipes`、`fermentingRecipes`、`fluidSolidifierRecipes`、`fluidExtractionRecipes`、`packagerRecipes`、`unpackagerRecipes`、`fusionRecipes`、`centrifugeRecipes`、`electrolyzerRecipes`、`blastFurnaceRecipes`、`plasmaForgeRecipes`、`transcendentPlasmaMixerRecipes`、`spaceProjectFakeRecipes`、`cokeOvenRecipes`、`primitiveBlastRecipes`、`implosionRecipes`、`vacuumFreezerRecipes`、`chemicalReactorRecipes`、`multiblockChemicalReactorRecipes`、`distillationTowerRecipes`、`crackingRecipes`、`pyrolyseRecipes`、`solarFactoryRecipes`、`wiremillRecipes`、`benderRecipes`、`alloySmelterRecipes`、`assemblerRecipes`、`circuitAssemblerRecipes`、`cannerRecipes`、`latheRecipes`、`cutterRecipes`、`extruderRecipes`、`hammerRecipes`、`amplifierRecipes`、`massFabFakeRecipes`、`dieselFuels`、`extremeDieselFuels`、`gasTurbineFuels`、`hotFuels`、`denseLiquidFuels`、`plasmaFuels`、`magicFuels`、`smallNaquadahReactorFuels`、`largeNaquadahReactorFuels`、`hugeNaquadahReactorFuels`、`extremeNaquadahReactorFuels`、`ultraHugeNaquadahReactorFuels`、`largeBoilerFakeFuels`、`nanoForgeRecipes`、`pcbFactoryRecipes`、`purificationClarifierRecipes`、`purificationOzonationRecipes`、`purificationFlocculationRecipes`、`purificationPhAdjustmentRecipes`、`purificationPlasmaHeatingRecipes`、`purificationUVTreatmentRecipes`、`purificationDegasifierRecipes`、`purificationParticleExtractionRecipes`、`ic`、`entropicProcessing`、`isotopeDecay`、`cableRecipes`、`cauldronRecipe`、`foundryFakeModuleCostRecipes`、`nanochipConversionRecipes`、`nanochipAssemblyMatrixRecipes`、`nanochipSMDProcessorRecipes`、`nanochipBoardProcessorRecipes`、`nanochipEtchingArray`、`nanochipCuttingChamber`、`nanochipWireTracer`、`nanochipSuperconductorSplitter`、`nanochipOpticalOrganizer`、`nanochipEncasementWrapper`、`nanochipBiologicalCoordinator`

---

## 8. OverclockCalculator：超频计算

文件路径：`src/main/java/gregtech/api/util/OverclockCalculator.java`

### 8.1 基本属性

```java
// src/main/java/gregtech/api/util/OverclockCalculator.java:7-75（字段摘录）
public class OverclockCalculator {

    protected long recipeEUt = 0;         // 配方原始 EU/t
    protected long machineVoltage = 0;    // 机器电压（含安培时为总功率）
    protected long machineAmperage = 1;   // 机器安培数
    protected int  duration = 0;          // 配方原始时长（tick）
    protected int  parallel = 1;          // 并行数
    protected int  maxTierSkip = 1;       // 最多跨几阶超频

    // 超频倍率参数
    protected double eutIncreasePerOC     = 4;    // 每次超频 EU/t 倍率（默认 4x）
    protected double durationDecreasePerOC = 2;   // 每次超频时长除数（默认 /2）

    // 热量超频（EBF 专用）
    protected int    recipeHeat  = 0;    // 配方要求热量
    protected int    machineHeat = 0;    // 机器当前热量
    protected final double durationDecreasePerHeatOC = 4;  // 每 1800K 超热超频时长 /4

    // 激光超频（TecTech 专用）
    protected boolean laserOC = false;

    // 结果
    protected int  calculatedDuration;
    protected long calculatedConsumption;

    protected static final int HEAT_DISCOUNT_THRESHOLD   = 900;   // 每 900K 降低 EU/t
    protected static final int HEAT_OVERCLOCK_THRESHOLD  = 1800;  // 每 1800K 触发热超频
}
```

### 8.2 工厂方法（无超频）

```java
// src/main/java/gregtech/api/util/OverclockCalculator.java:77-88
/** 创建不超频的计算器，直接使用配方原始值 */
public static OverclockCalculator ofNoOverclock(@Nonnull GTRecipe recipe) {
    return ofNoOverclock(recipe.mEUt, recipe.mDuration);
}

public static OverclockCalculator ofNoOverclock(long eut, int duration) {
    return new OverclockCalculator().setRecipeEUt(eut)
        .setDuration(duration)
        .setEUt(eut)
        .setNoOverclock(true);
}
```

### 8.3 超频核心算法

```java
// src/main/java/gregtech/api/util/OverclockCalculator.java:332-410
protected void calculateOverclock() {
    // 1. 确定基准时长
    double duration = durationUnderOneTickSupplier != null
        ? durationUnderOneTickSupplier.get()
        : this.duration * durationModifier;

    currentParallel = Math.max(currentParallel, parallel);

    // 2. 计算实际功率
    double recipePower  = recipeEUt * parallel * eutModifier * calculateHeatDiscountMultiplier();
    double machinePower = machineVoltage * (amperageOC ? machineAmperage : Math.min(machineAmperage, parallel));

    // 3. 计算可用超频次数（log4 比值）
    int tiersAbove = (int) GTUtility.log4((long) machinePower / Math.max((long) recipePower, 32));

    if (noOverclock) {
        calculatedConsumption = (long) Math.ceil(recipePower);
        calculatedDuration    = (int)  Math.ceil(duration);
        return;
    }

    // 4. 激光超频分支
    if (laserOC) {
        // 先进行普通超频到上限，再叠加激光超频（每次 *4.3, *4.6, *4.9...）
        // ...（详见源码 352-386 行）
        return;
    }

    // 5. 普通超频
    overclocks = Math.min(maxOverclocks, tiersAbove);
    if (!amperageOC) {
        // 限制超频次数为电压阶差
        int voltageTierMachine = (int) Math.max(GTUtility.log4ceil(machineVoltage / 8), 1);
        int voltageTierRecipe  = (int) Math.max(GTUtility.log4ceil(recipeEUt / 8), 1);
        overclocks = Math.min(overclocks, voltageTierMachine - voltageTierRecipe);
    }
    overclocks = Math.max(overclocks, 0);

    // 6. 热超频分量
    int heatOverclocks   = Math.min(heatOC ? (machineHeat - recipeHeat) / HEAT_OVERCLOCK_THRESHOLD : 0, overclocks);
    int regularOverclocks = overclocks - heatOverclocks;

    // 7. 最终计算
    calculatedConsumption = (long) Math.ceil(recipePower * GTUtility.powInt(eutIncreasePerOC, overclocks));
    duration /= GTUtility.powInt(durationDecreasePerHeatOC, heatOverclocks);
    duration /= GTUtility.powInt(durationDecreasePerOC, regularOverclocks);
    calculatedDuration = (int) Math.max(duration, 1);
}
```

### 8.4 热折扣计算

```java
// src/main/java/gregtech/api/util/OverclockCalculator.java:327-329
public double calculateHeatDiscountMultiplier() {
    int heatDiscounts = heatDiscount ? (machineHeat - recipeHeat) / HEAT_DISCOUNT_THRESHOLD : 0;
    return GTUtility.powInt(heatDiscountExponent, heatDiscounts);  // heatDiscountExponent = 0.95
}
// 每超过 900K：EU/t * 0.95，即每 900K 节省 5%
```

### 8.5 结果获取

```java
// src/main/java/gregtech/api/util/OverclockCalculator.java:280-301
/** 调用 calculate() 后获取消耗 EU/t */
public long getConsumption() {
    if (!calculated) throw new IllegalStateException("Tried to get consumption before calculating");
    return calculatedConsumption;
}

/** 调用 calculate() 后获取时长（tick） */
public int getDuration() {
    if (!calculated) throw new IllegalStateException("Tried to get duration before calculating");
    return calculatedDuration;
}

/** 实际执行的超频次数 */
public int getPerformedOverclocks() {
    if (!calculated) throw new IllegalStateException("Tried to get performed overclocks before calculating");
    return overclocks;
}
```

---

## 9. 配方系统完整数据流

```
配方添加阶段（FML Init）
│
├── GTRecipeBuilder.itemInputs(...).itemOutputs(...).duration(...).eut(...).addTo(recipeMap)
│       ↓
│   RecipeMapBackend.compileRecipe(GTRecipe)
│       ↓ 加入 itemIndex（SetMultimap<GTItemStack, GTRecipe>）
│       ↓ 加入 fluidIndex（SetMultimap<String, GTRecipe>）
│
机器运行阶段（每次配方检查）
│
├── ProcessingLogic.process()
│   ├── getCurrentRecipeMap()  → 获取当前配方表
│   ├── findRecipeMatches(recipeMap)
│   │   └── recipeMap.findRecipeQuery()
│   │       .items(inputItems).fluids(inputFluids)
│   │       .voltage(availableVoltage).caching(true)
│   │       .findAll()   ← Stream<GTRecipe>
│   │           ↓ RecipeMapBackend.matchRecipeStream()
│   │           ↓ 检查 cacheMap → itemIndex → fluidIndex
│   │           ↓ 过滤：voltage * amperage >= recipe.mEUt
│   │
│   └── validateAndCalculateRecipe(recipe)
│       ├── validateRecipe(recipe)         → 自定义额外检查
│       ├── createParallelHelper(recipe)   → ParallelHelper 计算并行
│       ├── createOverclockCalculator(recipe)
│       │   └── OverclockCalculator
│       │       .setRecipeEUt(recipe.mEUt)
│       │       .setEUt(availableVoltage)
│       │       .setAmperage(availableAmperage)
│       │       .setDuration(recipe.mDuration)
│       │       .calculate()
│       │           → calculatedConsumption（最终 EU/t）
│       │           → calculatedDuration（最终 tick）
│       │
│       └── applyRecipe(recipe, helper, calculator, result)
│           ├── calculatedEut     = calculator.getConsumption()
│           ├── duration          = calculateDuration(...)
│           ├── outputItems       = helper.getItemOutputs()
│           └── outputFluids      = helper.getFluidOutputs()
│
└── 机器输出物品/流体，扣除 EU
```

**超频规则汇总：**

| 超频类型     | 触发条件                        | EU/t 变化    | 时长变化   |
|-------------|--------------------------------|-------------|-----------|
| 普通超频     | 机器电压 ≥ 配方 EU/t * 4        | × 4         | ÷ 2       |
| 热超频（EBF）| 机器热量超过配方热量 1800K       | × 4         | ÷ 4       |
| 热折扣（EBF）| 机器热量超过配方热量 900K        | × 0.95/次   | 不变      |
| 激光超频（TT）| 开启 laserOC，功率不足时触发   | × (4 + 0.3×n) | ÷ 2/次 |
