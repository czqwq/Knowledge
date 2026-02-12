# 第三方私货模组代码库分析

> **⚠️ 重要声明**：
> 
> 本文档记录的是第三方社区开发者创建的模组，这些模组中：
> - ✅ **部分接口来自GT5U/GTNH官方**（如IMetaTileEntity, IStructureProvider等）
> - ✅ **部分接口为模组自己实现**（如IModularHatch, ICPUCluster等）
> - ✅ **可能包含对官方代码的Mixin修改**
> - ✅ **可能包含实验性或非标准实现**
> 
> 使用这些模组的代码作为参考时，请注意区分官方接口和自定义接口。

---

## 📚 包含的模组

| 模组 | 仓库 | 定位 | 接口数量 |
|-----|------|------|---------|
| **Programmable-Hatches** | [reobf/Programmable-Hatches-Mod](https://github.com/reobf/Programmable-Hatches-Mod) | AE2深度集成 + GT可编程 | 48个 |
| **GT-Not-Leisure** | [ABKQPO/GT-Not-Leisure](https://github.com/ABKQPO/GT-Not-Leisure) | 超大型多块机械 | 68个 |
| **Twist-Space-Technology** | [Nxer/Twist-Space-Technology-Mod](https://github.com/Nxer/Twist-Space-Technology-Mod) | 模块化机械 + 戴森球 | 17个 |
| **AE2Things** | [asdflj/AE2Things](https://github.com/asdflj/AE2Things) | AE2扩展生态 | 51个 |
| **NH-Utilities** | [Keriils/NH-Utilities](https://github.com/Keriils/NH-Utilities) | GTNH工具框架 | 14个 |
| **123Technology** | [CallmeSHaobe/123Technology](https://github.com/CallmeSHaobe/123Technology) | 计算机械 | 3个 |

**总计**: 201个接口（其中约60%为自定义）

---

## 1. Programmable-Hatches-Mod

**核心特色**: 将AE2的合成系统深度集成到GT多块机械中

### 1.1 自定义接口（官方无）

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `IMultiCircuitSupport` | `reobf.proghatches.gt.metatileentity.util` | 多电路支持 | 🔴 自定义 |
| `IMEHatchOverrided` | `reobf.proghatches.gt.metatileentity` | ME仓口重载 | 🔴 自定义 |
| `ISpecialOptimize` | `reobf.proghatches.gt.metatileentity` | 特殊优化标记 | 🔴 自定义 |
| `ISkipStackSizeCheck` | `reobf.proghatches.gt.metatileentity` | 跳过堆叠检查 | 🔴 自定义 |
| `ICircuitProvider` | `reobf.proghatches.gt.metatileentity.util` | 电路提供者 | 🔴 自定义 |
| `IProgrammingCoverBlacklisted` | `reobf.proghatches.gt.cover` | 编程覆盖黑名单 | 🔴 自定义 |
| `IInputStateProvider` | `reobf.proghatches.gt.metatileentity.util` | 输入状态提供 | 🔴 自定义 |
| `IRecipeProcessingAwareDualHatch` | `reobf.proghatches.gt.metatileentity` | 配方感知双路仓 | 🔴 自定义 |
| `IMultiplePatternPushable` | `reobf.proghatches.gt.metatileentity` | 多模式推送 | 🔴 自定义 |
| `ICraftingV2` | `reobf.proghatches.ae.crafting.v2` | 合成系统V2 | 🔴 自定义 |
| `IExternalManager` | `reobf.proghatches.ae.crafting.v2` | 外部管理器 | 🔴 自定义 |
| `ICraftingCacheAccessor` | `reobf.proghatches.ae.crafting.accessor` | 合成缓存访问器 | 🔴 自定义 |
| `ICondenser` | `reobf.proghatches.ae.tiles` | 压缩器接口 | 🔴 自定义 |
| `IProgrammer` | `reobf.proghatches.ae.tiles` | 编程器接口 | 🔴 自定义 |
| `IExternalManagerHolder` | `reobf.proghatches.ae.tiles` | 外部管理器持有者 | 🔴 自定义 |

### 1.2 使用的官方接口

| 接口 | 来源 | 使用场景 |
|------|-----|---------|
| `IMetaTileEntity` | GT5U | 所有GT机器基类 |
| `IDualInputHatch` | GT5U | 双输入仓基础 |
| `IGridProxyable` | AE2 | 网格代理 |
| `ICellContainer` | AE2 | 单元格容器 |
| `ICraftingProvider` | AE2 | 合成提供者 |
| `IMEHost` | AE2 | ME主机 |
| `IGridNode` | AE2 | 网格节点 |
| `ICraftingMachine` | AE2 | 合成机器 |

### 1.3 核心机制

#### A. CPU复制系统
```java
// 自定义接口
public interface IExternalManager {
    void postUpdate();
    boolean handleCraftingRequest(IAEItemStack request);
}

// Mixin拦截
@Mixin(CraftingCPUCluster.class)
public class MixinCPUCluster {
    @Inject(method = "markDirty")
    private void onMarkDirty(CallbackInfo ci) {
        // 通知外部管理器
        externalManager.postUpdate();
    }
}
```

#### B. ME仓集成
```java
// 继承官方接口 + 自定义扩展
public class ProgrammingMEHatch extends MTEHatchInput 
    implements IDualInputHatch, IMEHatchOverrided {
    
    // 官方接口实现
    @Override
    public IGridNode getGridNode(ForgeDirection dir) {
        return gridProxy.getNode();
    }
    
    // 自定义接口实现
    @Override
    public void overrideItemFilter(Predicate<IAEItemStack> filter) {
        this.customFilter = filter;
    }
}
```

### 1.4 工具类

| 类名 | 功能 | 类型 |
|------|------|-----|
| `StackTraceUtil` | 堆栈追踪工具 | 🔧 Util |
| `ProghatchesUtil` | 模组通用工具 | 🔧 Util |
| `EUUtil` | EU能量计算 | 🔧 Util |
| `CTexture` | 纹理常量 | 📦 Constants |

---

## 2. GT-Not-Leisure

**核心特色**: 超过50个大型多块机械，包含无限仓和混合动力系统

### 2.1 自定义接口

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `IControllerInfo` | `com.Nxer.TwistSpaceTechnology.common.multiblock.base` | 控制器信息 | 🔴 自定义 |
| `IGreenHouse` | `com.Nxer.TwistSpaceTechnology.common.machine.multiMachineClasses` | 温室接口 | 🔴 自定义 |
| `IControllerUpgrade` | `com.Nxer.TwistSpaceTechnology.common.multiblock.upgrade` | 控制器升级 | 🔴 自定义 |
| `IItemStackExtra` | `com.Nxer.TwistSpaceTechnology.common.api` | 物品堆扩展 | 🔴 自定义 |
| `IMetaBlock` | `com.Nxer.TwistSpaceTechnology.common.block` | 元方块 | 🔴 自定义 |
| `IRecipePool` | `com.Nxer.TwistSpaceTechnology.recipe` | 配方池 | 🔴 自定义 |
| `IInfinitySlot` | `com.Nxer.TwistSpaceTechnology.common.item` | 无限槽 | 🔴 自定义 |
| `ICasing` | `com.Nxer.TwistSpaceTechnology.common.block.blockClass.BlockCasingBase` | 机械外壳 | 🔴 自定义 |
| `ITileEntityTickAcceleration` | `com.Nxer.TwistSpaceTechnology.common.api.TileEntityHelper` | Tile加速 | 🔴 自定义 |
| `IWirelessEnergy` | `com.Nxer.TwistSpaceTechnology.common.machine` | 无线能量 | 🔴 自定义 |
| `IItemVault` | `com.Nxer.TwistSpaceTechnology.common.machine.multiMachineClasses` | 物品仓库 | 🔴 自定义 |
| `IFluidsLockable` | `com.Nxer.TwistSpaceTechnology.common.machine.multiMachineClasses` | 流体锁定 | 🔴 自定义 |
| `IKeyHandler` | `com.Nxer.TwistSpaceTechnology.common.keys` | 按键处理 | 🔴 自定义 |

### 2.2 使用的官方接口

| 接口 | 来源 | 使用场景 |
|------|-----|---------|
| `IStructureProvider` | GT5U | 多块结构定义 |
| `IMetaTileEntity` | GT5U | 机器实体 |
| `IDualInputHatch` | GT5U | 双输入仓 |
| `IMultiBlockController` | GT5U | 多块控制器 |
| `IGridNode` | AE2 | AE2网络节点 |
| `ICPUCluster` | AE2 | CPU集群访问 |

### 2.3 核心机制

#### A. 无限仓系统
```java
// 自定义接口
public interface IInfinitySlot {
    void setInfinityMode(boolean enabled);
    boolean isInfinityMode();
    long getStoredAmount();
}

// 实现
public class InfinityChest extends MTEHatch implements IInfinitySlot {
    private boolean infinityMode = false;
    private final Map<GTItemStack, Long> storage = new HashMap<>();
    
    @Override
    public ItemStack insertItem(ItemStack stack) {
        if (infinityMode) {
            GTItemStack key = new GTItemStack(stack);
            long current = storage.getOrDefault(key, 0L);
            storage.put(key, current + stack.stackSize);
            return null; // 全部接受
        }
        return super.insertItem(stack);
    }
}
```

#### B. 混合动力系统（眼之和谐）
```java
// 组合多种能源
public class EyeOfHarmony extends MTEMultiBlockBase {
    private long storedEU = 0;
    private int storedRF = 0;
    private long storedVis = 0;
    
    public boolean consumeEnergy(long eu) {
        // 优先级: EU -> RF -> Vis
        if (storedEU >= eu) {
            storedEU -= eu;
            return true;
        }
        // RF转EU (1:4)
        int rfNeeded = (int)((eu - storedEU) * 4);
        if (storedRF >= rfNeeded) {
            storedRF -= rfNeeded;
            storedEU = 0;
            return true;
        }
        // Vis转EU (1 Vis = 10000 EU)
        // ...
        return false;
    }
}
```

### 2.4 工具类

| 类名 | 功能 | 类型 |
|------|------|-----|
| `GTNLParallelHelper` | 并行计算辅助 | 🔧 Helper |
| `RecipeBuilder` | 配方构建器 | 🏗️ Builder |
| `StructureUtils` | 结构工具 | 🔧 Util |
| `TTMultiblockBaseHelper` | TecTech多块辅助 | 🔧 Helper |
| `DisassemblerHelper` | 拆解机辅助 | 🔧 Helper |
| `ItemUtils` | 物品工具 | 🔧 Util |
| `MaterialUtils` | 材料工具 | 🔧 Util |
| `ManaHelper` | 魔力辅助（植物魔法） | 🔧 Helper |

---

## 3. Twist-Space-Technology-Mod

**核心特色**: 模块化多块机械系统 + 戴森球计划

### 3.1 自定义接口

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `IRecipeProvider` | `com.Twist.TwistSpaceTechnology.common.recipeMap` | 配方提供者 | 🔴 自定义 |
| `IItemHasCooldown` | `com.Twist.TwistSpaceTechnology.common.api` | 物品冷却 | 🔴 自定义 |
| `IDSP_IO` | `com.Twist.TwistSpaceTechnology.common.machine.singleblock.DSP` | 戴森球IO | 🔴 自定义 |
| `IDSP_DataCell` | `com.Twist.TwistSpaceTechnology.common.machine.multiblock.DSP` | 数据单元 | 🔴 自定义 |
| `IModularHatch` | `com.Twist.TwistSpaceTechnology.common.modularization` | 模块化舱口 | 🔴 自定义 |
| `IDynamicModularHatch` | `com.Twist.TwistSpaceTechnology.common.modularization.DynamicHatch` | 动态模块舱 | 🔴 自定义 |
| `IExecutionCore` | `com.Twist.TwistSpaceTechnology.common.modularization.ExecutionCore` | 执行核心 | 🔴 自定义 |
| `IStaticModularHatch` | `com.Twist.TwistSpaceTechnology.common.modularization.StaticHatch` | 静态模块舱 | 🔴 自定义 |
| `IModularizedMachine` | `com.Twist.TwistSpaceTechnology.common.modularization.ModularizedMachine` | 模块化机器 | 🔴 自定义 |
| `ICombatGear` | `com.Twist.TwistSpaceTechnology.common.item.combat` | 战斗装备 | 🔴 自定义 |

### 3.2 核心机制

#### A. 模块化系统
```java
// 模块化机器接口
public interface IModularizedMachine {
    List<IModularHatch> getModules();
    void addModule(IModularHatch module);
    void removeModule(IModularHatch module);
    boolean validateModules();
}

// 模块接口
public interface IModularHatch {
    ModuleType getType();
    boolean canAttachTo(IModularizedMachine machine);
    void onAttach(IModularizedMachine machine);
    void onDetach();
}

// 使用示例
public class ModularAssemblyLine extends MTEMultiBlockBase 
    implements IModularizedMachine {
    
    private List<IModularHatch> modules = new ArrayList<>();
    
    @Override
    public boolean checkStructure() {
        if (!super.checkStructure()) return false;
        
        // 验证模块配置
        long totalSpeed = modules.stream()
            .filter(m -> m.getType() == ModuleType.SPEED)
            .count();
        
        if (totalSpeed > 16) {
            return false; // 最多16个加速模块
        }
        
        return validateModules();
    }
    
    @Override
    protected GTRecipe.GTRecipeBuilder createRecipeBuilder() {
        GTRecipe.GTRecipeBuilder builder = super.createRecipeBuilder();
        
        // 模块修改配方
        for (IModularHatch module : modules) {
            if (module instanceof IRecipeModifier) {
                builder = ((IRecipeModifier) module).modifyRecipe(builder);
            }
        }
        
        return builder;
    }
}
```

#### B. 戴森球系统
```java
// 戴森球数据单元接口
public interface IDSP_DataCell {
    long getStoredEnergy();
    void addEnergy(long amount);
    double getEfficiency();
}

// 戴森球IO接口
public interface IDSP_IO {
    void connectToDysonSphere(IDSP_DataCell dataCell);
    long extractEnergy(long maxAmount);
}

// 实现
public class DysonSphereReceiver extends MTESingleBlockMachine 
    implements IDSP_IO {
    
    private IDSP_DataCell connectedSphere;
    
    @Override
    public void connectToDysonSphere(IDSP_DataCell dataCell) {
        this.connectedSphere = dataCell;
    }
    
    @Override
    public long extractEnergy(long maxAmount) {
        if (connectedSphere == null) return 0;
        
        long available = connectedSphere.getStoredEnergy();
        long extracted = Math.min(available, maxAmount);
        
        connectedSphere.addEnergy(-extracted);
        return extracted;
    }
    
    @Override
    public boolean onRunningTick(ItemStack stack) {
        // 每tick提取能量
        long extracted = extractEnergy(voltage * 20); // 20 tick/s
        if (extracted > 0) {
            energyBuffer += extracted;
            return true;
        }
        return false;
    }
}
```

### 3.3 工具类

| 类名 | 功能 | 类型 |
|------|------|-----|
| `TST_RecipeBuilder` | TST配方构建器 | 🏗️ Builder |
| `MathUtils` | 数学工具 | 🔧 Util |
| `RecipeMathUtils` | 配方数学 | 🔧 Util |
| `TSTStructureUtility` | TST结构工具 | 🔧 Util |
| `GTCM_ParallelHelper` | GT并行辅助 | 🔧 Helper |
| `DimensionBuilder` | 维度构建器 | 🏗️ Builder |
| `BloodMagicHelper` | 血魔法集成 | 🔧 Helper |

---

## 4. AE2Things

**核心特色**: AE2终端生态扩展 + 跨模组兼容

### 4.1 自定义接口

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `IGuiDrawSlot` | `com.asdflj.ae2thing.client.gui` | GUI绘制槽 | 🔴 自定义 |
| `IWidgetGui` | `com.asdflj.ae2thing.client.gui` | 小部件GUI | 🔴 自定义 |
| `IScrollable` | `com.asdflj.ae2thing.client.gui` | 可滚动接口 | 🔴 自定义 |
| `IPatternTerminal` | `com.asdflj.ae2thing.api.IPatternTerminal` | 模式终端 | 🔴 自定义 |
| `IEssentiaContainer` | `com.asdflj.ae2thing.api` | 要素容器（神秘） | 🔴 自定义 |
| `IClickableInTerminal` | `com.asdflj.ae2thing.client.gui.button` | 终端可点击 | 🔴 自定义 |
| `IAEBasePanel` | `com.asdflj.ae2thing.client.gui` | AE基础面板 | 🔴 自定义 |
| `ITerminal` | `com.asdflj.ae2thing.common.parts` | 终端接口 | 🔴 自定义 |
| `ICraftingTerminalAdapter` | `com.asdflj.ae2thing.api` | 合成终端适配器 | 🔴 自定义 |
| `IPatternTerminalAdapter` | `com.asdflj.ae2thing.api` | 模式终端适配器 | 🔴 自定义 |

### 4.2 使用的官方接口

| 接口 | 来源 | 使用场景 |
|------|-----|---------|
| `IMEMonitor` | AE2 | ME监控器 |
| `ITerminalHost` | AE2 | 终端主机 |
| `IGridProxyable` | AE2 | 网格代理 |
| `IStorageNode` | AE2 | 存储节点 |
| `ICellHandler` | AE2 | 单元格处理 |
| `IPart` | AE2 | Part基类 |

### 4.3 核心机制

#### A. 终端适配器系统
```java
// 终端适配器接口
public interface ICraftingTerminalAdapter {
    void openTerminal(EntityPlayer player);
    IMEMonitor<IAEItemStack> getInventory();
    boolean hasPermission(EntityPlayer player);
}

// 多终端支持
public class MultiTerminalAdapter implements ICraftingTerminalAdapter {
    private final List<ICraftingTerminalAdapter> adapters = new ArrayList<>();
    
    public void registerAdapter(ICraftingTerminalAdapter adapter) {
        adapters.add(adapter);
    }
    
    @Override
    public void openTerminal(EntityPlayer player) {
        // 打开菜单选择
        player.openGui(AE2Things.INSTANCE, GuiType.MULTI_TERMINAL.ordinal(), ...);
    }
}
```

#### B. 背包系统
```java
// 背包接口（继承AE2官方接口）
public interface IBackpackItem extends IItemInventory, ITerminalHost {
    ItemStack getBackpackItem(EntityPlayer player);
    IStorageChannel getChannel();
}

// 实现
public class WirelessBackpack implements IBackpackItem {
    @Override
    public IMEMonitor<IAEItemStack> getInventory(ItemStack backpack) {
        // 从NBT加载存储
        NBTTagCompound nbt = backpack.getTagCompound();
        return new BackpackInventory(nbt);
    }
    
    @Override
    public void openTerminal(EntityPlayer player, ItemStack backpack) {
        // 打开背包GUI
        player.openGui(AE2Things.INSTANCE, GuiType.BACKPACK.ordinal(), ...);
    }
}
```

### 4.4 工具类

| 类名 | 功能 | 类型 |
|------|------|-----|
| `InvUtil` | 物品栏工具 | 🔧 Util |
| `GTUtil` | GT集成工具 | 🔧 Util |
| `ClientHelper` | 客户端辅助 | 🔧 Helper |
| `RenderHelper` | 渲染辅助 | 🔧 Helper |
| `CraftingDebugHelper` | 合成调试 | 🔧 Helper |
| `NEIUtils` | NEI工具 | 🔧 Util |

---

## 5. NH-Utilities

**核心特色**: GTNH框架级优化和元对象系统

### 5.1 自定义接口

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `ILoadMetaItem` | `com.Nxer.TwistSpaceTechnology.loader` | 加载元物品 | 🔴 自定义 |
| `IRegisterProvider` | `com.Nxer.TwistSpaceTechnology.loader` | 注册提供者 | 🔴 自定义 |
| `IRegisterTileProvider` | `com.Nxer.TwistSpaceTechnology.loader` | Tile注册提供 | 🔴 自定义 |
| `IMetaObjectProvider` | `com.Nxer.TwistSpaceTechnology.common.object` | 元对象提供者 | 🔴 自定义 |
| `IMetaTypeObject` | `com.Nxer.TwistSpaceTechnology.common.object` | 元类型对象 | 🔴 自定义 |
| `IItemContainer` | `com.Nxer.TwistSpaceTechnology.common.api` | 物品容器 | 🔴 自定义 |
| `ITileEntityTickAcceleration` | `com.Nxer.TwistSpaceTechnology.common.api` | Tile加速 | 🔴 自定义 |

### 5.2 核心机制

#### A. 元对象系统（MST）
```java
// 元类型对象接口
public interface IMetaTypeObject {
    String getObjectName();
    ObjectType getType();
    void register();
}

// 元对象提供者
public interface IMetaObjectProvider {
    List<IMetaTypeObject> getObjects();
    void preLoad();
    void load();
    void postLoad();
}

// 实现示例
public class MetaMachineProvider implements IMetaObjectProvider {
    private final List<IMetaTypeObject> machines = new ArrayList<>();
    
    @Override
    public void preLoad() {
        // 定义元对象
        machines.add(new MetaMachine("超级压缩机", MachineType.COMPRESSOR));
        machines.add(new MetaMachine("超级打粉机", MachineType.MACERATOR));
    }
    
    @Override
    public void load() {
        // 延迟注册
        for (IMetaTypeObject machine : machines) {
            machine.register();
        }
    }
}
```

#### B. 懒加载系统
```java
public class LazyObjectHelper {
    private static final Map<String, Supplier<?>> lazyObjects = new HashMap<>();
    
    public static <T> void registerLazy(String key, Supplier<T> supplier) {
        lazyObjects.put(key, supplier);
    }
    
    @SuppressWarnings("unchecked")
    public static <T> T get(String key) {
        Supplier<?> supplier = lazyObjects.get(key);
        if (supplier == null) return null;
        return (T) supplier.get();
    }
}

// 使用
LazyObjectHelper.registerLazy("superChest", () -> new SuperChest(10000));
SuperChest chest = LazyObjectHelper.get("superChest");
```

---

## 6. 123Technology

**核心特色**: OTE计算机和维度资源系统

### 6.1 自定义接口

| 接口 | 包 | 功能 | 标记 |
|------|----|----|-----|
| `IRecipePool` | `com.CallmeSHaobe.technology.recipe` | 配方池 | 🔴 自定义 |
| `IRegistry` | `com.CallmeSHaobe.technology.loader` | 注册表 | 🔴 自定义 |

---

## 🔧 跨模组集成模式总结

### 1. AE2 + GT混合模式（Programmable-Hatches）

```java
// 同时实现两个体系的接口
public class DualSystemHatch extends MTEHatchInput 
    implements IDualInputHatch, ICellContainer, ICraftingProvider {
    
    // GT侧接口
    @Override
    public boolean justUpdated() {
        return mJustHadNewItems;
    }
    
    // AE2侧接口
    @Override
    public IGridNode getGridNode(ForgeDirection dir) {
        return gridProxy.getNode();
    }
    
    @Override
    public void blinkCell(int slot) {
        // 单元格闪烁
    }
}
```

### 2. Mixin深度修改（GT-Not-Leisure）

```java
// 修改官方类行为
@Mixin(MTEHatchInput.class)
public class MixinHatchInput {
    @Inject(method = "onPostTick", at = @At("HEAD"))
    private void onPostTick(IGregTechTileEntity baseMetaTileEntity, long aTick, CallbackInfo ci) {
        // 插入自定义逻辑
        if (this instanceof IInfinitySlot) {
            ((IInfinitySlot) this).updateInfinityStorage();
        }
    }
}
```

### 3. 适配器模式（AE2Things）

```java
// 适配不同终端系统
public class TerminalAdapter implements ICraftingTerminalAdapter {
    private final Object foreignTerminal;  // 其他Mod的终端
    
    @Override
    public void openTerminal(EntityPlayer player) {
        if (foreignTerminal instanceof WCTTerminal) {
            // 适配 Wireless Crafting Terminal
            ((WCTTerminal) foreignTerminal).open(player);
        } else if (foreignTerminal instanceof NETerminal) {
            // 适配 Not Enough Items Terminal
            ((NETerminal) foreignTerminal).show(player);
        }
    }
}
```

---

## 📊 接口复杂度分析

| 模组 | 自定义接口 | 官方接口 | 混合度 | Mixin使用 |
|------|----------|---------|--------|----------|
| Programmable-Hatches | 44 | 8 | ⭐⭐⭐⭐⭐ | 🟢 重度 |
| GT-Not-Leisure | 15 | 6 | ⭐⭐⭐⭐ | 🟢 重度 |
| Twist-Space-Tech | 16 | 4 | ⭐⭐⭐ | 🟡 中度 |
| AE2Things | 40 | 6 | ⭐⭐⭐⭐ | 🟡 中度 |
| NH-Utilities | 10 | 2 | ⭐⭐ | 🔴 轻度 |
| 123Technology | 2 | 2 | ⭐ | 🔴 轻度 |

---

## 🎯 使用建议

### 学习路径
1. **入门**: 先学习官方接口（GT5U_Readme.md + AE_README.md）
2. **进阶**: 研究NH-Utilities的框架设计
3. **高级**: 分析Programmable-Hatches的Mixin技术

### 代码复用
- ✅ **可复用**: 工具类、Helper类、Builder模式
- ⚠️ **谨慎使用**: Mixin代码（可能影响稳定性）
- ❌ **避免直接复制**: 自定义接口（缺少上下文）

### 兼容性注意
- �� **Mixin冲突**: 多个模组修改同一类时可能冲突
- 🟡 **接口变更**: 自定义接口可能随版本变化
- 🟢 **官方接口**: 相对稳定，推荐优先使用

---

## 📚 相关文档

- [GT5U_Readme.md](./GT5U_Readme.md) - GT5U官方接口列表
- [AE_README.md](./AE_README.md) - AE2官方接口详解
- [Useful_Readme.md](./Useful_Readme.md) - 官方可重用代码

---

**最后更新**: 2026-02-12
**维护者**: AI Knowledge Base
