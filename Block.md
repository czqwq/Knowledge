# GT5-Unofficial 方块列表

**来源**: GT5-Unofficial源码  
**主要来源**: ItemList枚举中的方块类物品  
**总数**: 约202个方块相关枚举

---

## 使用说明

GT5U的方块主要通过ItemList枚举获取：

```java
// 获取方块
ItemStack block = ItemList.方块名.get(数量);

// 示例
ItemStack casing = ItemList.Casing_BronzePlatedBricks.get(1);
ItemStack hull = ItemList.Hull_LV.get(1);
```

---

## 方块分类

### 机器外壳 (Machine Casings)

#### 基础外壳
```
Casing_BronzePlatedBricks          // 青铜镀层砖
Casing_SolidSteel                  // 实心钢
Casing_StableTitanium              // 稳定钛
Casing_HeatProof                   // 耐热外壳
Casing_FrostProof                  // 防冻外壳
Casing_CleanStainlessSteel         // 洁净不锈钢
Casing_RobustTungstenSteel         // 坚固钨钢
Casing_Grate                       // 格栅
Casing_Vent                        // 通风口
Casing_RadiationProof              // 防辐射外壳
```

#### 线圈方块
```
Casing_Coil_Cupronickel            // 铜镍线圈方块
Casing_Coil_Kanthal                // 康铜线圈方块
Casing_Coil_Nichrome               // 镍铬线圈方块
Casing_Coil_TungstenSteel          // 钨钢线圈方块
Casing_Coil_HSSG                   // HSSG线圈方块
Casing_Coil_Naquadah                // 硅岩线圈方块
Casing_Coil_NaquadahAlloy          // 硅岩合金线圈方块
Casing_Coil_Trinium                // Trinium线圈方块
Casing_Coil_Superconductor         // 超导线圈方块
Casing_Coil_Eternal                // 永恒线圈方块
```

#### 涡轮外壳
```
Casing_Turbine                     // 涡轮外壳
Casing_Turbine1                    // 钢涡轮外壳
Casing_Turbine2                    // 不锈钢涡轮外壳
Casing_Turbine3                    // 钛涡轮外壳
Casing_Turbine4                    // 钨钢涡轮外壳
```

#### 管道外壳
```
Casing_Pipe_Bronze                 // 青铜管道外壳
Casing_Pipe_Steel                  // 钢管道外壳
Casing_Pipe_Titanium               // 钛管道外壳
Casing_Pipe_TungstenSteel          // 钨钢管道外壳
Casing_Pipe_Polytetrafluoroethylene  // PTFE管道外壳
```

#### 齿轮箱外壳
```
Casing_Gearbox_Bronze              // 青铜齿轮箱
Casing_Gearbox_Steel               // 钢齿轮箱
Casing_Gearbox_Titanium            // 钛齿轮箱
Casing_Gearbox_TungstenSteel       // 钨钢齿轮箱
```

### 机器外壳 (Machine Hulls)

按电压等级：

```
Hull_Bronze                        // 青铜外壳
Hull_Bronze_Bricks                 // 青铜砖外壳
Hull_Steel                         // 钢外壳
Hull_LV                            // LV机器外壳
Hull_MV                            // MV机器外壳
Hull_HV                            // HV机器外壳
Hull_EV                            // EV机器外壳
Hull_IV                            // IV机器外壳
Hull_LuV                           // LuV机器外壳
Hull_ZPM                           // ZPM机器外壳
Hull_UV                            // UV机器外壳
Hull_UHV                           // UHV机器外壳
Hull_UEV                           // UEV机器外壳
Hull_UIV                           // UIV机器外壳
Hull_UMV                           // UMV机器外壳
Hull_UXV                           // UXV机器外壳
```

### 多方块结构方块

