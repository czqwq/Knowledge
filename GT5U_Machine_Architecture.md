# GT5-Unofficial 机器架构完整知识库

> **代码来源**：https://github.com/GTNewHorizons/GT5-Unofficial（本地克隆探索，`--depth=1`）  
> **严禁伪造代码，所有代码片段均来自真实源文件，标注有文件路径和行号**

---

## 目录

1. [双层架构：World端 与 MTE端](#一双层架构world端-与-mte端)
2. [电压等级系统（GTValues）](#二电压等级系统gtvalues)
3. [单方块机器基类链](#三单方块机器基类链)
4. [多方块机器基类主链](#四多方块机器基类主链)
5. [GT++ 子模块基类链](#五gt-子模块基类链)
6. [TecTech 基类链](#六tectech-基类链)
7. [GoodGenerator 子模块基类](#七goodgenerator-子模块基类)
8. [BartWorks / KubaTech / KekzTech 基类](#八bartworks--kubatech--kekztech-基类)
9. [中间层抽象基类（机器类型专用）](#九中间层抽象基类机器类型专用)
10. [Hatch（仓口）系统](#十hatch仓口系统)
11. [机器生命周期（Lifecycle）](#十一机器生命周期lifecycle)
12. [ProcessingLogic（配方处理逻辑）](#十二processinglogic配方处理逻辑)
13. [OverclockCalculator（超频计算器）](#十三overclockCalculator超频计算器)
14. [完整继承树](#十四完整继承树)

---

## 一、双层架构：World端 与 MTE端

GT5U 的机器采用**双层设计**：每一个机器方块在世界中对应一个 `BaseMetaTileEntity`（World 端，Minecraft TileEntity 子类），其内部持有一个 `MetaTileEntity`（MTE 端，机器逻辑实体）。这两者通过 `IGregTechTileEntity` 接口关联。

### 1.1 World 端（TileEntity 侧）继承链

```
net.minecraft.tileentity.TileEntity
  └── BaseTileEntity
        └── CoverableTileEntity
              └── CommonBaseMetaTileEntity
                    └── BaseMetaTileEntity  (implements IGregTechTileEntity)
```

**`BaseTileEntity`**  
- 文件：`src/main/java/gregtech/api/metatileentity/BaseTileEntity.java`  
- 第 74 行：
```java
public abstract class BaseTileEntity extends TileEntity
    implements IHasWorldObjectAndCoords, IIC2Enet, IGTEnet, ...
```
提供坐标访问、IC2 能量网络接口等基础功能。

**`CoverableTileEntity`**  
- 文件：`src/main/java/gregtech/api/metatileentity/CoverableTileEntity.java`  
- 第 62 行：
```java
public abstract class CoverableTileEntity extends BaseTileEntity
    implements ICoverable, IGregtechWailaProvider {
```
添加**盖板（Cover）系统**支持，以及 Waila 信息提供接口。

**`CommonBaseMetaTileEntity`**  
- 文件：`src/main/java/gregtech/api/metatileentity/CommonBaseMetaTileEntity.java`  
- 第 36 行：
```java
public abstract class CommonBaseMetaTileEntity extends CoverableTileEntity
    implements IGregTechTileEntity {
```
实现 `IGregTechTileEntity` 大多数接口方法（活动状态、颜色、朝向、能量存储等）。

**`BaseMetaTileEntity`**（最终实体类）  
- 文件：`src/main/java/gregtech/api/metatileentity/BaseMetaTileEntity.java`  
- 第 96–97 行：
```java
public class BaseMetaTileEntity extends CommonBaseMetaTileEntity
    implements IGregTechTileEntity, IActionHost, IGridProxyable,
               IAlignmentProvider, IConstructableProvider, ...
```
- 持有字段 `mStoredEnergy`（long，内部 EU 储量）和 `mStoredSteam`（long，蒸汽储量）。  
- 持有指向 `MetaTileEntity` 的引用，通过 `getMetaTileEntity()` / `setMetaTileEntity()` 访问。  
- 每个世界中的机器方块，其 TileEntity 实例均为 `BaseMetaTileEntity`，而具体机器逻辑由其内部 MTE 实现。

---

### 1.2 MTE 端（MetaTileEntity 侧）继承链

```
CommonMetaTileEntity  (implements IMetaTileEntity)
  └── MetaTileEntity
        ├── MTETieredMachineBlock → MTEBasicTank → MTEHatch, MTEBasicMachine, ...
        └── MTEMultiBlockBase → ... (多方块)
```

**`CommonMetaTileEntity`**  
- 文件：`src/main/java/gregtech/api/metatileentity/CommonMetaTileEntity.java`  
- 第 61 行：
```java
public abstract class CommonMetaTileEntity implements IMetaTileEntity {
```
持有 `mInventory: ItemStack[]`（物品槽数组）、颜色（`mColor`）等最基础数据，以及 `mName`。

**`MetaTileEntity`**（MTE 根抽象类）  
- 文件：`src/main/java/gregtech/api/metatileentity/MetaTileEntity.java`  
- 第 67 行：
```java
public abstract class MetaTileEntity extends CommonMetaTileEntity
    implements ICraftingIconProvider {
```
- 持有 `mBaseMetaTileEntity: IGregTechTileEntity`（对应 World 端），通过 `getBaseMetaTileEntity()` 获取。  
- 定义了机器的能量属性方法（全部有默认实现，子类按需重写）：

```java
// 是否消耗 EU
public boolean isEnetInput()  { return false; }
// 是否输出 EU
public boolean isEnetOutput() { return false; }
// 是否蒸汽驱动
public boolean isSteampowered() { return false; }
// EU 容量
public long maxEUStore()  { return 0; }
// 每 tick 最大输入 EU
public long maxEUInput()  { return 0; }
// 每 tick 最大输出 EU
public long maxEUOutput() { return 0; }
// 最大输入安培数
public long maxAmperesIn()  { return 1; }
// 最大输出安培数
public long maxAmperesOut() { return 1; }
```

---

## 二、电压等级系统（GTValues）

所有机器的电压等级均来自 `GTValues.V[]` 和 `GTValues.VN[]`。

- 文件：`src/main/java/gregtech/api/enums/GTValues.java`

**电压数组**（第 121 行）：
```java
public static final long[] V = new long[] {
    8L,              // 0  ULV
    32L,             // 1  LV
    128L,            // 2  MV
    512L,            // 3  HV
    2048L,           // 4  EV
    8192L,           // 5  IV
    32_768L,         // 6  LuV
    131_072L,        // 7  ZPM
    524_288L,        // 8  UV
    2_097_152L,      // 9  UHV
    8_388_608L,      // 10 UEV
    33_554_432L,     // 11 UIV
    134_217_728L,    // 12 UMV
    536_870_912L,    // 13 UXV
    Integer.MAX_VALUE - 7, // 14 MAX
    8_589_934_592L   // 15 MAX+（错误等级，防止越界）
};
```

**等级名称数组**（第 163 行）：
```java
public static final String[] VN = new String[] {
    "ULV", "LV", "MV", "HV", "EV", "IV",
    "LuV", "ZPM", "UV", "UHV", "UEV", "UIV",
    "UMV", "UXV", "MAX", "MAX+"
};
```

`MTETieredMachineBlock`（及所有 Hatch）中 `mTier` 字段即为上述数组下标，`V[mTier]` 即为该等级的额定电压（EU/t）。

---

## 三、单方块机器基类链

```
MetaTileEntity
  └── MTETieredMachineBlock
        └── MTEBasicTank
              ├── MTEHatch              ← 所有仓口根类
              ├── MTEBasicMachine       ← 单方块机器根类
              │     ├── MTEBasicMachineBronze   ← 蒸汽青铜机器
              │     │     └── MTEBasicMachineSteel ← 蒸汽钢铁机器
              │     └── MTEBasicMachineWithRecipe ← 通用配方机器
              └── MTEBasicGenerator     ← 发电机根类
```

### 3.1 MTETieredMachineBlock

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTETieredMachineBlock.java`  
- 第 17 行：
```java
public abstract class MTETieredMachineBlock extends MetaTileEntity {
```
核心字段（第 22 行）：
```java
public final byte mTier;
```
`mTier` 为 0~14，对应 `GTValues.VN` 等级。所有带等级的机器（包括所有仓口）均继承此类。

### 3.2 MTEBasicTank

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEBasicTank.java`  
- 第 38 行：
```java
public abstract class MTEBasicTank extends MTETieredMachineBlock
    implements IAddUIWidgets {
```
提供流体槽（`IFluidTank`）功能，是所有需要存储流体的单方块机器、发电机和 Hatch 的共同基类。

### 3.3 MTEBasicMachine（单方块电力机器基类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java`  
- 第 112 行：
```java
public abstract class MTEBasicMachine extends MTEBasicTank
    implements RecipeMapWorkable, IConfigurationCircuitSupport,
               IOverclockDescriptionProvider, IAddGregtechLogo, IAddUIWidgets {
```
核心字段（第 124、130 行）：
```java
public final int mInputSlotCount, mAmperage;
public int mProgresstime = 0, mMaxProgresstime = 0, mEUt = 0, mOutputBlocked = 0;
```
`checkRecipe()` 返回值常量（第 117–119 行）：
```java
protected static final int DID_NOT_FIND_RECIPE = 0,
    FOUND_RECIPE_BUT_DID_NOT_MEET_REQUIREMENTS = 1,
    FOUND_AND_SUCCESSFULLY_USED_RECIPE = 2;
```

### 3.4 MTEBasicMachineBronze（蒸汽青铜机器）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachineBronze.java`  
- 第 50 行：
```java
public abstract class MTEBasicMachineBronze extends MTEBasicMachine {
```
重写蒸汽标记（第 123 行）：
```java
@Override
public boolean isSteampowered() { return true; }
```
蒸汽容量（第 136 行等价行）：
```java
@Override
public long maxSteamStore() { return 16000; }
```

### 3.5 MTEBasicMachineSteel（蒸汽钢铁机器）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachineSteel.java`  
- 第 25 行：
```java
public abstract class MTEBasicMachineSteel extends MTEBasicMachineBronze
    implements IGetTitleColor {
```
在青铜基础上调整 GUI 颜色主题，对应 Steel 风格 UI。

### 3.6 MTEBasicGenerator（发电机基类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEBasicGenerator.java`  
- 第 29 行：
```java
public abstract class MTEBasicGenerator extends MTEBasicTank
    implements RecipeMapWorkable {
```
消耗燃料配方（`RecipeMap`）输出 EU，是所有单方块发电机的抽象基类。

---

## 四、多方块机器基类主链

```
MetaTileEntity
  └── MTEMultiBlockBase
        └── MTETooltipMultiBlockBase
              └── MTEEnhancedMultiBlockBase<T>   (引入 StructureLib)
                    └── MTEExtendedPowerMultiBlockBase<T>  (long EU 支持)
```

### 4.1 MTEMultiBlockBase（多方块机器根类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java`  
- 第 165–167 行：
```java
public abstract class MTEMultiBlockBase extends MetaTileEntity
    implements IControllerWithOptionalFeatures, IAddGregtechLogo,
               IGuiHolder<PosGuiData>, IAddUIWidgets, IBindPlayerInventoryUI {
```

#### 核心字段（第 170–232 行，全部来自源码）

```java
// 维护状态（6 种工具各对应一个 boolean）
public boolean mMachine = false, mWrench = false, mScrewdriver = false,
    mSoftMallet = false, mHardHammer = false, mSolderingTool = false,
    mCrowbar = false, mRunningOnLoad = false;
public boolean mStructureChanged = false;

// 核心运行计数器
public int mPollution = 0, mProgresstime = 0, mMaxProgresstime = 0,
    mEUt = 0, mEfficiencyIncrease = 0, mStartUpCheck = 100,
    mRuntime = 0, mEfficiency = 0, lastParallel = 0;
public long recipesDone = 0;

// 延迟更新触发器
public volatile boolean mUpdated = false;
public int mUpdate = 0;

// 配方输出缓冲（配方完成时暂存，下一 tick 输出）
public ItemStack[] mOutputItems = null;
public FluidStack[] mOutputFluids = null;

// 机器模式（部分多方块支持多模式）
public int machineMode = 0;

// 高级特性开关
public boolean mLockedToSingleRecipe = getDefaultRecipeLockingMode();
protected boolean inputSeparation = getDefaultInputSeparationMode();
protected VoidingMode voidingMode = getDefaultVoidingMode();
protected boolean batchMode = getDefaultBatchMode() && supportsBatchMode();

// 并行控制
protected int powerPanelMaxParallel = 1;
protected boolean alwaysMaxParallel = true;
protected int maxParallel = 1;

// 仓口列表
public ArrayList<MTEHatchInput> mInputHatches = new ArrayList<>();
public ArrayList<MTEHatchOutput> mOutputHatches = new ArrayList<>();
public ArrayList<MTEHatchInputBus> mInputBusses = new ArrayList<>();
public ArrayList<MTEHatchOutputBus> mOutputBusses = new ArrayList<>();
public ArrayList<IDualInputHatch> mDualInputHatches = new ArrayList<>();   // AE2 合成输入仓
public ArrayList<ISmartInputHatch> mSmartInputHatches = new ArrayList<>(); // 快速配方匹配仓
public ArrayList<MTEHatchDynamo> mDynamoHatches = new ArrayList<>();
public ArrayList<MTEHatchMuffler> mMufflerHatches = new ArrayList<>();
public ArrayList<MTEHatchEnergy> mEnergyHatches = new ArrayList<>();
public ArrayList<MTEHatchMaintenance> mMaintenanceHatches = new ArrayList<>();

// 线圈坐标列表（EBF、ABS 等使用，存储线圈方块的 long 型世界坐标）
public LongArrayList mCoils = new LongArrayList();

// 异域能量仓（TecTech 多安培仓、激光仓等）
protected List<MTEHatch> mExoticEnergyHatches = new ArrayList<>();
protected List<MTEHatch> mExoticDynamoHatches = new ArrayList<>();

// 配方处理器（由 createProcessingLogic() 在构造时初始化，null 表示子类自行管理配方）
protected final ProcessingLogic processingLogic;

// 时间追踪（用于决定配方重检频率）
protected long mLastWorkingTick = 0, mTotalRunTime = 0;
```

#### 唯一抽象方法

第 1291 行：
```java
public abstract boolean checkMachine(IGregTechTileEntity aBaseMetaTileEntity, ItemStack aStack);
```
子类在此方法中调用 StructureLib 或手动检查结构，并将找到的 Hatch 注册到对应 List 中。

#### 重要非抽象方法（子类可覆盖）

| 方法 | 默认行为 | 子类覆盖目的 |
|------|---------|-------------|
| `getRecipeMap()` | 返回 `null` | 指定使用的配方表 |
| `createProcessingLogic()` | 返回 `null` | 创建并配置 `ProcessingLogic` 实例 |
| `setProcessingLogicPower(ProcessingLogic)` | 使用平均电压和可用安培 | 修改电压/安培参数 |
| `getMaxEfficiency(ItemStack)` | 返回 `10000`（100%） | 限制最大效率 |
| `getIdealStatus()` | 返回 `6` | 指定满维护需要几种工具 |
| `getMaxParallelRecipes()` | 返回 `1` | 指定最大并行数 |
| `getPollutionPerSecond(ItemStack)` | 返回 `0` | 指定每秒污染量 |
| `supportsBatchMode()` | 返回 `true` | 是否支持批处理模式 |
| `addToMachineList(IGregTechTileEntity, int)` | 自动分类 Hatch | 添加自定义仓口类型 |

#### `addToMachineList` 内部分类逻辑（第 2044–2095 行）

```java
public boolean addToMachineList(IGregTechTileEntity aTileEntity, int aBaseCasingIndex) {
    // ...
    if (aMetaTileEntity instanceof IDualInputHatch hatch)  return mDualInputHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchInput hatch)    return mInputHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchInputBus hatch) return mInputBusses.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchOutput hatch)   return mOutputHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchOutputBus hatch)return mOutputBusses.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchEnergy hatch)   return mEnergyHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchDynamo hatch)   return mDynamoHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchMaintenance hatch) return mMaintenanceHatches.add(hatch);
    if (aMetaTileEntity instanceof MTEHatchMuffler hatch)  return mMufflerHatches.add(hatch);
    return false;
}
```

#### 维护系统

`getRepairStatus()`（第 1396 行）= 六种工具各占 1 分（0–6）：
```java
public int getRepairStatus() {
    return (mWrench ? 1 : 0) + (mScrewdriver ? 1 : 0)
        + (mSoftMallet ? 1 : 0)  + (mHardHammer ? 1 : 0)
        + (mSolderingTool ? 1 : 0) + (mCrowbar ? 1 : 0);
}
```
`getIdealStatus()` 默认返回 `6`（需要全部维修才能满效率）。  
实际效率（`getCurrentEfficiency`）：`maxEff - (idealStatus - repairStatus) * maxEff / 10`。  
即每缺少一个工具，效率降低 `maxEff / 10`（即 10%）。

#### 能量输入计算（第 1583–1605 行）

```java
// 所有能量仓电压之和（不考虑安培）
public long getMaxInputVoltage() {
    long rVoltage = 0;
    for (MTEHatchEnergy tHatch : validMTEList(mEnergyHatches))
        rVoltage += tHatch.getBaseMetaTileEntity().getInputVoltage();
    return rVoltage;
}

// 通过 ExoticEnergyInputHelper 计算平均电压（用于 ProcessingLogic 电压参数）
public long getAverageInputVoltage() {
    return ExoticEnergyInputHelper.getAverageInputVoltageMulti(mEnergyHatches);
}

// 所有能量仓总工作安培数
public long getMaxInputAmps() {
    return ExoticEnergyInputHelper.getMaxWorkingInputAmpsMulti(mEnergyHatches);
}
```

#### 并行相关（第 2920–2940 行）

```java
// 子类覆盖此方法返回最大并行数（注：不要将此方法作为 ProcessingLogic 的 supplier）
public int getMaxParallelRecipes() { return 1; }

// 实际并行数 = min(getMaxParallelRecipes(), powerPanelMaxParallel)
// alwaysMaxParallel = true 时忽略 powerPanelMaxParallel 限制
// 应将此方法作为 ProcessingLogic.setMaxParallelSupplier 的目标
public final int getTrueParallel() {
    return Math.max(1,
        alwaysMaxParallel ? getMaxParallelRecipes()
                          : Math.min(getMaxParallelRecipes(), powerPanelMaxParallel));
}
```

---

### 4.2 MTETooltipMultiBlockBase

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTETooltipMultiBlockBase.java`  
- 声明：
```java
public abstract class MTETooltipMultiBlockBase extends MTEMultiBlockBase
    implements ISecondaryDescribable {
```
新增抽象方法：
```java
protected abstract MultiblockTooltipBuilder createTooltip();
```
将多方块的所有 Tooltip 信息（功能描述 + 结构描述）统一交由 `MultiblockTooltipBuilder` 管理，使用缓存避免重复构建。

---

### 4.3 MTEEnhancedMultiBlockBase\<T\>（StructureLib 结构检查基类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEEnhancedMultiBlockBase.java`  
- 第 51–52 行：
```java
public abstract class MTEEnhancedMultiBlockBase<T extends MTEEnhancedMultiBlockBase<T>>
    extends MTETooltipMultiBlockBase implements IAlignment, IConstructable {
```

**新增抽象方法**（第 145 行）：
```java
public abstract IStructureDefinition<T> getStructureDefinition();
```
引入 **StructureLib**（`com.gtnewhorizon.structurelib`）声明式结构检查，通过 `IStructureDefinition` 定义多方块的每一层结构布局和允许的方块类型/Hatch 类型。

**结构方向旋转/翻转**：  
持有 `mExtendedFacing: ExtendedFacing`（方向 + 旋转 + 翻转状态），允许多方块在不同朝向摆放，同步通过网络包发送给客户端。

**结构检查辅助方法**：
```java
// 检查某一段结构（piece = IStructureDefinition 中注册的片段名）
protected final boolean checkPiece(String piece, int horizontalOffset, int verticalOffset, int depthOffset)

// 生存模式自动建造
protected final int survivalBuildPiece(String piece, ItemStack trigger,
    int horizontalOffset, int verticalOffset, int depthOffset,
    int elementsBudget, ISurvivalBuildEnvironment env, boolean check)
```
其中 `horizontalOffset`、`verticalOffset`、`depthOffset` 均以控制器方块正面为基准，左右/上下/前后各方向的偏移量（可为负值）。

---

### 4.4 MTEExtendedPowerMultiBlockBase\<T\>（long EU 基类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEExtendedPowerMultiBlockBase.java`  
- 第 28–29 行：
```java
public abstract class MTEExtendedPowerMultiBlockBase<T extends MTEEnhancedMultiBlockBase<T>>
    extends MTEEnhancedMultiBlockBase<T> {
```

**核心新增字段**：
```java
public long lEUt;
```
将 `MTEMultiBlockBase.mEUt`（int，最大约 2.1G EU/t）扩展为 `lEUt`（long），支持 LuV 以上的高压机器。

**重写 `onRunningTick(ItemStack)`**（每 tick 执行）：
```java
@Override
public boolean onRunningTick(ItemStack aStack) {
    if (this.lEUt > 0) {
        addEnergyOutput((this.lEUt * mEfficiency) / 10000);
        return true;
    }
    if (this.lEUt < 0) {
        if (!drainEnergyInput(getActualEnergyUsage())) {
            stopMachine(ShutDownReasonRegistry.POWER_LOSS);
            return false;
        }
    }
    return true;
}
```
约定：`lEUt < 0` 表示**消耗** EU，`lEUt > 0` 表示**产生** EU。

**`setEnergyUsage(ProcessingLogic)`**：将 `ProcessingLogic.getCalculatedEut()` 赋给 `lEUt`（取负值，因为消耗）：
```java
@Override
protected void setEnergyUsage(ProcessingLogic processingLogic) {
    lEUt = processingLogic.getCalculatedEut();
    if (lEUt > 0) { lEUt = (-lEUt); }
}
```

**重写能量 drain**（同时支持普通和 TecTech 异域能量仓）：
```java
@Override
public boolean drainEnergyInput(long aEU) {
    return ExoticEnergyInputHelper.drainEnergy(aEU, getExoticAndNormalEnergyHatchList());
}

public List<MTEHatch> getExoticAndNormalEnergyHatchList() {
    List<MTEHatch> tHatches = new ArrayList<>();
    tHatches.addAll(filterValidMTEs(mExoticEnergyHatches));
    tHatches.addAll(filterValidMTEs(mEnergyHatches));
    return tHatches;
}
```

**重写电压/安培计算**（同样加入异域能量仓）：  
`getMaxInputVoltage()`、`getAverageInputVoltage()`、`getMaxInputAmps()`、`getMaxInputEu()` 均通过 `ExoticEnergyInputHelper.getXxxMulti(getExoticAndNormalEnergyHatchList())` 计算。

---

## 五、GT++ 子模块基类链

```
MTEExtendedPowerMultiBlockBase<T>
  └── GTPPMultiBlockBase<T>
        └── MTESteamMultiBase<T>     ← 蒸汽多方块
        └── MTELargerTurbineBase     ← 大型汽轮机（GT++）
```

### 5.1 GTPPMultiBlockBase\<T\>

- 文件：`src/main/java/gtPlusPlus/xmod/gregtech/api/metatileentity/implementations/base/GTPPMultiBlockBase.java`  
- 第 96–97 行：
```java
public abstract class GTPPMultiBlockBase<T extends MTEExtendedPowerMultiBlockBase<T>>
    extends MTEExtendedPowerMultiBlockBase<T> {
```

**新增字段**：
```java
public GTRecipe mLastRecipe;   // 最后匹配到的配方（调试/显示用）

public ArrayList<MTEHatchAirIntake> mAirIntakes = new ArrayList<>();       // 空气进气仓
public ArrayList<MTEHatchInputBattery> mChargeHatches = new ArrayList<>(); // 充能仓（电池输入）
public ArrayList<MTEHatchOutputBattery> mDischargeHatches = new ArrayList<>(); // 放能仓（电池输出）
public ArrayList<MTEHatch> mAllEnergyHatches = new ArrayList<>();  // 全部能量仓汇总
public ArrayList<MTEHatch> mAllDynamoHatches = new ArrayList<>();  // 全部发电仓汇总
```

**新增抽象方法**（第 128 行）：
```java
public abstract String getMachineType();
```
返回机器类型标识字符串，用于 tooltip 和 Waila 信息显示。

提供 `getStoredEnergyInAllEnergyHatches()` 等辅助方法，以及 GT++ 风格的并行、调试功能实现。

---

### 5.2 MTESteamMultiBase\<T\>（GT++ 蒸汽多方块基类）

- 文件：`src/main/java/gtPlusPlus/xmod/gregtech/api/metatileentity/implementations/base/MTESteamMultiBase.java`  
- 第 68 行：
```java
public abstract class MTESteamMultiBase<T extends MTESteamMultiBase<T>>
    extends GTPPMultiBlockBase<T> implements IOverclockDescriptionProvider {
```

**专用蒸汽仓口列表**：
```java
public ArrayList<MTEHatchSteamBusInput> mSteamInputs = new ArrayList<>();
public ArrayList<MTEHatchSteamBusOutput> mSteamOutputs = new ArrayList<>();
public ArrayList<MTEHatchCustomFluidBase> mSteamInputFluids = new ArrayList<>();
```

**新增抽象方法**：
```java
// 配方等级（决定可处理哪个蒸汽配方层级，传给 ProcessingLogic.setAvailableVoltage(V[getTierRecipes()])）
public abstract int getTierRecipes();

// GUI 主题等级：1 = 青铜风格，2 = 钢铁风格
public abstract int getThemeTier();
```

**`createProcessingLogic()` 实现**（第 103 行）：
```java
@Override
protected ProcessingLogic createProcessingLogic() {
    return new ProcessingLogic().setMaxParallelSupplier(this::getTrueParallel);
}
```

**`setProcessingLogicPower(ProcessingLogic)` 实现**（第 108–112 行）：
```java
@Override
protected void setProcessingLogicPower(ProcessingLogic logic) {
    logic.setAvailableVoltage(V[getTierRecipes()]);
    logic.setAvailableAmperage(getMaxParallelRecipes());
    logic.setAmperageOC(false);   // 蒸汽机器不允许安培超频
    logic.setMaxTierSkips(0);     // 不允许跳级超频
}
```

**`onRunningTick(ItemStack)`**（蒸汽消耗替代 EU）：
```java
@Override
public boolean onRunningTick(ItemStack aStack) {
    if (lEUt < 0) {
        long aSteamVal = ((-lEUt * 10000) / Math.max(1000, mEfficiency));
        if (!tryConsumeSteam((int) aSteamVal)) {
            stopMachine(ShutDownReasonRegistry.POWER_LOSS);
            return false;
        }
    }
    return true;
}
```

**维护检查默认禁用**（第 520 行左右）：
```java
@Override
public boolean getDefaultHasMaintenanceChecks() { return false; }
```

蒸汽机器不需要维修工具，结构完整即可正常运行。

**高压提示常量**（第 82–86 行）：
```java
protected static final String HIGH_PRESSURE_TOOLTIP_NOTICE =
    "High Pressure Doubles " + EnumChatFormatting.GREEN + "Speed"
    + EnumChatFormatting.GRAY + " and "
    + EnumChatFormatting.AQUA + "Steam Usage";
```

**使用此基类的具体机器**（均在 `gtPlusPlus/.../multi/steam/` 包下）：  
`MTESteamMacerator`、`MTESteamCentrifuge`、`MTESteamCompressor`、`MTESteamFurnaceMulti`、  
`MTESteamWasher`、`MTESteamForgeHammer`、`MTESteamAlloySmelter`、`MTESteamMixer`、  
`MTESteamWaterPump`——均为 `implements ISurvivalConstructable`。

---

### 5.3 MTELargerTurbineBase（GT++ 大型汽轮机基类）

- 文件：`src/main/java/gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/turbines/MTELargerTurbineBase.java`  
- 声明：
```java
public abstract class MTELargerTurbineBase extends GTPPMultiBlockBase<MTELargerTurbineBase>
```
GT++ 专用大型（比原版大型汽轮机更大）蒸汽/等离子/气体/超临界汽轮机的抽象基类，重写 `getMaxParallelRecipes()`（第 538 行）等方法。

---

## 六、TecTech 基类链

```
MTEExtendedPowerMultiBlockBase<TTMultiblockBase>
  └── TTMultiblockBase
        └── MTEBaseModule        ← ForgeOfGods 模块
        └── MTEQuantumComputer, MTEForgeOfGods, MTEEyeOfHarmony, ...（具体机器）
```

### 6.1 TTMultiblockBase

- 文件：`src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java`  
- 第 117–118 行：
```java
public abstract class TTMultiblockBase
    extends MTEExtendedPowerMultiBlockBase<TTMultiblockBase>
    implements IAlignment, IBindPlayerInventoryUI {
```

**唯一新增抽象方法**（第 235 行）：
```java
public abstract IStructureDefinition<? extends TTMultiblockBase> getStructure_EM();
```

**`getStructureDefinition()` 的桥接**（第 243 行）：
```java
@Override
public IStructureDefinition<TTMultiblockBase> getStructureDefinition() {
    return getStructure_EM_Internal();
}
```
即 TecTech 将原有的 `getStructureDefinition()` 桥接到自己的 `getStructure_EM()` 方法，子类只需实现 `getStructure_EM()`。

**`checkMachine()` 的桥接**（第 814–819 行）：
```java
@Override
public final boolean checkMachine(IGregTechTileEntity iGregTechTileEntity, ItemStack itemStack) {
    mMachine = checkMachine_EM(iGregTechTileEntity, itemStack);
    onStructureCheckFinished();
    return mMachine;
}
```
子类覆盖 `checkMachine_EM()`（默认返回 `false`）而非 `checkMachine()`。

**`checkProcessing()` 的桥接**（第 837–843 行）：
```java
@Override
public final CheckRecipeResult checkProcessing() {
    hatchesStatusUpdate_EM();
    CheckRecipeResult result = checkProcessing_EM();
    hatchesStatusUpdate_EM();
    return result;
}
```
子类覆盖 `checkProcessing_EM()`（默认调用 `super.checkProcessing()` 即 ProcessingLogic 路径）。

**`hatchesStatusUpdate_EM()`**（第 847 行）：更新 TecTech 数据参数系统（Parameters），维护 `eUncertainHatches` 和 LED 状态指示灯。

**`outputAfterRecipe_EM()`**：空实现，供子类在配方成功完成后输出 TecTech 专用数据（如量子数据包）。

**TecTech 专属 Hatch 注册辅助方法**（第 1952–1990 行）：
```java
// 注册经典 GT 仓口（标准能量仓 + TT 多安培仓）
protected static <T extends TTMultiblockBase> IStructureElement<T>
    classicHatches(int casingIndex, int dot, ...)

// 注册所有类型仓口
protected static <T extends TTMultiblockBase> IStructureElement<T>
    allHatches(int casingIndex, int dot, ...)
```

---

## 七、GoodGenerator 子模块基类

### 7.1 MTETooltipMultiBlockBaseEM（GoodGenerator TecTech 风格基类）

- 文件：`src/main/java/goodgenerator/blocks/tileEntity/base/MTETooltipMultiBlockBaseEM.java`  
- 第 10 行：
```java
public abstract class MTETooltipMultiBlockBaseEM extends TTMultiblockBase
    implements ISecondaryDescribable {
```
在 `TTMultiblockBase` 基础上增加了 `MultiblockTooltipBuilder` 双页 Tooltip（按 Shift 可切换结构信息）。

**使用此基类的具体机器**：  
`MTELargeFusionComputer`、`MTECoolantTower`、`MTEFuelRefineFactory`、`MTEYottaFluidTank`、  
`MTEMultiNqGenerator`、`MTENeutronActivator`、`MTEExtremeHeatExchanger`、  
`MTEUniversalChemicalFuelEngine`、`MTELargeEssentiaSmeltery`。

### 7.2 MTELargeFusionComputer（GoodGenerator 大型聚变基类）

- 文件：`src/main/java/goodgenerator/blocks/tileEntity/base/MTELargeFusionComputer.java`  
- 第 78–79 行：
```java
public abstract class MTELargeFusionComputer extends MTETooltipMultiBlockBaseEM
    implements IConstructable, ISurvivalConstructable, IOverclockDescriptionProvider {
```
子类：`MTELargeFusionComputer1/2/3`（继承本类），`MTELargeFusionComputer4/5`（继承 `MTELargeFusionComputerPP`）。

### 7.3 MTELargeTurbineBase（GoodGenerator 大型汽轮机基类）

- 文件：`src/main/java/goodgenerator/blocks/tileEntity/base/MTELargeTurbineBase.java`  
- 第 49–50 行：
```java
public abstract class MTELargeTurbineBase extends MTEEnhancedMultiBlockBase<MTELargeTurbineBase>
    implements ISurvivalConstructable, INEIPreviewModifier {
```
注意：GoodGenerator 的大型汽轮机**直接继承 `MTEEnhancedMultiBlockBase`**（不走 TecTech 路线）。  
子类：`MTESupercriticalFluidTurbine`。

---

## 八、BartWorks / KubaTech / KekzTech 基类

### 8.1 MegaMultiBlockBase\<T\>（BartWorks 超级多方块基类）

- 文件：`src/main/java/bartworks/common/tileentities/multis/mega/MegaMultiBlockBase.java`  
- 第 27 行：
```java
public abstract class MegaMultiBlockBase<T extends MegaMultiBlockBase<T>>
    extends MTEExtendedPowerMultiBlockBase<T> {
```
BartWorks Mega 系列（超大型）多方块的基类，直接继承 `MTEExtendedPowerMultiBlockBase`。  
内部定义了 `StructureElementAirNoHint<T>` 等辅助内类用于结构检查中的空气位占位。  
子类：`MTEMegaBlastFurnace`、`MTEMegaVacuumFreezer`、`MTEMegaOilCracker`、`MTEMegaDistillTower`、`MTEMegaChemicalReactorLegacy`。

### 8.2 KubaTechGTMultiBlockBase\<T\>（KubaTech 多方块基类）

- 文件：`src/main/java/kubatech/api/implementations/KubaTechGTMultiBlockBase.java`  
- 第 71–72 行：
```java
public abstract class KubaTechGTMultiBlockBase<T extends MTEExtendedPowerMultiBlockBase<T>>
    extends MTEExtendedPowerMultiBlockBase<T> {
```
提供 KubaTech 专用 ModularUI 界面构建器（`createKTMetaTileEntityUI`）和相关接口实现。  
子类：`MTEMegaIndustrialApiary`、`MTEExtremeIndustrialGreenhouse`、`MTEHighTempGasCooledReactor`、`MTEDEFusionCrafter`、`MTEExtremeEntityCrusher`。

### 8.3 KekzTech（无专用基类）

KekzTech 的多方块机器（`MTETankTFFT`、`MTELapotronicSuperCapacitor`、`MTESOFuelCellMK1/2`）直接继承 `TTMultiblockBase` 或 `MTEExtendedPowerMultiBlockBase`，无额外封装基类。

---

## 九、中间层抽象基类（机器类型专用）

这些类处于继承链中间，为同类型机器提取公共逻辑，子类无需重复实现。

### 9.1 MTEAbstractMultiFurnace\<T\>（多方块炉公共基类）

- 文件：`src/main/java/gregtech/common/tileentities/machines/multi/MTEAbstractMultiFurnace.java`  
- 声明：
```java
public abstract class MTEAbstractMultiFurnace<T extends MTEAbstractMultiFurnace<T>>
    extends MTEExtendedPowerMultiBlockBase<T> {
```
唯一新增内容：管理线圈等级（`HeatingCoilLevel mCoilLevel`）：
```java
private HeatingCoilLevel mCoilLevel;

public HeatingCoilLevel getCoilLevel() { return mCoilLevel; }
public void setCoilLevel(HeatingCoilLevel aCoilLevel) { mCoilLevel = aCoilLevel; }
```
子类：`MTEElectricBlastFurnace`（电弧炉）、`MTEMultiFurnace`（大熔炉）。

### 9.2 MTELargeBoiler（大型锅炉抽象基类）

- 文件：`src/main/java/gregtech/common/tileentities/machines/multi/MTELargeBoiler.java`  
- 第 61–62 行：
```java
public abstract class MTELargeBoiler extends MTEEnhancedMultiBlockBase<MTELargeBoiler>
    implements ISurvivalConstructable {
```
子类：`MTELargeBoilerBronze`、`MTELargeBoilerSteel`、`MTELargeBoilerTitanium`、`MTELargeBoilerTungstenSteel`。

### 9.3 MTELargeTurbine（大型汽轮机抽象基类）

- 文件：`src/main/java/gregtech/common/tileentities/machines/multi/MTELargeTurbine.java`  
- 第 62–63 行：
```java
public abstract class MTELargeTurbine extends MTEEnhancedMultiBlockBase<MTELargeTurbine>
    implements ISurvivalConstructable, INEIPreviewModifier {
```
子类：`MTELargeTurbineSteam`、`MTELargeTurbineGas`、`MTELargeTurbineHPSteam`、`MTELargeTurbinePlasma`。

### 9.4 MTEFusionComputer（聚变反应堆抽象基类）

- 文件：`src/main/java/gregtech/common/tileentities/machines/multi/MTEFusionComputer.java`  
- 第 84–85 行：
```java
public abstract class MTEFusionComputer extends MTEEnhancedMultiBlockBase<MTEFusionComputer>
    implements ISurvivalConstructable, IAddUIWidgets, IOverclockDescriptionProvider {
```
子类：`MTEFusionComputer1`、`MTEFusionComputer2`、`MTEFusionComputer3`；  
GT++ 扩展子类：`MTEAdvFusionMk4`、`MTEAdvFusionMk5`（在 `gtPlusPlus` 包下，继承 `MTEFusionComputer`）。

### 9.5 MTEDrillerBase（钻机抽象基类）

- 文件：`src/main/java/gregtech/common/tileentities/machines/multi/MTEDrillerBase.java`  
- 第 86–87 行：
```java
public abstract class MTEDrillerBase extends MTEEnhancedMultiBlockBase<MTEDrillerBase>
    implements IChunkLoader, ISurvivalConstructable {
```
子类：`MTEOilDrillBase`（抽象，再派生出 `MTEOilDrill2/3/4/Infinite`）、`MTEConcreteBackfillerBase`（抽象，再派生出具体回填钻机）、`MTEDeepEarthHeatingPump`。

### 9.6 MTEBaseModule（TecTech ForgeOfGods 模块基类）

- 文件：`src/main/java/tectech/thing/metaTileEntity/multi/MTEBaseModule.java`  
- 声明：
```java
public abstract class MTEBaseModule extends TTMultiblockBase
    implements IConstructable, ISurvivalConstructable {
```
ForgeOfGods（神锻炉）的各加工模块基类。子类：`MTEMoltenModule`、`MTEPlasmaModule`、`MTESmeltingModule`、`MTEExoticModule`。

---

## 十、Hatch（仓口）系统

### 10.1 MTEHatch（仓口根抽象类）

- 文件：`src/main/java/gregtech/api/metatileentity/implementations/MTEHatch.java`  
- 第 15 行：
```java
public abstract class MTEHatch extends MTEBasicTank implements ICraftingIconProvider {
```
所有仓口的根类，继承 `MTEBasicTank`（即具有 `mTier` 字段和流体槽）。  
提供 `updateTexture(int aBaseCasingIndex)` 将仓口外观贴图同步为对应多方块的外壳贴图。

---

### 10.2 能量类仓口

| 仓口类 | 继承自 | 文件路径 | 说明 |
|--------|--------|----------|------|
| `MTEHatchEnergy` | `MTEHatch` | `gregtech/.../MTEHatchEnergy.java` | 标准能量输入仓，`maxEUInput()=V[mTier]`，`maxAmperesIn()=2`（工作 1A） |
| `MTEHatchDynamo` | `MTEHatch` | `gregtech/.../MTEHatchDynamo.java` | 标准能量输出仓，`maxEUOutput()=V[mTier]` |
| `MTEHatchDynamoBuffer` | `MTEHatchDynamo` | `gregtech/.../MTEHatchDynamoBuffer.java` | 带缓冲的发电仓（`maxEUStore` 更大） |
| `MTEHatchEnergyMulti` | `MTEHatch` | `tectech/.../MTEHatchEnergyMulti.java` | TecTech 多安培能量输入仓，持有 `int Amperes` 字段，`maxWorkingAmperesIn()=Amperes` |
| `MTEHatchDynamoMulti` | `MTEHatch` | `tectech/.../MTEHatchDynamoMulti.java` | TecTech 多安培能量输出仓 |
| `MTEHatchEnergyTunnel` | `MTEHatchEnergyMulti` | `tectech/.../MTEHatchEnergyTunnel.java` | 激光能量隧道（实现 `IConnectsToEnergyTunnel`） |
| `MTEHatchDynamoTunnel` | `MTEHatchDynamoMulti` | `tectech/.../MTEHatchDynamoTunnel.java` | 激光发电隧道 |
| `MTEWirelessEnergy` | `MTEHatchEnergy` | `gregtech/.../MTEWirelessEnergy.java` | 无线能量输入仓（EU 通过无线网络传输） |
| `MTEHatchWirelessMulti` | `MTEHatchEnergyMulti` | `tectech/.../MTEHatchWirelessMulti.java` | TecTech 无线多安培能量输入仓 |
| `MTEHatchWirelessDynamoMulti` | `MTEHatchDynamoMulti` | `tectech/.../MTEHatchWirelessDynamoMulti.java` | TecTech 无线多安培能量输出仓 |
| `MTEHatchInputBattery` | `MTEHatch` | `gregtech/.../MTEHatchInputBattery.java` | 电池输入仓（充电用） |
| `MTEHatchOutputBattery` | `MTEHatch` | `gregtech/.../MTEHatchOutputBattery.java` | 电池输出仓（放电用） |
| `MTEHatchCapacitor` | `MTEHatch` | `tectech/.../MTEHatchCapacitor.java` | 电容仓（KekzTech LSC 专用） |

**`MTEHatchEnergyMulti` 关键字段和方法**（文件第 32–140 行）：
```java
public final int maxAmperes;  // 最大安培数（固定，注册时确定）
public int Amperes;           // 当前实际安培数（可动态修改）

@Override
public long maxEUInput() { return V[mTier]; }   // 电压不变，还是 V[mTier]

@Override
public long maxAmperesIn() { return Amperes + (Amperes >> 2); }  // 容忍略高于额定安培

@Override
public long maxWorkingAmperesIn() { return Amperes; }  // 实际工作安培

@Override
public long maxEUStore() { return 512L + V[mTier] * 4L * Amperes; }
```

---

### 10.3 流体/物品 I/O 仓口

| 仓口类 | 继承自 | 说明 |
|--------|--------|------|
| `MTEHatchInput` | `MTEHatch` | 流体输入仓 |
| `MTEHatchOutput` | `MTEHatch` | 流体输出仓（impl `IFluidStore, IFluidLockable`） |
| `MTEHatchInputBus` | `MTEHatch` | 物品输入总线（impl `IConfigurationCircuitSupport`） |
| `MTEHatchOutputBus` | `MTEHatch` | 物品输出总线（impl `IOutputBus`） |
| `MTEHatchVoid` | `MTEHatchOutput` | 流体虚空仓（丢弃多余流体） |
| `MTEHatchVoidBus` | `MTEHatchOutputBus` | 物品虚空总线 |
| `MTEHatchInputBusCompressed` | `MTEHatchInputBus` | 压缩输入总线（连接 AE2 网络） |
| `MTEHatchSteamBusInput` | `MTEHatchInputBus` | GT++ 蒸汽时代物品输入总线 |
| `MTEHatchSteamBusOutput` | `MTEHatchOutputBus` | GT++ 蒸汽时代物品输出总线 |
| `MTEHatchCustomFluidBase` | `MTEHatch` | GT++ 自定义流体仓（蒸汽多方块蒸汽输入仓） |
| `MTEHatchMultiInput` | `MTEHatchInput` | 多槽流体输入仓 |
| `MTEHatchQuadrupleHumongous` | `MTEHatchMultiInput` | 超大型多槽流体输入仓 |
| `MTEHatchFluidGenerator` | `MTEHatchInput` | 流体生成仓（持续生成特定流体） |
| `MTEHatchReservoir` | `MTEHatchFluidGenerator` | 水仓（蓄水仓） |
| `MTEHatchAirIntake` | `MTEHatchFluidGenerator` | 空气进气仓 |
| `MTEYOTTAHatch` | `MTEHatch` | GoodGenerator YOTTA 流体仓（超大容量 AE2 流体存储） |
| `MTEHatchSuperBusInput` | `MTEHatchInputBus` | GT++ 超级物品输入总线 |
| `MTESuperBusOutput` | `MTEHatchOutputBus` | GT++ 超级物品输出总线 |

---

### 10.4 维护/功能仓口

| 仓口类 | 继承自 | 说明 |
|--------|--------|------|
| `MTEHatchMaintenance` | `MTEHatch` | 维护仓（存放扳手/螺丝刀/软锤/硬锤/焊枪/撬棍，影响机器效率） |
| `MTEHatchMuffler` | `MTEHatch` | 消音仓（处理污染，不装则机器不工作） |
| `MTEHatchTurbine` | `MTEHatch` | 汽轮机叶片仓（大型汽轮机专用） |
| `MTEHatchTurbineProvider` | `MTEHatchInputBus` | 汽轮机叶片供应仓（自动补充叶片） |
| `MTEHatchDataAccess` | `MTEHatch` | 数据访问仓（AE2 样式图案存储） |
| `MTEHatchMagnet` | `MTEHatch` | 磁铁仓（矿洞钻机配件） |
| `MTEHatchExtrusion` | `MTEHatchInputBus` | 挤压仓（提供挤压模具） |
| `MTEHatchChiselBus` | `MTEHatchInputBus` | 凿子总线 |
| `MTEHatchSolidifier` | `MTEHatchInput` | 固化仓（提供固化模具） |
| `MTEHatchCokeOven` | `MTEHatch` | 焦炉专用输入仓 |
| `MTEHatchMufflerAdvanced` | `MTEHatchMuffler` | 高级消音仓（实现 `IAddGregtechLogo`） |
| `MTEHatchEnergyDebug` | `MTEHatchEnergy` | 调试能量仓（无限 EU，仅开发模式） |
| `MTEHatchInputBusDebug` | `MTEHatchInputBus` | 调试物品输入总线 |

---

### 10.5 TecTech 专属仓口

| 仓口类 | 继承自 | 说明 |
|--------|--------|------|
| `MTEHatchDataConnector<T>` | `MTEHatch` | 数据管道连接抽象基类（`impl IConnectsToDataPipe`） |
| `MTEHatchDataInput` | `MTEHatchDataConnector<QuantumDataPacket>` | 量子数据输入仓 |
| `MTEHatchDataOutput` | `MTEHatchDataConnector<QuantumDataPacket>` | 量子数据输出仓 |
| `MTEHatchDataItemsInput` | `MTEHatchDataAccess` | 数据物品输入仓（impl `IConnectsToDataPipe`） |
| `MTEHatchDataItemsOutput` | `MTEHatchDataConnector<ALRecipeDataPacket>` | 数据物品输出仓（用于装配线配方数据） |
| `MTEHatchUncertainty` | `MTEHatch` | 不确定仓（ForgeOfGods 专用，提供参数不确定性） |
| `MTEHatchRack` | `MTEHatch` | 机架仓（量子计算机专用） |
| `MTEHatchObjectHolder` | `MTEHatch` | 对象持有仓（量子计算机专用） |
| `MTEHatchCreativeData` | `MTEHatchDataConnector<QuantumDataPacket>` | 创造模式数据仓（调试） |
| `MTEHatchCreativeMaintenance` | `MTEHatchMaintenance` | 创造模式维护仓（无需工具，始终满维护） |

---

## 十一、机器生命周期（Lifecycle）

多方块机器每 tick 执行的主循环定义在 `MTEMultiBlockBase.onPostTick()` 中（第 605 行起）。

### 完整流程图

```
每 tick：onPostTick(IGregTechTileEntity, long aTick)
│
├─ [Server Side]
│   ├─ mTotalRunTime++
│   ├─ if mUpdate==0 OR mStartUpCheck==0:
│   │   └─ checkStructure(true, aBaseMetaTileEntity)     ← 结构检查入口
│   │       ├─ clearHatches()                            ← 清空所有 Hatch 列表
│   │       ├─ checkMachine(aBaseMetaTileEntity, mInventory[1]) ← 子类实现
│   │       │   （在 MTEEnhancedMultiBlockBase 中调用 checkPiece() / StructureLib 扫描）
│   │       │   （识别的 Hatch 通过 addToMachineList() 注册到各 List）
│   │       └─ onStructureCheckFinished()
│   │           └─ validateStructure(errors, context)   ← 验证 Hatch 数量/类型完整性
│   │               （有误则 mMachine = false）
│   │
│   ├─ if mStartUpCheck < 0:
│   │   ├─ if mMachine:
│   │   │   ├─ checkMaintenance()                        ← 检查维护状态（6 种工具）
│   │   │   └─ if getRepairStatus() > 0:
│   │   │       └─ runMachine(aBaseMetaTileEntity, aTick)  ← 机器运行主逻辑
│   │   │           │
│   │   │           ├─ [if mMaxProgresstime > 0]
│   │   │           │   ├─ onRunningTick(mInventory[1])    ← 每 tick 消耗/产出 EU
│   │   │           │   ├─ polluteEnvironment(...)         ← 释放污染
│   │   │           │   ├─ mProgresstime++
│   │   │           │   └─ [if mProgresstime >= mMaxProgresstime]
│   │   │           │       ├─ addItemOutputs(mOutputItems)
│   │   │           │       ├─ addFluidOutputs(mOutputFluids)
│   │   │           │       ├─ outputAfterRecipe()         ← 自定义后处理（TT 数据输出等）
│   │   │           │       ├─ mProgresstime = 0; mMaxProgresstime = 0
│   │   │           │       ├─ 更新 mEfficiency
│   │   │           │       └─ if allowedToWork: checkRecipe()  ← 立即开始下一配方
│   │   │           │
│   │   │           └─ [else if mMaxProgresstime == 0 AND shouldCheckRecipeThisTick]
│   │   │               └─ checkRecipe()                   ← 定期检查配方
│   │   │
│   │   └─ if !mMachine AND allowedToWork:
│   │       └─ stopMachine(STRUCTURE_INCOMPLETE)
│   │
│   └─ aBaseMetaTileEntity.setActive(mMaxProgresstime > 0)
│
└─ [Client Side]
    └─ startActivitySound()    ← 播放运行音效循环
```

### `checkRecipe()` 内部流程（第 704–717 行）

```java
protected final boolean checkRecipe() {
    startRecipeProcessing();           // 通知 IRecipeProcessingAwareHatch 准备
    CheckRecipeResult result = checkProcessing();  // 核心：通过 ProcessingLogic 匹配配方
    // ...
    if (result.wasSuccessful()) {
        sendStartMultiBlockSoundLoop(); // 播放开始音效
    }
    this.checkRecipeResult = result;
    endRecipeProcessing();             // 通知 IRecipeProcessingAwareHatch 结束
    return this.checkRecipeResult.wasSuccessful();
}
```

### `stopMachine(ShutDownReason)` 清零操作（第 1370–1394 行）

```java
public void stopMachine(@Nonnull ShutDownReason reason) {
    mLastWorkingTick = mTotalRunTime;
    mOutputItems = null;
    mOutputFluids = null;
    mEUt = 0;
    mEfficiency = 0;
    mProgresstime = 0;
    mMaxProgresstime = 0;
    mEfficiencyIncrease = 0;
    // 设置停机原因，禁止工作，广播事件...
}
```

---

## 十二、ProcessingLogic（配方处理逻辑）

- 文件：`src/main/java/gregtech/api/logic/ProcessingLogic.java`  
- 第 35 行：`public class ProcessingLogic {`

`ProcessingLogic` 是 GT5U 现代多方块机器配方匹配和超频计算的核心类，采用流式 API（Builder 模式）配置后调用 `process()` 执行。

### 核心字段

```java
protected int maxParallel = 1;                       // 最大并行数
protected Supplier<Integer> maxParallelSupplier;     // 动态并行数提供者

protected int duration;    // 计算后的配方持续时间（tick）
// 以及 EUt、电压、安培、RecipeMap 等（通过 setter 注入）
```

### 关键 Setter（第 93–280 行，全部链式返回 ProcessingLogic）

```java
setMachine(IVoidable machine)                       // 绑定机器（用于虚空保护判断）
setInputItems(ItemStack... itemInputs)              // 设置输入物品
setInputFluids(FluidStack... fluidInputs)           // 设置输入流体
setSpecialSlotItem(ItemStack specialSlotItem)       // 设置特殊槽物品（控制器槽）
setRecipeMap(RecipeMap<?> recipeMap)                // 设置配方表
setRecipeMapSupplier(Supplier<RecipeMap<?>>)        // 动态配方表
setAvailableVoltage(long voltage)                   // 设置可用电压
setAvailableAmperage(long amperage)                 // 设置可用安培
setMaxParallel(int maxParallel)                     // 设置最大并行
setMaxParallelSupplier(Supplier<Integer> supplier)  // 动态最大并行
setEuModifier(double modifier)                      // EU 倍率（如 EBF 线圈折扣）
setSpeedBonus(double speedModifier)                 // 速度加成
setOverclock(double timeReduction, double powerIncrease)  // 自定义超频比例
setAmperageOC(boolean amperageOC)                   // 是否允许安培超频
setMaxTierSkips(int tierSkips)                      // 最大可跳过的电压等级数
setBatchSize(int size)                              // 批处理倍数
setVoidProtection(boolean, boolean)                 // 物品/流体虚空保护
```

### `process()` 核心逻辑（第 375–490 行摘要）

1. 从 `maxParallelSupplier` 获取最大并行数（若有）。
2. 通过 `RecipeMap` 搜索匹配当前输入的配方。
3. 调用内部 `OverclockCalculator` 计算超频后的 EU/t 和持续时间。
4. 通过 `ParallelHelper` 计算实际能支撑的并行数（受电压、安培、输出槽位限制）。
5. 消耗输入，设置 `mOutputItems`/`mOutputFluids`（作为输出缓冲）。
6. 将结果回写到 `lEUt`/`mEUt` 和 `mMaxProgresstime`。
7. 返回 `CheckRecipeResult`（成功/失败原因）。

### 在 MTEMultiBlockBase 中的默认 `setProcessingLogicPower` 实现（第 1108–1113 行）

```java
protected void setProcessingLogicPower(ProcessingLogic logic) {
    // 只有 1 个能量仓且非调试模式时用 1A（单安培超频，不考虑安培数）
    boolean useSingleAmp = !debugEnergyPresent
        && mEnergyHatches.size() == 1
        && mExoticEnergyHatches.isEmpty();
    logic.setAvailableVoltage(getAverageInputVoltage());
    logic.setAvailableAmperage(useSingleAmp ? 1 : getMaxInputAmps());
    logic.setAmperageOC(true);
}
```

---

## 十三、OverclockCalculator（超频计算器）

- 文件：`src/main/java/gregtech/api/util/OverclockCalculator.java`  
- 第 7 行：`public class OverclockCalculator {`

是 `ProcessingLogic` 内部使用的超频算法实现类，也可由机器直接使用（历史遗留接口）。

### 默认超频参数（第 33–57 行）

```java
protected double eutIncreasePerOC = 4;        // 每次超频 EU 倍率（默认 4x）
protected double durationDecreasePerOC = 2;   // 每次超频时间缩短（默认 /2）
protected final double durationDecreasePerHeatOC = 4;  // 热超频时间缩短（/4，仅 EBF）
protected double heatDiscountExponent = 0.95; // 热折扣指数（每 900K 超额，EU ×0.95）

protected static final int HEAT_DISCOUNT_THRESHOLD  = 900;   // 热折扣间隔温度（K）
protected static final int HEAT_OVERCLOCK_THRESHOLD = 1800;  // 热超频间隔温度（K）
```

### 标准超频计算核心逻辑（`calculateOverclock()`，第 333–410 行摘要）

```java
// 1. 计算热折扣（EBF 专用）
double recipePower = recipeEUt * parallel * eutModifier * calculateHeatDiscountMultiplier();
double machinePower = machineVoltage * (amperageOC ? machineAmperage : min(machineAmperage, parallel));

// 2. 计算可超频次数（log4 = 对数以 4 为底）
int tiersAbove = (int) GTUtility.log4((long) machinePower / max((long) recipePower, 32));
overclocks = min(maxOverclocks, tiersAbove);

// 3. 分离热超频和普通超频次数
int heatOverclocks = min(heatOC ? (machineHeat - recipeHeat) / HEAT_OVERCLOCK_THRESHOLD : 0, overclocks);
int regularOverclocks = overclocks - heatOverclocks;

// 4. 计算最终消耗和时间
calculatedConsumption = (long) ceil(recipePower * pow(eutIncreasePerOC, overclocks));
duration /= pow(durationDecreasePerHeatOC, heatOverclocks);  // 热超频 /4
duration /= pow(durationDecreasePerOC, regularOverclocks);   // 普通超频 /2
calculatedDuration = (int) max(duration, 1);                  // 最小 1 tick
```

**标准超频公式**：
- 每次超频：EU/t ×4，时间 ÷2（即总能耗翻倍，效率翻倍）
- EBF 热超频（每超额 1800K）：EU/t ×4，时间 ÷4（相当于完美超频）
- EBF 热折扣（每超额 900K）：EU ×0.95（可与热超频叠加）

**激光超频**（`laserOC = true`）：每次激光超频倍率为 `4.0 + 0.3 × n`（n 从 1 开始），时间缩短倍率仍使用 `durationDecreasePerOC`。

---

## 十四、完整继承树

```
net.minecraft.tileentity.TileEntity
  └── BaseTileEntity                                   (gregtech/api/metatileentity/)
        └── CoverableTileEntity
              └── CommonBaseMetaTileEntity
                    └── BaseMetaTileEntity             ← 世界中实际存在的 TileEntity
                          └─ 持有 → MetaTileEntity 实例

CommonMetaTileEntity                                   (gregtech/api/metatileentity/)
  └── MetaTileEntity
        │
        ├── MTETieredMachineBlock                      (gregtech/.../implementations/)
        │     └── MTEBasicTank
        │           ├── MTEHatch                       ← 所有仓口根类
        │           │     ├── MTEHatchEnergy / MTEHatchDynamo
        │           │     ├── MTEHatchEnergyMulti / MTEHatchDynamoMulti    (TecTech)
        │           │     ├── MTEHatchInput / MTEHatchOutput
        │           │     ├── MTEHatchInputBus / MTEHatchOutputBus
        │           │     ├── MTEHatchMaintenance / MTEHatchMuffler
        │           │     └── ... (其他特殊仓口)
        │           │
        │           ├── MTEBasicMachine
        │           │     ├── MTEBasicMachineBronze     ← 蒸汽青铜单方块
        │           │     │     └── MTEBasicMachineSteel ← 蒸汽钢铁单方块
        │           │     └── MTEBasicMachineWithRecipe ← 通用配方单方块
        │           │
        │           └── MTEBasicGenerator              ← 单方块发电机根类
        │
        └── MTEMultiBlockBase                          (gregtech/.../implementations/)
              └── MTETooltipMultiBlockBase
                    └── MTEEnhancedMultiBlockBase<T>   ← 引入 StructureLib
                          └── MTEExtendedPowerMultiBlockBase<T>  ← long EU
                                │
                                ├── GTPPMultiBlockBase<T>          (gtPlusPlus/...)
                                │     └── MTESteamMultiBase<T>     ← GT++ 蒸汽多方块
                                │     └── MTELargerTurbineBase     ← GT++ 大型汽轮机
                                │     └── 众多 GT++ 具体多方块（直接继承）
                                │
                                ├── TTMultiblockBase               (tectech/...)
                                │     └── MTETooltipMultiBlockBaseEM  (goodgenerator/...)
                                │     │     └── MTELargeFusionComputer (GG 聚变基类)
                                │     │     └── 众多 GoodGenerator 多方块
                                │     └── MTEBaseModule             ← ForgeOfGods 模块基类
                                │     └── MTEQuantumComputer, MTEForgeOfGods, ... (直接继承)
                                │
                                ├── MegaMultiBlockBase<T>          (bartworks/...)
                                │     └── MTEMegaBlastFurnace, MTEMegaVacuumFreezer, ...
                                │
                                ├── KubaTechGTMultiBlockBase<T>    (kubatech/...)
                                │     └── MTEMegaIndustrialApiary, ...
                                │
                                ├── MTEAbstractMultiFurnace<T>     ← 多方块炉基类
                                │     └── MTEElectricBlastFurnace (EBF)
                                │     └── MTEMultiFurnace
                                │
                                ├── MTELargeBoiler                 ← 大型锅炉基类
                                │     └── MTELargeBoilerBronze/Steel/Titanium/TungstenSteel
                                │
                                ├── MTELargeTurbine                ← 大型汽轮机基类
                                │     └── MTELargeTurbineSteam/Gas/HPSteam/Plasma
                                │
                                ├── MTEFusionComputer              ← 聚变反应堆基类
                                │     └── MTEFusionComputer1/2/3
                                │     └── MTEAdvFusionMk4/5        (GT++ 扩展)
                                │
                                └── MTEDrillerBase                 ← 钻机基类
                                      └── MTEOilDrillBase → MTEOilDrill2/3/4/Infinite
                                      └── MTEConcreteBackfillerBase → ...
```

---

## 附：关键工具类速查

| 类名 | 文件路径 | 作用 |
|------|---------|------|
| `ProcessingLogic` | `gregtech/api/logic/ProcessingLogic.java` | 配方匹配与超频计算主类 |
| `OverclockCalculator` | `gregtech/api/util/OverclockCalculator.java` | 超频算法实现（EU/时间计算） |
| `ParallelHelper` | `gregtech/api/util/ParallelHelper.java` | 并行配方匹配辅助（计算最大可并行数） |
| `ExoticEnergyInputHelper` | `gregtech/api/util/ExoticEnergyInputHelper.java` | 聚合普通+异域能量仓的电压/安培计算 |
| `GTStructureUtility` | `gregtech/api/util/GTStructureUtility.java` | StructureLib 辅助（Hatch 注册元素构建） |
| `MultiblockTooltipBuilder` | `gregtech/api/util/MultiblockTooltipBuilder.java` | 多方块 Tooltip 构建器 |
| `GTValues` | `gregtech/api/enums/GTValues.java` | 电压数组 `V[]`、等级名 `VN[]` 等全局常量 |
| `HeatingCoilLevel` | `gregtech/api/enums/HeatingCoilLevel.java` | 线圈等级枚举（EBF / IBC 等用） |
| `CheckRecipeResultRegistry` | `gregtech/api/recipe/check/` | 配方检查结果注册与常量 |
| `RecipeMap<B>` | `gregtech/api/recipe/RecipeMap.java` | 配方表（`public final class RecipeMap<B extends RecipeMapBackend>`） |
