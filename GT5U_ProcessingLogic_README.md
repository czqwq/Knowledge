# GT5-Unofficial ProcessingLogic 详细逻辑知识库

> **代码来源：** https://github.com/GTNewHorizons/GT5-Unofficial  
> **本地路径：** /tmp/GT5-Unofficial  
> **文件路径：** `src/main/java/gregtech/api/logic/ProcessingLogic.java`  
> **所有代码均经本地源码核实，不含虚假代码。**

---

## 目录

1. [概述与定位](#1-概述与定位)
2. [完整字段说明](#2-完整字段说明)
3. [Setter API（配置机器参数）](#3-setter-api配置机器参数)
4. [process()：配方检查主入口](#4-process配方检查主入口)
5. [findRecipeMatches()：配方搜索](#5-findrecipematches配方搜索)
6. [validateAndCalculateRecipe()：验证+计算](#6-validateandcalculaterecipe验证计算)
7. [createParallelHelper()：并行计算](#7-createparallelhelper并行计算)
8. [createOverclockCalculator()：超频计算](#8-createoverclocalculator超频计算)
9. [applyRecipe()：应用配方结果](#9-applyrecipe应用配方结果)
10. [可重写扩展方法](#10-可重写扩展方法)
11. [Getter API（获取计算结果）](#11-getter-api获取计算结果)
12. [完整生命周期时序图](#12-完整生命周期时序图)
13. [典型多方块机器使用示例](#13-典型多方块机器使用示例)

---

## 1. 概述与定位

`ProcessingLogic` 是 GT5U 中**多方块机器配方处理的核心逻辑类**，负责将"机器输入"转化为"配方匹配→超频计算→输出产物"的完整流程。

**架构位置：**
```
MTEMultiBlockBase.checkProcessing()
        ↓
ProcessingLogic.process()
        ↓
RecipeMap.findRecipeQuery() → RecipeMapBackend.matchRecipeStream()
        ↓
ParallelHelper（并行计算）+ OverclockCalculator（超频计算）
        ↓
applyRecipe()（结果写入 outputItems/outputFluids/calculatedEut/duration）
```

ProcessingLogic **不直接操作 TileEntity**，它只持有输入数据和计算结果，由机器本身在 `checkProcessing()` 前后负责读取仓位数据和写入输出。

---

## 2. 完整字段说明

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:35-84
public class ProcessingLogic {

    // ── 机器特性 ──────────────────────────────────────────────
    protected IVoidable machine;                        // 虚空保护接口
    protected IRecipeLockable recipeLockableMachine;    // 配方锁定接口
    protected boolean isRecipeLocked;                   // 是否处于配方锁定模式

    // ── 当前 tick 输入 ────────────────────────────────────────
    protected ItemStack[]  inputItems;                  // 物品输入
    protected FluidStack[] inputFluids;                 // 流体输入
    protected ItemStack    specialSlotItem;             // 特殊槽位物品

    // ── 并行控制 ──────────────────────────────────────────────
    protected int maxParallel = 1;                      // 最大并行数
    protected Supplier<Integer> maxParallelSupplier;    // 动态并行数提供者
    protected int batchSize = 1;                        // 批处理大小

    // ── 配方表 ────────────────────────────────────────────────
    protected Supplier<RecipeMap<?>> recipeMapSupplier; // 配方表提供者（支持动态切换）

    // ── 能量参数 ──────────────────────────────────────────────
    protected double euModifier = 1.0;                  // EU/t 修正系数
    protected double speedBoost = 1.0;                  // 速度加成（时长修正）
    protected long availableVoltage;                    // 机器可用电压（或总功率）
    protected long availableAmperage;                   // 机器安培数

    // ── 超频参数 ──────────────────────────────────────────────
    protected int maxTierSkips = 1;                     // 最多跨几阶超频（默认 1 阶）
    protected double overClockTimeReduction  = 2.0;    // 每次超频时长除数（默认 2）
    protected double overClockPowerIncrease  = 4.0;    // 每次超频 EU/t 倍率（默认 4）
    protected boolean amperageOC = true;                // 是否允许安培数参与超频

    // ── 虚空保护 ──────────────────────────────────────────────
    protected boolean protectItems;                     // 物品虚空保护
    protected boolean protectFluids;                    // 流体虚空保护

    // ── 缓存 ──────────────────────────────────────────────────
    protected boolean recipeCaching = true;             // 是否启用配方缓存
    protected RecipeMap<?> lastRecipeMap;               // 上次配方表（用于检测切换）
    protected GTRecipe lastRecipe;                      // 上次成功配方（缓存命中优先）
    // DualInput 模式缓存（用于 ME 接口图案）
    protected Map<IDualInputInventoryWithPattern, Set<GTRecipe>> dualInvWithPatternToRecipeCache = new HashMap<>();

    // ── 计算结果 ──────────────────────────────────────────────
    protected ItemStack[]  outputItems;                 // 产出物品
    protected FluidStack[] outputFluids;                // 产出流体
    protected long calculatedEut;                       // 最终 EU/t（超频后）
    protected int  duration;                            // 最终时长（tick，超频后）
    protected int  calculatedParallels = 0;             // 实际并行数
}
```

---

## 3. Setter API（配置机器参数）

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:88-270（Setter 方法）

// 设置虚空保护
public ProcessingLogic setMachine(IVoidable machine)

// 启用配方锁定
public ProcessingLogic setRecipeLocking(IRecipeLockable recipeLockableMachine, boolean isRecipeLocked)

// 设置物品输入
public ProcessingLogic setInputItems(ItemStack... itemInputs)
public ProcessingLogic setInputItems(List<ItemStack> itemInputs)

// 设置流体输入
public ProcessingLogic setInputFluids(FluidStack... fluidInputs)
public ProcessingLogic setInputFluids(List<FluidStack> fluidInputs)

// 设置特殊槽位
public ProcessingLogic setSpecialSlotItem(ItemStack specialSlotItem)

// 设置并行
public ProcessingLogic setMaxParallel(int maxParallel)
public ProcessingLogic setMaxParallelSupplier(Supplier<Integer> supplier)
public ProcessingLogic setBatchSize(int size)

// 设置配方表
public ProcessingLogic setRecipeMap(RecipeMap<?> recipeMap)
public ProcessingLogic setRecipeMapSupplier(Supplier<RecipeMap<?>> supplier)

// 设置能量修正
public ProcessingLogic setEuModifier(double modifier)
public ProcessingLogic setSpeedBonus(double speedModifier)

/**
 * 设置机器可用电压。
 * 对大多数多方块机器：传入"总输入功率"（电压 * 安培），同时 setAvailableAmperage(1)，
 * 这样 findRecipeQuery 会用总功率匹配配方，避免阶级限制。
 */
public ProcessingLogic setAvailableVoltage(long voltage)

/**
 * 设置安培数（不参与配方搜索电压计算，但影响超频的功率计算）。
 */
public ProcessingLogic setAvailableAmperage(long amperage)

// 超频阶级限制
public ProcessingLogic setMaxTierSkips(int tierSkips)
public ProcessingLogic setUnlimitedTierSkips()

// 虚空保护
public ProcessingLogic setVoidProtection(boolean protectItems, boolean protectFluids)

// 超频参数
public ProcessingLogic setOverclock(double timeReduction, double powerIncrease)
public ProcessingLogic setAmperageOC(boolean amperageOC)

// 重置（每次 checkProcessing 前必须重置输出）
public ProcessingLogic clear()
```

---

## 4. `process()`：配方检查主入口

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:374-432
/**
 * 执行配方检查：从配方表查找配方 → 计算并行 → 计算超频 → 计算输出。
 */
@Nonnull
public CheckRecipeResult process() {
    RecipeMap<?> recipeMap = getCurrentRecipeMap();

    if (maxParallelSupplier != null) {
        maxParallel = maxParallelSupplier.get();
    }

    if (inputItems == null)  inputItems  = GTValues.emptyItemStackArray;
    if (inputFluids == null) inputFluids = GTValues.emptyFluidStackArray;
    inputItems = prepareCatalyst(inputItems);  // 注入催化剂（可重写）

    // 优先走 DualInput 模式缓存（ME 接口图案）
    if (activeDualInv != null) {
        Set<GTRecipe> matchedRecipes = dualInvWithPatternToRecipeCache.get(activeDualInv);
        for (GTRecipe matchedRecipe : matchedRecipes) {
            if (matchedRecipe.maxParallelCalculatedByInputs(1, inputFluids, inputItems) == 1) {
                CalculationResult foundResult = validateAndCalculateRecipe(matchedRecipe);
                return foundResult.checkRecipeResult;
            }
        }
        // 缓存不匹配则清除，下次重新生成
        dualInvWithPatternToRecipeCache.remove(activeDualInv);
        activeDualInv = null;
    }

    // 配方锁定模式：只检查锁定的那一个配方
    if (isRecipeLocked && recipeLockableMachine != null
        && recipeLockableMachine.getSingleRecipeCheck() != null) {
        SingleRecipeCheck singleRecipeCheck = recipeLockableMachine.getSingleRecipeCheck();
        if (singleRecipeCheck.checkRecipeInputs(false, 1, inputItems, inputFluids) == 0) {
            return CheckRecipeResultRegistry.NO_RECIPE;
        }
        return validateAndCalculateRecipe(
            recipeLockableMachine.getSingleRecipeCheck().getRecipe()).checkRecipeResult;
    }

    // 普通模式：遍历所有匹配配方
    Stream<GTRecipe> matchedRecipes = findRecipeMatches(recipeMap);
    CheckRecipeResult checkRecipeResult = CheckRecipeResultRegistry.NO_RECIPE;
    for (GTRecipe matchedRecipe : (Iterable<GTRecipe>) matchedRecipes::iterator) {
        CalculationResult foundResult = validateAndCalculateRecipe(matchedRecipe);
        if (foundResult.successfullyConsumedInputs) {
            return foundResult.checkRecipeResult;  // 找到并消耗成功，直接返回
        }
        if (foundResult.checkRecipeResult != CheckRecipeResultRegistry.NO_RECIPE) {
            checkRecipeResult = foundResult.checkRecipeResult;  // 记录有趣的失败原因
        }
    }
    return checkRecipeResult;
}
```

---

## 5. `findRecipeMatches()`：配方搜索

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:516-528
@Nonnull
protected Stream<GTRecipe> findRecipeMatches(@Nullable RecipeMap<?> map) {
    if (map == null) {
        return Stream.empty();
    }
    return map.findRecipeQuery()
        .caching(recipeCaching)       // 启用 cacheMap 缓存
        .items(inputItems)            // 物品输入
        .fluids(inputFluids)          // 流体输入
        .specialSlot(specialSlotItem) // 特殊槽位
        .cachedRecipe(lastRecipe)     // 上次配方（优先检查）
        .findAll();                   // 返回 Stream<GTRecipe>
}
```

**内部过滤条件（来自 `FindRecipeQuery.findAll()`）：**
```java
// src/main/java/gregtech/api/recipe/FindRecipeQuery.java:91
.filter(recipe -> voltage * recipeMap.getAmperage() >= recipe.mEUt && filter.test(recipe))
```
即：`availableVoltage * recipeMap.getAmperage() >= recipe.mEUt` 才会被返回。

---

## 6. `validateAndCalculateRecipe()`：验证+计算

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:441-458
@Nonnull
private CalculationResult validateAndCalculateRecipe(@Nonnull GTRecipe recipe) {
    // 1. 自定义额外验证（默认直接返回 SUCCESSFUL）
    CheckRecipeResult result = validateRecipe(recipe);
    if (!result.wasSuccessful()) {
        return CalculationResult.ofFailure(result);
    }

    // 2. 创建并行计算器
    ParallelHelper helper = createParallelHelper(recipe);

    // 3. 创建超频计算器
    OverclockCalculator calculator = createOverclockCalculator(recipe);

    // 4. 关联：超频计算器在并行计算时被调用
    helper.setCalculator(calculator);
    helper.build();   // ← 触发并行计算（内部调用 calculator.calculate()）

    if (!helper.getResult().wasSuccessful()) {
        return CalculationResult.ofFailure(helper.getResult());
    }

    // 5. 应用结果
    return CalculationResult.ofSuccess(applyRecipe(recipe, helper, calculator, result));
}
```

---

## 7. `createParallelHelper()`：并行计算

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:542-554
@Nonnull
protected ParallelHelper createParallelHelper(@Nonnull GTRecipe recipe) {
    return new ParallelHelper()
        .setRecipe(recipe)
        .setItemInputs(inputItems)
        .setFluidInputs(inputFluids)
        .setAvailableEUt(availableVoltage * availableAmperage)  // 总可用功率
        .setMachine(machine, protectItems, protectFluids)
        .setRecipeLocked(recipeLockableMachine, isRecipeLocked)
        .setMaxParallel(maxParallel)
        .setEUtModifier(euModifier)
        .enableBatchMode(batchSize)
        .setConsumption(true)        // 消耗输入
        .setOutputCalculation(true); // 计算输出
}
```

**`ParallelHelper` 工作原理：**
- 在 `build()` 时调用 `setCalculator(calculator)` 绑定的 `OverclockCalculator`
- 不断尝试增加并行数（1 → 2 → ... → maxParallel），直到总 EU/t 超过 `availableVoltage * availableAmperage`
- 同时检查输出槽是否有足够空间（虚空保护模式下跳过此检查）

---

## 8. `createOverclockCalculator()`：超频计算

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:560-571
@Nonnull
protected OverclockCalculator createOverclockCalculator(@Nonnull GTRecipe recipe) {
    return new OverclockCalculator()
        .setRecipeEUt(recipe.mEUt)              // 配方原始 EU/t
        .setAmperage(availableAmperage)          // 机器安培数
        .setEUt(availableVoltage)                // 机器电压（或总功率）
        .setMaxTierSkips(maxTierSkips)           // 最大跨阶数
        .setDuration(recipe.mDuration)           // 配方原始时长
        .setDurationModifier(speedBoost)         // 速度加成修正
        .setEUtDiscount(euModifier)              // EU/t 折扣系数
        .setAmperageOC(amperageOC)               // 是否允许安培超频
        .setDurationDecreasePerOC(overClockTimeReduction)  // 时长减少倍数
        .setEUtIncreasePerOC(overClockPowerIncrease);      // EU/t 增加倍数
}
```

---

## 9. `applyRecipe()`：应用配方结果

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:465-508
@Nonnull
protected CheckRecipeResult applyRecipe(@Nonnull GTRecipe recipe, @Nonnull ParallelHelper helper,
    @Nonnull OverclockCalculator calculator, @Nonnull CheckRecipeResult result) {

    if (recipe.mCanBeBuffered) {
        lastRecipe = recipe;  // 缓存配方（下次优先匹配）
    } else {
        lastRecipe = null;
    }

    calculatedParallels = helper.getCurrentParallel();

    // 溢出保护
    if (calculator.getConsumption() == Long.MAX_VALUE) {
        return CheckRecipeResultRegistry.POWER_OVERFLOW;
    }
    if (calculator.getDuration() == Integer.MAX_VALUE) {
        return CheckRecipeResultRegistry.DURATION_OVERFLOW;
    }

    calculatedEut = calculator.getConsumption();  // 写入最终 EU/t

    double finalDuration = calculateDuration(recipe, helper, calculator);
    if (finalDuration >= Integer.MAX_VALUE) {
        return CheckRecipeResultRegistry.DURATION_OVERFLOW;
    }
    duration = (int) finalDuration;               // 写入最终时长

    CheckRecipeResult hookResult = onRecipeStart(recipe);  // 配方开始钩子
    if (!hookResult.wasSuccessful()) {
        return hookResult;
    }

    outputItems  = helper.getItemOutputs();    // 写入产出物品
    outputFluids = helper.getFluidOutputs();   // 写入产出流体

    return result;
}
```

---

## 10. 可重写扩展方法

| 方法 | 默认行为 | 重写用途 |
|------|---------|---------|
| `validateRecipe(GTRecipe)` | 直接返回 `SUCCESSFUL` | 添加电压、特殊材料等自定义检查 |
| `findRecipeMatches(RecipeMap)` | 标准配方查询 | 非标准配方表（如 TecTech 组装线） |
| `createParallelHelper(GTRecipe)` | 标准并行构建 | 自定义并行逻辑 |
| `createOverclockCalculator(GTRecipe)` | 标准超频构建 | 热超频、激光超频等 |
| `onRecipeStart(GTRecipe)` | 返回 `SUCCESSFUL` | 配方开始时触发副作用（如扣除催化剂） |
| `prepareCatalyst(ItemStack[])` | 原样返回 | 注入研磨球、催化剂等 |

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:534-590（摘录）

/** 额外验证（默认通过） */
@Nonnull
protected CheckRecipeResult validateRecipe(@Nonnull GTRecipe recipe) {
    return CheckRecipeResultRegistry.SUCCESSFUL;
}

/** 配方开始钩子 */
@Nonnull
protected CheckRecipeResult onRecipeStart(@Nonnull GTRecipe recipe) {
    return CheckRecipeResultRegistry.SUCCESSFUL;
}

/** 催化剂注入（不修改原数组，返回新数组） */
protected ItemStack[] prepareCatalyst(ItemStack[] inputs) {
    return inputs;
}
```

---

## 11. Getter API（获取计算结果）

```java
// src/main/java/gregtech/api/logic/ProcessingLogic.java:594-614
public ItemStack[]  getOutputItems()   { return outputItems; }
public FluidStack[] getOutputFluids()  { return outputFluids; }
public int          getDuration()      { return duration; }
public long         getCalculatedEut() { return calculatedEut; }
public int          getCurrentParallels() { return calculatedParallels; }
```

---

## 12. 完整生命周期时序图

```
每次 checkProcessing（约每 20~80 tick 一次）
│
├─ 机器（MTEMultiBlockBase）
│   ├─ 收集 mInputHatches → setInputItems(items)
│   ├─ 收集 mInputBusses  → setInputFluids(fluids)
│   ├─ 设置 setAvailableVoltage(maxEU) / setAvailableAmperage(amperes)
│   └─ processingLogic.process()
│          │
│          ├─ getCurrentRecipeMap()（检测配方表是否切换，切换时清缓存）
│          │
│          ├─ findRecipeMatches()
│          │   └─ RecipeMap.findRecipeQuery()
│          │       .items / .fluids / .cachedRecipe / .findAll()
│          │           ↓ cacheMap 命中 → 直接返回
│          │           ↓ itemIndex 搜索 → 返回候选 Stream
│          │           ↓ 按 voltage >= mEUt 过滤
│          │
│          ├─ for each candidateRecipe:
│          │   ├─ validateRecipe()（可重写）
│          │   ├─ createParallelHelper().build()
│          │   │   └─ 计算最大并行（逐步增加，直到超过总功率）
│          │   │   └─ 消耗 inputItems / inputFluids
│          │   ├─ createOverclockCalculator().calculate()
│          │   │   └─ 计算超频次数（log4 比值）
│          │   │   └─ 计算最终 EU/t 和时长
│          │   └─ applyRecipe()
│          │       ├─ calculatedEut   = calculator.getConsumption()
│          │       ├─ duration        = finalDuration
│          │       ├─ outputItems     = helper.getItemOutputs()
│          │       └─ outputFluids    = helper.getFluidOutputs()
│          │
│          └─ 返回 CheckRecipeResult
│
└─ 机器（MTEMultiBlockBase）
    ├─ mEUt              = -(int) processingLogic.getCalculatedEut()
    ├─ mMaxProgresstime  = processingLogic.getDuration()
    ├─ mOutputItems      = processingLogic.getOutputItems()
    └─ mOutputFluids     = processingLogic.getOutputFluids()
```

---

## 13. 典型多方块机器使用示例

```java
// 典型多方块机器使用 ProcessingLogic 的方式（基于 GTMultiBlockBase 子类）

@Override
public RecipeMap<?> getRecipeMap() {
    return RecipeMaps.blastFurnaceRecipes;
}

@Override
protected ProcessingLogic createProcessingLogic() {
    return new ProcessingLogic()
        .setRecipeMap(getRecipeMap())
        .setEuModifier(getEnergyModifier())
        .setMaxParallelSupplier(this::getMaxParallel)
        .setAmperageOC(false);              // 高炉不允许安培超频
}

@Override
public CheckRecipeResult checkProcessing() {
    // 机器在 checkProcessing 前设置输入/能量
    processingLogic
        .setInputItems(getAllInputItems())
        .setInputFluids(getAllInputFluids())
        .setAvailableVoltage(getMaxInputEu())
        .setAvailableAmperage(1L);

    return processingLogic.process();
}
```

**关键注意事项：**
1. `setAvailableVoltage` 传入的通常是**总功率**（电压 × 安培），`setAvailableAmperage` 传 `1`
2. 若要限制超频阶级（如只允许超频1阶），使用 `setMaxTierSkips(1)`
3. `processingLogic.clear()` 必须在每次 `process()` 前调用（清除上次输出），否则复用旧结果
4. 重写 `createOverclockCalculator()` 时，调用 `super.createOverclockCalculator(recipe)` 获取基础构建器再追加热超频参数
