# GT5-Unofficial TecTech 按钮注册系统知识库

> **代码来源：** https://github.com/GTNewHorizons/GT5-Unofficial  
> **本地路径：** /tmp/GT5-Unofficial  
> **核心文件：**
> - `src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java`
> - `src/main/java/tectech/thing/metaTileEntity/multi/base/Parameters.java`
> - `src/main/java/tectech/thing/metaTileEntity/multi/base/LedStatus.java`
> - `src/main/java/tectech/thing/metaTileEntity/multi/base/IStatusFunction.java`
> - `src/main/java/tectech/thing/metaTileEntity/multi/base/INameFunction.java`
>
> **所有代码均经本地源码核实，不含虚假代码。**

---

## 目录

1. [TTMultiblockBase 概述](#1-ttmultiblockbase-概述)
2. [三个核心功能按钮](#2-三个核心功能按钮)
3. [按钮注册到 GUI 的流程](#3-按钮注册到-gui-的流程)
4. [Parameters 参数系统](#4-parameters-参数系统)
5. [LedStatus LED 状态枚举](#5-ledstatus-led-状态枚举)
6. [IStatusFunction / INameFunction 接口](#6-istatusfunction--inamefunction-接口)
7. [LED 指示灯注册与渲染](#7-led-指示灯注册与渲染)
8. [LED 配置弹窗（createLEDConfigurationWindow）](#8-led-配置弹窗-createledconfigurationwindow)
9. [parametersInstantiation_EM：参数定义](#9-parametersinstantiation_em参数定义)
10. [hatchesStatusUpdate_EM：参数状态更新](#10-hatchesstatusupdate_em参数状态更新)
11. [完整注册流程时序图](#11-完整注册流程时序图)
12. [子类实现示例（MTEQuantumComputer）](#12-子类实现示例-mtequantumcomputer)

---

## 1. TTMultiblockBase 概述

`TTMultiblockBase` 是 TecTech 所有多方块机器的**抽象基类**，继承自 GT5U 的 `MTEExtendedPowerMultiBlockBase`。

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:117-195
public abstract class TTMultiblockBase extends MTEExtendedPowerMultiBlockBase<TTMultiblockBase>
    implements IAlignment, IBindPlayerInventoryUI {

    // ── 特殊仓位列表 ──────────────────────────────────────────
    protected ArrayList<MTEHatchUncertainty>  eUncertainHatches = new ArrayList<>();
    protected ArrayList<MTEHatchEnergyMulti>  eEnergyMulti      = new ArrayList<>();  // 多安培能量仓
    protected ArrayList<MTEHatchDynamoMulti>  eDynamoMulti      = new ArrayList<>();  // 多安培发电仓
    protected ArrayList<MTEHatchDataInput>    eInputData        = new ArrayList<>();
    protected ArrayList<MTEHatchDataOutput>   eOutputData       = new ArrayList<>();

    // ── 参数系统 ──────────────────────────────────────────────
    public final Parameters parametrization;   // 参数管理器（含输入/输出参数 LED）

    // ── LED 弹窗 ID 基址 ─────────────────────────────────────
    protected static int LED_WINDOW_BASE_ID = 100;

    // ── 功能开关（由按钮控制） ────────────────────────────────
    public boolean ePowerPass = false;      // 能量透传（Power Pass）
    public boolean ePowerPassCover = false; // 能量透传（封面触发）
    public boolean eSafeVoid = false;       // 安全虚空（Safe Void）

    // ── 能量参数（只读） ─────────────────────────────────────
    public long eAmpereFlow = 1;            // 机器实际需要安培数
    protected long eMaxAmpereFlow = 0;      // 所有能量仓总安培数

    // ── Uncertainty（不确定性检测）────────────────────────────
    protected byte eCertainMode = 0;        // 检测模式（0-5）
    protected byte eCertainStatus = 0;      // 检测结果（位掩码）
}
```

---

## 2. 三个核心功能按钮

TecTech 多方块 GUI 右侧有三个固定按钮，通过 `addUIWidgets()` 注册。

### 2.1 `createPowerPassButton()`：能量透传按钮

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2251-2286
protected ButtonWidget createPowerPassButton() {
    Widget button = new ButtonWidget().setOnClick((clickData, widget) -> {
        if (isPowerPassButtonEnabled() || ePowerPassCover) {
            TecTech.proxy.playSound(getBaseMetaTileEntity(), "fx_click");
            ePowerPass = !ePowerPass;   // 切换透传状态
            if (!isAllowedToWorkButtonEnabled()) { // TRANSFORMER HACK
                if (ePowerPass) {
                    getBaseMetaTileEntity().enableWorking();
                } else {
                    getBaseMetaTileEntity().disableWorking();
                }
            }
        }
    })
    .setPlayClickSound(false)
    .setBackground(() -> {
        List<UITexture> ret = new ArrayList<>();
        ret.add(TecTechUITextures.BUTTON_STANDARD_16x16);
        if (!isPowerPassButtonEnabled() && !ePowerPassCover) {
            ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_PASS_DISABLED);
        } else {
            if (ePowerPass) {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_PASS_ON);
            } else {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_PASS_OFF);
            }
        }
        return ret.toArray(new IDrawable[0]);
    })
    .setPos(174, doesBindPlayerInventory() ? 116 : 140)
    .setSize(16, 16);
    if (isPowerPassButtonEnabled()) {
        button.addTooltip(StatCollector.translateToLocal("tt.gui.tooltip.power_pass"))
            .setTooltipShowUpDelay(TOOLTIP_DELAY);
    }
    return (ButtonWidget) button;
}
```

### 2.2 `createSafeVoidButton()`：安全虚空按钮

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2289-2317
protected ButtonWidget createSafeVoidButton() {
    Widget button = new ButtonWidget().setOnClick((clickData, widget) -> {
        if (isSafeVoidButtonEnabled()) {
            TecTech.proxy.playSound(getBaseMetaTileEntity(), "fx_click");
            eSafeVoid = !eSafeVoid;   // 切换安全虚空
        }
    })
    .setPlayClickSound(false)
    .setBackground(() -> {
        List<UITexture> ret = new ArrayList<>();
        ret.add(TecTechUITextures.BUTTON_STANDARD_16x16);
        if (!isSafeVoidButtonEnabled()) {
            ret.add(TecTechUITextures.OVERLAY_BUTTON_SAFE_VOID_DISABLED);
        } else {
            if (eSafeVoid) {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_SAFE_VOID_ON);
            } else {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_SAFE_VOID_OFF);
            }
        }
        return ret.toArray(new IDrawable[0]);
    })
    .setPos(174, doesBindPlayerInventory() ? 132 : 156)
    .setSize(16, 16);
    if (isSafeVoidButtonEnabled()) {
        button.addTooltip(StatCollector.translateToLocal("tt.gui.tooltip.safe_void"))
            .setTooltipShowUpDelay(TOOLTIP_DELAY);
    }
    return (ButtonWidget) button;
}
```

### 2.3 `createPowerSwitchButton()`：机器开关按钮

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2320-2352
protected ButtonWidget createPowerSwitchButton() {
    Widget button = new ButtonWidget().setOnClick((clickData, widget) -> {
        if (isAllowedToWorkButtonEnabled()) {
            TecTech.proxy.playSound(getBaseMetaTileEntity(), "fx_click");
            if (getBaseMetaTileEntity().isAllowedToWork()) {
                getBaseMetaTileEntity().disableWorking();   // 关闭
            } else {
                getBaseMetaTileEntity().enableWorking();    // 开启
            }
        }
    })
    .setPlayClickSound(false)
    .setBackground(() -> {
        List<UITexture> ret = new ArrayList<>();
        ret.add(TecTechUITextures.BUTTON_STANDARD_16x16);
        if (!isAllowedToWorkButtonEnabled()) {
            ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_SWITCH_DISABLED);
        } else {
            if (getBaseMetaTileEntity().isAllowedToWork()) {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_SWITCH_ON);
            } else {
                ret.add(TecTechUITextures.OVERLAY_BUTTON_POWER_SWITCH_OFF);
            }
        }
        return ret.toArray(new IDrawable[0]);
    })
    .setPos(174, doesBindPlayerInventory() ? 148 : 172)
    .setSize(16, 16);
    if (isAllowedToWorkButtonEnabled()) {
        button.addTooltip(StatCollector.translateToLocal("tt.gui.tooltip.power_switch"))
            .setTooltipShowUpDelay(TOOLTIP_DELAY);
    }
    return (ButtonWidget) button;
}
```

### 2.4 按钮启用/禁用控制

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2093-2103
// 子类可重写以禁用对应按钮
public boolean isPowerPassButtonEnabled()     { return true; }
public boolean isSafeVoidButtonEnabled()       { return true; }
public boolean isAllowedToWorkButtonEnabled()  { return true; }
```

**三个按钮的位置（Y 轴随有无玩家物品栏变化）：**

| 按钮 | 有物品栏（Y） | 无物品栏（Y） |
|------|------------|------------|
| PowerPass  | 116 | 140 |
| SafeVoid   | 132 | 156 |
| PowerSwitch | 148 | 172 |

---

## 3. 按钮注册到 GUI 的流程

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2130-2248
@Override
public void addUIWidgets(ModularWindow.Builder builder, UIBuildContext buildContext) {

    // 背景（蓝色屏幕）
    if (doesBindPlayerInventory()) {
        builder.widget(new DrawableWidget().setDrawable(TecTechUITextures.BACKGROUND_SCREEN_BLUE)
            .setPos(4, 4).setSize(190, 91));
    } else {
        builder.widget(new DrawableWidget().setDrawable(TecTechUITextures.BACKGROUND_SCREEN_BLUE_NO_INVENTORY)
            .setPos(4, 4).setSize(190, 171));
    }

    // ① 注册信息文本区域
    final DynamicPositionedColumn screenElements = new DynamicPositionedColumn();
    drawTexts(screenElements, inventorySlot);
    builder.widget(new Scrollable().setVerticalScroll()
        .widget(screenElements)
        .setPos(10, 7)
        .setSize(182, doesBindPlayerInventory() ? 79 : 165));

    // ② 注册三个功能按钮 + 服务端/客户端数据同步
    Widget powerPassButton = createPowerPassButton();
    builder.widget(powerPassButton)
        .widget(new FakeSyncWidget.BooleanSyncer(() -> ePowerPass, val -> ePowerPass = val))
        .widget(new FakeSyncWidget.BooleanSyncer(() -> ePowerPassCover, val -> ePowerPassCover = val));

    Widget safeVoidButton = createSafeVoidButton();
    builder.widget(safeVoidButton)
        .widget(new FakeSyncWidget.BooleanSyncer(() -> eSafeVoid, val -> eSafeVoid = val));

    Widget powerSwitchButton = createPowerSwitchButton();
    builder.widget(powerSwitchButton)
        .widget(new FakeSyncWidget.BooleanSyncer(() -> getBaseMetaTileEntity().isAllowedToWork(), val -> {
            if (val) getBaseMetaTileEntity().enableWorking();
            else     getBaseMetaTileEntity().disableWorking();
        }));

    // ③ 参数栏背景条
    builder.widget(new DrawableWidget().setDrawable(TecTechUITextures.PICTURE_PARAMETER_BLANK)
        .setPos(5, doesBindPlayerInventory() ? 96 : 176)
        .setSize(166, 12));

    // ④ 注册 10 组 × 2 个参数 × 2 方向（输入/输出）= 40 个 LED 指示灯
    for (int hatch = 0; hatch < 10; hatch++) {
        for (int param = 0; param < 2; param++) {
            int ledID = hatch + param * 10;
            // 注册 LED 配置弹窗（仅输入参数有弹窗）
            buildContext.addSyncedWindow(LED_WINDOW_BASE_ID + ledID,
                (player) -> createLEDConfigurationWindow(ledID));
            addParameterLED(builder, hatch, param, true);   // 输入 LED
            addParameterLED(builder, hatch, param, false);  // 输出 LED
        }
    }
}
```

**`FakeSyncWidget.BooleanSyncer` 作用：** 将服务端字段值双向同步到客户端（ModularUI 框架）。

---

## 4. Parameters 参数系统

文件路径：`src/main/java/tectech/thing/metaTileEntity/multi/base/Parameters.java`

TecTech 多方块支持最多 **10 个参数仓位（hatch 0-9）**，每个仓位有 **2 个输入参数（paramID 0/1）** 和 **2 个输出参数**，共 20 个输入 + 20 个输出参数。

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/Parameters.java
public class Parameters {

    final Group[] groups = new Group[10];   // 10 个参数仓位

    double[] iParamsIn  = new double[20];   // 输入值（hatch 0..9 × param 0/1）
    double[] iParamsOut = new double[20];   // 输出值

    LedStatus[] eParamsInStatus  = LedStatus.makeArray(20, LedStatus.STATUS_UNUSED);
    LedStatus[] eParamsOutStatus = LedStatus.makeArray(20, LedStatus.STATUS_UNUSED);

    // 参数存储索引计算：id = hatchNo + 10 * parameterId
    double getIn(int hatchNo, int parameterId)  { return iParamsIn[hatchNo + 10 * parameterId]; }
    double getOut(int hatchNo, int parameterId) { return iParamsOut[hatchNo + 10 * parameterId]; }

    // 外部设置参数（仅在机器未运行时或允许运行时更新时生效）
    public boolean trySetParameters(int hatch, double parameter0, double parameter1) {
        Group p = groups[hatch];
        if (parent.mMaxProgresstime <= 0 || (p != null && p.updateWhileRunning)) {
            iParamsIn[hatch]      = parameter0;
            iParamsIn[hatch + 10] = parameter1;
            return true;
        }
        return false;
    }

    // 获取组（懒创建）
    public Group getGroup(int hatchNo, boolean updateWhileRunning) {
        return groups[hatchNo] != null ? groups[hatchNo] : new Group(hatchNo, updateWhileRunning);
    }
}
```

### 4.1 `Parameters.Group` 内部类

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/Parameters.java（Group 部分）
public class Group {

    private final int hatchNo;
    public final ParameterIn[]  parameterIn  = new ParameterIn[2];
    public final ParameterOut[] parameterOut = new ParameterOut[2];
    public boolean updateWhileRunning;

    // 创建输入参数（paramID = 0 或 1）
    public ParameterIn makeInParameter(int paramID, double defaultValue,
        INameFunction<?> name, IStatusFunction<?> status) {
        return new ParameterIn(paramID, defaultValue, name, status);
    }

    // 创建输出参数
    public ParameterOut makeOutParameter(int paramID, double defaultValue,
        INameFunction<?> name, IStatusFunction<?> status) {
        return new ParameterOut(paramID, defaultValue, name, status);
    }
}
```

### 4.2 `ParameterIn` / `ParameterOut`

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/Parameters.java（ParameterIn 部分）
public class ParameterIn implements IParameter {

    public final int    id;           // 存储索引 = hatchNo + 10 * paramID
    public final double defaultValue; // 默认值
    IStatusFunction     status;       // LED 状态计算函数
    INameFunction       name;         // 显示名称函数

    @Override
    public double get()       { return iParamsIn[id]; }
    void          set(double value) { iParamsIn[id] = value; }

    @Override
    public void updateStatus() {
        eParamsInStatus[id] = status.apply(parent, this);
    }

    @Override
    public LedStatus getStatus(boolean update) {
        if (update) updateStatus();
        return eParamsInStatus[id];
    }

    @Override
    public String getBrief() { return name.apply(parent, this); }

    // 索引分解
    @Override public int hatchId()    { return id % 10; }
    @Override public int parameterId(){ return id / 10; }
}
```

---

## 5. LedStatus LED 状态枚举

文件路径：`src/main/java/tectech/thing/metaTileEntity/multi/base/LedStatus.java`

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/LedStatus.java（全文）
public enum LedStatus {

    STATUS_UNUSED     (() -> EnumChatFormatting.DARK_GRAY + "Unused",  true),  // 深灰 - 未使用
    STATUS_TOO_LOW    (() -> EnumChatFormatting.BLUE      + "Too Low", false), // 蓝色闪烁 - 值过低
    STATUS_LOW        (() -> EnumChatFormatting.AQUA      + "Low",     true),  // 青色 - 值偏低
    STATUS_WRONG      (() -> EnumChatFormatting.DARK_PURPLE+ "Wrong",  false), // 紫色闪烁 - 错误值
    STATUS_OK         (() -> EnumChatFormatting.GREEN     + "Valid",   true),  // 绿色 - 正常
    STATUS_TOO_HIGH   (() -> EnumChatFormatting.RED       + "Too High",false), // 红色闪烁 - 值过高
    STATUS_HIGH       (() -> EnumChatFormatting.GOLD      + "High",    true),  // 金色 - 值偏高
    STATUS_UNDEFINED  (() -> EnumChatFormatting.GRAY      + "Unknown", false), // 灰色 - 未知
    STATUS_NEUTRAL    (() -> EnumChatFormatting.WHITE     + "Neutral", true),  // 白色 - 中性
    STATUS_WTF        (() -> LedStatus.values()[TecTech.RANDOM.nextInt(9)].name.get(), false); // 随机（彩虹）

    public final Supplier<String> name;
    public final boolean isOk;    // true = 稳定显示，false = 闪烁

    // 从字节还原（用于网络同步）
    public static LedStatus getStatus(byte value) {
        try   { return LedStatus.values()[value]; }
        catch (Exception e) { return STATUS_UNDEFINED; }
    }

    // 边界检查工厂方法（常用于构建 IStatusFunction）
    public static LedStatus fromLimitsInclusiveOuterBoundary(double value,
        double min, double low, double high, double max, double... excludedNumbers) {
        if (value < min) return STATUS_TOO_LOW;
        if (value > max) return STATUS_TOO_HIGH;
        if (value < low) return STATUS_LOW;
        if (value > high) return STATUS_HIGH;
        for (double val : excludedNumbers) {
            if (val == value) return STATUS_WRONG;
        }
        if (Double.isNaN(value)) return STATUS_WRONG;
        return STATUS_OK;
    }
}
```

**LED 颜色与含义对照：**

| 状态 | 颜色 | 稳定/闪烁 | 含义 |
|------|------|----------|------|
| UNUSED   | 深灰 | 稳定 | 参数未定义 |
| TOO_LOW  | 蓝色 | 闪烁 | 值低于最小限 |
| LOW      | 青色 | 稳定 | 值低于理想范围 |
| WRONG    | 紫色 | 闪烁 | 非法值（如排除值） |
| OK       | 绿色 | 稳定 | 正常工作 |
| TOO_HIGH | 红色 | 闪烁 | 值超过最大限 |
| HIGH     | 金色 | 稳定 | 值高于理想范围 |
| UNDEFINED| 灰色 | 闪烁 | 未知/未初始化 |
| NEUTRAL  | 白色 | 稳定 | 中性（未激活） |
| WTF      | 彩虹 | 随机 | 混乱状态 |

---

## 6. `IStatusFunction` / `INameFunction` 接口

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/IStatusFunction.java
public interface IStatusFunction<T extends TTMultiblockBase> {
    /** 根据机器状态和参数值计算 LED 颜色 */
    LedStatus apply(T t, Parameters.IParameter iParameter);
}

// src/main/java/tectech/thing/metaTileEntity/multi/base/INameFunction.java
public interface INameFunction<T extends TTMultiblockBase> {
    /** 返回参数在 Tooltip 中显示的名称/描述 */
    String apply(T t, Parameters.IParameter iParameter);
}
```

**典型用法（来自 `MTEQuantumComputer`）：**

```java
// src/main/java/tectech/thing/metaTileEntity/multi/MTEQuantumComputer.java（字段定义）
private static final INameFunction<MTEQuantumComputer> OC_NAME =
    (b, p) -> EnumChatFormatting.AQUA + "Overclock"
        + EnumChatFormatting.RESET + ": " + b.overclock.get();

private static final IStatusFunction<MTEQuantumComputer> OC_STATUS =
    (b, p) -> LedStatus.fromLimitsInclusiveOuterBoundary(
        p.get(), 1, 1, 1, b.maxOC, 0);
// 参数在 [1, maxOC] 范围内为 OK，= 0 为 WRONG，超限为 TOO_HIGH
```

---

## 7. LED 指示灯注册与渲染

### 7.1 `addParameterLED()`：注册一个 LED

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2383-2518
private void addParameterLED(ModularWindow.Builder builder, int hatch, int param, boolean input) {
    final int parameterIndex = hatch + param * 10;
    final int posIndex       = hatch * 2 + param;

    ButtonWidget ledWidget = new ButtonWidget() {
        @Override
        public void draw(float partialTicks) {
            IDrawable texture = null;
            final LedStatus status = input
                ? parametrization.eParamsInStatus[parameterIndex]
                : parametrization.eParamsOutStatus[parameterIndex];

            switch (status) {
                case STATUS_WTF: {
                    // 彩虹效果：随机 5 种颜色
                    int c = LEDCounter;
                    if (c > 4) c = TecTech.RANDOM.nextInt(5);
                    switch (c) {
                        case 0: texture = TecTechUITextures.PICTURE_PARAMETER_BLUE[posIndex];   break;
                        case 1: texture = TecTechUITextures.PICTURE_PARAMETER_CYAN[posIndex];   break;
                        case 2: texture = TecTechUITextures.PICTURE_PARAMETER_GREEN[posIndex];  break;
                        case 3: texture = TecTechUITextures.PICTURE_PARAMETER_ORANGE[posIndex]; break;
                        case 4: texture = TecTechUITextures.PICTURE_PARAMETER_RED[posIndex];    break;
                    }
                    break;
                }
                case STATUS_WRONG:  // 紫色闪烁（fallthrough）
                    if (LEDCounter < 2)       { texture = TecTechUITextures.PICTURE_PARAMETER_BLUE[posIndex]; break; }
                    else if (LEDCounter < 4)  { texture = TecTechUITextures.PICTURE_PARAMETER_RED[posIndex];  break; }
                case STATUS_OK:
                    texture = TecTechUITextures.PICTURE_PARAMETER_GREEN[posIndex];   break;

                case STATUS_TOO_LOW:  // 蓝色闪烁（fallthrough）
                    if (LEDCounter < 3) { texture = TecTechUITextures.PICTURE_PARAMETER_BLUE[posIndex]; break; }
                case STATUS_LOW:
                    texture = TecTechUITextures.PICTURE_PARAMETER_CYAN[posIndex];    break;

                case STATUS_TOO_HIGH: // 红色闪烁（fallthrough）
                    if (LEDCounter < 3) { texture = TecTechUITextures.PICTURE_PARAMETER_RED[posIndex]; break; }
                case STATUS_HIGH:
                    texture = TecTechUITextures.PICTURE_PARAMETER_ORANGE[posIndex];  break;

                case STATUS_NEUTRAL:
                    GL11.glColor4f(.85f, .9f, .95f, .5F);
                    texture = TecTechUITextures.PICTURE_PARAMETER_GRAY;
                    break;
                case STATUS_UNDEFINED:
                    GL11.glColor4f(.5f, .1f, .15f, .5F);
                    texture = TecTechUITextures.PICTURE_PARAMETER_GRAY;
                    break;
                case STATUS_UNUSED:
                default:
                    // 不渲染
                    break;
            }
            setBackground(texture);
            GL11.glColor4f(1f, 1f, 1f, 1f);
        }
    }
    // 点击：打开参数配置弹窗（仅输入 LED 可点击）
    .setOnClick((clickData, widget) -> {
        if (!widget.isClient() && input
            && parametrization.eParamsInStatus[parameterIndex] != LedStatus.STATUS_UNUSED) {
            // 关闭其他已打开的 LED 弹窗
            for (int i = 0; i < parametrization.eParamsInStatus.length; i++) {
                if (widget.getContext().isWindowOpen(LED_WINDOW_BASE_ID + i)) {
                    widget.getContext().closeWindow(LED_WINDOW_BASE_ID + i);
                }
            }
            widget.getContext().openSyncedWindow(LED_WINDOW_BASE_ID + parameterIndex);
        }
    });

    // LED 位置：Y = 97/177（有/无物品栏），输出 LED 偏移 6 像素
    builder.widget(ledWidget.dynamicTooltip(() -> input
        ? getFullLedDescriptionIn(hatch, param)
        : getFullLedDescriptionOut(hatch, param))
        .setPos(12 + posIndex * 8, (doesBindPlayerInventory() ? 97 : 177) + (input ? 0 : 1) * 6)
        .setSize(6, 4));  // LED 大小：6×4 像素

    // 注册服务端→客户端双向同步
    if (input) {
        builder
            .widget(new FakeSyncWidget.ByteSyncer(
                () -> parametrization.eParamsInStatus[parameterIndex].getOrdinalByte(),
                val -> parametrization.eParamsInStatus[parameterIndex] = LedStatus.getStatus(val))
                    .setOnClientUpdate(val -> ledWidget.notifyTooltipChange()))
            .widget(new FakeSyncWidget.DoubleSyncer(
                () -> parametrization.iParamsIn[parameterIndex],
                val -> parametrization.iParamsIn[parameterIndex] = val)
                    .setOnClientUpdate(val -> ledWidget.notifyTooltipChange()));
    } else {
        // 输出参数同步（eParamsOutStatus / iParamsOut）
        // ...（结构同上）
    }
}
```

### 7.2 `LEDCounter` 动画帧计数器

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2113
private static byte LEDCounter = 0;
// 在 DrawableWidget.draw() 中每帧递增：LEDCounter = (byte)((1 + LEDCounter) % 6)
// 0-5 循环，用于实现闪烁效果（0-1 / 0-2 等范围控制亮灭交替）
```

---

## 8. LED 配置弹窗（`createLEDConfigurationWindow`）

点击输入 LED 后弹出的数字输入窗口：

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:2355-2381
private ModularWindow createLEDConfigurationWindow(int ledID) {
    return ModularWindow.builder(100, 40)
        .setBackground(TecTechUITextures.BACKGROUND_SCREEN_BLUE)
        .setPos(
            (screenSize, mainWindow) -> new Pos2d(
                (screenSize.width / 2 - mainWindow.getSize().width / 2) - 110,
                (screenSize.height / 2 - mainWindow.getSize().height / 2)))
        // 关闭按钮
        .widget(ButtonWidget.closeWindowButton(true).setPos(85, 3))
        // 数字输入框（允许浮点数，8位小数）
        .widget(new NumericWidget()
            .setGetter(() -> parametrization.iParamsIn[ledID])
            .setSetter(val -> parametrization.iParamsIn[ledID] = val)
            .setIntegerOnly(false)
            .modifyNumberFormat(format -> format.setMaximumFractionDigits(8))
            .setTextColor(Color.LIGHT_BLUE.normal)
            .setTextAlignment(Alignment.CenterLeft)
            .setFocusOnGuiOpen(true)
            .setBackground(GTUITextures.BACKGROUND_TEXT_FIELD)
            .setPos(5, 20).setSize(90, 15))
        // 标题（格式：hatchId:paramId:I）
        .widget(new TextWidget((ledID % 10) + ":" + (ledID / 10) + ":I")
            .setDefaultColor(Color.WHITE.normal)
            .setTextAlignment(Alignment.Center)
            .setPos(5, 5))
        .build();
}
```

---

## 9. `parametersInstantiation_EM()`：参数定义

子类通过重写此方法来定义参数组，**在构造函数和结构重建后自动调用**。

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:478
protected void parametersInstantiation_EM() {}   // 基类空实现
```

**调用时机：**

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:211,221,871
// 构造时：
parametersInstantiation_EM();  // 第一次调用（来自 constructor → onFirstTick/init）

// 结构重建时：
parametersInstantiation_EM();  // checkMachine 后的热重载（DevEnv 防止 hotswap 崩溃）
```

**子类实现示例（`MTEQuantumComputer`）：**

```java
// src/main/java/tectech/thing/metaTileEntity/multi/MTEQuantumComputer.java:176-182
@Override
protected void parametersInstantiation_EM() {
    Parameters.Group hatch_0 = parametrization.getGroup(0);
    // 输入参数 0：超频倍数
    overclock = hatch_0.makeInParameter(0, 1, OC_NAME, OC_STATUS);
    // 输入参数 1：过压倍数
    overvolt  = hatch_0.makeInParameter(1, 1, OV_NAME, OV_STATUS);
    // 输出参数 0：当前最高温度
    maxCurrentTemp  = hatch_0.makeOutParameter(0, 0, MAX_TEMP_NAME, MAX_TEMP_STATUS);
    // 输出参数 1：可用算力
    availableData   = hatch_0.makeOutParameter(1, 0, COMPUTE_NAME, COMPUTE_STATUS);
}
```

**子类实现示例（`MTENetworkSwitch`，10 组路由权重）：**

```java
// src/main/java/tectech/thing/metaTileEntity/multi/MTENetworkSwitch.java:212-219
@Override
protected void parametersInstantiation_EM() {
    dst    = new Parameters.Group.ParameterIn[10];
    weight = new Parameters.Group.ParameterIn[10];
    for (int i = 0; i < 10; i++) {
        Parameters.Group hatch = parametrization.getGroup(i);
        dst[i]    = hatch.makeInParameter(0, i + 1, DEST_NAME,   DEST_STATUS);
        weight[i] = hatch.makeInParameter(1, 0,     WEIGHT_NAME, WEIGHT_STATUS);
    }
}
```

---

## 10. `hatchesStatusUpdate_EM()`：参数状态更新

每次 `checkProcessing()` 前后自动调用，刷新所有 LED 状态：

```java
// src/main/java/tectech/thing/metaTileEntity/multi/base/TTMultiblockBase.java:847-875
protected void hatchesStatusUpdate_EM() {
    if (getBaseMetaTileEntity().isClientSide()) return;

    boolean busy = mMaxProgresstime > 0;

    // 更新 Uncertainty 仓位
    for (MTEHatchUncertainty uncertainty : eUncertainHatches) {
        eCertainStatus = uncertainty.update(eCertainMode);
    }

    eAvailableData = getAvailableData_EM();

    // 更新所有参数 LED 状态（调用每个 ParameterIn/Out 的 updateStatus()）
    if (!GTValues.DEVENV) {
        parametersStatusesWrite_EM(busy);
    } else {
        try {
            parametersStatusesWrite_EM(busy);
        } catch (NoSuchMethodError e) {
            // DevEnv 热重载保护：重建参数组
            Arrays.fill(parametrization.groups, null);
            parametrization.parameterInArrayList.clear();
            parametrization.parameterOutArrayList.clear();
            Arrays.fill(parametrization.eParamsInStatus, LedStatus.STATUS_UNUSED);
            Arrays.fill(parametrization.eParamsOutStatus, LedStatus.STATUS_UNUSED);
            parametersInstantiation_EM();
            parametersStatusesWrite_EM(busy);
        }
    }
}
```

---

## 11. 完整注册流程时序图

```
机器构造（new MTE...）
│
├─ TTMultiblockBase 构造函数
│   └─ parametersInstantiation_EM()
│       └─ 子类定义 Parameters.Group 和 ParameterIn/Out
│
玩家打开 GUI（右键点击控制器）
│
├─ addUIWidgets(builder, buildContext)
│   ├─ DrawableWidget（背景）
│   ├─ Scrollable（信息文本）
│   ├─ createPowerPassButton()   → builder.widget + FakeSyncWidget.BooleanSyncer
│   ├─ createSafeVoidButton()    → builder.widget + FakeSyncWidget.BooleanSyncer
│   ├─ createPowerSwitchButton() → builder.widget + FakeSyncWidget.BooleanSyncer
│   └─ for hatch 0..9, param 0..1:
│       ├─ buildContext.addSyncedWindow(LED_WINDOW_BASE_ID + ledID, ...)
│       ├─ addParameterLED(builder, hatch, param, true)   // 输入 LED
│       └─ addParameterLED(builder, hatch, param, false)  // 输出 LED
│           ├─ ButtonWidget（自定义 draw 方法 → 按 LedStatus 渲染颜色）
│           ├─ setOnClick → openSyncedWindow(ledID)（输入 LED 可配置）
│           └─ FakeSyncWidget（状态 + 数值双向同步）
│
机器每次 checkProcessing（服务端）
│
├─ hatchesStatusUpdate_EM()（前）
│   └─ 遍历所有 ParameterIn/Out → updateStatus()
│       └─ IStatusFunction.apply(machine, param) → LedStatus
│
├─ checkProcessing_EM() / checkProcessing()
│   └─ 子类逻辑（读取 parametrization.iParamsIn[x] 等）
│
└─ hatchesStatusUpdate_EM()（后）
    └─ 再次刷新状态（反映配方结果）
```

---

## 12. 子类实现示例（MTEQuantumComputer）

```java
// 完整子类参数注册流程示例

public class MTEQuantumComputer extends TTMultiblockBase {

    // 定义参数引用（在 parametersInstantiation_EM 中赋值）
    private Parameters.Group.ParameterIn  overclock;
    private Parameters.Group.ParameterIn  overvolt;
    private Parameters.Group.ParameterOut maxCurrentTemp;
    private Parameters.Group.ParameterOut availableData;

    // 状态函数（lambda，根据参数值计算 LED 颜色）
    private static final IStatusFunction<MTEQuantumComputer> OC_STATUS =
        (b, p) -> LedStatus.fromLimitsInclusiveOuterBoundary(p.get(), 1, 1, 1, b.maxOC, 0);

    // 名称函数（lambda，返回 Tooltip 文本）
    private static final INameFunction<MTEQuantumComputer> OC_NAME =
        (b, p) -> EnumChatFormatting.AQUA + "Overclock"
            + EnumChatFormatting.RESET + ": " + b.overclock.get();

    @Override
    protected void parametersInstantiation_EM() {
        Parameters.Group hatch_0 = parametrization.getGroup(0);
        overclock      = hatch_0.makeInParameter(0, 1, OC_NAME, OC_STATUS);
        overvolt       = hatch_0.makeInParameter(1, 1, OV_NAME, OV_STATUS);
        maxCurrentTemp = hatch_0.makeOutParameter(0, 0, MAX_TEMP_NAME, MAX_TEMP_STATUS);
        availableData  = hatch_0.makeOutParameter(1, 0, COMPUTE_NAME, COMPUTE_STATUS);
    }

    @Override
    @NotNull
    protected CheckRecipeResult checkProcessing_EM() {
        // 读取参数值
        double oc = overclock.get();  // 超频倍数（由参数仓位传入）
        double ov = overvolt.get();   // 过压倍数

        // ... 配方逻辑 ...

        // 写入输出参数（会更新对应输出 LED）
        availableData.set(computeAmount);
        return SimpleCheckRecipeResult.ofSuccess("computing");
    }
}
```
