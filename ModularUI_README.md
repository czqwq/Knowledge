# ModularUI 完整分析文档

**分析版本**: ModularUI1 (v1.x) 和 ModularUI2 (v2.x)  
**目的**: 为AI提供GTNH GUI框架的完整知识库

---

## 目录

1. [版本概览](#版本概览)
2. [ModularUI1 详细分析](#modularui1-详细分析)
3. [ModularUI2 详细分析](#modularui2-详细分析)
4. [版本对比](#版本对比)
5. [迁移指南](#迁移指南)
6. [最佳实践](#最佳实践)

---

## 版本概览

### 基本信息

| 版本 | 包路径 | GitHub | 状态 |
|------|--------|--------|------|
| **ModularUI1** | `com.gtnewhorizons.modularui` | [GTNewHorizons/ModularUI](https://github.com/GTNewHorizons/ModularUI) | 🟡 维护中 |
| **ModularUI2** | `com.cleanroommc.modularui` | [GTNewHorizons/ModularUI2](https://github.com/GTNewHorizons/ModularUI2) | 🟢 活跃开发 |

### 文件统计

| 指标 | ModularUI1 | ModularUI2 |
|------|-----------|-----------|
| Java文件 | 146 | 637 |
| 接口数量 | 27 | 113 |
| 代码复杂度 | 中等 | 高 |
| 最新版本 | v1.x | v2.0+ |

### 核心差异

```
ModularUI1               ModularUI2
  ↓                        ↓
基础GUI框架          →   现代化重写版本
简单数据绑定        →   高级同步系统
代码配置主题        →   JSON ResourcePack主题
2D布局              →   3D矩阵变换
基础Widget          →   丰富组件库
```

---

## ModularUI1 详细分析

**包路径根**: `com.gtnewhorizons.modularui`

### 核心接口（27个）

#### A. Widget系统接口

##### 1. Widget基础

| 接口名 | 完整路径 | 功能 | 关键方法 |
|--------|---------|------|---------|
| **Widget** | `com.gtnewhorizons.modularui.api.widget.Widget` | 所有UI元素基类（抽象类） | `draw()`, `onInit()`, `isUnderMouse()`, `detectable()` |
| **ISyncedWidget** | `com.gtnewhorizons.modularui.api.widget.ISyncedWidget` | 客户端-服务器数据同步 | `readOnClient()`, `readOnServer()`, `detectAndSendChanges()`, `markForUpdate()` |
| **IWidgetParent** | `com.gtnewhorizons.modularui.api.widget.IWidgetParent` | 容器Widget接口 | `getChildren()`, `layoutChildren()`, `drawChildren()` |
| **IWidgetBuilder<T>** | `com.gtnewhorizons.modularui.api.widget.IWidgetBuilder<T>` | Builder模式API | `addWidgetInternal()`, `widget()`, `widgets()`, `widgetWhen()` |

##### 2. 交互接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **Interactable** | `com.gtnewhorizons.modularui.api.widget.Interactable` | 可交互事件处理 |
| **IDraggable** | `com.gtnewhorizons.modularui.api.widget.IDraggable` | 可拖拽Widget |
| **IDragAndDropHandler** | `com.gtnewhorizons.modularui.api.widget.IDragAndDropHandler` | NEI拖拽处理 |
| **IHasStackUnderMouse** | `com.gtnewhorizons.modularui.api.widget.IHasStackUnderMouse` | 鼠标下物品堆 |

**Interactable方法**:
```java
ClickResult onClick(int buttonId, boolean doubleClick);
boolean onClickReleased(int buttonId);
boolean onMouseDragged(int buttonId, long deltaTime);
boolean onMouseScroll(int direction);
boolean onKeyPressed(char character, int keyCode);
```

##### 3. 滚动接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IHorizontalScrollable** | `com.gtnewhorizons.modularui.api.widget.scroll.IHorizontalScrollable` | 水平滚动 |
| **IVerticalScrollable** | `com.gtnewhorizons.modularui.api.widget.scroll.IVerticalScrollable` | 竖直滚动 |

#### B. 屏幕和集成接口

| 接口名 | 完整路径 | 功能 | 备注 |
|--------|---------|------|------|
| **ITileWithModularUI** | `com.gtnewhorizons.modularui.api.screen.ITileWithModularUI` | GT5U TileEntity集成 | ⭐ 核心集成点 |
| **IItemWithModularUI** | `com.gtnewhorizons.modularui.api.screen.IItemWithModularUI` | GT5U Item集成 | ⭐ 核心集成点 |
| **IWindowCreator** | `com.gtnewhorizons.modularui.api.screen.IWindowCreator` | 窗口创建工厂 | - |
| **IContainerCreator** | `com.gtnewhorizons.modularui.api.screen.IContainerCreator` | Container创建工厂 | - |
| **IGuiCreator** | `com.gtnewhorizons.modularui.api.screen.IGuiCreator` | GUI创建工厂 | - |

**GT5U集成示例**:
```java
public class MyGTTile extends MTEHatch implements ITileWithModularUI {
    @Override
    public ModularWindow createWindow(UIBuildContext buildContext) {
        return ModularWindow.builder(176, 166)
            .widget(SlotWidget.ofItemHandler(inventory, 0)
                .pos(10, 10))
            .widget(ProgressBar.ofEnergyBar()
                .pos(50, 30))
            .build();
    }
}
```

#### C. Drawable接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IDrawable** | `com.gtnewhorizons.modularui.api.drawable.IDrawable` | 可绘制对象基础 |
| **IEase** | `com.gtnewhorizons.modularui.api.animation.IEase` | 动画缓动函数 |

#### D. Forge兼容接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IItemHandler** | `com.gtnewhorizons.modularui.api.forge.IItemHandler` | Forge物品处理 |
| **IItemHandlerModifiable** | `com.gtnewhorizons.modularui.api.forge.IItemHandlerModifiable` | 可修改物品处理 |
| **IFluidTankLong** | `com.gtnewhorizons.modularui.api.fluids.IFluidTankLong` | 长整数液体储存 |
| **IFluidTanksHandler** | `com.gtnewhorizons.modularui.api.fluids.IFluidTanksHandler` | 多液体储存 |
| **INBTSerializable<T>** | `com.gtnewhorizons.modularui.api.forge.INBTSerializable<T>` | NBT序列化 |

#### E. 其他接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IVanillaSlot** | `com.gtnewhorizons.modularui.api.widget.IVanillaSlot` | 原版Slot兼容 |
| **IWidgetDrawable** | `com.gtnewhorizons.modularui.api.widget.IWidgetDrawable` | 自定义Widget绘制 |
| **IOverflowableTank** | `com.gtnewhorizons.modularui.common.fluid.IOverflowableTank` | 溢出液体储存 |
| **IPacket** | `com.gtnewhorizons.modularui.common.internal.network.IPacket` | 网络包 |

### Widget组件系统

#### Widget继承树

```
Widget (abstract)
├── SyncedWidget (abstract)
│   ├── ButtonWidget
│   ├── ProgressBar
│   ├── SliderWidget
│   ├── CycleButtonWidget
│   ├── TextWidget
│   ├── DynamicTextWidget
│   ├── FluidSlotWidget
│   └── TabButton
├── MultiChildWidget (abstract)
│   ├── Row (水平布局)
│   │   └── DynamicPositionedRow
│   ├── Column (竖直布局)
│   │   └── DynamicPositionedColumn
│   ├── TabContainer
│   ├── ExpandTab
│   ├── ListWidget
│   └── SlotGroup
├── SingleChildWidget (abstract)
│   ├── Scrollable
│   ├── DrawableWidget
│   └── DropDownWidget
├── SlotWidget (IVanillaSlot + Interactable)
├── ScrollBar
├── PageControlWidget
└── TextFieldWidget系列
    ├── BaseTextFieldWidget
    ├── TextFieldWidget
    ├── NumericWidget
    └── TextEditorWidget
```

#### 布局Widget

**Row / Column**:
```java
// 包路径:
com.gtnewhorizons.modularui.common.widget.Row
com.gtnewhorizons.modularui.common.widget.Column

// 对齐选项:
MainAxisAlignment: START, CENTER, END, SPACE_BETWEEN, SPACE_AROUND, SPACE_EVENLY
CrossAxisAlignment: START, CENTER, END, STRETCH

// 使用示例:
Row row = new Row()
    .setMainAxisAlignment(MainAxisAlignment.CENTER)
    .widget(button1)
    .widget(button2);
```

### 数据绑定与同步

#### ISyncedWidget机制

```
服务器 ←→ 网络 ←→ 客户端

服务器端:
├─ detectAndSendChanges(init)  [每tick调用]
│  └─ markForUpdate() → 标记需要同步
├─ syncToClient(id, bufBuilder) → 发送网络包
└─ readOnServer(id, buf) ← 接收客户端消息

客户端:
├─ readOnClient(id, buf) ← 接收服务器消息
└─ syncToServer(id, bufBuilder) → 发送用户操作
```

**同步示例**:
```java
public class MyProgressBar extends SyncedWidget {
    private float progress = 0;
    
    @Override
    public void detectAndSendChanges(boolean init) {
        // 服务器检测变化并同步
        syncToClient(0, buf -> buf.writeFloat(this.progress));
    }
    
    @Override
    public void readOnClient(int id, PacketBuffer buf) {
        // 客户端接收更新
        if (id == 0) {
            this.progress = buf.readFloat();
        }
    }
}
```

### 布局系统

```
ModularWindow
  ├─ onResize(Size screenSize) → 重新计算
  ├─ rebuild() → layoutChildren()
  │  └─ IWidgetParent.layoutChildren(maxWidth, maxHeight)
  │     ├─ 计算子Widget大小 (determineSize)
  │     ├─ 应用布局对齐
  │     └─ 递归布局所有子Widget
  └─ drawChildren(float partialTicks)
```

---

## ModularUI2 详细分析

**包路径根**: `com.cleanroommc.modularui`

### 核心接口（113个）

#### A. 顶层架构接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IWidget** | `com.cleanroommc.modularui.api.widget.IWidget` | 所有UI组件基础 |
| **IParentWidget<I,W>** | `com.cleanroommc.modularui.api.widget.IParentWidget<I,W>` | 父容器接口 |
| **IMuiScreen** | `com.cleanroommc.modularui.api.IMuiScreen` | GUI屏幕包装 |
| **IPanelHandler** | `com.cleanroommc.modularui.api.IPanelHandler` | 面板管理 |

#### B. 渲染与可视化接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **IDrawable** | `com.cleanroommc.modularui.api.drawable.IDrawable` | 可绘制对象 |
| **IIcon** | `com.cleanroommc.modularui.api.drawable.IIcon` | 固定大小图标 |
| **IKey** | `com.cleanroommc.modularui.api.drawable.IKey` | i18n国际化 |
| **IHoverable** | `com.cleanroommc.modularui.api.drawable.IHoverable` | 可悬停状态 |
| **IRichTextBuilder<T>** | `com.cleanroommc.modularui.api.drawable.IRichTextBuilder<T>` | 富文本构造器 |

#### C. 布局与响应式系统

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **ILayoutWidget** | `com.cleanroommc.modularui.api.layout.ILayoutWidget` | 布局容器 |
| **IViewport** | `com.cleanroommc.modularui.api.layout.IViewport` | 视口接口 |
| **IViewportStack** | `com.cleanroommc.modularui.api.layout.IViewportStack` | 变换矩阵堆栈 |
| **IResizeable** | `com.cleanroommc.modularui.api.layout.IResizeable` | 可调整大小 |

**IViewportStack方法**:
```java
void pushViewport(IWidget widget, Area area);
void translate(float x, float y);
void rotate(float angle, float x, float y, float z);
void scale(float x, float y);
float transformX(float x, float y);
void applyToOpenGl();
```

#### D. 数据绑定与同步系统（30+接口）

##### 值接口层次

```
ISyncOrValue (标记接口)
├─ IValue<T> (只读值)
│  ├─ IIntValue<T>
│  ├─ IDoubleValue<T>
│  ├─ IBoolValue<T>
│  ├─ IStringValue<T>
│  ├─ IByteValue<T>
│  ├─ ILongValue<T>
│  ├─ IFloatValue<T>
│  └─ IEnumValue<T extends Enum<T>>
└─ IValueSyncHandler<T> (同步值)
   ├─ IIntSyncValue<T>
   ├─ IDoubleSyncValue<T>
   ├─ IBoolSyncValue<T>
   ├─ IStringSyncValue<T>
   ├─ IFloatSyncValue<T>
   ├─ IByteSyncValue<T>
   └─ ILongSyncValue<T>
```

**完整路径**:
- `com.cleanroommc.modularui.api.value.IValue<T>`
- `com.cleanroommc.modularui.api.value.IIntValue<T>`
- `com.cleanroommc.modularui.api.value.sync.IValueSyncHandler<T>`
- `com.cleanroommc.modularui.api.value.sync.IIntSyncValue<T>`
- ... (其他类型同理)

**IValueSyncHandler关键方法**:
```java
void setValue(T value, boolean setSource, boolean sync);
boolean updateCacheFromSource(boolean isFirstSync);
void notifyUpdate();
void write(PacketBuffer buffer);
void read(PacketBuffer buffer);
```

##### 交互事件接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **ISynced<W>** | `com.cleanroommc.modularui.api.widget.ISynced<W>` | Widget同步标记 |
| **IServerMouseAction** | `com.cleanroommc.modularui.api.value.sync.IServerMouseAction` | 服务端鼠标事件 |
| **IServerKeyboardAction** | `com.cleanroommc.modularui.api.value.sync.IServerKeyboardAction` | 服务端键盘事件 |
| **ISyncedAction** | `com.cleanroommc.modularui.api.ISyncedAction` | 同步行为 |

#### E. 主题系统接口

| 接口名 | 完整路径 | 功能 |
|--------|---------|------|
| **ITheme** | `com.cleanroommc.modularui.api.ITheme` | 主题接口 |
| **IThemeApi** | `com.cleanroommc.modularui.api.IThemeApi` | 主题管理API |
| **IJsonSerializable** | `com.cleanroommc.modularui.api.IJsonSerializable` | JSON序列化 |

### Widget组件系统

#### Widget继承树（简化）

```
IWidget (接口)
└── AbstractWidget
    └── Widget<W>
        ├── SingleChildWidget<W>
        │   ├── ButtonWidget<W>
        │   ├── DropDownMenu
        │   └── CycleButtonWidget
        ├── AbstractParentWidget<I,W>
        │   ├── ParentWidget<W>
        │   │   └── ModularPanel ⭐
        │   └── AbstractScrollWidget<I,W>
        │       ├── ListWidget<I,W>
        │       ├── Grid
        │       └── TextEditorWidget
        ├── TextWidget<W>
        ├── ProgressWidget
        ├── SliderWidget
        ├── ValueWidget<W,T> ⭐
        └── DraggableWidget<W>
```

**核心Widget**:
- **ModularPanel** (`com.cleanroommc.modularui.screen.ModularPanel`) - 窗口级面板
- **ValueWidget<W,T>** (`com.cleanroommc.modularui.widgets.ValueWidget`) - 值绑定Widget
- **ItemSlot** (`com.cleanroommc.modularui.widgets.ItemSlot`) - 物品槽
- **FluidSlot** (`com.cleanroommc.modularui.widgets.FluidSlot`) - 流体槽

#### 布局Widget

| Widget | 完整路径 | 功能 |
|--------|---------|------|
| **Flow** | `com.cleanroommc.modularui.widgets.layout.Flow` | 流式布局 |
| **Grid** | `com.cleanroommc.modularui.widgets.layout.Grid` | 网格布局 |
| **ListWidget** | `com.cleanroommc.modularui.widgets.ListWidget` | 列表布局 |

### 主题系统（JSON配置）

#### 主题结构

```java
// 位置: com.cleanroommc.modularui.theme

ITheme
├─ getFallback()
├─ getPanelTheme()
├─ getButtonTheme()
├─ getScrollbarTheme()
├─ getItemSlotTheme()
├─ getFluidSlotTheme()
├─ getTextFieldTheme()
└─ getToggleButtonTheme()
```

#### JSON配置示例

```json
{
  "themes": {
    "dark": {
      "widgets": {
        "button": {
          "color": "#FF0000",
          "background": "textures/button.png",
          "padding": 5
        },
        "panel": {
          "color": "#2E2E2E",
          "border": {
            "width": 1,
            "color": "#FFFFFF"
          }
        }
      }
    }
  }
}
```

**配置位置**:
- 默认: `assets/modularui/gui.json`
- 资源包: `resourcepacks/your_pack/assets/modularui/gui.json`

### 响应式布局系统

#### 大小计算

```java
// 包路径: com.cleanroommc.modularui.widget.sizer

Unit (大小单位)
├─ px(int value)          // 像素
├─ percentage(int value)  // 百分比
├─ relative(float value)  // 相对值
└─ auto()                 // 自动

Area (位置和大小)
├─ x, y (位置)
├─ width, height (大小)
└─ contains(x, y)

Box (边距/内边距)
├─ top, bottom, left, right
├─ horizontal() / vertical()
└─ all()
```

#### 布局示例

```java
Flow column = new Flow()
    .vertical()
    .child(label.size(100, 20))
    .child(input.flex(c -> c.grow(1)))  // 自动扩展
    .child(button.size(100, 20));

Grid grid = new Grid()
    .rows(3)
    .columns(3)
    .child(widget1, 0, 0)  // 第1行第1列
    .child(widget2, 1, 1); // 第2行第2列
```

### 变换与矩阵系统

```java
IViewportStack stack = context.getViewportStack();

// 推入视口
stack.pushViewport(panel, area);

// 变换操作
stack.translate(10, 20);  // 平移
stack.rotate((float)Math.PI/4, 0, 0, 1);  // 旋转45度
stack.scale(2.0f, 2.0f);  // 2倍缩放

// 应用到OpenGL
stack.applyToOpenGl();

// 坐标变换
float screenX = stack.transformX(localX, localY);
float screenY = stack.transformY(localX, localY);

// 弹出视口
stack.popViewport();
```

---

## 版本对比

### 架构对比

| 特性 | ModularUI1 | ModularUI2 |
|------|-----------|-----------|
| **包路径** | `com.gtnewhorizons.modularui` | `com.cleanroommc.modularui` |
| **接口数量** | 27 | 113 |
| **Widget数量** | 20+ | 50+ |
| **布局系统** | Row/Column + 对齐 | Flow/Grid + 响应式 |
| **数据绑定** | ISyncedWidget (基础) | IValueSyncHandler (高级) |
| **主题系统** | 代码配置 | JSON ResourcePack |
| **变换支持** | 2D | 3D矩阵堆栈 |
| **动画系统** | IEase (简单) | IAnimatable + Animator |
| **富文本** | 无 | IRichTextBuilder |
| **国际化** | 部分 | IKey完整支持 |

### 功能对比

| 功能 | v1 | v2 | 备注 |
|------|----|----|------|
| 基础Widget | ✅ | ✅+ | v2更多预制 |
| 布局容器 | ✅ Row/Column | ✅ Flow/Grid | v2更强大 |
| 物品槽 | ✅ SlotWidget | ✅ ItemSlot | v2类型安全 |
| 流体槽 | ✅ FluidSlotWidget | ✅ FluidSlot | v2功能更全 |
| 数据同步 | ✅ 手动 | ✅ 自动 | v2类型安全 |
| 主题 | ❌ | ✅ JSON | v2独有 |
| Recipe Viewer | ✅ NEI | ✅ 通用接口 | v2更灵活 |
| 工具提示 | ✅ 基础 | ✅ RichTooltip | v2更丰富 |
| 屏幕管理 | ✅ 基础 | ✅ IPanelHandler | v2更完善 |
| 视口裁剪 | ❌ | ✅ IViewport | v2独有 |

### API对比

#### 创建窗口

**v1**:
```java
// 包: com.gtnewhorizons.modularui.api.screen
ModularWindow window = ModularWindow.builder(176, 166)
    .widget(button)
    .build();
```

**v2**:
```java
// 包: com.cleanroommc.modularui.screen
ModularPanel panel = ModularPanel.defaultPanel("myGui", 176, 166)
    .child(button);
```

#### 数据绑定

**v1**:
```java
// 包: com.gtnewhorizons.modularui.api.widget
class MyWidget extends SyncedWidget {
    @Override
    public void detectAndSendChanges(boolean init) {
        syncToClient(0, buf -> buf.writeInt(value));
    }
    
    @Override
    public void readOnClient(int id, PacketBuffer buf) {
        value = buf.readInt();
    }
}
```

**v2**:
```java
// 包: com.cleanroommc.modularui.api.value
IntValue<Container> value = new IntValue<>(
    container::getValue,
    container::setValue
);
widget.syncHandler(value);  // 自动同步
```

#### 布局

**v1**:
```java
// 包: com.gtnewhorizons.modularui.common.widget
Row row = new Row()
    .setMainAxisAlignment(MainAxisAlignment.CENTER)
    .widget(button1)
    .widget(button2);
```

**v2**:
```java
// 包: com.cleanroommc.modularui.widgets.layout
Flow flow = new Flow()
    .horizontal()
    .child(button1)
    .child(button2.flex(c -> c.grow(1)));
```

---

## 迁移指南

### v1 → v2 迁移步骤

#### 1. 更新包导入

```java
// v1
import com.gtnewhorizons.modularui.api.widget.Widget;
import com.gtnewhorizons.modularui.api.screen.ModularWindow;

// v2
import com.cleanroommc.modularui.api.widget.IWidget;
import com.cleanroommc.modularui.screen.ModularPanel;
```

#### 2. Widget创建

```java
// v1: ModularWindow.builder()
ModularWindow window = ModularWindow.builder(176, 166)
    .widget(new ButtonWidget())
    .build();

// v2: ModularPanel.defaultPanel()
ModularPanel panel = ModularPanel.defaultPanel("myGui", 176, 166)
    .child(new ButtonWidget<>());
```

#### 3. 数据同步

```java
// v1: 手动同步
class MyWidget extends SyncedWidget {
    private int value;
    
    @Override
    public void detectAndSendChanges(boolean init) {
        syncToClient(0, buf -> buf.writeInt(value));
    }
    
    @Override
    public void readOnClient(int id, PacketBuffer buf) {
        this.value = buf.readInt();
    }
}

// v2: 自动同步
IntValue<Container> value = new IntValue<>(
    container::getValue,
    container::setValue
);
new ValueWidget<>().syncHandler(value);
```

#### 4. 布局

```java
// v1: Row/Column
Row row = new Row()
    .widget(button1)
    .widget(button2);

// v2: Flow (更灵活)
Flow flow = new Flow()
    .horizontal()
    .child(button1)
    .child(button2.flex(c -> c.grow(1)));
```

### 兼容性注意事项

1. **包路径完全不同** - 需要完全替换import
2. **API不兼容** - 不能混用v1和v2
3. **数据同步机制** - v2需要使用IValueSyncHandler
4. **主题系统** - v2支持JSON，v1不支持
5. **依赖版本** - 确保使用正确的ModularUI版本

---

## 最佳实践

### v1 最佳实践

#### 1. 使用Builder模式

```java
ModularWindow window = ModularWindow.builder(176, 166)
    .widget(SlotWidget.ofItemHandler(inventory, 0).pos(10, 10))
    .widget(ProgressBar.ofEnergyBar().pos(50, 30))
    .widget(new ButtonWidget()
        .setOnClick(() -> System.out.println("Clicked"))
        .pos(100, 50)
        .size(60, 20))
    .build();
```

#### 2. 正确实现同步

```java
public class SyncedProgressBar extends SyncedWidget {
    private final Supplier<Float> progressGetter;
    private float progress;
    
    public SyncedProgressBar(Supplier<Float> progressGetter) {
        this.progressGetter = progressGetter;
    }
    
    @Override
    public void detectAndSendChanges(boolean init) {
        float newProgress = progressGetter.get();
        if (newProgress != progress || init) {
            progress = newProgress;
            syncToClient(0, buf -> buf.writeFloat(progress));
        }
    }
    
    @Override
    public void readOnClient(int id, PacketBuffer buf) {
        if (id == 0) {
            progress = buf.readFloat();
        }
    }
}
```

#### 3. 使用Row/Column布局

```java
Column column = new Column()
    .setMainAxisAlignment(MainAxisAlignment.START)
    .setCrossAxisAlignment(CrossAxisAlignment.CENTER)
    .widget(title)
    .widget(content)
    .widget(footer);
```

### v2 最佳实践

#### 1. 使用值绑定

```java
// 类型安全的数据绑定
IntValue<MyContainer> energy = new IntValue<>(
    MyContainer::getEnergy,
    MyContainer::setEnergy
);

SliderWidget slider = new SliderWidget()
    .bounds(0, 10000)
    .syncHandler(energy);
```

#### 2. 使用响应式布局

```java
Flow mainLayout = new Flow()
    .vertical()
    .child(header.size(100, 20))
    .child(content.flex(c -> c.grow(1)))  // 自动填充剩余空间
    .child(footer.size(100, 20));
```

#### 3. 使用主题系统

```java
// 创建JSON主题
// assets/modularui/gui.json
{
  "themes": {
    "myTheme": {
      "widgets": {
        "button": {
          "color": "#4CAF50",
          "hoverColor": "#45A049"
        }
      }
    }
  }
}

// 应用主题
panel.theme("myTheme");
```

#### 4. 使用变换

```java
IViewportStack stack = context.getViewportStack();
stack.pushViewport(widget, area);
stack.translate(offsetX, offsetY);
stack.rotate(angle, 0, 0, 1);
stack.scale(scaleX, scaleY);
// 绘制...
stack.popViewport();
```

### 通用最佳实践

#### 1. 模块化设计

```java
// 将复杂GUI分解为多个方法
public ModularWindow createWindow(UIBuildContext ctx) {
    return ModularWindow.builder(200, 150)
        .widget(createHeader())
        .widget(createInventory())
        .widget(createControls())
        .build();
}

private Widget createHeader() {
    return new Row()
        .widget(titleText)
        .widget(closeButton);
}
```

#### 2. 复用Widget

```java
// 创建可重用的Widget工厂
public static SlotWidget createOutputSlot(IItemHandler handler, int slot) {
    return SlotWidget.ofItemHandler(handler, slot)
        .setEnabled(false)
        .setCanInsertItem(false);
}
```

#### 3. 错误处理

```java
@Override
public ModularWindow createWindow(UIBuildContext ctx) {
    try {
        return buildWindow();
    } catch (Exception e) {
        ModularUI.LOGGER.error("Failed to create GUI", e);
        return createFallbackWindow();
    }
}
```

---

## 接口完整索引

### ModularUI1 接口（27个）

**核心包路径**: `com.gtnewhorizons.modularui`

#### Widget系统（8个）
- `api.widget.Widget`
- `api.widget.ISyncedWidget`
- `api.widget.IWidgetParent`
- `api.widget.IWidgetBuilder<T>`
- `api.widget.Interactable`
- `api.widget.IDraggable`
- `api.widget.IDragAndDropHandler`
- `api.widget.IWidgetDrawable`

#### 滚动系统（2个）
- `api.widget.scroll.IHorizontalScrollable`
- `api.widget.scroll.IVerticalScrollable`

#### 屏幕集成（5个）
- `api.screen.ITileWithModularUI`
- `api.screen.IItemWithModularUI`
- `api.screen.IWindowCreator`
- `api.screen.IContainerCreator`
- `api.screen.IGuiCreator`

#### Drawable（2个）
- `api.drawable.IDrawable`
- `api.animation.IEase`

#### Forge兼容（5个）
- `api.forge.IItemHandler`
- `api.forge.IItemHandlerModifiable`
- `api.forge.INBTSerializable<T>`
- `api.fluids.IFluidTankLong`
- `api.fluids.IFluidTanksHandler`

#### 其他（5个）
- `api.widget.IHasStackUnderMouse`
- `api.widget.IVanillaSlot`
- `common.fluid.IOverflowableTank`
- `common.internal.network.IPacket`

### ModularUI2 接口（113个）

**核心包路径**: `com.cleanroommc.modularui`

#### 顶层架构（4个）
- `api.widget.IWidget`
- `api.widget.IParentWidget<I,W>`
- `api.IMuiScreen`
- `api.IPanelHandler`

#### Drawable（5个）
- `api.drawable.IDrawable`
- `api.drawable.IIcon`
- `api.drawable.IKey`
- `api.drawable.IHoverable`
- `api.drawable.IRichTextBuilder<T>`

#### 布局（5个）
- `api.layout.ILayoutWidget`
- `api.layout.IViewport`
- `api.layout.IViewportStack`
- `api.layout.IResizeable`
- `api.layout.IResizeParent`

#### 值系统（30+个）
- `api.value.IValue<T>`
- `api.value.ISyncOrValue`
- `api.value.IIntValue<T>` ... (9种基础类型)
- `api.value.sync.IValueSyncHandler<T>`
- `api.value.sync.IIntSyncValue<T>` ... (9种同步类型)

#### 主题（3个）
- `api.ITheme`
- `api.IThemeApi`
- `api.IJsonSerializable`

#### 其他（60+个）
- Widget接口、同步接口、事件接口等

---

## 相关文档

- [Core_Infrastructure_README.md](./Core_Infrastructure_README.md) - 核心基础设施
- [GT5U_Readme.md](./GT5U_Readme.md) - GT5U接口
- [GTNH_Repos_Index.md](./GTNH_Repos_Index.md) - 仓库总索引

---

**最后更新**: 2026-02-12  
**维护者**: AI Knowledge Base Team  
**版本**: 1.0
