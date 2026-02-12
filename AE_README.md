# Applied-Energistics-2-Unofficial 接口与架构文档

**仓库地址**: https://github.com/GTNewHorizons/Applied-Energistics-2-Unofficial  
**项目定位**: GTNH版本的AE2，提供物质能量(ME)存储和自动化系统

**接口总数**: 286个  
**核心系统**: 网络(Grid)、存储(Storage)、合成(Crafting)、Part系统

---

## 目录

1. [核心接口分类](#核心接口分类)
2. [扩展点与API](#扩展点与api)
3. [系统架构](#系统架构)
4. [使用示例](#使用示例)
5. [与其他模组集成](#与其他模组集成)

---

## 核心接口分类

### 1. 网络系统 (Networking)

#### A. 基础网络接口

| 接口 | 包路径 | 功能 | 关键方法 |
|------|--------|------|---------|
| `IGrid` | `appeng.api.networking` | 网格核心 | `getCache()`, `postEvent()`, `getMachines()` |
| `IGridNode` | `appeng.api.networking` | 网格节点 | `updateState()`, `destroy()`, `getConnections()` |
| `IGridHost` | `appeng.api.networking` | 网格主机 | `getGridNode(dir)`, `getCableConnectionType(dir)` |
| `IGridBlock` | `appeng.api.networking` | 节点定义 | `getMachineRepresentation()`, `getIdlePowerUsage()` |
| `IGridConnection` | `appeng.api.networking` | 节点连接 | `getOtherSide()`, `destroy()` |
| `IGridMultiblock` | `appeng.api.networking` | 多方块网格 | `getIterator()`, `size()` |

**代码示例**:
```java
// 实现网格主机
public class MyMEDevice extends TileEntity implements IGridHost {
    private AENetworkProxy gridProxy;
    
    public MyMEDevice() {
        gridProxy = new AENetworkProxy(this, "proxy", getItemFromTile(this), true);
        gridProxy.setFlags(GridFlags.REQUIRE_CHANNEL);
        gridProxy.setIdlePowerUsage(1.0);
    }
    
    @Override
    public IGridNode getGridNode(ForgeDirection dir) {
        return gridProxy.getNode();
    }
    
    @Override
    public AECableType getCableConnectionType(ForgeDirection dir) {
        return AECableType.SMART;
    }
    
    @Override
    public void securityBreak() {
        // 安全破坏时的处理
    }
}
```

#### B. 网格缓存接口

| 接口 | 包路径 | 功能 |
|------|--------|------|
| `IGridCache` | `appeng.api.networking` | 缓存基类 |
| `IEnergyGrid` | `appeng.api.networking.energy` | 能量缓存 |
| `IStorageGrid` | `appeng.api.storage` | 存储缓存 |
| `ICraftingGrid` | `appeng.api.networking.crafting` | 合成缓存 |
| `ISecurityGrid` | `appeng.api.networking.security` | 安全缓存 |
| `IPathingGrid` | `appeng.api.networking.pathing` | 路由缓存 |
| `ITickManager` | `appeng.api.networking.ticking` | 时序缓存 |
| `ISpatialCache` | `appeng.api.networking.spatial` | 空间缓存 |

**使用示例**:
```java
// 访问网格缓存
IGrid grid = gridNode.getGrid();

// 能量操作
IEnergyGrid eg = grid.getCache(IEnergyGrid.class);
double available = eg.getAvgPowerInjection();
double stored = eg.getStoredPower();

// 存储操作
IStorageGrid sg = grid.getCache(IStorageGrid.class);
IMEMonitor<IAEItemStack> items = sg.getItemInventory();

// 合成操作
ICraftingGrid cg = grid.getCache(ICraftingGrid.class);
ICraftingJob job = cg.beginCraftingJob(world, grid, source, craftItem, null);
```

---

### 2. 存储系统 (Storage)

#### A. 存储核心接口

| 接口 | 包路径 | 功能 | 类型 |
|------|--------|------|-----|
| `IMEInventory<T>` | `appeng.api.storage` | 基础存储 | 🔵 核心 |
| `IMEInventoryHandler<T>` | `appeng.api.storage` | 存储处理器 | 🔵 核心 |
| `IMEMonitor<T>` | `appeng.api.storage` | 存储监听器 | 🔵 核心 |
| `ICellInventory<T>` | `appeng.api.storage` | 单元格存储 | 🟢 扩展 |
| `ICellHandler` | `appeng.api.storage` | 单元格处理 | 🟢 扩展点 |
| `ICellProvider` | `appeng.api.storage` | 单元格提供 | 🟢 扩展 |
| `ICellContainer` | `appeng.api.storage` | 单元格容器 | 🟢 扩展 |
| `IExternalStorageHandler` | `appeng.api.storage` | 外部存储 | 🟢 扩展点 |
| `IStorageMonitorable` | `appeng.api.storage` | 可监听存储 | 🟡 接口 |
| `ITerminalHost` | `appeng.api.storage` | 终端主机 | 🟡 接口 |

**接口层次**:
```
IMEInventory<T>
  ├─ injectItems(input, mode, src)
  ├─ extractItems(request, mode, src)
  ├─ getAvailableItems(out)
  └─ getChannel()

IMEInventoryHandler<T> extends IMEInventory<T>
  ├─ validForPass(pass)
  ├─ canAccept(input)
  ├─ isPrioritized(input)
  ├─ extractItems(request, mode, src)
  └─ getAccess()

IMEMonitor<T> extends IMEInventoryHandler<T>
  ├─ addListener(listener, verificationToken)
  ├─ removeListener(listener)
  ├─ getStorageList()
  └─ getChannel()
```

**泛型支持**:
- `IAEItemStack` - 物品存储
- `IAEFluidStack` - 流体存储

**代码示例**:
```java
// 实现自定义存储
public class CustomMEInventory implements IMEInventory<IAEItemStack> {
    private final IItemList<IAEItemStack> storage = AEApi.instance()
        .storage().createItemList();
    
    @Override
    public IAEItemStack injectItems(IAEItemStack input, Actionable mode, BaseActionSource src) {
        if (input == null) return null;
        
        IAEItemStack existing = storage.findPrecise(input);
        if (existing != null) {
            long total = existing.getStackSize() + input.getStackSize();
            if (mode == Actionable.MODULATE) {
                existing.setStackSize(total);
            }
            return null; // 全部接受
        }
        
        if (mode == Actionable.MODULATE) {
            storage.add(input.copy());
        }
        return null;
    }
    
    @Override
    public IAEItemStack extractItems(IAEItemStack request, Actionable mode, BaseActionSource src) {
        IAEItemStack stored = storage.findPrecise(request);
        if (stored == null) return null;
        
        long toExtract = Math.min(request.getStackSize(), stored.getStackSize());
        IAEItemStack result = stored.copy();
        result.setStackSize(toExtract);
        
        if (mode == Actionable.MODULATE) {
            stored.decStackSize(toExtract);
            if (stored.getStackSize() <= 0) {
                storage.remove(stored);
            }
        }
        
        return result;
    }
    
    @Override
    public IItemList<IAEItemStack> getAvailableItems(IItemList<IAEItemStack> out) {
        for (IAEItemStack stack : storage) {
            out.add(stack);
        }
        return out;
    }
    
    @Override
    public StorageChannel getChannel() {
        return StorageChannel.ITEMS;
    }
}
```

#### B. 数据结构接口

| 接口 | 包路径 | 功能 |
|------|--------|------|
| `IAEStack<T>` | `appeng.api.storage.data` | 基础栈接口 |
| `IAEItemStack` | `appeng.api.storage.data` | 物品栈 |
| `IAEFluidStack` | `appeng.api.storage.data` | 流体栈 |
| `IItemList<T>` | `appeng.api.storage.data` | 物品列表 |
| `IAETagCompound` | `appeng.api.storage.data` | NBT数据 |

**IAEStack特性**:
```java
public interface IAEStack<T extends IAEStack<T>> {
    // 数量操作
    long getStackSize();
    void setStackSize(long stackSize);
    void incStackSize(long i);
    void decStackSize(long i);
    
    // 比较
    boolean isSameType(T other);
    boolean fuzzyComparison(T other, FuzzyMode mode);
    
    // 复制
    T copy();
    
    // 序列化
    void writeToNBT(NBTTagCompound tag);
    
    // 显示
    String getModID();
    ItemStack getItemStack();
}
```

---

### 3. 合成系统 (Crafting)

#### A. 合成核心接口

| 接口 | 包路径 | 功能 | 角色 |
|------|--------|------|-----|
| `ICraftingGrid` | `appeng.api.networking.crafting` | 合成网格 | 🔵 核心 |
| `ICraftingPatternDetails` | `appeng.api.networking.crafting` | 配方详情 | 🟢 数据 |
| `ICraftingProvider` | `appeng.api.networking.crafting` | 合成提供者 | 🟡 实现 |
| `ICraftingCPU` | `appeng.api.networking.crafting` | CPU单元 | 🔵 核心 |
| `ICraftingJob<T>` | `appeng.api.networking.crafting` | 合成任务 | 🟢 任务 |
| `ICraftingLink` | `appeng.api.networking.crafting` | 合成链接 | 🟡 通信 |
| `ICraftingRequester` | `appeng.api.networking.crafting` | 合成请求者 | 🟡 实现 |
| `ICraftingMedium` | `appeng.api.networking.crafting` | 合成媒介 | 🟡 实现 |
| `ICraftingCallback` | `appeng.api.networking.crafting` | 完成回调 | 🟢 回调 |

**合成流程**:
```
1. Pattern识别
   ICraftingPatternDetails details = provider.getPatternDetails();
   
2. 任务创建
   ICraftingJob job = craftingGrid.beginCraftingJob(world, grid, src, what, null);
   
3. CPU分配
   ICraftingCPU cpu = craftingGrid.getCpu(0);
   ICraftingLink link = craftingGrid.startJob(world, cpu, link, details);
   
4. 执行与回调
   link.onRequestComplete(result);
```

**代码示例**:
```java
// 实现合成提供者
public class MyCraftingInterface extends TileEntity 
    implements ICraftingProvider, IGridHost {
    
    private List<ICraftingPatternDetails> patterns = new ArrayList<>();
    private AENetworkProxy gridProxy;
    
    @Override
    public void provideCrafting(ICraftingProviderHelper helper) {
        // 提供所有模式
        for (ICraftingPatternDetails pattern : patterns) {
            helper.addCraftingOption(this, pattern);
        }
    }
    
    @Override
    public boolean pushPattern(ICraftingPatternDetails details, InventoryCrafting ic) {
        // 推送模式到机器
        ItemStack[] inputs = new ItemStack[9];
        for (int i = 0; i < 9; i++) {
            inputs[i] = ic.getStackInSlot(i);
        }
        
        // 发送到处理机器
        return sendToMachine(inputs, details.getOutputs());
    }
    
    @Override
    public boolean isBusy() {
        return isProcessing;
    }
}

// 请求合成
public void requestCrafting(IAEItemStack what, long amount) {
    IGrid grid = gridProxy.getGrid();
    ICraftingGrid cg = grid.getCache(ICraftingGrid.class);
    
    // 检查是否可合成
    ICraftingPatternDetails pattern = cg.getCraftingFor(
        what, null, 0, world
    );
    
    if (pattern != null) {
        // 开始任务
        ICraftingJob job = cg.beginCraftingJob(
            world, grid, source, 
            what.copy().setStackSize(amount), 
            null
        );
        
        if (job != null) {
            // 提交
            ICraftingLink link = cg.submitJob(
                job, this, null, false, source
            );
        }
    }
}
```

---

### 4. Part系统 (Parts & Cables)

#### A. Part核心接口

| 接口 | 包路径 | 功能 | 方法数 |
|------|--------|------|-------|
| `IPart` | `appeng.api.parts` | Part基类 | 60+ |
| `IPartHost` | `appeng.api.parts` | Part宿主 | 15 |
| `IPartHelper` | `appeng.api.parts` | Part辅助 | 10 |
| `IPartCollisionHelper` | `appeng.api.parts` | 碰撞辅助 | 8 |
| `IPartRenderHelper` | `appeng.api.parts` | 渲染辅助 | 12 |

**IPart关键方法**:
```java
public interface IPart {
    // 生命周期
    void onNeighborChanged();
    void onEntityCollision(Entity entity);
    void onPlacement(EntityPlayer player, ItemStack held, ForgeDirection side);
    void onRemove();
    
    // 网络
    IGridNode getGridNode();
    void getBoxes(IPartCollisionHelper bch);
    
    // 渲染
    void renderInventory(IPartRenderHelper rh, RenderBlocks renderer);
    void renderStatic(int x, int y, int z, IPartRenderHelper rh, RenderBlocks renderer);
    void renderDynamic(double x, double y, double z, IPartRenderHelper rh, Tessellator tess);
    
    // 交互
    boolean onActivate(EntityPlayer player, Vec3 pos);
    boolean onShiftActivate(EntityPlayer player, Vec3 pos);
    void onPartShiftActivate(EntityPlayer player, Vec3 pos);
    
    // 物品
    ItemStack getItemStack(PartItemStack type);
    ItemStack getPickBlock(Vec3 pos);
    
    // 状态
    int getLightLevel();
    boolean canConnectRedstone();
    void randomDisplayTick(World world, int x, int y, int z, Random r);
}
```

#### B. 特殊Part接口

| 接口 | 包路径 | 功能 |
|------|--------|------|
| `ICraftingTerminal` | `appeng.api.parts` | 合成终端 |
| `IPatternTerminal` | `appeng.api.parts` | 模式终端 |
| `IInterfaceTerminal` | `appeng.api.parts` | 接口终端 |
| `IStorageBus` | `appeng.api.parts` | 存储总线 |
| `ILevelEmitter` | `appeng.api.parts` | 电平发射器 |
| `IFacadePart` | `appeng.api.parts` | 立面 |

**创建自定义Part**:
```java
public class MyCustomPart implements IPart, IGridHost {
    private IPartHost host;
    private AENetworkProxy gridProxy;
    
    @Override
    public void setPartHostInfo(ForgeDirection side, IPartHost host, TileEntity tile) {
        this.host = host;
        this.gridProxy = new AENetworkProxy(this, "part", getItemStack(PartItemStack.Network), true);
    }
    
    @Override
    public void getBoxes(IPartCollisionHelper bch) {
        // 定义碰撞体积
        bch.addBox(5, 5, 12, 11, 11, 16);
    }
    
    @Override
    public void renderStatic(int x, int y, int z, IPartRenderHelper rh, RenderBlocks renderer) {
        // 静态渲染
        rh.setTexture(myTexture);
        rh.setBounds(5, 5, 12, 11, 11, 16);
        rh.renderBlock(x, y, z, renderer);
    }
    
    @Override
    public boolean onActivate(EntityPlayer player, Vec3 pos) {
        if (!player.worldObj.isRemote) {
            // 打开GUI
            player.openGui(...);
        }
        return true;
    }
}
```

---

### 5. 安全系统 (Security)

| 接口 | 包路径 | 功能 |
|------|--------|------|
| `ISecurityGrid` | `appeng.api.networking.security` | 安全网格 |
| `ISecurityProvider` | `appeng.api.networking.security` | 安全提供者 |
| `IActionHost` | `appeng.api.networking.security` | 动作宿主 |
| `BaseActionSource` | `appeng.api.networking.security` | 动作源 |

**使用示例**:
```java
// 权限检查
public boolean hasPermission(EntityPlayer player, SecurityPermissions perm) {
    IGrid grid = gridProxy.getGrid();
    ISecurityGrid sg = grid.getCache(ISecurityGrid.class);
    
    BaseActionSource src = new PlayerSource(player, this);
    return sg.hasPermission(src, perm);
}

// 安全操作
if (hasPermission(player, SecurityPermissions.EXTRACT)) {
    // 允许提取
    extractItems(...);
}
```

---

## 扩展点与API

### 1. IRegistryContainer - 主扩展接口

```java
IRegistryContainer registries = AEApi.instance().registries();
```

#### A. 存储扩展

```java
// 1. 自定义单元格类型
ICellRegistry cellRegistry = registries.cell();
cellRegistry.addCellHandler(new ICellHandler() {
    @Override
    public boolean isCell(ItemStack is) {
        return is.getItem() instanceof MyCustomCell;
    }
    
    @Override
    public IMEInventoryHandler getCellInventory(ItemStack is, ISaveProvider host, StorageChannel channel) {
        return new MyCustomCellInventory(is, host);
    }
});

// 2. 外部存储连接
IExternalStorageRegistry extStorage = registries.externalStorage();
extStorage.addExternalStorageInterface(new IExternalStorageHandler() {
    @Override
    public boolean canHandle(TileEntity te, ForgeDirection d, StorageChannel channel, BaseActionSource src) {
        return te instanceof MyCustomContainer;
    }
    
    @Override
    public IMEInventory getInventory(TileEntity te, ForgeDirection d, StorageChannel channel, BaseActionSource src) {
        return new MyContainerAdapter((MyCustomContainer) te);
    }
});
```

#### B. P2P隧道扩展

```java
IP2PTunnelRegistry p2pRegistry = registries.p2pTunnel();
p2pRegistry.addNewAttunement(new ItemStack(Items.diamond), TunnelType.ME);
p2pRegistry.addNewAttunement(new ItemStack(Blocks.glass), TunnelType.LIGHT);
```

#### C. 物品比较扩展

```java
ISpecialComparisonRegistry comparison = registries.specialComparison();
comparison.addComparison(new IItemComparison() {
    @Override
    public boolean isSameAsPrecise(IAEItemStack a, IAEItemStack b) {
        // 自定义精确比较（如蜜蜂基因）
        return compareGenetics(a, b);
    }
    
    @Override
    public boolean isSameAsFuzzy(IAEItemStack a, IAEItemStack b) {
        // 模糊比较
        return compareSpecies(a, b);
    }
});
```

#### D. 配方扩展

```java
// 磨粉机配方
IGrinderRegistry grinder = registries.grinder();
grinder.addRecipe(input, output, chance);

// 铭刻器配方
IInscriberRegistry inscriber = registries.inscriber();
inscriber.addRecipe(new InscriberRecipe(inputs, output, top, bottom, type));
```

#### E. 无线终端扩展

```java
IWirelessTermRegistry wireless = registries.wireless();
wireless.registerWirelessHandler(new IWirelessTermHandler() {
    @Override
    public boolean canHandle(ItemStack is) {
        return is.getItem() instanceof MyWirelessTerm;
    }
    
    @Override
    public boolean usePower(EntityPlayer player, double amount, ItemStack is) {
        // 消耗能量
        return drainPower(is, amount);
    }
});
```

---

### 2. 主要扩展点总结

| 扩展点 | 注册方法 | 用途 |
|-------|---------|-----|
| **ICellHandler** | `cellRegistry.addCellHandler()` | 自定义存储单元 |
| **IExternalStorageHandler** | `extStorage.addExternalStorageInterface()` | 连接外部容器 |
| **IGridCache** | `gridCacheRegistry.registerGridCache()` | 自定义网格模块 |
| **IWirelessTermHandler** | `wireless.registerWirelessHandler()` | 无线终端协议 |
| **IP2PTunnelAttunement** | `p2pTunnel.addNewAttunement()` | P2P隧道类型 |
| **IItemComparison** | `comparison.addComparison()` | 特殊物品比较 |
| **IGrinderEntry** | `grinder.addRecipe()` | 磨粉配方 |
| **IInscriberRecipe** | `inscriber.addRecipe()` | 铭刻配方 |
| **IMovableHandler** | `movable.registerHandler()` | 可传送方块 |
| **IMatterCannonAmmo** | `matterCannon.registerAmmo()` | 物质炮弹药 |
| **ILocatable** | `locatable.registerLocatable()` | 可定位对象 |

---

## 系统架构

### 架构图

```
┌──────────────────────────────────────────────────┐
│           AEApi (Singleton Entry Point)          │
├──────────────────────────────────────────────────┤
│                                                  │
│  ┌────────────── IRegistryContainer ──────────┐ │
│  │  ├─ ICellRegistry                          │ │
│  │  ├─ IExternalStorageRegistry               │ │
│  │  ├─ IGridCacheRegistry                     │ │
│  │  ├─ IWirelessTermRegistry                  │ │
│  │  ├─ IP2PTunnelRegistry                     │ │
│  │  └─ ...其他注册表                           │ │
│  └────────────────────────────────────────────┘ │
│                                                  │
│  ┌────────────── IDefinitions ────────────────┐ │
│  │  ├─ blocks() → IBlocks                     │ │
│  │  ├─ items() → IItems                       │ │
│  │  ├─ parts() → IParts                       │ │
│  │  └─ materials() → IMaterials               │ │
│  └────────────────────────────────────────────┘ │
│                                                  │
│  ┌────────────── IStorageHelper ──────────────┐ │
│  │  ├─ createItemList()                       │ │
│  │  ├─ createFluidList()                      │ │
│  │  └─ loadItemList()                         │ │
│  └────────────────────────────────────────────┘ │
│                                                  │
│  ┌────────────── IPartHelper ────────────────┐ │
│  │  ├─ registerNewLayer()                     │ │
│  │  ├─ getPartHostClass()                     │ │
│  │  └─ getCableRenderMode()                   │ │
│  └────────────────────────────────────────────┘ │
│                                                  │
└──────────────────────────────────────────────────┘
                        ▼
┌──────────────────────────────────────────────────┐
│           IGrid (Runtime Network Instance)       │
├──────────────────────────────────────────────────┤
│                                                  │
│  ┌──────────── Grid Cache System ────────────┐  │
│  │  ├─ IEnergyGrid      (能量子系统)         │  │
│  │  ├─ IStorageGrid     (存储子系统)         │  │
│  │  ├─ ICraftingGrid    (合成子系统)         │  │
│  │  ├─ ISecurityGrid    (安全子系统)         │  │
│  │  ├─ IPathingGrid     (路由子系统)         │  │
│  │  ├─ ITickManager     (时序子系统)         │  │
│  │  ├─ ISpatialCache    (空间子系统)         │  │
│  │  └─ 自定义缓存...                          │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
│  ┌──────────── Node System ──────────────────┐  │
│  │  IGridNode (网格节点)                      │  │
│  │  ├─ IGridBlock (节点定义)                 │  │
│  │  ├─ IGridConnection (连接)                │  │
│  │  └─ IGridHost (主机实现)                  │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
│  ┌──────────── Event System ─────────────────┐  │
│  │  MENetworkEvent (网络事件基类)             │  │
│  │  ├─ MENetworkPowerStatusChange            │  │
│  │  ├─ MENetworkChannelsChanged              │  │
│  │  ├─ MENetworkStorageEvent                 │  │
│  │  └─ MENetworkCraftingCpuChange            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
└──────────────────────────────────────────────────┘
```

---

## 使用示例

### 示例1: 创建ME存储设备

```java
public class MyMEDrive extends TileEntity 
    implements IGridHost, ICellContainer, IStorageMonitorable {
    
    private AENetworkProxy gridProxy;
    private MEMonitorHandler<IAEItemStack> internalHandler;
    private ItemStack[] cells = new ItemStack[10];
    
    public MyMEDrive() {
        gridProxy = new AENetworkProxy(this, "drive", 
            getItemFromTile(this), true);
        gridProxy.setFlags(GridFlags.REQUIRE_CHANNEL);
        
        internalHandler = new MEMonitorHandler<>(this, StorageChannel.ITEMS);
    }
    
    @Override
    public void onReady() {
        gridProxy.onReady();
    }
    
    @Override
    public IGridNode getGridNode(ForgeDirection dir) {
        return gridProxy.getNode();
    }
    
    @Override
    public int getCellCount() {
        return cells.length;
    }
    
    @Override
    public IMEInventoryHandler getCellInventory(int slot) {
        ItemStack cell = cells[slot];
        if (cell == null) return null;
        
        ICellHandler handler = AEApi.instance()
            .registries()
            .cell()
            .getHandler(cell);
            
        if (handler != null) {
            return handler.getCellInventory(cell, this, StorageChannel.ITEMS);
        }
        
        return null;
    }
    
    @Override
    public IMEMonitor<IAEItemStack> getItemInventory() {
        return internalHandler;
    }
    
    @Override
    public void blinkCell(int slot) {
        // 单元格闪烁动画
    }
}
```

### 示例2: 实现合成接口

```java
public class MyCraftingInterface extends TileEntity 
    implements ICraftingProvider, IGridHost {
    
    private AENetworkProxy gridProxy;
    private List<ICraftingPatternDetails> patterns = new ArrayList<>();
    private ItemStack[] patternSlots = new ItemStack[9];
    
    @Override
    public void provideCrafting(ICraftingProviderHelper helper) {
        // 解析所有模式
        for (ItemStack pattern : patternSlots) {
            if (pattern != null && pattern.getItem() instanceof ICraftingPatternItem) {
                ICraftingPatternItem pi = (ICraftingPatternItem) pattern.getItem();
                ICraftingPatternDetails details = pi.getPatternForItem(pattern, worldObj);
                if (details != null) {
                    helper.addCraftingOption(this, details);
                }
            }
        }
    }
    
    @Override
    public boolean pushPattern(ICraftingPatternDetails details, InventoryCrafting ic) {
        // 将模式推送到机器
        IAEItemStack[] inputs = details.getInputs();
        IAEItemStack[] outputs = details.getOutputs();
        
        // 检查输入
        for (IAEItemStack input : inputs) {
            if (input != null && !hasItem(input)) {
                return false;
            }
        }
        
        // 执行合成
        for (IAEItemStack input : inputs) {
            if (input != null) {
                consumeItem(input);
            }
        }
        
        for (IAEItemStack output : outputs) {
            if (output != null) {
                produceItem(output);
            }
        }
        
        return true;
    }
    
    @Override
    public boolean isBusy() {
        return isProcessing;
    }
}
```

---

## 与其他模组集成

### 1. 存储集成（箱子、管道等）

```java
// 注册外部存储处理器
IExternalStorageRegistry reg = AEApi.instance()
    .registries()
    .externalStorage();

reg.addExternalStorageInterface(new IExternalStorageHandler() {
    @Override
    public boolean canHandle(TileEntity te, ForgeDirection d, 
        StorageChannel channel, BaseActionSource src) {
        
        // 支持所有IInventory
        return te instanceof IInventory && channel == StorageChannel.ITEMS;
    }
    
    @Override
    public IMEInventory getInventory(TileEntity te, ForgeDirection d,
        StorageChannel channel, BaseActionSource src) {
        
        return new InventoryAdaptor((IInventory) te);
    }
});
```

### 2. 能量集成

```java
// RF能量转换
public class RFEnergyBridge implements IEnergySource {
    private IEnergyStorage rfStorage;
    
    @Override
    public double extractAEPower(double amt, Actionable mode, PowerMultiplier pm) {
        int rfAmount = (int)(amt * AE_TO_RF_RATIO);
        int extracted = rfStorage.extractEnergy(rfAmount, mode == Actionable.SIMULATE);
        return extracted / AE_TO_RF_RATIO;
    }
}
```

### 3. 合成集成（JEI/NEI）

```java
// 注册合成配方查看
@Override
public void registerRecipeCategories(IRecipeCategoryRegistration registry) {
    registry.addRecipeCategories(new InscriberRecipeCategory(guiHelper));
    registry.addRecipeCategories(new GrinderRecipeCategory(guiHelper));
}

@Override
public void registerRecipes(IRecipeRegistration registry) {
    // AE2铭刻器配方
    Collection<IInscriberRecipe> inscriber = AEApi.instance()
        .registries()
        .inscriber()
        .getRecipes();
    registry.addRecipes(inscriber, INSCRIBER_UID);
    
    // AE2磨粉机配方
    Collection<IGrinderEntry> grinder = AEApi.instance()
        .registries()
        .grinder()
        .getRecipes();
    registry.addRecipes(grinder, GRINDER_UID);
}
```

---

## 快速参考

### 常用API调用

```java
// 获取API实例
AEApi api = AEApi.instance();

// 创建物品列表
IItemList<IAEItemStack> items = api.storage().createItemList();

// 创建流体列表
IItemList<IAEFluidStack> fluids = api.storage().createFluidList();

// 获取定义
IDefinitions defs = api.definitions();
IBlocks blocks = defs.blocks();
IItems items = defs.items();

// 注册表
IRegistryContainer reg = api.registries();
ICellRegistry cells = reg.cell();
IExternalStorageRegistry extStorage = reg.externalStorage();

// Part辅助
IPartHelper partHelper = api.partHelper();
```

### 网格操作

```java
// 获取网格
IGridNode node = gridProxy.getNode();
IGrid grid = node.getGrid();

// 获取缓存
IEnergyGrid energy = grid.getCache(IEnergyGrid.class);
IStorageGrid storage = grid.getCache(IStorageGrid.class);
ICraftingGrid crafting = grid.getCache(ICraftingGrid.class);
ISecurityGrid security = grid.getCache(ISecurityGrid.class);

// 发送事件
grid.postEvent(new MENetworkStorageEvent(storage, StorageChannel.ITEMS));
```

### 存储操作

```java
// 获取存储监控器
IStorageGrid sg = grid.getCache(IStorageGrid.class);
IMEMonitor<IAEItemStack> monitor = sg.getItemInventory();

// 注入物品
IAEItemStack stack = AEItemStack.create(new ItemStack(Items.diamond));
stack.setStackSize(64);
IAEItemStack remaining = monitor.injectItems(stack, Actionable.MODULATE, source);

// 提取物品
IAEItemStack request = AEItemStack.create(new ItemStack(Items.diamond));
request.setStackSize(32);
IAEItemStack extracted = monitor.extractItems(request, Actionable.MODULATE, source);

// 获取可用物品列表
IItemList<IAEItemStack> available = monitor.getStorageList();
```

---

## 总结

### AE2-Unofficial核心优势

✅ **高度模块化**: 网格缓存系统支持独立扩展  
✅ **泛型设计**: 同一套接口支持物品和流体  
✅ **丰富扩展点**: 11+注册表支持第三方集成  
✅ **事件驱动**: 异步更新机制提升性能  
✅ **强大的权限系统**: 基于玩家/机器的双重权限

### 接口使用建议

1. **基础集成**: 从`IGridHost`开始，接入ME网络
2. **存储扩展**: 实现`IExternalStorageHandler`连接外部容器
3. **合成扩展**: 实现`ICraftingProvider`提供配方
4. **自定义Part**: 继承`AEBasePart`快速创建组件
5. **能量集成**: 实现`IEnergySource`桥接其他能量系统

---

**最后更新**: 2026-02-12  
**文档版本**: 1.0  
**AE2版本**: rv3-beta (GTNH)
