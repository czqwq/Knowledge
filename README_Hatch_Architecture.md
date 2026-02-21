# GT5U 舱室架构深度解析

> **代码来源**: https://github.com/GTNewHorizons/GT5-Unofficial (以下简称 GT5U)  
> 以及 https://github.com/GTNewHorizons/Applied-Energistics-2-Unofficial (以下简称 AE2U)  
> 所有代码引用均来自本地克隆版本，精确到文件路径与行号。

---

## 目录

1. [舱室（Hatch）总览与类层次](#1-舱室hatch总览与类层次)
2. [舱室注册流程](#2-舱室注册流程)
3. [标准输入/输出舱室实现原理](#3-标准输入输出舱室实现原理)
   - [流体输入舱室 MTEHatchInput](#31-流体输入舱室-mtehatchinput)
   - [物品输入总线 MTEHatchInputBus](#32-物品输入总线-mtehatchinputbus)
   - [流体输出舱室 MTEHatchOutput](#33-流体输出舱室-mtehatchoutput)
   - [物品输出总线 MTEHatchOutputBus](#34-物品输出总线-mtehatchoutputbus)
4. [ME 舱室注册与实现](#4-me-舱室注册与实现)
   - [ME 输入总线 MTEHatchInputBusME](#41-me-输入总线-mtehatchinputbusme)
   - [ME 流体输入舱室 MTEHatchInputME](#42-me-流体输入舱室-mtehatchinputme)
   - [ME 输出总线 MTEHatchOutputBusME](#43-me-输出总线-mtehatchoutputbusme)
   - [ME 流体输出舱室 MTEHatchOutputME](#44-me-流体输出舱室-mtehatchoutputme)
   - [ME 输出基类 MTEHatchOutputMEBase](#45-me-输出基类-mtehatchoutputmebase)
5. [物品与流体如何吞吐](#5-物品与流体如何吞吐)
   - [读取输入](#51-读取输入)
   - [消耗输入](#52-消耗输入)
   - [输出物品](#53-输出物品)
   - [输出流体](#54-输出流体)
6. [舱室格子（Inventory Slot）实现原理](#6-舱室格子inventory-slot实现原理)
7. [结构识别——底层逻辑](#7-结构识别底层逻辑)
   - [IHatchElement 与 HatchElement 枚举](#71-ihatchelement-与-hatchelement-枚举)
   - [HatchElementBuilder 与 buildHatchAdder](#72-hatchelementbuilder-与-buildhatchadder)
   - [checkMachine 与 checkPiece](#73-checkmachine-与-checkpiece)
   - [addToMachineList 与 addInputBusToMachineList 等](#74-addtomachinelist-与-addinputbustomachinelist-等)
   - [clearHatches 与 checkStructure](#75-clearhatches-与-checkstructure)
8. [如何实现一个新的自定义舱室](#8-如何实现一个新的自定义舱室)
   - [Step 1：继承正确的基类](#step-1继承正确的基类)
   - [Step 2：选取 MetaTile ID](#step-2选取-metatile-id)
   - [Step 3：在 ItemList 中注册 enum 常量](#step-3在-itemlist-中注册-enum-常量)
   - [Step 4：在加载器中实例化并绑定 ItemStack](#step-4在加载器中实例化并绑定-itemstack)
   - [Step 5：在多方块中加入识别逻辑](#step-5在多方块中加入识别逻辑)
   - [Step 6：实现自定义 IHatchElement（可选）](#step-6实现自定义-ihatchelement可选)
9. [真实案例：EBF 中的完整流程](#9-真实案例ebf-中的完整流程)
10. [GT5U 与 AE2U 交互——ME 舱室底层](#10-gt5u-与-ae2u-交互me-舱室底层)

---

## 1. 舱室（Hatch）总览与类层次

GT5U 中所有舱室的基类链：

```
MetaTileEntity
  └── MTETieredMachineBlock
        └── MTEBasicTank            (provides fluid tank + inventory)
              └── MTEHatch           (adds texture management + AE2 crafting icon)
                    ├── MTEHatchInput          (流体输入)
                    │     └── MTEHatchInputME  (ME 流体输入)
                    ├── MTEHatchOutput         (流体输出)
                    │     └── MTEHatchOutputME (ME 流体输出)
                    ├── MTEHatchInputBus       (物品输入总线)
                    │     ├── MTEHatchInputBusME      (ME 物品输入总线)
                    │     └── MTEHatchInputBusCompressed (压缩输入总线)
                    ├── MTEHatchOutputBus      (物品输出总线)
                    │     └── MTEHatchOutputBusME     (ME 物品输出总线)
                    ├── MTEHatchEnergy         (能量输入)
                    ├── MTEHatchDynamo         (能量输出)
                    ├── MTEHatchMaintenance    (维护)
                    └── MTEHatchMuffler        (消音器)
```

**文件对应关系**（`GT5-Unofficial/src/main/java/`，下同省略前缀）：

| 类名 | 文件路径 |
|------|----------|
| `MTEHatch` | `gregtech/api/metatileentity/implementations/MTEHatch.java` |
| `MTEHatchInput` | `gregtech/api/metatileentity/implementations/MTEHatchInput.java` |
| `MTEHatchInputBus` | `gregtech/api/metatileentity/implementations/MTEHatchInputBus.java` |
| `MTEHatchOutput` | `gregtech/api/metatileentity/implementations/MTEHatchOutput.java` |
| `MTEHatchOutputBus` | `gregtech/api/metatileentity/implementations/MTEHatchOutputBus.java` |
| `MTEHatchInputBusME` | `gregtech/common/tileentities/machines/MTEHatchInputBusME.java` |
| `MTEHatchInputME` | `gregtech/common/tileentities/machines/MTEHatchInputME.java` |
| `MTEHatchOutputBusME` | `gregtech/common/tileentities/machines/outputme/MTEHatchOutputBusME.java` |
| `MTEHatchOutputME` | `gregtech/common/tileentities/machines/outputme/MTEHatchOutputME.java` |
| `MTEHatchOutputMEBase` | `gregtech/common/tileentities/machines/outputme/base/MTEHatchOutputMEBase.java` |

### MTEHatch 基类核心逻辑

**文件**: `gregtech/api/metatileentity/implementations/MTEHatch.java`

```java
// 行 15
public abstract class MTEHatch extends MTEBasicTank implements ICraftingIconProvider {

    // 行 18-22：枚举连接类型（普通电缆/无线/激光）
    public enum ConnectionType {
        CABLE,
        WIRELESS,
        LASER
    }

    // 行 41: 每个 tier 的背包格子数公式
    public static int getSlots(int aTier) {
        return (aTier + 1) * (aTier + 1);
    }
    // tier 0 (ULV) → 1格, tier 1 (LV) → 4格, tier 2 (MV) → 9格, ..., tier 8 (UV) → 81格

    // 行 115-128: 贴图更新（在结构识别成功后调用）
    public final void updateTexture(int id) {
        int newTexturePage = id >> 7;
        int newTextureIndex = id & 127;
        if (newTexturePage == texturePage && newTextureIndex == textureIndex) return;
        texturePage = newTexturePage;
        textureIndex = newTextureIndex;
        IGregTechTileEntity base = getBaseMetaTileEntity();
        if (base.isServerSide()) {
            base.issueTileUpdate();
        } else {
            base.issueTextureUpdate();
        }
    }

    // 行 151: 由多方块在结构成功后设置 AE2 合成图标
    public final void updateCraftingIcon(ItemStack icon) {
        this.ae2CraftingIcon = icon;
    }

    // 行 166-168: 子类可重写此方法以返回用于结构检查的等级
    public byte getTierForStructure() {
        return mTier;
    }
}
```

---

## 2. 舱室注册流程

GT5U 的 MetaTileEntity 注册分四步：

### 2.1 在 `MetaTileEntity` 构造函数中注册到全局 Block

**文件**: `gregtech/api/metatileentity/MetaTileEntity.java`，行 113-115

```java
public MetaTileEntity(int aID, ...) {
    setBaseMetaTileEntity(GregTechAPI.constructBaseMetaTileEntity());
    getBaseMetaTileEntity().setMetaTileID((short) aID);
    // setMetaTileID 将此 MTE 注册进 BaseMetaTileEntity，其 ID 作为 GregTechAPI.sBlockMachines 的 ItemStack meta 值
}
```

`getStackForm(long aAmount)` 在行 187：

```java
public ItemStack getStackForm(long aAmount) {
    return new ItemStack(GregTechAPI.sBlockMachines, (int) aAmount, getBaseMetaTileEntity().getMetaTileID());
}
```

### 2.2 在 `ItemList` 枚举中声明

**文件**: `gregtech/api/enums/ItemList.java`

```java
// 行 1031-1040: 标准输入流体舱室
Hatch_Input_ULV,
Hatch_Input_LV,
Hatch_Input_MV,
Hatch_Input_HV,
Hatch_Input_EV,
Hatch_Input_IV,
// ...
// 行 1054-1063: 标准物品输入总线
Hatch_Input_Bus_ULV,
Hatch_Input_Bus_LV,
// ...
// 行 2144-2147: ME 舱室
Hatch_Input_Bus_ME,
Hatch_Input_Bus_ME_Advanced,
Hatch_Input_ME,
Hatch_Input_ME_Advanced,
// 行 1678-1679: ME 输出
Hatch_Output_Bus_ME,
Hatch_Output_ME,
```

### 2.3 在 `LoaderMetaTileEntities` 中实例化并绑定

**文件**: `gregtech/loaders/preload/LoaderMetaTileEntities.java`

```java
// 行 9025-9053: 注册标准流体输入舱室（所有 Tier）
ItemList.Hatch_Input_ULV
    .set(new MTEHatchInput(INPUT_HATCH_ULV.ID, "hatch.input.tier.00", "Input Hatch (ULV)", 0).getStackForm(1L));
ItemList.Hatch_Input_LV
    .set(new MTEHatchInput(INPUT_HATCH_LV.ID,  "hatch.input.tier.01", "Input Hatch (LV)",  1).getStackForm(1L));
// ... 依此类推到 MAX tier

// 行 9141-9169: 注册标准流体输出舱室
ItemList.Hatch_Output_ULV
    .set(new MTEHatchOutput(OUTPUT_HATCH_ULV.ID, "hatch.output.tier.00", "Output Hatch (ULV)", 0).getStackForm(1L));
// ...

// 行 9439-...: 注册标准物品输入总线
ItemList.Hatch_Input_Bus_ULV
    .set(new MTEHatchInputBus(INPUT_BUS_ULV.ID, "hatch.input_bus.tier.00", "Input Bus (ULV)", 0).getStackForm(1L));
// ...

// 行 9386-9411: 注册 ME 舱室（registerAE2Hatches 方法内）
ItemList.Hatch_Output_Bus_ME
    .set(new MTEHatchOutputBusME(OUTPUT_BUS_ME.ID, "hatch.output_bus.me", "Output Bus (ME)").getStackForm(1L));
ItemList.Hatch_Input_Bus_ME
    .set(new MTEHatchInputBusME(INPUT_BUS_ME.ID, false, "hatch.input_bus.me.basic", "Stocking Input Bus (ME)").getStackForm(1L));
ItemList.Hatch_Input_Bus_ME_Advanced
    .set(new MTEHatchInputBusME(INPUT_BUS_ME_ADVANCED.ID, true, "hatch.input_bus.me", "Advanced Stocking Input Bus (ME)").getStackForm(1L));
ItemList.Hatch_Input_ME
    .set(new MTEHatchInputME(INPUT_HATCH_ME.ID, false, "hatch.input.me.basic", "Stocking Input Hatch (ME)").getStackForm(1L));
ItemList.Hatch_Input_ME_Advanced
    .set(new MTEHatchInputME(INPUT_HATCH_ME_ADVANCED.ID, true, "hatch.input.me", "Advanced Stocking Input Hatch (ME)").getStackForm(1L));
ItemList.Hatch_Output_ME
    .set(new MTEHatchOutputME(OUTPUT_HATCH_ME.ID, "hatch.output.me", "Output Hatch (ME)").getStackForm(1L));
```

**注意**：`ItemList.Hatch_Input_Bus_ME_Advanced` 第二个参数 `autoPullAvailable=true` 开启了"自动从 ME 网络拉取物品列表"功能。基础版本 `false` 只做 Stocking（按格子配置提取）。

---

## 3. 标准输入/输出舱室实现原理

### 3.1 流体输入舱室 MTEHatchInput

**文件**: `gregtech/api/metatileentity/implementations/MTEHatchInput.java`

#### 容量与格子数

```java
// 行 44-50: 单格子构造（默认 4 个槽：容器输入 + 流体输出容器 + 显示槽 + 保留）
public MTEHatchInput(int aID, String aName, String aNameRegional, int aTier) {
    super(aID, aName, aNameRegional, aTier, 4, new String[]{
        "Fluid Input for Multiblocks",
        "Right click with screwdriver to toggle input filter",
        String.format("Capacity: %sL", formatNumber(8000L * (1L << aTier)))
    });
}

// 行 70: 每个格子的容量
public int getCapacityPerTank(int aTier, int aSlot) {
    return (int) (8000L * (1L << aTier) / aSlot);
}

// 行 213: 总容量（单格子版本）
@Override
public int getCapacity() {
    return customCapacity != 0 ? customCapacity : (8000 * (1 << mTier));
}
```

容量公式：`8000 * 2^tier` 毫升，即：
- LV（tier 1）：16,000 mL
- HV（tier 3）：64,000 mL
- EV（tier 4）：128,000 mL

#### 流体过滤

```java
// 行 193-195: 过滤器控制（可通过螺丝刀关闭过滤）
@Override
public boolean isFluidInputAllowed(FluidStack aFluid) {
    return mRecipeMap == null || disableFilter || mRecipeMap.containsInput(aFluid);
}
```

`mRecipeMap` 在结构识别时由 `addInputHatchToMachineList` → `setHatchRecipeMap(hatch)` 注入，代表多方块所用的配方表。过滤器开启时只允许该配方表中涉及的流体进入。

#### 物品槽允许访问规则

```java
// 行 198-211
@Override
public boolean allowPullStack(IGregTechTileEntity aBaseMetaTileEntity, int aIndex, ForgeDirection side, ItemStack aStack) {
    return side == aBaseMetaTileEntity.getFrontFacing() && aIndex == 1;  // 只允许从正面拉出 index=1 的容器输出槽
}

@Override
public boolean allowPutStack(IGregTechTileEntity aBaseMetaTileEntity, int aIndex, ForgeDirection side, ItemStack aStack) {
    return side == aBaseMetaTileEntity.getFrontFacing() && aIndex == 0   // 只允许从正面放入 index=0 的容器输入槽
        && (mRecipeMap == null || disableFilter
            || mRecipeMap.containsInput(aStack)
            || mRecipeMap.containsInput(GTUtility.getFluidForFilledItem(aStack, true)));
}
```

#### onPostTick 流体自动推送（输出舱 MTEHatchOutput 的行为）

流体输入舱不自动推出，而输出舱（`MTEHatchOutput`）在 `onPostTick` 中主动推送：  
（见第3.3节）

---

### 3.2 物品输入总线 MTEHatchInputBus

**文件**: `gregtech/api/metatileentity/implementations/MTEHatchInputBus.java`

#### 格子数量

```java
// 行 63: 构造函数调用 getSlots(tier) + 1（最后一格是电路板槽）
public MTEHatchInputBus(int id, String name, String nameRegional, int tier) {
    this(id, name, nameRegional, tier, getSlots(tier) + 1);
}
// getSlots(tier) = (tier+1)^2，来自 MTEHatch 行 41
// tier 1 (LV) → 4 + 1 = 5 槽; tier 4 (EV) → 25 + 1 = 26 槽
```

#### 每 tick 整理背包

```java
// 行 162-167: 服务端每 tick 调用
@Override
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTimer) {
    if (aBaseMetaTileEntity.isServerSide()) {
        updateSlots();
    }
    super.onPostTick(aBaseMetaTileEntity, aTimer);
}

// 行 168-172
public void updateSlots() {
    for (int i = 0; i < mInventory.length - 1; i++)
        if (mInventory[i] != null && mInventory[i].stackSize <= 0) mInventory[i] = null;
    if (!disableSort) fillStacksIntoFirstSlots();
}

// 行 174-176: 将物品压缩到最前面的格子
protected void fillStacksIntoFirstSlots() {
    GTUtility.compactInventory(Arrays.asList(mInventory), 0, mInventory.length - 1);
}
```

#### 电路板槽（Circuit Slot）

```java
// 行 268-270: 电路板固定在最后一个槽
@Override
public int getCircuitSlot() {
    return getSlots(mTier);  // 即 (tier+1)^2
}
```

#### 过滤器与单格子限制

```java
// 行 249-255
@Override
public boolean allowPutStack(IGregTechTileEntity aBaseMetaTileEntity, int aIndex, ForgeDirection side, ItemStack aStack) {
    return side == getBaseMetaTileEntity().getFrontFacing() && aIndex != getCircuitSlot()
        && (mRecipeMap == null || disableFilter || mRecipeMap.containsInput(aStack))
        && (disableLimited || limitedAllowPutStack(aIndex, aStack));
}
// disableLimited=false 时每种物品只允许进一个格子（"一格一种"模式）
```

---

### 3.3 流体输出舱室 MTEHatchOutput

**文件**: `gregtech/api/metatileentity/implementations/MTEHatchOutput.java`

#### 主动推出流体

```java
// 行 111-125: 每 tick 主动向正面推送流体
@Override
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    super.onPostTick(aBaseMetaTileEntity, aTick);
    if (aBaseMetaTileEntity.isServerSide() && aBaseMetaTileEntity.isAllowedToWork() && mFluid != null) {
        IFluidHandler tTileEntity = aBaseMetaTileEntity
            .getITankContainerAtSide(aBaseMetaTileEntity.getFrontFacing());
        if (tTileEntity != null) {
            GTUtility.moveFluid(
                aBaseMetaTileEntity,
                tTileEntity,
                aBaseMetaTileEntity.getFrontFacing(),
                Math.max(1, mFluid.amount),
                null);
        }
    }
}
```

#### 输出模式（10 种）

```java
// 行 140-205: 螺丝刀切换 mMode（0-9）
// mMode 0: 输出所有（Steam + 杂液 + 物品）
// mMode 5: 只输出物品
// mMode 8/9: 锁定输出特定流体

public boolean outputsSteam() { return mMode < 4; }
public boolean outputsLiquids() { return mMode % 2 == 0 || mMode == 9; }
public boolean outputsItems() { return mMode % 4 < 2 && mMode != 9; }

// 行 381-395: canStoreFluid 决定是否接受特定流体的写入（由多方块在 addOutput 时调用）
@Override
public boolean canStoreFluid(@Nonnull FluidStack fluidStack) {
    if (mFluid != null && !GTUtility.areFluidsEqual(mFluid, fluidStack)) return false;
    if (isFluidLocked()) {
        if (lockedFluidName == null) return true;
        return lockedFluidName.equals(fluidStack.getFluid().getName());
    }
    if (GTModHandler.isSteam(fluidStack)) return outputsSteam();
    return outputsLiquids();
}
```

---

### 3.4 物品输出总线 MTEHatchOutputBus

**文件**: `gregtech/api/metatileentity/implementations/MTEHatchOutputBus.java`

#### 主动推出物品

```java
// 行 247-262: 每 8 tick 向正面推送一次物品
@Override
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    super.onPostTick(aBaseMetaTileEntity, aTick);
    if (aBaseMetaTileEntity.isServerSide() && aBaseMetaTileEntity.isAllowedToWork()
        && (aTick & 0x7) == 0
        && pushOutputInventory()) {
        GTItemTransfer transfer = new GTItemTransfer();
        transfer.push(aBaseMetaTileEntity, aBaseMetaTileEntity.getFrontFacing());
        transfer.setStacksToTransfer(getStackTransferAmount());
        transfer.setMaxItemsPerTransfer(getStackSizeLimit(-1, null));
        if (transfer.transfer() > 0) {
            GTUtility.cleanInventory(this);
        }
    }
}
```

#### 物品写入（storePartial，由多方块配方结果写入）

```java
// 行 187-208
@Override
public boolean storePartial(ItemStack stack, boolean simulate) {
    if (!simulate) markDirty();
    if (lockedItem != null && !lockedItem.isItemEqual(stack)) return false;
    int invLength = mInventory.length;
    for (int i = 0; i < invLength && stack.stackSize > 0; i++) {
        ItemStack slot = mInventory[i];
        if (!isStackInvalid(slot) && !areStacksEqual(slot, stack)) continue;
        int inSlot = slot == null ? 0 : slot.stackSize;
        int toInsert = Math.min(Math.min(getInventoryStackLimit(), getStackSizeLimit(i, slot) - inSlot), stack.stackSize);
        if (toInsert == 0) continue;
        if (!simulate) {
            if (isStackInvalid(slot)) mInventory[i] = slot = stack.splitStack(0);
            slot.stackSize += toInsert;
        }
        stack.stackSize -= toInsert;
    }
    return stack.stackSize == 0;
}
```

**事务（Transaction）机制**：`createTransaction()` 返回 `StandardOutputBusTransaction`，支持批量写入再一次性 `commit()`，避免中途失败导致物品丢失：

```java
// 行 340-420（StandardOutputBusTransaction 内部类）
@Override
public boolean storePartial(GTUtility.ItemId id, ItemStack stack) {
    if (!active) throw new IllegalStateException("Cannot add to a transaction after committing it");
    // ... 模拟写入
}

@Override
public void commit() {
    assert mInventory.length == inventory.length;
    System.arraycopy(inventory, 0, mInventory, 0, inventory.length);
    MTEHatchOutputBus.this.markDirty();
    active = false;
}
```

---

## 4. ME 舱室注册与实现

### 4.1 ME 输入总线 MTEHatchInputBusME

**文件**: `gregtech/common/tileentities/machines/MTEHatchInputBusME.java`

继承 `MTEHatchInputBus`，同时实现 `IRecipeProcessingAwareHatch`（感知配方处理的开始/结束）、`ISmartInputHatch`（快速配方检测）、`IMEConnectable`（ME 网络连接）。

#### 构造与 AE2 代理

```java
// 行 122-127
public MTEHatchInputBusME(int aID, boolean autoPullAvailable, String aName, String aNameRegional) {
    super(aID, aName, aNameRegional, autoPullAvailable ? 6 : 4, 2, getDescriptionArray(autoPullAvailable));
    this.autoPullAvailable = autoPullAvailable;
    disableSort = true;  // ME 总线禁用自动排序
}

// 行 262-280: AENetworkProxy 懒初始化
@Override
public @NotNull AENetworkProxy getProxy() {
    if (gridProxy == null) {
        if (getBaseMetaTileEntity() instanceof IGridProxyable) {
            gridProxy = new AENetworkProxy(
                (IGridProxyable) getBaseMetaTileEntity(),
                "proxy",
                autoPullAvailable ? ItemList.Hatch_Input_Bus_ME_Advanced.get(1)
                                  : ItemList.Hatch_Input_Bus_ME.get(1),
                true);
            gridProxy.setFlags(GridFlags.REQUIRE_CHANNEL);
            updateValidGridProxySides();
            // ...
        }
    }
    return this.gridProxy;
}
```

#### ME 连接侧面控制

```java
// 行 227-239
protected void updateValidGridProxySides() {
    if (additionalConnection) {
        getProxy().setValidSides(EnumSet.complementOf(EnumSet.of(ForgeDirection.UNKNOWN)));  // 全侧连接
    } else {
        getProxy().setValidSides(EnumSet.of(getBaseMetaTileEntity().getFrontFacing()));  // 只正面
    }
}
// 行 241-247: 使用线剪右键切换 additionalConnection
```

#### 配方执行钩子

```java
// 行 649-655: 配方开始前调用
@Override
public void startRecipeProcessing() {
    cachedActivity = isAllowedToWork();
    processingRecipe = true;
    updateAllInformationSlots();  // 将当前 ME 网络的物品量同步到内部 slots[]
}

// 行 717-760: 配方结束后从 ME 网络实际提取物品
@Override
public CheckRecipeResult endRecipeProcessing(MTEMultiBlockBase controller) {
    // ...
    IMEMonitor<IAEItemStack> sg = proxy.getStorage().getItemInventory();
    IEnergyGrid energy = getProxy().getEnergy();

    for (Slot slot : slots) {
        if (slot == null || slot.extracted == null || slot.extractedAmount == 0) continue;
        int toExtract = slot.extractedAmount - slot.extracted.stackSize;
        if (toExtract <= 0) continue;

        IAEItemStack request = slot.createAEStack(toExtract);
        // Platform.poweredExtraction 从 ME 网络扣款 AE2 能量并提取物品
        IAEItemStack result = Platform.poweredExtraction(energy, sg, request, getRequestSource());

        if (result == null || result.getStackSize() != toExtract) {
            controller.stopMachine(ShutDownReasonRegistry.CRITICAL_NONE);
            return SimpleCheckRecipeResult.ofFailurePersistOnShutdown("stocking_bus_fail_extraction");
        }
    }
    processingRecipe = false;
    return checkRecipeResult;
}
```

**关键**：ME 输入总线在配方执行过程中，`startRecipeProcessing` 将 ME 网络当前物品快照同步到虚拟格子；配方匹配使用这些虚拟格子的物品；`endRecipeProcessing` 在配方真正开始执行后才从 ME 网络实际扣除物品，如果此时 ME 网络中物品已不足则停机。

#### 自动拉取模式（Advanced 版本）

```java
// 行 656-705: 仅 autoPullAvailable=true 时可用
protected void refreshItemList() {
    if (!isAllowedToWork()) return;
    IMEMonitor<IAEItemStack> sg = getProxy().getStorage().getItemInventory();
    Iterator<IAEItemStack> iterator = sg.getStorageList().iterator();
    int index = 0;
    clearSlotConfigs();
    while (iterator.hasNext() && index < SLOT_COUNT) {
        IAEItemStack curr = iterator.next();
        if (curr.getStackSize() < minAutoPullStackSize) continue;
        setSlotConfig(index, GTUtility.copyAmount(1, curr.getItemStack()));
        Slot newSlot = slots[index];
        if (newSlot != null) {
            newSlot.extracted = curr.getItemStack();
            newSlot.extractedAmount = newSlot.extracted.stackSize;
        }
        // ...
        index++;
    }
}
// 由 onPostTick 每 autoPullRefreshTime (默认100) tick 调用一次
```

---

### 4.2 ME 流体输入舱室 MTEHatchInputME

**文件**: `gregtech/common/tileentities/machines/MTEHatchInputME.java`

与 `MTEHatchInputBusME` 设计完全对称，继承 `MTEHatchInput`，逻辑核心相同，处理的对象是 `IAEFluidStack` 而不是 `IAEItemStack`。

```java
// 行 103: 类声明
public class MTEHatchInputME extends MTEHatchInput implements IPowerChannelState, IAddGregtechLogo,
    IAddUIWidgets, IRecipeProcessingAwareHatch, ISmartInputHatch, IDataCopyable, IMEConnectable {

    protected static final int SLOT_COUNT = 16;  // 行 106: 支持 16 种流体配置
```

`drain()` 从虚拟槽提供流体给多方块：

```java
// 行 370-412
@Override
public FluidStack drain(ForgeDirection side, FluidStack fluid, boolean doDrain) {
    for (int i = 0; i < SLOT_COUNT; i++) {
        Slot slot = slots[i];
        if (slot == null || slot.extracted == null) continue;
        if (slot.extracted.isFluidEqual(fluid)) {
            int toDrain = Math.min(slot.extracted.amount, fluid.amount);
            if (!doDrain) return new FluidStack(fluid, toDrain);
            slot.extracted.amount -= toDrain;
            return new FluidStack(fluid, toDrain);
        }
    }
    return null;
}
```

---

### 4.3 ME 输出总线 MTEHatchOutputBusME

**文件**: `gregtech/common/tileentities/machines/outputme/MTEHatchOutputBusME.java`

继承 `MTEHatchOutputBus`，核心逻辑委托给内部的 `MTEHatchOutputMEBase<IAEItemStack, MEFilterItem, ItemStack> provider`。

```java
// 行 71-83: 构造
public MTEHatchOutputBusME(int aID, String aName, String aNameRegional) {
    super(aID, aName, aNameRegional, 4,
        new String[]{
            "Item Output for Multiblocks",
            "Stores directly into ME",
            "Can cache 1600 items by default",
            "Change cache size by inserting a storage cell",
            // ...
        }, 1);  // inventorySize=1：只有一个槽放 AE2 存储元件
}

// 行 107-115: provider 是真正的 ME 逻辑承载者
private final MTEHatchOutputMEBase<IAEItemStack, MEFilterItem, ItemStack> provider =
    new MTEHatchOutputMEBase<IAEItemStack, MEFilterItem, ItemStack>(
        this,
        new MEFilterItem(),
        1_600  // 默认缓存容量 1600 个物品
    ) {};
```

#### storePartial：直接写入 ME 缓存

```java
// 行 124-127
@Override
public boolean storePartial(ItemStack stack, boolean simulate) {
    return provider.storePartial(stack, simulate);
    // provider.storePartial 实际上是 MTEHatchOutputMEBase.storePartial（见4.5节）
}
```

#### 禁止自动推送（Override pushOutputInventory）

```java
// 行 318
@Override
public boolean pushOutputInventory() {
    return false;  // ME 输出总线不向外推送，而是缓存后周期性推入 ME 网络
}
```

#### 事务机制（MEOutputBusTransaction）

```java
// 行 130-175: ME 专用事务
class MEOutputBusTransaction implements IOutputBusTransaction {
    private final AECacheCounter<GTUtility.ItemId> cache = new AECacheCounter<>();
    // ...

    @Override
    public boolean storePartial(GTUtility.ItemId id, ItemStack stack) {
        if (!canStore(id, stack)) return false;
        cache.insert(id, stack.stackSize);
        stack.stackSize = 0;
        return true;
    }

    @Override
    public void commit() {
        cache.iterateAll((id, amount) -> {
            provider.addToCache(
                provider.getFilter().fromNative(id.getItemStack()).setStackSize(amount));
        });
        MTEHatchOutputBusME.this.markDirty();
        active = false;
    }
}
```

---

### 4.4 ME 流体输出舱室 MTEHatchOutputME

**文件**: `gregtech/common/tileentities/machines/outputme/MTEHatchOutputME.java`

与 `MTEHatchOutputBusME` 完全对称，处理 `IAEFluidStack`，继承 `MTEHatchOutput`，内部 provider 使用 `MTEHatchOutputMEBase<IAEFluidStack, MEFilterFluid, FluidStack>`，默认缓存容量 `81_000` mL。

---

### 4.5 ME 输出基类 MTEHatchOutputMEBase

**文件**: `gregtech/common/tileentities/machines/outputme/base/MTEHatchOutputMEBase.java`

这是 ME 输出逻辑的核心，通过 `Environment<T, F, I>` 接口与具体舱室解耦。

#### 缓存机制

```java
// 行 112-115
protected final AECacheCounter<T> cache = new AECacheCounter<>();
public static long DEFAULT_CAPACITY;
protected long baseCapacity;
protected long cacheCapacity;
```

`AECacheCounter` 是一个 `IAEStack → long` 的计数映射，追踪当前待推入 ME 的物品总量。

#### storePartial（写入缓存）

```java
// 行 529-537
public boolean storePartial(I stack, boolean simulate) {
    if (lastInputTick != tickCounter && !canStore(stack)) {
        return false;  // 如果本 tick 没有输入过且容量满，拒绝
    }
    if (!simulate) {
        addToCache(stack);
    }
    return true;
}
```

#### flushCachedStack（周期性推入 ME 网络）

```java
// 行 471-487: 每 40 tick 或缓存超时后执行
protected void flushCachedStack() {
    var proxy = getProxy();
    if (!proxy.isActive() || cache.isEmpty()) return;
    try {
        final IEnergySource energy = proxy.getEnergy();
        IMEInventory<T> sg = (cacheMode && cell != null) ? cell : env.getNetworkInvtory();
        BaseActionSource source = env.getActionSource();
        cache.updateAll((stack, amount) -> {
            stack.setStackSize(amount);
            T rest = Platform.poweredInsert(energy, sg, stack, source);
            // Platform.poweredInsert 会消耗 AE2 能量并把物品注入 ME 网络
            if (rest == null) return 0L;
            return rest.getStackSize();  // 返回未能注入的余量
        });
    } catch (final GridAccessException ignored) {}
    lastOutputTick = tickCounter;
}
```

#### Cache Mode 与 Check Mode

```java
// 行 155-162: Cache Mode 开启时使用内部 AE2 存储元件而不是直接推入网络
public List<IMEInventoryHandler> getCellArray(final StorageChannel channel) {
    if (cacheMode && this.getProxy().isActive() && channel == env.getChannel()) {
        if (cellRead != null) return Collections.singletonList(cellRead);
    }
    return Collections.emptyList();
}
// 当 cacheMode=true 时，插入的存储元件可作为 ME 网络的一部分，暂存超出默认容量的物品

// 行 227-237: Check Mode（只在 cacheMode 下有效）
// 若 checkMode=true，storePartial 会使用 cell.injectItems(..., SIMULATE) 检查元件是否还有空间
// 可以精确避免因存储元件满而丢失物品
```

---

## 5. 物品与流体如何吞吐

### 5.1 读取输入

**文件**: `gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java`

#### 读取所有输入物品

```java
// 行 1877-1930 (getStoredInputs)
public ArrayList<ItemStack> getStoredInputs() {
    ArrayList<ItemStack> rList = new ArrayList<>();
    Map<GTUtility.ItemId, ItemStack> inputsFromME = new HashMap<>();
    for (MTEHatchInputBus tHatch : validMTEList(mInputBusses)) {
        if (tHatch instanceof MTEHatchCraftingInputME) continue;
        tHatch.mRecipeMap = getRecipeMap();
        IGregTechTileEntity tileEntity = tHatch.getBaseMetaTileEntity();
        boolean isMEBus = tHatch instanceof MTEHatchInputBusME;
        for (int i = tileEntity.getSizeInventory() - 1; i >= 0; i--) {
            ItemStack itemStack = tileEntity.getStackInSlot(i);
            if (itemStack != null) {
                if (isMEBus) {
                    // ME 总线：相同物品只出现一次（取 ID 去重）
                    inputsFromME.put(GTUtility.ItemId.createNoCopy(itemStack), itemStack);
                } else {
                    rList.add(itemStack);
                }
            }
        }
    }
    // 也包含主控台 slot 1 的电路板
    ItemStack stackInSlot1 = getStackInSlot(1);
    if (stackInSlot1 != null && stackInSlot1.getUnlocalizedName().startsWith("gt.integrated_circuit"))
        rList.add(stackInSlot1);
    rList.addAll(inputsFromME.values());
    return rList;
}
```

#### 读取所有输入流体

```java
// 行 1794-1815 (getStoredFluids)
public ArrayList<FluidStack> getStoredFluids() {
    ArrayList<FluidStack> rList = new ArrayList<>();
    for (MTEHatchInput tHatch : validMTEList(mInputHatches)) {
        setHatchRecipeMap(tHatch);
        if (tHatch.getFluid() != null && tHatch.isFluidInputAllowed(tHatch.getFluid())) {
            rList.add(tHatch.getFluid());
        }
        // 处理多格子舱室（MultiInput 子类）
    }
    return rList;
}
```

---

### 5.2 消耗输入

#### 消耗物品

```java
// 行 1763-1793 (depleteInput for ItemStack)
public boolean depleteInput(ItemStack aStack) {
    if (GTUtility.isStackInvalid(aStack)) return false;
    FluidStack aLiquid = GTUtility.getFluidForFilledItem(aStack, true);
    if (aLiquid != null) return depleteInput(aLiquid);  // 液体容器转为流体消耗
    for (MTEHatchInput tHatch : validMTEList(mInputHatches)) { ... }
    for (MTEHatchInputBus tHatch : validMTEList(mInputBusses)) {
        tHatch.mRecipeMap = getRecipeMap();
        final IGregTechTileEntity baseMetaTileEntity = tHatch.getBaseMetaTileEntity();
        for (int i = baseMetaTileEntity.getSizeInventory() - 1; i >= 0; i--) {
            if (i == tHatch.getCircuitSlot()) continue;
            if (GTUtility.areStacksEqual(aStack, baseMetaTileEntity.getStackInSlot(i))) {
                baseMetaTileEntity.decrStackSize(i, aStack.stackSize);
                tHatch.updateSlots();
                return true;
            }
        }
    }
    return false;
}
```

**ME 总线的消耗**：ME 总线通过 `startRecipeProcessing`/`endRecipeProcessing` 两步机制来消耗，而不是 `depleteInput`。多方块的处理逻辑如下：

```java
// 行 2010-2040 (startRecipeProcessing / endRecipeProcessing)
public void startRecipeProcessing() {
    for (IRecipeProcessingAwareHatch aware : mSmartInputHatches) {
        aware.startRecipeProcessing();
    }
    for (IDualInputHatch dualInputHatch : mDualInputHatches) {
        ((IRecipeProcessingAwareHatch) dualInputHatch).startRecipeProcessing();
    }
}

public void endRecipeProcessing() {
    for (IRecipeProcessingAwareHatch aware : mSmartInputHatches) {
        setResultIfFailure(aware.endRecipeProcessing(this));
    }
    // ...
}
```

#### 消耗流体

```java
// 行 1692-1710 (depleteInput for FluidStack)
public boolean depleteInput(FluidStack aLiquid) {
    if (aLiquid == null) return false;
    for (MTEHatchInput tHatch : validMTEList(mInputHatches)) {
        setHatchRecipeMap(tHatch);
        FluidStack tLiquid = tHatch.drain(ForgeDirection.UNKNOWN, aLiquid, false);
        if (tLiquid != null && tLiquid.amount >= aLiquid.amount) {
            tLiquid = tHatch.drain(ForgeDirection.UNKNOWN, aLiquid, true);  // 真正扣除
            return tLiquid != null && tLiquid.amount >= aLiquid.amount;
        }
    }
    return false;
}
```

---

### 5.3 输出物品

```java
// 行 1743-1765 (addItemOutputs)
public boolean addItemOutputs(ItemStack[] outputItems) {
    ItemEjectionHelper ejectionHelper = new ItemEjectionHelper(this);
    int ejected = ejectionHelper.ejectItems(Arrays.asList(outputItems), 1);
    ejectionHelper.commit();
    return ejected == 1;
}
```

`ItemEjectionHelper` 调用每个 `IOutputBus.createTransaction()` 创建事务，依次尝试写入各总线（优先写入过滤/锁定总线），最后 `commit()` 将所有待写入一次性提交。

对于 ME 输出总线，`commit()` 调用 `provider.addToCache(...)` 将物品加入 `AECacheCounter`，由 `flushCachedStack()` 在下次周期（最多 40 tick 后）推入 ME 网络。

---

### 5.4 输出流体

```java
// 行 1677-1690 (addOutput FluidStack)
// 注意：此方法始终 return false，这是 GT5U 源码中的设计行为，调用方不依赖其返回值
public boolean addOutput(FluidStack aLiquid) {
    if (aLiquid == null) return false;
    FluidStack copiedFluidStack = aLiquid.copy();
    if (!dumpFluid(mOutputHatches, copiedFluidStack, true)) {
        dumpFluid(mOutputHatches, copiedFluidStack, false);  // 先尝试精确匹配，再尝试任意匹配
    }
    return false;  // 始终返回 false，实际成功与否由 dumpFluid 内部处理
}

// 行 1652-1676 (dumpFluid)
protected static boolean dumpFluid(List<MTEHatchOutput> outputHatches, FluidStack copiedFluidStack, boolean strictMode) {
    for (MTEHatchOutput tHatch : validMTEList(outputHatches)) {
        if (strictMode && !tHatch.isEmptyAndAcceptsAnyFluid()
            && !tHatch.canStoreFluid(copiedFluidStack)) continue;
        if (tHatch instanceof MTEHatchOutputME tMEHatch) {
            if (!tMEHatch.canAcceptFluid()) continue;
        }
        int tAmount = tHatch.fill(copiedFluidStack, false);
        if (tAmount >= copiedFluidStack.amount) {
            tHatch.fill(copiedFluidStack, true);
            return true;
        } else if (tAmount > 0) {
            copiedFluidStack.amount -= tHatch.fill(copiedFluidStack, true);
        }
    }
    return false;
}
```

---

## 6. 舱室格子（Inventory Slot）实现原理

GT5U 使用 `mInventory: ItemStack[]` 数组作为背包底层存储，继承自 `MetaTileEntity`。

```
MetaTileEntity
  ├── mInventory: ItemStack[]   ← 物品数组，大小在构造时由 aInvSlotCount 决定
  └── mFluid: FluidStack        ← 单格流体 Tank（在 MTEBasicTank 中）
```

#### 格子大小由 Tier 决定（MTEHatch.getSlots）

```java
// gregtech/api/metatileentity/implementations/MTEHatch.java 行 41
public static int getSlots(int aTier) {
    return (aTier + 1) * (aTier + 1);
}
```

| Tier | 名称 | 格子数 |
|------|------|--------|
| 0 | ULV | 1 |
| 1 | LV | 4 |
| 2 | MV | 9 |
| 3 | HV | 16 |
| 4 | EV | 25 |
| 8 | UV | 81 |

#### 与 `IInventory` 的集成

`BaseMetaTileEntity` 实现了 Minecraft 的 `IInventory` 接口，所有 `getStackInSlot`/`setInventorySlotContents`/`decrStackSize` 调用都通过它转发到 `MetaTileEntity.mInventory[]`。

```java
// gregtech/api/metatileentity/BaseMetaTileEntity.java 行 1357
public ItemStack getStackInSlot(int slot) {
    if (hasValidMetaTileEntity()) return mMetaTileEntity.getStackInSlot(slot);
    return null;
}
```

#### isValidSlot 控制槽位可见性

`allowPutStack` / `allowPullStack` 控制外部 Hopper/管道等的访问权；`isValidSlot` 控制 GUI 显示和内部循环是否跳过某个槽（如电路板槽：`MTEHatchInputBus.isValidSlot` 排除了电路板槽）：

```java
// MTEHatchInputBus.java 行 104-106
@Override
public boolean isValidSlot(int aIndex) {
    return aIndex != getCircuitSlot();
}
```

#### 多格子流体（MultiInput）

`MTEHatchMultiInput` / `MTEHatchInputBusCompressed` 等子类拥有多个 `FluidTank`，通过重写 `getTankInfo()`、`fill()`、`drain()` 来提供多槽流体存储，但底层机制与单格子相同。

---

## 7. 结构识别——底层逻辑

GT5U 的多方块结构识别基于 **StructureLib**（`com.gtnewhorizon:structurelib`）框架，GT5U 在其上封装了 `GTStructureUtility` 和 `HatchElement` 枚举。

### 7.1 IHatchElement 与 HatchElement 枚举

**文件**: `gregtech/api/enums/HatchElement.java`

```java
// 行 27: 枚举实现 IHatchElement<MTEMultiBlockBase>
public enum HatchElement implements IHatchElement<MTEMultiBlockBase> {

    // 每个枚举项绑定：
    // 1. 显示名本地化 Key
    // 2. 结构扫描时添加到多方块列表的方法引用（IGTHatchAdder）
    // 3. 允许的 MTE 类型（白名单）
    // 4. 黑名单（如 Steam 总线不被普通 InputBus 识别）

    InputHatch("GT5U.MBTT.InputHatch", MTEMultiBlockBase::addInputHatchToMachineList, MTEHatchInput.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mInputHatches.size(); }
    },
    InputBus("GT5U.MBTT.InputBus", MTEMultiBlockBase::addInputBusToMachineList, MTEHatchInputBus.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mInputBusses.size(); }
        @Override
        public List<Class<? extends IMetaTileEntity>> mteBlacklist() {
            return ImmutableList.of(MTEHatchLensHousing.class, MTEHatchSteamBusInput.class);
        }
    },
    OutputHatch("GT5U.MBTT.OutputHatch", MTEMultiBlockBase::addOutputHatchToMachineList, MTEHatchOutput.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mOutputHatches.size(); }
    },
    OutputBus("GT5U.MBTT.OutputBus", MTEMultiBlockBase::addOutputBusToMachineList, MTEHatchOutputBus.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mOutputBusses.size(); }
    },
    Energy("GT5U.MBTT.EnergyHatch", MTEMultiBlockBase::addEnergyInputToMachineList, MTEHatchEnergy.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mEnergyHatches.size(); }
    },
    Maintenance("GT5U.MBTT.MaintenanceHatch", MTEMultiBlockBase::addMaintenanceToMachineList, MTEHatchMaintenance.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mMaintenanceHatches.size(); }
    },
    Muffler("GT5U.MBTT.MufflerHatch", MTEMultiBlockBase::addMufflerToMachineList, MTEHatchMuffler.class) {
        @Override
        public long count(MTEMultiBlockBase t) { return t.mMufflerHatches.size(); }
    },
    // 还有 Dynamo, ExoticEnergy, MultiAmpEnergy, ExoticDynamo
    ;
}
```

**`IHatchElement<T>` 接口**（`gregtech/api/interfaces/IHatchElement.java`，行 20）：

```java
public interface IHatchElement<T> {
    List<? extends Class<? extends IMetaTileEntity>> mteClasses();  // 允许的 MTE 类型
    IGTHatchAdder<? super T> adder();                               // 添加到列表的方法
    String getDisplayName();                                        // UI 提示
    long count(T t);                                                // 当前已识别数量
    // ...
    // withMteClasses / withAdder / withCount 等默认方法用于动态修改
}
```

---

### 7.2 HatchElementBuilder 与 buildHatchAdder

**文件**: `gregtech/api/util/GTStructureUtility.java`

```java
// 行 257-266
public static <T> HatchElementBuilder<T> buildHatchAdder() {
    return HatchElementBuilder.builder();
}

public static <T> HatchElementBuilder<T> buildHatchAdder(Class<T> typeToken) {
    return HatchElementBuilder.builder();
}
```

`HatchElementBuilder` 提供链式 API：

- `.atLeast(InputHatch, OutputHatch, InputBus, ...)` — 声明此位置至少接受哪些类型的舱室（对应 `addXxxToMachineList`）
- `.casingIndex(int)` — 识别成功后用于更新贴图的外壳纹理 ID
- `.hint(int)` — 结构提示颜色（用于 Structure Visualizer）
- `.buildAndChain(Block, int meta)` — 链接普通方块识别（如外壳方块）

示例（`MTEElectricBlastFurnace.java` 行 75-90）：

```java
.addElement(
    'b',
    buildHatchAdder(MTEElectricBlastFurnace.class)
        .atLeast(InputHatch, OutputHatch, InputBus, OutputBus, Maintenance, Energy)
        .casingIndex(CASING_INDEX)
        .hint(1)
        .buildAndChain(GregTechAPI.sBlockCasings1, CASING_INDEX)
)
```

含义：字符 `'b'` 对应的位置，可以放置以上任意一种舱室，或者放置普通外壳（`sBlockCasings1:11`）。

---

### 7.3 checkMachine 与 checkPiece

**文件**: `gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java`

```java
// 行 1291
public abstract boolean checkMachine(IGregTechTileEntity aBaseMetaTileEntity, ItemStack aStack);
```

每个多方块必须实现 `checkMachine()`。推荐做法是调用 StructureLib 的 `checkPiece`（继承自 `MTETooltipMultiBlockBase.checkPiece`）：

```java
// MTEElectricBlastFurnace.java 行 220-231
@Override
public boolean checkMachine(IGregTechTileEntity aBaseMetaTileEntity, ItemStack aStack) {
    this.mHeatingCapacity = 0;
    setCoilLevel(HeatingCoilLevel.None);

    if (!checkPiece(STRUCTURE_PIECE_MAIN, 1, 3, 0)) return false;
    // 参数：结构片名称，x偏移（相对于控制器），y偏移，z偏移

    if (getCoilLevel() == HeatingCoilLevel.None) return false;
    if (mMaintenanceHatches.size() != 1) return false;

    this.mHeatingCapacity = (int) getCoilLevel().getHeat() + 100 * (GTUtility.getTier(getMaxInputVoltage()) - 2);
    return true;
}
```

`checkPiece` 内部遍历 `STRUCTURE_DEFINITION` 中每个字符对应的 `IStructureElement`，对每个位置的 Block/TileEntity 调用 `element.check(controller, world, x, y, z)` 来验证。如果是 `HatchElementBuilder` 生成的元素，则：
1. 检查此位置是否有 `IGregTechTileEntity`
2. 获取其 `MetaTileEntity`
3. 遍历 `atLeast()` 中列出的 `IHatchElement`，调用其 `adder.apply(controller, tileEntity, casingIndex)`
4. `adder` 就是对应的 `addXxxToMachineList` 方法

---

### 7.4 addToMachineList 与 addInputBusToMachineList 等

**文件**: `gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java`，行 2044-2270

`addToMachineList` 是最通用的版本，自动判断类型：

```java
// 行 2044-2090
public boolean addToMachineList(IGregTechTileEntity aTileEntity, int aBaseCasingIndex) {
    if (aTileEntity == null) return false;
    IMetaTileEntity aMetaTileEntity = aTileEntity.getMetaTileEntity();
    if (aMetaTileEntity == null) return false;

    // IDualInputHatch（Crafting Input Buffer/Bus）
    if (aMetaTileEntity instanceof IDualInputHatch hatch) {
        if (!supportsCraftingMEBuffer()) return false;
        hatch.updateTexture(aBaseCasingIndex);
        hatch.updateCraftingIcon(this.getMachineCraftingIcon());
        // ...
        return mDualInputHatches.add(hatch);
    }
    // ISmartInputHatch（MTEHatchInputBusME 实现此接口）
    if (aMetaTileEntity instanceof ISmartInputHatch hatch) {
        mSmartInputHatches.add(hatch);
    }
    // MTEHatchInput（含 MTEHatchInputME）
    if (aMetaTileEntity instanceof MTEHatchInput hatch) {
        setHatchRecipeMap(hatch);
        return mInputHatches.add(hatch);
    }
    // MTEHatchInputBus（含 MTEHatchInputBusME）
    if (aMetaTileEntity instanceof MTEHatchInputBus hatch) {
        hatch.mRecipeMap = getRecipeMap();
        return mInputBusses.add(hatch);
    }
    // MTEHatchOutput（含 MTEHatchOutputME）
    if (aMetaTileEntity instanceof MTEHatchOutput hatch) return mOutputHatches.add(hatch);
    // MTEHatchOutputBus（含 MTEHatchOutputBusME）
    if (aMetaTileEntity instanceof MTEHatchOutputBus hatch) return mOutputBusses.add(hatch);
    // MTEHatchEnergy, MTEHatchDynamo, MTEHatchMaintenance, MTEHatchMuffler...
    return false;
}
```

**关键细节**：
- `updateTexture(aBaseCasingIndex)` 调用 `MTEHatch.updateTexture`，将舱室贴图更新为外壳贴图，从而视觉上融入多方块结构。
- `updateCraftingIcon(getMachineCraftingIcon())` 让 AE2 合成界面显示正确的机器图标。
- 舱室类型通过 Java `instanceof` 链来判断，利用多方块类型继承：`MTEHatchInputBusME extends MTEHatchInputBus extends MTEHatch`，因此 `MTEHatchInputBusME` 实例会同时被 `ISmartInputHatch` 和 `MTEHatchInputBus` 分支识别并处理。

---

### 7.5 clearHatches 与 checkStructure

```java
// 行 506-523 (clearHatches)
public void clearHatches() {
    mInputHatches.clear();
    mInputBusses.clear();
    mOutputHatches.clear();
    mOutputBusses.clear();
    mDynamoHatches.clear();
    mEnergyHatches.clear();
    setMufflers(false);
    mMufflerHatches.clear();
    mMaintenanceHatches.clear();
    mDualInputHatches.clear();
    mSmartInputHatches.clear();
    mCoils.clear();
    // ...
}

// 行 528-550 (checkStructure)
public boolean checkStructure(boolean aForceReset, IGregTechTileEntity aBaseMetaTileEntity) {
    if (!aBaseMetaTileEntity.isServerSide()) return mMachine;
    if (mStructureChanged || aForceReset) {
        clearHatches();                               // 先清空所有列表
        mMachine = checkMachine(aBaseMetaTileEntity, mInventory[1]);  // 重新扫描
        onStructureCheckFinished();
    }
    mStructureChanged = false;
    return mMachine;
}
```

`mStructureChanged` 由 `onMachineBlockUpdate()` 置位，当周围方块变化时触发重新扫描。

---

## 8. 如何实现一个新的自定义舱室

以实现一个"自定义催化剂输入总线"为例：

### Step 1：继承正确的基类

```java
// 文件: yourmod/tileentity/MTEHatchCatalystBus.java
package yourmod.tileentity;

import gregtech.api.metatileentity.implementations.MTEHatchInputBus;
// 继承 MTEHatchInputBus，因为这是一个物品输入总线

public class MTEHatchCatalystBus extends MTEHatchInputBus {

    public MTEHatchCatalystBus(int aID, String aName, String aNameRegional, int aTier) {
        // 固定 4 个格子（不随 tier 变化），禁用电路板槽
        super(aID, aName, aNameRegional, aTier, 4,
            new String[]{ "Catalyst Input Bus", "For Catalysts only" });
    }

    // 序列化构造（newMetaEntity 使用）
    public MTEHatchCatalystBus(String aName, int aTier, String[] aDescription, ITexture[][][] aTextures) {
        super(aName, aTier, 4, aDescription, aTextures);
    }

    @Override
    public MetaTileEntity newMetaEntity(IGregTechTileEntity aTileEntity) {
        return new MTEHatchCatalystBus(mName, mTier, mDescriptionArray, mTextures);
    }

    // 重写贴图（必须实现）
    @Override
    public ITexture[] getTexturesActive(ITexture aBaseTexture) {
        return new ITexture[]{ aBaseTexture, TextureFactory.of(OVERLAY_PIPE_IN) };
    }

    @Override
    public ITexture[] getTexturesInactive(ITexture aBaseTexture) {
        return new ITexture[]{ aBaseTexture, TextureFactory.of(OVERLAY_PIPE_IN) };
    }

    // 禁用电路板槽（可选，视需求）
    @Override
    public boolean allowSelectCircuit() {
        return false;
    }

    // 只接受催化剂类物品（示例过滤）
    @Override
    public boolean allowPutStack(IGregTechTileEntity aBaseMetaTileEntity, int aIndex,
                                  ForgeDirection side, ItemStack aStack) {
        return super.allowPutStack(aBaseMetaTileEntity, aIndex, side, aStack)
            && isCatalyst(aStack);
    }

    private boolean isCatalyst(ItemStack stack) {
        // 自定义判断逻辑，如检查 OreDictionary 等
        return GTOreDictUnificator.getAssociation(stack) != null
            && GTOreDictUnificator.getAssociation(stack).mPrefix.toString().startsWith("catalyst");
    }
}
```

### Step 2：选取 MetaTile ID

在模组的 ID 枚举中声明：

```java
// 在 MetaTileIDs 或自定义 ID 枚举中
CATALYST_BUS_LV(12345),
CATALYST_BUS_MV(12346),
// ...
```

**注意**：ID 范围不能与其他模组冲突，GT5U 核心占据 0-1999，各子模组各有范围。

### Step 3：在 ItemList 中注册 enum 常量

```java
// yourmod/enums/YourItemList.java
public enum YourItemList {
    Hatch_Catalyst_Bus_LV,
    Hatch_Catalyst_Bus_MV,
    // ...
}
```

也可以直接使用 `ItemStack` 变量而不用枚举，只要调用 `getStackForm(1L)` 拿到 ItemStack 并储存。

### Step 4：在加载器中实例化并绑定 ItemStack

```java
// 在 Mod 的 PreInit 或 Init 阶段
YourItemList.Hatch_Catalyst_Bus_LV.set(
    new MTEHatchCatalystBus(CATALYST_BUS_LV.ID, "hatch.catalyst_bus.lv", "Catalyst Bus (LV)", 1)
        .getStackForm(1L));
YourItemList.Hatch_Catalyst_Bus_MV.set(
    new MTEHatchCatalystBus(CATALYST_BUS_MV.ID, "hatch.catalyst_bus.mv", "Catalyst Bus (MV)", 2)
        .getStackForm(1L));
```

### Step 5：在多方块中加入识别逻辑

```java
// 在你的 MultiBlock 的 STRUCTURE_DEFINITION 中：
.addElement(
    'i',
    buildHatchAdder(YourMultiBlock.class)
        .atLeast(InputBus)   // 允许标准输入总线
        .orElseAdder(YourMultiBlock::addCatalystBusToMachineList)  // 也允许催化剂总线
        .casingIndex(MY_CASING_INDEX)
        .buildAndChain(GregTechAPI.sBlockCasings1, MY_CASING_INDEX)
)

// 在 YourMultiBlock 中添加方法：
public ArrayList<MTEHatchCatalystBus> mCatalystBusses = new ArrayList<>();

public boolean addCatalystBusToMachineList(IGregTechTileEntity aTileEntity, int aBaseCasingIndex) {
    if (aTileEntity == null) return false;
    IMetaTileEntity mte = aTileEntity.getMetaTileEntity();
    if (mte instanceof MTEHatchCatalystBus hatch) {
        hatch.updateTexture(aBaseCasingIndex);
        hatch.updateCraftingIcon(this.getMachineCraftingIcon());
        mCatalystBusses.add(hatch);
        return mInputBusses.add(hatch);  // 同时加入标准列表以参与 getStoredInputs
    }
    return false;
}

// 在 clearHatches() 中清空：
@Override
public void clearHatches() {
    super.clearHatches();
    mCatalystBusses.clear();
}
```

### Step 6：实现自定义 IHatchElement（可选）

如需在 `buildHatchAdder().atLeast(...)` 中使用自定义 HatchElement：

```java
// 参考 HatchElement.java 的写法
public enum YourHatchElement implements IHatchElement<YourMultiBlock> {
    CatalystBus("YourMod.MBTT.CatalystBus",
        YourMultiBlock::addCatalystBusToMachineList,
        MTEHatchCatalystBus.class) {
        @Override
        public long count(YourMultiBlock t) { return t.mCatalystBusses.size(); }
    };

    private final String name;
    private final List<Class<? extends IMetaTileEntity>> mteClasses;
    private final IGTHatchAdder<YourMultiBlock> adder;

    YourHatchElement(String name, IGTHatchAdder<YourMultiBlock> adder,
                     Class<? extends IMetaTileEntity>... mteClasses) {
        this.name = name;
        this.mteClasses = Collections.unmodifiableList(Arrays.asList(mteClasses));
        this.adder = adder;
    }

    @Override
    public List<? extends Class<? extends IMetaTileEntity>> mteClasses() { return mteClasses; }
    @Override
    public IGTHatchAdder<? super YourMultiBlock> adder() { return adder; }
    @Override
    public String getDisplayName() { return GTUtility.translate(name); }
}
```

---

## 9. 真实案例：EBF 中的完整流程

以电弧爆炸炉（Electric Blast Furnace，EBF）为例，展示完整的注册—识别—工作流程：

**文件**: `gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java`

### 结构定义

```java
// 行 67-90
private static final IStructureDefinition<MTEElectricBlastFurnace> STRUCTURE_DEFINITION = StructureDefinition
    .<MTEElectricBlastFurnace>builder()
    .addShape(STRUCTURE_PIECE_MAIN, transpose(new String[][] {
        { "fff", "fmf", "fff" },   // 顶层：f=输出舱/外壳，m=消音器
        { "CCC", "C-C", "CCC" },   // 中层：C=加热线圈，-=内部空气
        { "CCC", "C-C", "CCC" },   // 中层
        { "b~b", "bbb", "bbb" }    // 底层：b=输入/输出/维护/能量舱/外壳，~=控制器
    }))
    // 'f'：只允许输出舱或外壳
    .addElement('f', buildHatchAdder(MTEElectricBlastFurnace.class)
        .atLeast(OutputHatch)
        .casingIndex(CASING_INDEX)
        .hint(3)
        .buildAndChain(GregTechAPI.sBlockCasings1, CASING_INDEX))
    // 'm'：消音器
    .addElement('m', Muffler.newAny(CASING_INDEX, 2))
    // 'C'：加热线圈（任意等级）
    .addElement('C', GTStructureChannels.HEATING_COIL.use(
        activeCoils(ofCoil(MTEElectricBlastFurnace::setCoilLevel, MTEElectricBlastFurnace::getCoilLevel))))
    // 'b'：输入/输出各类舱室或外壳
    .addElement('b', buildHatchAdder(MTEElectricBlastFurnace.class)
        .atLeast(InputHatch, OutputHatch, InputBus, OutputBus, Maintenance, Energy)
        .casingIndex(CASING_INDEX)
        .hint(1)
        .buildAndChain(GregTechAPI.sBlockCasings1, CASING_INDEX))
    .build();
```

### checkMachine

```java
// 行 220-231
@Override
public boolean checkMachine(IGregTechTileEntity aBaseMetaTileEntity, ItemStack aStack) {
    this.mHeatingCapacity = 0;
    setCoilLevel(HeatingCoilLevel.None);

    if (!checkPiece(STRUCTURE_PIECE_MAIN, 1, 3, 0)) return false;
    // checkPiece 遍历 'b' 位置时依次尝试：
    //   InputHatch.adder → addInputHatchToMachineList → mInputHatches.add
    //   InputBus.adder → addInputBusToMachineList → mInputBusses.add
    //   ... 依次类推
    // 每成功识别一个舱室，调用 hatch.updateTexture(CASING_INDEX) 改变外观

    if (getCoilLevel() == HeatingCoilLevel.None) return false;
    if (mMaintenanceHatches.size() != 1) return false;  // 必须恰好一个维护舱

    this.mHeatingCapacity = (int) getCoilLevel().getHeat() + 100 * (GTUtility.getTier(getMaxInputVoltage()) - 2);
    return true;
}
```

### 配方处理时的吞吐

1. `startRecipeProcessing()` → 调用所有 `ISmartInputHatch`（含 ME 总线）的 `startRecipeProcessing()`
2. `getStoredInputs()` + `getStoredFluids()` → 读取所有输入总线/舱室的物品/流体
3. `RecipeMap.findRecipe(...)` → 匹配配方
4. `depleteInput(item/fluid)` → 消耗普通总线中的物品/流体
5. `endRecipeProcessing()` → ME 总线从 AE2 网络提取物品
6. `addItemOutputs(items)` / `addOutput(fluid)` → 写入输出总线/输出舱

---

## 10. GT5U 与 AE2U 交互——ME 舱室底层

### AE2 网络代理（AENetworkProxy）

**文件（AE2U）**: `appeng/me/helpers/AENetworkProxy.java`

ME 舱室通过 `AENetworkProxy` 接入 AE2 网格：

```
AENetworkProxy
  ├── getStorage() → IStorageGrid
  │     ├── getItemInventory() → IMEMonitor<IAEItemStack>
  │     └── getFluidInventory() → IMEMonitor<IAEFluidStack>
  ├── getEnergy() → IEnergyGrid (用于 poweredExtraction/poweredInsert 扣除 AE2 能量)
  └── getGrid() → IGrid (用于 postEvent)
```

### 关键 AE2 API 方法

**文件（AE2U）**: `appeng/util/Platform.java`

```java
// 行 1262-1295: 从 ME 网络提取物品（消耗 AE2 能量）
public static <StackType extends IAEStack> StackType poweredExtraction(
        final IEnergySource energy,
        final IMEInventory<StackType> cell,
        final StackType request,
        final BaseActionSource src) {
    final StackType possible = cell.extractItems((StackType) request.copy(), Actionable.SIMULATE, src);
    // 先模拟计算能量消耗
    // ...
    final StackType ret = cell.extractItems(possible, Actionable.MODULATE, src);
    // 真正提取
    return ret;
}

// 行 1298-1340: 向 ME 网络注入物品（消耗 AE2 能量）
public static <StackType extends IAEStack> StackType poweredInsert(
        final IEnergySource energy,
        final IMEInventory<StackType> cell,
        final StackType input,
        final BaseActionSource src) {
    final StackType possible = cell.injectItems((StackType) input.copy(), Actionable.SIMULATE, src);
    // ...
    final StackType ret = cell.injectItems(input, Actionable.MODULATE, src);
    return ret;
}
```

### IMEMonitor / IStorageGrid

**文件（AE2U）**: `appeng/api/storage/IMEMonitor.java`

```java
// 行 20: IMEMonitor 继承 IMEInventoryHandler 和 IBaseMonitor
public interface IMEMonitor<T extends IAEStack> extends IMEInventoryHandler<T>, IBaseMonitor<T> {
    IItemList<T> getStorageList();  // 获取网络中所有物品的列表（用于自动拉取模式）
}
```

ME 输入舱室（`MTEHatchInputBusME.refreshItemList`）调用 `sg.getStorageList().iterator()` 遍历 ME 网络全部物品，填写自己的 16 个虚拟槽，供配方匹配使用。

### GridFlags.REQUIRE_CHANNEL

两类 ME 舱室都使用了 `GridFlags.REQUIRE_CHANNEL`：

```java
// MTEHatchInputBusME.java 行 227
gridProxy.setFlags(GridFlags.REQUIRE_CHANNEL);
```

这意味着 ME 舱室必须分配到 AE2 的数据通道（Channel）才能工作，与 AE2 原版 IO 端口行为一致。每个 ME 控制器默认 32 个通道（密集电缆），普通电缆 8 个。

---

## 总结

| 功能 | 类 | 关键文件 |
|------|----|---------|
| 所有舱室的基础 | `MTEHatch` | `gregtech/api/metatileentity/implementations/MTEHatch.java` |
| 流体输入 | `MTEHatchInput` | 同包 |
| 流体输出 | `MTEHatchOutput` | 同包 |
| 物品输入总线 | `MTEHatchInputBus` | 同包 |
| 物品输出总线 | `MTEHatchOutputBus` | 同包 |
| ME 物品输入总线 | `MTEHatchInputBusME` | `gregtech/common/tileentities/machines/` |
| ME 流体输入 | `MTEHatchInputME` | 同包 |
| ME 物品输出总线 | `MTEHatchOutputBusME` | `gregtech/common/tileentities/machines/outputme/` |
| ME 流体输出 | `MTEHatchOutputME` | 同包 |
| ME 输出通用逻辑 | `MTEHatchOutputMEBase` | 同包 `base/` |
| 舱室枚举 | `HatchElement` | `gregtech/api/enums/HatchElement.java` |
| 结构识别工具 | `GTStructureUtility` | `gregtech/api/util/GTStructureUtility.java` |
| 多方块基类 | `MTEMultiBlockBase` | `gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java` |
| 舱室注册加载器 | `LoaderMetaTileEntities` | `gregtech/loaders/preload/LoaderMetaTileEntities.java` |
| AE2 Platform API | `Platform` | `appeng/util/Platform.java`（AE2U） |