```
Casing_Assembler                   // 组装机外壳
Casing_Assembler_Perfect           // 完美组装机外壳
Casing_CuttingFactory              // 切割工厂外壳
Casing_FusionCoil                  // 聚变线圈
Casing_FusionCoil2                 // 聚变线圈II
Casing_FusionCoil3                 // 聚变线圈III
Casing_FusionCasing                // 聚变外壳
Casing_FusionCasing2               // 聚变外壳II
Casing_FusionCasing3               // 聚变外壳III
Casing_Mining_Osmiridium           // 铱锇采矿外壳
Casing_Mining_Naquadah             // 硅岩采矿外壳
Casing_Mining_NaquadahAlloy        // 硅岩合金采矿外壳
Casing_Mining_Neutronium           // 中子素采矿外壳
Casing_MiningBlackPlutonium        // 黑钚采矿外壳
```

### 管道方块

```
// 小型管道
Pipe_Bronze_Small
Pipe_Steel_Small
Pipe_Titanium_Small
Pipe_TungstenSteel_Small
Pipe_Plastic_Small

// 中型管道
Pipe_Bronze_Medium
Pipe_Steel_Medium
Pipe_Titanium_Medium
Pipe_TungstenSteel_Medium
Pipe_Plastic_Medium

// 大型管道
Pipe_Bronze_Large
Pipe_Steel_Large
Pipe_Titanium_Large
Pipe_TungstenSteel_Large
Pipe_Plastic_Large

// 巨型管道
Pipe_Bronze_Huge
Pipe_Steel_Huge
Pipe_Titanium_Huge
Pipe_TungstenSteel_Huge
Pipe_Plastic_Huge
```

### 框架方块

```
Frame_Bronze                       // 青铜框架
Frame_Steel                        // 钢框架
Frame_Titanium                     // 钛框架
Frame_TungstenSteel                // 钨钢框架
```

---

## 方块meta值

许多GT方块使用meta值区分不同变体。例如：

```java
// 机器外壳方块使用meta区分不同类型
// Meta 0-15代表不同的外壳类型

// 通过ItemList获取特定meta的方块
ItemStack specificCasing = ItemList.Casing_SolidSteel.getWithDamage(1, metaValue);
```

---

## 方块类文件

### 主要方块类

| 类名 | 文件路径 | 用途 |
|------|---------|------|
| GTBlockCasings | `gregtech/common/blocks/GTBlockCasings.java` | 机器外壳 |
| GTBlockCasings2 | `gregtech/common/blocks/GTBlockCasings2.java` | 更多外壳 |
| GTBlockCasings3 | `gregtech/common/blocks/GTBlockCasings3.java` | 更多外壳 |
| GTBlockMachines | `gregtech/common/blocks/GTBlockMachines.java` | 机器方块 |
| GTBlockOres | `gregtech/common/blocks/GTBlockOres.java` | 矿石方块 |

---

## 在配方中使用方块

### 1. 合成表中使用

```java
// 使用ItemList中的方块
GTModHandler.addCraftingRecipe(
    someOutput,
    new Object[] {
        "CSC",
        "SHS",
        "CSC",
        'C', ItemList.Casing_SolidSteel.get(1),  // 方块
        'H', ItemList.Hull_MV.get(1),
        'S', OrePrefixes.screw.get(Materials.Steel)
    }
);
```

### 2. 多方块结构中使用

```java
// 多方块结构定义中指定方块
public IStructureDefinition<MultiBlockMachine> getStructure() {
    return IStructureDefinition.builder()
        .addShape("main", new String[][] {
            {"CCC", "CCC", "CCC"},
            {"C~C", "C C", "CCC"},
        })
        .addElement('C', ofBlock(
            GregTechAPI.sBlockCasings1, 0  // 使用特定meta的外壳方块
        ))
        .build();
}
```

---

## 方块ID和Meta

GT5U方块通常使用以下方式标识：

```
方块ID:Meta值

示例:
- gregtech:blockcasings:0   // 第一个外壳
- gregtech:blockcasings:1   // 第二个外壳
- gregtech:blockmachines:1  // 第一个机器
```

---

## 相关文档

- [Registry_README.md](./Registry_README.md) - 注册系统详细说明
- [Item.md](./Item.md) - 物品列表
- [Liquid.md](./Liquid.md) - 流体列表

---

**数据来源**: GT5-Unofficial master分支  
**最后更新**: 2026-02-19  
**方块相关枚举**: 约202个
