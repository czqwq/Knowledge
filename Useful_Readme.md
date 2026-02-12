# GT5-Unofficial 可重用代码知识库

**仓库地址**: https://github.com/GTNewHorizons/GT5-Unofficial  
**目的**: 为AI整合GT5U所有可造轮子的代码、实现机制和功能

---

## 目录

1. [工具类体系](#工具类体系)
2. [设计模式实现](#设计模式实现)
3. [核心系统架构](#核心系统架构)
4. [数据结构与算法](#数据结构与算法)
5. [扩展点与API](#扩展点与api)
6. [实战代码示例](#实战代码示例)

---

## 工具类体系

### 1.1 gregtech.api.util - 核心工具集

#### 基础工具类

| 类名 | 包路径 | 核心功能 | 常用方法 |
|------|--------|---------|---------|
| **GTUtility** | gregtech.api.util | 通用工具集合 | `isStackValid()`, `areStacksEqual()`, `copyAmount()` |
| **GTModHandler** | gregtech.api.util | Mod互操作 | `getRecipeOutput()`, `addCraftingRecipe()`, `getEnchantment()` |
| **GTOreDictUnificator** | gregtech.api.util | 矿物词典统一 | `get()`, `isItemStackInstanceOf()`, `setStack()` |
| **GTStructureUtility** | gregtech.api.util | 结构验证 | `buildHatchAdder()`, `ofHatchAdder()` |
| **GTRecipeMapUtil** | gregtech.api.util | 配方工具 | `buildOrEmpty()`, `ofRecipe()` |

**代码示例 - GTUtility**:
```java
// 物品堆比较
if (GTUtility.areStacksEqual(stack1, stack2, true)) {
    // 忽略NBT的比较
}

// 安全复制并设置数量
ItemStack result = GTUtility.copyAmount(64, template);

// 获取方块硬度
float hardness = GTUtility.getHardnessOf(block, meta);
```

---

#### Builder模式工具类

| 类名 | 用途 | 链式方法 |
|------|------|---------|
| **GTRecipeBuilder** | 配方构建 | `.itemInputs()` → `.itemOutputs()` → `.duration()` → `.EUt()` → `.buildAndRegister()` |
| **HatchElementBuilder<T>** | 多方块舱口 | `.atLeast()` → `.casingIndex()` → `.dot()` → `.build()` |
| **MultiblockTooltipBuilder** | 工具提示 | `.addMachineType()` → `.addInfo()` → `.addSeparator()` → `.build()` |
| **RecipeMapBuilder** | 配方表构建 | `.maxIO()` → `.minInputs()` → `.frontend()` → `.build()` |

**代码示例 - GTRecipeBuilder**:
```java
GTValues.RA.stdBuilder()
    .itemInputs(
        GTUtility.getIntegratedCircuit(1),
        GTOreDictUnificator.get(OrePrefixes.plate, Materials.Iron, 4)
    )
    .itemOutputs(new ItemStack(Items.bucket))
    .fluidInputs(Materials.Water.getFluid(1000))
    .duration(200)  // 10秒 (20 ticks/s)
    .EUt(16)        // 16 EU/t (LV)
    .addTo(RecipeMaps.assemblerRecipes);
```

---

#### Factory模式实现

| 类名 | 创建对象 | 位置 |
|------|---------|------|
| **GTFluidFactory** | Fluid流体 | gregtech.api.fluid |
| **TextureFactory** | 纹理 | gregtech.api.render |
| **CoverFactory** | Cover覆盖物 | gregtech.api.covers |
| **CoverUIFactory** | Cover UI | gregtech.common.gui.mui1.cover (40+子类) |

**代码示例 - GTFluidFactory**:
```java
// 创建自定义流体
Fluid myFluid = GTFluidFactory.builder("myfluid")
    .withLocalizedName("My Fluid")
    .withTexture(textures)
    .withColorRGBA(0x3366FF)
    .buildAndRegister();
```

---

### 1.2 Helper类集合

| 类名 | 功能 | 使用场景 |
|------|------|---------|
| **ExoticEnergyInputHelper** | 异域能源输入 | 激光、等离子体等高级能源 |
| **GTToolHarvestHelper** | 工具采集检查 | 判断玩家工具是否能挖掘方块 |
| **VoidProtectionHelper** | 虚空保护 | 防止物品掉入虚空 |
| **LightingHelper** | 光照计算 | 渲染优化，动态光照 |
| **ItemEjectionHelper** | 物品弹出 | 自动输出到相邻容器 |
| **ParallelHelper** | 并行处理 | 多线程配方处理辅助 |

**代码示例 - ParallelHelper**:
```java
ParallelHelper helper = new ParallelHelper();
helper.setAvailableEUt(voltage * amperage);
helper.setRecipe(baseRecipe);
helper.setItemInputs(inputItems);
helper.setFluidInputs(inputFluids);
helper.setMachine(multiblock);

int parallel = helper.calculateParallel();
GTRecipe parallelRecipe = helper.build();
```

---

### 1.3 Manager类 - 单例模式

| 类名 | 管理对象 | 设计模式 |
|------|---------|---------|
| **PCBFactoryManager** | PCB工厂等级 | 单例 + BiMap |
| **GTLanguageManager** | 多语言 | 单例 + HashMap缓存 |
| **OreManager** | 矿物生成 | 单例 + 集中管理 |

**代码示例 - PCBFactoryManager**:
```java
// 获取单例
PCBFactoryManager manager = PCBFactoryManager.getInstance();

// 注册PCB等级
manager.registerPCBFactory(
    tier,           // 等级
    plasticTier,    // 塑料等级
    machineName,    // 机器名
    glassType       // 玻璃类型
);

// 查询
int plasticTier = manager.getPlasticTier(tier);
```

---

## 设计模式实现

### 2.1 建造者模式 (Builder Pattern)

**优势**: 
- 链式调用，代码可读性高
- 参数校验集中
- 支持可选参数

**实现列表**:
1. GTRecipeBuilder - 配方构建
2. RecipeMapBuilder - 配方表
3. HatchElementBuilder - 结构元素
4. WorldSpawnedEventBuilder - 世界事件
5. MaterialBuilder - 材料定义
6. OrePrefixBuilder - 矿物前缀

**完整示例 - RecipeMapBuilder**:
```java
RecipeMap<RecipeMapBackend> customMap = RecipeMapBuilder
    .of("my.custom.recipes")
    .maxIO(4, 2, 2, 1)      // 4in 2out items, 2in 1out fluids
    .minInputs(1, 0)         // 至少1个物品输入
    .slotOverlays(
        (index, isFluid, isOutput, isSpecial) -> 
            isOutput ? GTUITextures.OVERLAY_SLOT_OUT 
                     : GTUITextures.OVERLAY_SLOT_IN
    )
    .progressBar(GTUITextures.PROGRESSBAR_ARROW)
    .neiHandlerInfo(builder -> 
        builder.setDisplayStack(myMachine.getStackForm(1))
    )
    .logo(myLogo)
    .logoSize(18, 18)
    .logoPos(151, 63)
    .build();
```

---

### 2.2 工厂模式 (Factory Pattern)

**类型**: 简单工厂 + 抽象工厂

**Cover工厂示例**:
```java
// 定义工厂函数
CoverFactory factory = (context) -> new MyCover(context);

// 注册到全局注册表
CoverRegistry.registerCover(
    new ItemStack(myItem),          // 触发物品
    GTUITextures.OVERLAY_PIPE_OUT,  // 图标
    factory,                         // 工厂
    CoverPlacer.builder()           // 放置规则
        .allowOnPrimitiveBlock()
        .allowOnWorkable()
        .build()
);

// 使用时自动调用工厂创建
Cover cover = factory.create(context);
```

---

### 2.3 单例模式 (Singleton Pattern)

**实现方式**: 私有构造器 + 静态实例

**示例 - PCBFactoryManager**:
```java
public class PCBFactoryManager {
    private static final PCBFactoryManager INSTANCE = new PCBFactoryManager();
    
    private final BiMap<Integer, Integer> tierToPlastic = HashBiMap.create();
    
    private PCBFactoryManager() {
        // 私有构造器
    }
    
    public static PCBFactoryManager getInstance() {
        return INSTANCE;
    }
    
    // 业务方法...
}
```

---

### 2.4 懒加载模式 (Lazy Loading)

**实现 - Lazy<T>**:
```java
public class Lazy<T> implements Supplier<T> {
    private Supplier<T> supplier;
    private T value;
    
    public Lazy(Supplier<T> supplier) {
        this.supplier = supplier;
    }
    
    @Override
    public synchronized T get() {
        if (value == null && supplier != null) {
            value = supplier.get();
            supplier = null;  // 释放引用
        }
        return value;
    }
}

// 使用示例
Lazy<ExpensiveObject> lazy = new Lazy<>(() -> new ExpensiveObject());
ExpensiveObject obj = lazy.get();  // 首次调用时才创建
```

---

### 2.5 策略模式 (Strategy Pattern)

**OverclockCalculator - 超频策略**:
```java
public class OverclockCalculator {
    // 策略1: 标准超频
    public static OverclockResult calculateStandard(
        GTRecipe recipe, int voltage) {
        // 计算逻辑...
    }
    
    // 策略2: 激光超频
    public static OverclockResult calculateLaser(
        GTRecipe recipe, int voltage) {
        // 特殊计算...
    }
    
    // 策略3: 完美超频
    public static OverclockResult calculatePerfect(
        GTRecipe recipe, int voltage) {
        // 无惩罚计算...
    }
}

// 使用
OverclockResult result = calculator.calculate(
    recipe, 
    voltage, 
    OverclockStrategy.LASER
);
```

---

## 核心系统架构

### 3.1 Recipe系统 - 配方管理

**核心类**:
```
RecipeMap<B extends RecipeMapBackend>
├── RecipeMapBackend          // 存储引擎
│   ├── itemIndex: SetMultimap // 物品索引
│   ├── fluidIndex: SetMultimap // 流体索引
│   └── cacheMap: GTRecipe[]   // 哈希缓存(256槽)
├── RecipeMapFrontend         // NEI/GUI前端
└── FindRecipeQuery           // 查询API
```

**工作流程**:
```
1. 添加配方:
   Builder → validate() → build() → RecipeMapBackend.compileRecipe()
   → 构建索引 → 添加到cacheMap

2. 查找配方:
   FindRecipeQuery → 计算hash → cacheMap快速查找
   → 如果miss，则遍历itemIndex/fluidIndex → 验证完全匹配
```

**扩展点**:
```java
// 1. 自定义Backend
public class MyBackend extends RecipeMapBackend {
    @Override
    protected GTRecipe doFindRecipe(ItemStack[] items, FluidStack[] fluids) {
        // 自定义查找逻辑
    }
}

RecipeMap<MyBackend> map = RecipeMapBuilder
    .of("custom", MyBackend::new)
    .build();

// 2. Builder变换器
map.appendBuilderTransformer(builder -> {
    builder.duration((int)(builder.duration() * 1.5));
    builder.EUt((int)(builder.EUt() * 0.9));
});

// 3. Recipe后处理
map.appendRecipeTransformer(recipe -> {
    recipe.mOutputs = processOutputs(recipe.mOutputs);
});
```

**最佳实践**:
```java
// 定义RecipeMap (模组加载阶段)
public static final RecipeMap<RecipeMapBackend> MY_RECIPES = 
    RecipeMapBuilder.of("my.recipes")
        .maxIO(3, 2, 1, 1)
        .build();

// 添加配方 (后加载阶段)
MY_RECIPES.recipeBuilder()
    .itemInputs(GTOreDictUnificator.get(OrePrefixes.dust, Materials.Iron, 1))
    .itemOutputs(new ItemStack(Items.iron_ingot))
    .duration(200)
    .EUt(30)
    .buildAndRegister();

// 查询配方 (运行时)
GTRecipe recipe = MY_RECIPES.findRecipeQuery()
    .items(inputs)
    .fluids(fluidInputs)
    .voltage(480)
    .find();
```

---

### 3.2 MetaTileEntity系统 - 机器实体

**类层次结构**:
```
MetaTileEntity (抽象基类)
├── CommonMetaTileEntity           // 通用MTE
├── MTEBasicMachine               // 单方块机器
│   └── MTEBasicMachineWithRecipe // 配方驱动机器
├── MTEMultiBlockBase             // 多方块基类
│   ├── MTEProcessingArray        // 处理阵列
│   └── MTELargeTurbine           // 大型涡轮
└── MTEHatch                      // 舱口基类
    ├── MTEHatchInput/Output      // 物品舱口
    ├── MTEHatchEnergy            // 能量舱口
    └── MTEHatchFluid             // 流体舱口
```

**生命周期**:
```
创建 → newMetaEntity()
放置 → onLoad()
每Tick → onPreTick() → onPostTick()
更新 → onBlockUpdate()
移除 → onUnload()
```

**能量系统**:
```java
public interface IEnergyConnected {
    long injectEnergyUnits(ForgeDirection side, long voltage, long amperage);
    boolean inputEnergyFrom(ForgeDirection side);
    boolean outputsEnergyTo(ForgeDirection side);
}

// 实现示例
@Override
public long injectEnergyUnits(ForgeDirection side, long voltage, long amperage) {
    if (voltage > getMaxInputVoltage()) {
        // 过载爆炸
        doExplosion(voltage);
        return 0;
    }
    long consumed = Math.min(amperage, getMaxInputAmperage());
    energyBuffer += voltage * consumed;
    return consumed;
}
```

**创建自定义机器**:
```java
public class MyCustomMachine extends MTEBasicMachineWithRecipe {
    public MyCustomMachine(int id, String name, int tier) {
        super(
            id,                          // 唯一ID
            name,                        // 内部名
            "My Machine",                // 显示名
            tier,                        // 等级 (0=ULV, 1=LV, ...)
            "Does something cool",       // 描述
            RecipeMaps.myRecipes,        // 配方表
            2, 2,                        // 输入/输出槽
            16000,                       // 流体容量(mB)
            SoundResource.ASSEMBLER      // 声音
        );
    }
    
    @Override
    public MetaTileEntity newMetaEntity(IGregTechTileEntity gte) {
        return new MyCustomMachine(mID, mName, mTier);
    }
    
    @Override
    protected void generateDefaultTextures() {
        mTextures[0] = new ITexture[]{/* 底部纹理 */};
        mTextures[1] = new ITexture[]{/* 顶部纹理 */};
        // ... 其他面
    }
    
    @Override
    public void onPostTick() {
        super.onPostTick();
        if (mProgresstime % 20 == 0) {
            // 每秒执行的逻辑
        }
    }
}

// 注册 (PreInit阶段)
new MyCustomMachine(3000, "gt.my.machine", 3);
```

---

### 3.3 Multiblock结构系统

**核心接口**:
```java
public interface IStructureProvider<MTE> {
    String[][] getDefinition();        // 最小结构
    String[][] getMaxDefinition();     // 最大结构(可选)
    IStructureDefinition<MTE> compile(String[][] definition);
}
```

**StructureWrapper**:
```java
public class StructureWrapper<MTE> {
    public Char2ObjectArrayMap<CasingInfo<MTE>> casings = new Char2ObjectArrayMap<>();
    
    public void loadStructure() {
        // 初始化casings
    }
    
    public IStructureDefinition<MTE> buildStructure(String[][] definition) {
        // 编译定义为验证逻辑
    }
}
```

**完整示例**:
```java
public class MyMultiblock extends MTEMultiBlockBase 
    implements IStructureProvider<MyMultiblock> {
    
    private final StructureWrapper<MyMultiblock> wrapper = 
        new StructureWrapper<>(this);
    
    @Override
    public String[][] getDefinition() {
        return new String[][] {
            //     前      中      后
            {"CCC", "CCC", "CCC"},  // 底层
            {"CCC", "CMC", "CCC"},  // 中层 (M=控制器)
            {"CCC", "CCC", "CCC"}   // 顶层
        };
    }
    
    @Override
    public IStructureDefinition<MyMultiblock> compile(String[][] definition) {
        wrapper.loadStructure();
        
        // 配置方块映射
        wrapper.casings.put('C', new CasingInfo<>(
            GregTechAPI.sBlockCasings1,   // 方块
            0,                             // 元数据
            GTUITextures.CASING_BRONZE_PLATED,
            (tile, world, pos) -> tile instanceof ICasingBlock
        ));
        
        wrapper.casings.put('M', new CasingInfo<>(
            this.getBlock(),
            this.getMetaID(),
            null,
            (tile, world, pos) -> tile == this
        ));
        
        return wrapper.buildStructure(definition);
    }
    
    @Override
    public boolean checkStructure() {
        // 自动调用compile()生成的验证逻辑
        return structureInstance.checkStructure(this);
    }
}
```

**HatchElementBuilder - 舱口定义**:
```java
// 添加能量舱口
HatchElementBuilder.<MyMultiblock>builder()
    .atLeast(Energy)              // 至少1个能量舱口
    .casingIndex(CASING_INDEX)    // 纹理索引
    .dot(2)                       // 结构提示中的标记
    .buildAndChain(definition);

// 添加输入总线
HatchElementBuilder.<MyMultiblock>builder()
    .atLeast(InputBus)
    .adder(MyMultiblock::addInputBus)
    .casingIndex(CASING_INDEX)
    .dot(1)
    .buildAndChain(definition);
```

---

### 3.4 GUI与ModularUI系统

**ModularUI架构**:
```
ModularWindow
├── Widget[]                  // 小部件数组
│   ├── SlotWidget           // 物品槽
│   ├── FluidSlotWidget      // 流体槽
│   ├── ButtonWidget         // 按钮
│   ├── TextWidget           // 文本
│   ├── ProgressBar          // 进度条
│   └── DynamicTextWidget    // 动态文本
└── PanelSyncManager         // 数据同步
    └── SyncedField<T>       // 同步字段
```

**创建GUI**:
```java
@Override
protected ModularWindow createWindow(PosGuiData guiData) {
    ModularWindow.Builder builder = ModularWindow.builder(176, 166);
    
    builder
        .setBackground(getGUITextureSet().getMainBackground())
        .setGuiTint(getGUIColorization())
        
        // 物品输入槽
        .widget(new SlotWidget(inventoryHandler, 0)
            .setPos(52, 26))
        
        // 流体输入槽
        .widget(new FluidSlotWidget(fluidHandler, 0)
            .setPos(52, 44)
            .setSize(18, 18))
        
        // 进度条
        .widget(new ProgressBar()
            .setProgress(() -> (double)mProgresstime / mMaxProgresstime)
            .setTexture(GTUITextures.PROGRESSBAR_ARROW, 20)
            .setPos(78, 24))
        
        // 输出槽
        .widget(new SlotWidget(inventoryHandler, 2)
            .setPos(106, 26)
            .setAccess(false, true));  // 只读
    
    return builder.build();
}
```

**数据同步**:
```java
// 定义同步字段
panel.syncManager.registerSlaves(
    new SyncedField<>(() -> energy, v -> energy = v),
    new SyncedField<>(() -> mProgresstime, v -> mProgresstime = v),
    new SyncedField<>(() -> mMaxProgresstime, v -> mMaxProgresstime = v)
);

// 自动同步：服务端值变化时自动发包到客户端
```

---

### 3.5 Cover系统 - 覆盖物

**Cover基类**:
```java
public abstract class Cover {
    protected final WeakReference<ICoverable> coverableRef;
    protected final ForgeDirection side;
    
    // 生命周期
    public abstract void onInstalled();
    public abstract void onRemoved();
    public abstract void onTick();
    
    // 交互
    public int onScrewdriverRightClick(EntityPlayer player);
    
    // 序列化
    protected abstract void readDataFromNbt(NBTBase nbt);
    protected abstract NBTBase saveDataToNbt();
    
    // 网络同步
    protected void readDataFromPacket(ByteBuf buf);
    protected void writeDataToPacket(ByteBuf buf);
}
```

**创建自定义Cover**:
```java
public class CoverItemFilter extends Cover {
    private FilterMode mode = FilterMode.WHITELIST;
    private final Set<GTItemStack> filter = new HashSet<>();
    
    public CoverItemFilter(CoverContext context) {
        super(context, GTUITextures.OVERLAY_ITEM_FILTER);
    }
    
    @Override
    public int onScrewdriverRightClick(EntityPlayer player) {
        mode = mode.next();
        return mode.ordinal();  // 返回用于同步
    }
    
    @Override
    public boolean letsItemsOut(int slot, ItemStack item) {
        boolean inFilter = filter.contains(new GTItemStack(item));
        return mode == FilterMode.WHITELIST ? inFilter : !inFilter;
    }
    
    @Override
    protected NBTBase saveDataToNbt() {
        NBTTagCompound nbt = new NBTTagCompound();
        nbt.setByte("mode", (byte)mode.ordinal());
        
        NBTTagList list = new NBTTagList();
        for (GTItemStack stack : filter) {
            list.appendTag(stack.toNBT());
        }
        nbt.setTag("filter", list);
        return nbt;
    }
}

// 注册
CoverRegistry.registerCover(
    new ItemStack(MyItems.itemFilter),
    GTUITextures.OVERLAY_ITEM_FILTER,
    CoverItemFilter::new,
    CoverPlacer.builder().allowOnAll().build()
);
```

---

### 3.6 Network通信系统

**GTPacket基类**:
```java
public abstract class GTPacket {
    public abstract byte getPacketID();
    public abstract void encode(ByteBuf buffer);
    public abstract GTPacket decode(ByteArrayDataInput buffer);
    public abstract void process(IBlockAccess world);
}
```

**自定义网络包**:
```java
public class PacketSyncEnergy extends GTPacket {
    private int x, y, z;
    private long energy;
    
    public PacketSyncEnergy() {}
    
    public PacketSyncEnergy(int x, int y, int z, long energy) {
        this.x = x; this.y = y; this.z = z;
        this.energy = energy;
    }
    
    @Override
    public byte getPacketID() { return 50; }
    
    @Override
    public void encode(ByteBuf buffer) {
        buffer.writeInt(x);
        buffer.writeInt(y);
        buffer.writeInt(z);
        buffer.writeLong(energy);
    }
    
    @Override
    public GTPacket decode(ByteArrayDataInput buffer) {
        return new PacketSyncEnergy(
            buffer.readInt(),
            buffer.readInt(),
            buffer.readInt(),
            buffer.readLong()
        );
    }
    
    @Override
    public void process(IBlockAccess world) {
        if (world != null) {  // 客户端
            TileEntity te = world.getTileEntity(x, y, z);
            if (te instanceof MyTile) {
                ((MyTile) te).clientEnergy = energy;
            }
        }
    }
}

// 发送
GregTechAPI.sNetworkHandler.sendPacketToAllPlayers(
    new PacketSyncEnergy(x, y, z, energy)
);
```

---

## 数据结构与算法

### 4.1 自定义集合类

#### GTBlockMap<V> - 方块映射
```java
public class GTBlockMap<V> {
    private final Map<Block, Map<Integer, V>> map = new HashMap<>();
    
    public V put(Block block, int meta, V value) {
        return map.computeIfAbsent(block, k -> new HashMap<>())
                  .put(meta, value);
    }
    
    public V get(Block block, int meta) {
        Map<Integer, V> subMap = map.get(block);
        return subMap != null ? subMap.get(meta) : null;
    }
}

// 使用
GTBlockMap<ICasing> casingMap = new GTBlockMap<>();
casingMap.put(Blocks.stone, 0, myCasing);
```

#### BlockPosMap<V> - 坐标映射
```java
// 使用Long压缩xyz坐标 (x: 26bits, y: 12bits, z: 26bits)
public class BlockPosMap<V> {
    private final Long2ObjectOpenHashMap<V> map = new Long2ObjectOpenHashMap<>();
    
    public V put(int x, int y, int z, V value) {
        return map.put(encodePos(x, y, z), value);
    }
    
    private static long encodePos(int x, int y, int z) {
        return ((long)x & 0x3FFFFFF) << 38 | 
               ((long)y & 0xFFF) << 26 | 
               ((long)z & 0x3FFFFFF);
    }
}
```

#### LRUCache<K,V> - LRU缓存
```java
public class LRUCache<K, V> {
    private final Object2ObjectLinkedOpenHashMap<K, V> map;
    private final int capacity;
    
    public V get(K key) {
        V value = map.getAndMoveToFirst(key);
        return value;
    }
    
    public V put(K key, V value) {
        if (map.size() >= capacity && !map.containsKey(key)) {
            map.removeLast();  // 移除最久未使用
        }
        map.putAndMoveToFirst(key, value);
        return value;
    }
}

// 使用
LRUCache<String, GTRecipe> cache = new LRUCache<>(256);
```

---

### 4.2 数学与物理计算

#### OverclockCalculator - 超频计算
```java
public class OverclockCalculator {
    public static OverclockResult calculateStandard(
        GTRecipe recipe, 
        long availableVoltage,
        long recipeVoltage
    ) {
        int tierDiff = getTierDifference(availableVoltage, recipeVoltage);
        
        // 每超频1次: 时间/2, EU/t*4
        int overclocks = tierDiff;
        long duration = recipe.mDuration >> overclocks;  // 除以2^n
        long eut = recipe.mEUt << (overclocks * 2);      // 乘以4^n
        
        return new OverclockResult(duration, eut, overclocks);
    }
    
    // 完美超频 (无惩罚)
    public static OverclockResult calculatePerfect(
        GTRecipe recipe, long voltage
    ) {
        int overclocks = getTierDifference(voltage, recipe.mEUt);
        long duration = recipe.mDuration >> (overclocks * 2);  // 除以4^n
        long eut = recipe.mEUt << overclocks;                  // 乘以2^n
        return new OverclockResult(duration, eut, overclocks);
    }
}
```

#### GodforgeMath - 复杂计算引擎
```java
public class GodforgeMath {
    // 燃料消耗计算
    public static long calculateFuelConsumption(
        long baseConsumption,
        int fuelFactor,
        boolean hasUpgrade
    ) {
        double multiplier = Math.pow(1.5, fuelFactor);
        if (hasUpgrade) multiplier *= 0.8;  // 20%折扣
        return (long)(baseConsumption * multiplier);
    }
    
    // 并行数计算
    public static int calculateMaxParallel(int modules) {
        // 基础64, 每个模块增加
        return 64 + modules * 64;  // 最大1024
    }
    
    // 热量惩罚
    public static double calculateHeatPenalty(int currentHeat, int maxHeat) {
        if (currentHeat > maxHeat) {
            double ratio = (double)currentHeat / maxHeat;
            return Math.pow(0.85, ratio - 1);  // 指数衰减
        }
        return 1.0;
    }
}
```

---

### 4.3 图论与网络算法

#### 管道网络拓扑
```java
public class Node {
    public final int x, y, z, dim;
    public final Node[] neighbors = new Node[6];  // 6个方向
    
    // DFS遍历网络
    public void traverse(Consumer<Node> visitor, Set<Node> visited) {
        if (!visited.add(this)) return;
        visitor.accept(this);
        
        for (Node neighbor : neighbors) {
            if (neighbor != null) {
                neighbor.traverse(visitor, visited);
            }
        }
    }
}

// 使用
Set<Node> network = new HashSet<>();
rootNode.traverse(node -> {
    network.add(node);
    // 处理每个节点
}, new HashSet<>());
```

---

## 扩展点与API

### 5.1 材料系统扩展

**Materials枚举**:
```java
// 定义新材料
public static Materials MyMaterial = new MaterialBuilder(980, "mymaterial")
    .addDustItems()
    .addMetalItems()
    .setRGBA(100, 150, 200, 255)
    .setMeltingPoint(1500)
    .setBlastFurnaceRequired(true, 1800)
    .constructMaterial();

// 为材料添加配方
GTOreDictUnificator.registerOre(
    OrePrefixes.dust, 
    Materials.MyMaterial, 
    new ItemStack(myDust)
);
```

---

### 5.2 RecipeMap扩展

```java
// 自定义RecipeMapBackend
public class CachedRecipeBackend extends RecipeMapBackend {
    private final Map<Integer, GTRecipe> customCache = new HashMap<>();
    
    @Override
    protected GTRecipe doFindRecipe(
        ItemStack[] items, 
        FluidStack[] fluids
    ) {
        int hash = calculateCustomHash(items, fluids);
        return customCache.computeIfAbsent(hash, 
            k -> super.doFindRecipe(items, fluids));
    }
}

// 使用自定义Backend
RecipeMap<CachedRecipeBackend> map = RecipeMapBuilder
    .of("cached.recipes", CachedRecipeBackend::new)
    .build();
```

---

### 5.3 Multiblock扩展

```java
// 添加自定义验证
@Override
public boolean checkStructure() {
    if (!super.checkStructure()) {
        return false;
    }
    
    // 自定义检查
    if (getEnergyHatches().size() < 2) {
        errorMessage = "需要至少2个能量舱口";
        return false;
    }
    
    return true;
}

// 添加自定义逻辑
@Override
public boolean onRunningTick(ItemStack stack) {
    boolean result = super.onRunningTick(stack);
    
    // 每100tick执行
    if (mProgresstime % 100 == 0) {
        doCustomAction();
    }
    
    return result;
}
```

---

## 实战代码示例

### 6.1 完整的配方驱动单方块机器

```java
public class MyCompressor extends MTEBasicMachineWithRecipe {
    public MyCompressor(int id) {
        super(
            id,
            "basicmachine.compressor.my",
            "My Compressor",
            2,  // LV tier
            "Compresses items with style",
            RecipeMaps.compressorRecipes,
            1, 1,     // 1 input, 1 output
            0,        // 无流体
            SoundResource.IC2_MACHINES_COMPRESSOR_OP
        );
    }
    
    @Override
    public MetaTileEntity newMetaEntity(IGregTechTileEntity gte) {
        return new MyCompressor(mID);
    }
    
    @Override
    public ITexture[] getTexture(
        IGregTechTileEntity baseMetaTileEntity,
        ForgeDirection side,
        ForgeDirection facing,
        int colorIndex,
        boolean active,
        boolean redstoneLevel
    ) {
        if (side == facing) {
            return new ITexture[]{
                Textures.BlockIcons.MACHINE_CASINGS[mTier][colorIndex + 1],
                active ? Textures.BlockIcons.OVERLAY_FRONT_COMPRESSOR_ACTIVE
                      : Textures.BlockIcons.OVERLAY_FRONT_COMPRESSOR
            };
        }
        return new ITexture[]{
            Textures.BlockIcons.MACHINE_CASINGS[mTier][colorIndex + 1]
        };
    }
}

// 注册 (在加载阶段)
new MyCompressor(900);

// 添加工作台配方
GTModHandler.addCraftingRecipe(
    ItemList.MyCompressor.get(1L),
    new Object[]{
        "PCP",
        "RMR",
        "WCW",
        'M', ItemList.Hull_LV,
        'P', OrePrefixes.piston.get(Materials.Steel),
        'C', OrePrefixes.circuit.get(Materials.Basic),
        'W', OrePrefixes.cableGt01.get(Materials.Tin),
        'R', OrePrefixes.plate.get(Materials.Bronze)
    }
);
```

---

### 6.2 完整的多方块机器

```java
public class MyProcessingPlant extends MTEMultiBlockBase 
    implements IStructureProvider<MyProcessingPlant> {
    
    private final StructureWrapper<MyProcessingPlant> wrapper = 
        new StructureWrapper<>(this);
    
    @Override
    public String[][] getDefinition() {
        return new String[][]{
            {"CCCCC", "CCCCC", "CCCCC", "CCCCC", "CCCCC"},
            {"CCCCC", "C~~~C", "C~~~C", "C~~~C", "CCCCC"},
            {"CCCCC", "C~M~C", "C~~~C", "C~~~C", "CCCCC"},
            {"CCCCC", "CCCCC", "CCCCC", "CCCCC", "CCCCC"}
        };
    }
    
    @Override
    public IStructureDefinition<MyProcessingPlant> compile(String[][] def) {
        wrapper.loadStructure();
        
        wrapper.casings.put('C', new CasingInfo<>(
            GregTechAPI.sBlockCasings1,
            10,  // 钢制外壳
            GTUITextures.CASING_STEEL_SOLID,
            (tile, world, pos) -> true
        ));
        
        wrapper.casings.put('~', new CasingInfo<>(
            Blocks.air,
            0,
            null,
            (tile, world, pos) -> world.isAirBlock(pos.x, pos.y, pos.z)
        ));
        
        // 添加舱口
        HatchElementBuilder.<MyProcessingPlant>builder()
            .atLeast(Energy, InputBus, OutputBus, InputHatch)
            .casingIndex(10)
            .dot(1)
            .buildAndChain(wrapper.structureDefinition);
        
        return wrapper.buildStructure(def);
    }
    
    @Override
    public RecipeMap<?> getRecipeMap() {
        return RecipeMaps.myPlantRecipes;
    }
    
    @Override
    public boolean checkStructure() {
        if (!super.checkStructure()) return false;
        
        // 确保至少有2个输入总线
        if (mInputBusses.size() < 2) {
            errorMessage = "需要至少2个输入总线";
            return false;
        }
        
        return true;
    }
    
    @Override
    public boolean onRunningTick(ItemStack stack) {
        // 自定义逻辑: 每秒消耗流体
        if (mProgresstime % 20 == 0) {
            FluidStack fluid = getStoredFluids()[0];
            if (fluid == null || fluid.amount < 100) {
                stopMachine();
                return false;
            }
            fluid.amount -= 100;
        }
        
        return super.onRunningTick(stack);
    }
    
    @Override
    protected MultiblockTooltipBuilder createTooltip() {
        return new MultiblockTooltipBuilder()
            .addMachineType("Processing Plant")
            .addInfo("Processes materials efficiently")
            .addInfo("Requires coolant (100mB/s)")
            .addSeparator()
            .addInfo("Structure: 5x4x5")
            .addInfo("Controller: Front center")
            .addInfo("Requires: 2+ Input Bus")
            .addInfo("Optional: Up to 16 Hatches")
            .beginStructureBlock(5, 4, 5)
            .addInputBus("Any casing", 1)
            .addOutputBus("Any casing", 1)
            .addInputHatch("Any casing", 1)
            .addOutputHatch("Any casing", 1)
            .addEnergyHatch("Any casing", 1)
            .toolTipFinisher("My Mod");
    }
}
```

---

### 6.3 使用Builder模式添加配方

```java
public class MyRecipes {
    public static void registerRecipes() {
        // 简单配方
        RecipeMaps.assemblerRecipes.recipeBuilder()
            .itemInputs(
                GTUtility.getIntegratedCircuit(1),
                GTOreDictUnificator.get(OrePrefixes.plate, Materials.Steel, 4)
            )
            .itemOutputs(new ItemStack(Items.bucket))
            .duration(100)
            .EUt(16)
            .buildAndRegister();
        
        // 带流体的配方
        RecipeMaps.chemicalReactorRecipes.recipeBuilder()
            .itemInputs(GTOreDictUnificator.get(OrePrefixes.dust, Materials.Carbon, 1))
            .fluidInputs(Materials.Oxygen.getGas(1000))
            .fluidOutputs(Materials.CarbonDioxide.getGas(1000))
            .duration(80)
            .EUt(30)
            .buildAndRegister();
        
        // 带概率输出
        RecipeMaps.centrifugeRecipes.recipeBuilder()
            .itemInputs(GTOreDictUnificator.get(OrePrefixes.dust, Materials.Redstone, 10))
            .itemOutputs(
                GTOreDictUnificator.get(OrePrefixes.dust, Materials.Silicon, 1),
                GTOreDictUnificator.get(OrePrefixes.dust, Materials.Pyrite, 3),
                GTOreDictUnificator.get(OrePrefixes.dust, Materials.Ruby, 1)
            )
            .outputChances(10000, 10000, 1000)  // 100%, 100%, 10%
            .duration(400)
            .EUt(80)
            .buildAndRegister();
        
        // 带NBT的配方
        ItemStack programmedCircuit = GTUtility.getIntegratedCircuit(24);
        RecipeMaps.assemblerRecipes.recipeBuilder()
            .itemInputs(
                programmedCircuit,
                new ItemStack(Items.diamond, 4)
            )
            .itemOutputs(new ItemStack(MyItems.advancedComponent))
            .duration(600)
            .EUt(256)
            .buildAndRegister();
    }
}
```

---

## 总结

GT5-Unofficial提供了完整的模组开发框架，包括：

✅ **工具类体系** - 160+工具类覆盖所有常用场景  
✅ **设计模式** - Builder、Factory、Singleton等经典模式  
✅ **核心系统** - Recipe、MTE、Multiblock等完整架构  
✅ **数据结构** - 高性能集合、缓存、图论算法  
✅ **扩展API** - 丰富的接口和扩展点  
✅ **实战示例** - 完整的机器实现代码  

这个知识库可以帮助AI理解GT5U的代码结构，并用于：
- 开发新的机器和多方块
- 添加自定义配方系统
- 实现新的材料和物品
- 创建自定义GUI和交互
- 优化性能和算法

---

**相关链接**:
- GT5U仓库: https://github.com/GTNewHorizons/GT5-Unofficial
- GT5U Wiki: https://gtnh.miraheze.org/
- Javadoc: (需要本地生成)

