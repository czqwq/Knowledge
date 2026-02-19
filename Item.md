# GT5-Unofficial 物品列表

**来源**: GT5-Unofficial ItemList枚举  
**文件**: `src/main/java/gregtech/api/enums/ItemList.java`  
**总数**: 2,716个物品枚举

---

## 使用说明

所有物品通过ItemList枚举获取：

```java
// 获取物品
ItemStack item = ItemList.物品名.get(数量);

// 示例
ItemStack macerator = ItemList.Machine_LV_Macerator.get(1);
ItemStack circuit = ItemList.Circuit_Integrated.get(16);
```

---

## 物品分类

### 机器 (Machines) - 333个

GT5U的各等级机器，命名格式：`Machine_<等级>_<类型>`

<details>
<summary>青铜时代机器 (Bronze Age)</summary>

```
Machine_Bronze_Boiler              // 青铜锅炉
Machine_Bronze_Boiler_Solar        // 太阳能青铜锅炉
Machine_HP_Solar                   // 高压太阳能锅炉
Machine_Bronze_CraftingTable       // 青铜工作台
Machine_Bronze_Furnace             // 青铜炉
Machine_Bronze_Macerator           // 青铜打粉机
Machine_Bronze_Extractor           // 青铜提取机
Machine_Bronze_Hammer              // 青铜锻造锤
Machine_Bronze_Compressor          // 青铜压缩机
Machine_Bronze_AlloySmelter        // 青铜合金炉
Machine_Bricked_BlastFurnace       // 砖制高炉
```

</details>

<details>
<summary>钢时代机器 (Steel Age)</summary>

```
Machine_Steel_Boiler_Lava          // 岩浆钢锅炉
Machine_Steel_Boiler               // 钢锅炉
Machine_HP_Furnace                 // 高压炉
Machine_HP_Macerator               // 高压打粉机
Machine_HP_Extractor               // 高压提取机
Machine_HP_Hammer                  // 高压锻造锤
Machine_HP_Compressor              // 高压压缩机
Machine_HP_AlloySmelter            // 高压合金炉
```

</details>

<details>
<summary>LV机器 (Low Voltage)</summary>

```
Machine_LV_AlloySmelter            // LV合金炉
Machine_LV_Assembler               // LV组装机
Machine_LV_Bender                  // LV卷板机
Machine_LV_Canner                  // LV装罐机
Machine_LV_Centrifuge              // LV离心机
Machine_LV_ChemicalBath            // LV化学浸洗器
Machine_LV_ChemicalReactor         // LV化学反应器
Machine_LV_Compressor              // LV压缩机
Machine_LV_Cutter                  // LV切割机
Machine_LV_Distillery              // LV蒸馏器
Machine_LV_ElectricFurnace         // LV电炉
Machine_LV_Electrolyzer            // LV电解机
Machine_LV_Extractor               // LV提取机
Machine_LV_Extruder                // LV挤压机
Machine_LV_FluidCanner             // LV流体装罐机
Machine_LV_FluidExtractor          // LV流体提取机
Machine_LV_FluidSolidifier         // LV流体固化机
Machine_LV_ForgeHammer             // LV锻造锤
Machine_LV_FormingPress            // LV冲压机
Machine_LV_Lathe                   // LV车床
Machine_LV_Macerator               // LV打粉机
Machine_LV_Microwave               // LV微波炉
Machine_LV_Mixer                   // LV搅拌机
Machine_LV_OreWasher               // LV洗矿机
Machine_LV_Packager                // LV打包机
Machine_LV_Polarizer               // LV极化器
Machine_LV_Printer                 // LV打印机
Machine_LV_Recycler                // LV回收机
Machine_LV_Scanner                 // LV扫描仪
Machine_LV_Sifter                  // LV筛选机
Machine_LV_Slicer                  // LV切片机
Machine_LV_ThermalCentrifuge       // LV热力离心机
Machine_LV_Unboxinator             // LV拆包机
Machine_LV_Wiremill                // LV线材轧机
```

</details>

<details>
<summary>MV-UV机器 (中高压机器)</summary>

```
// MV (Medium Voltage)
Machine_MV_AlloySmelter
Machine_MV_Assembler
Machine_MV_Centrifuge
Machine_MV_ChemicalReactor
// ... (与LV同样的机器类型，只是等级不同)

// HV (High Voltage)  
Machine_HV_AlloySmelter
Machine_HV_Assembler
// ...

// EV (Extreme Voltage)
Machine_EV_AlloySmelter
Machine_EV_Assembler
// ...

// IV (Insane Voltage)
Machine_IV_AlloySmelter
Machine_IV_Assembler
// ...

// LuV (Ludicrous Voltage)
Machine_LuV_AlloySmelter
Machine_LuV_Assembler
// ...

// ZPM (Zero Point Module)
Machine_ZPM_AlloySmelter
Machine_ZPM_Assembler
// ...

// UV (Ultimate Voltage)
Machine_UV_AlloySmelter
Machine_UV_Assembler
// ...
```

</details>

### 工具和装备 (Tools & Equipment) - 31个

```
Tool_Vajra                         // 金刚杵
Tool_Cover_Copy_Paste              // 覆盖物复制粘贴工具
Tool_Matches                       // 火柴
Tool_MatchBox_Used                 // 使用过的火柴盒
Tool_MatchBox_Full                 // 满火柴盒
Tool_Lighter_Invar_Empty           // 空因瓦打火机
Tool_Lighter_Invar_Used            // 使用过的因瓦打火机
Tool_Lighter_Invar_Full            // 满因瓦打火机
Tool_Lighter_Platinum_Empty        // 空铂打火机
Tool_Lighter_Platinum_Used         // 使用过的铂打火机
Tool_Lighter_Platinum_Full         // 满铂打火机
Tool_Cheat                         // 作弊工具
Tool_Scanner                       // 扫描仪
Tool_DataOrb                       // 数据球
Tool_DataStick                     // 数据棒
Tool_Sword_Bronze                  // 青铜剑
Tool_Pickaxe_Bronze                // 青铜镐
Tool_Shovel_Bronze                 // 青铜铲
Tool_Axe_Bronze                    // 青铜斧
Tool_Hoe_Bronze                    // 青铜锄
Tool_Axe_Flint                     // 燧石斧
// ... 更多工具
```

### 方块和外壳 (Blocks & Casings) - 202个

```
Casing_BronzePlatedBricks          // 青铜镀层砖
Casing_SolidSteel                  // 实心钢
Casing_StableTitanium              // 稳定钛
Casing_HeatProof                   // 耐热外壳
Casing_FrostProof                  // 防冻外壳
Casing_CleanStainlessSteel         // 洁净不锈钢
Casing_RobustTungstenSteel         // 坚固钨钢
Casing_Turbine                     // 涡轮外壳
Casing_Turbine1                    // 涡轮外壳1
Casing_Turbine2                    // 涡轮外壳2
Casing_Turbine3                    // 涡轮外壳3
Casing_Pipe_Bronze                 // 青铜管道外壳
Casing_Pipe_Steel                  // 钢管道外壳
Casing_Pipe_Titanium               // 钛管道外壳
Casing_Pipe_TungstenSteel          // 钨钢管道外壳
Casing_Pipe_Polytetrafluoroethylene  // PTFE管道外壳
Casing_Gearbox_Bronze              // 青铜齿轮箱
Casing_Gearbox_Steel               // 钢齿轮箱
Casing_Gearbox_Titanium            // 钛齿轮箱
Casing_Gearbox_TungstenSteel       // 钨钢齿轮箱
Casing_Coil_Cupronickel            // 铜镍线圈方块
Casing_Coil_Kanthal                // 康铜线圈方块
Casing_Coil_Nichrome               // 镍铬线圈方块
Casing_Coil_TungstenSteel          // 钨钢线圈方块
Casing_Coil_HSSG                   // HSSG线圈方块
Casing_Coil_Naquadah                // 硅岩线圈方块
Casing_Coil_NaquadahAlloy          // 硅岩合金线圈方块
Casing_Coil_Trinium                // Trinium线圈方块
Casing_Coil_Superconductor         // 超导线圈方块
// ... 更多外壳
```

### 电路和组件 (Circuits & Components) - 220个

```
Circuit_Integrated                 // 编程电路
Circuit_Board_Basic                // 基础电路板
Circuit_Board_Advanced             // 高级电路板
Circuit_Board_Elite                // 精英电路板
Circuit_Parts_Advanced             // 高级电路部件
Circuit_Parts_Wiring_Basic         // 基础电路布线
Circuit_Parts_Wiring_Advanced      // 高级电路布线
Circuit_Parts_Wiring_Elite         // 精英电路布线
Circuit_Parts_Crystal_Chip_Elite   // 精英水晶芯片
Circuit_Parts_Crystal_Chip_Master  // 大师水晶芯片
Component_Minecart_Wheels_Iron     // 铁矿车轮
Component_Minecart_Wheels_Steel    // 钢矿车轮
Component_Filter                   // 过滤器
Component_Grinder_Diamond          // 钻石研磨器
Component_Grinder_Tungsten         // 钨研磨器
// ... 更多组件
```

### 管道和线缆 (Pipes & Cables)

```
Pipe_Bronze_Small                  // 小型青铜管道
Pipe_Bronze_Medium                 // 中型青铜管道
Pipe_Bronze_Large                  // 大型青铜管道
Pipe_Steel_Small                   // 小型钢管道
Pipe_Steel_Medium                  // 中型钢管道
Pipe_Steel_Large                   // 大型钢管道
Cable_Copper_1x                    // 1x铜线缆
Cable_Copper_2x                    // 2x铜线缆
Cable_Copper_4x                    // 4x铜线缆
Cable_Copper_8x                    // 8x铜线缆
Cable_Copper_12x                   // 12x铜线缆
Cable_Copper_16x                   // 16x铜线缆
// ... 更多管道和线缆
```

### 其他mod物品引用 (Other Mod Items) - 1930个

这些是GT5U对其他mod物品的引用，例如：

```
// Forestry物品
FR_Lemon                           // 柠檬
FR_Mulch                           // 覆盖物
FR_Fertilizer                      // 肥料
FR_Compost                         // 堆肥
FR_Silk                            // 丝线
FR_Wax                             // 蜡
// ...

// IC2物品
IC2_Scrap                          // 废料
IC2_Scrapbox                       // 废料箱
IC2_Fertilizer                     // 肥料
IC2_Mixed_Metal_Ingot              // 混合金属锭
IC2_Resin                          // 树脂
IC2_Plantball                      // 植物球
// ...

// Railcraft物品
RC_ShuntingWire                    // 调车线
RC_Rail_Reinforced                 // 强化铁轨
RC_Rail_Electric                   // 电力铁轨
RC_Rail_Standard                   // 标准铁轨
// ...

// Thaumcraft物品
TC_Thaumometer                     // 神秘使之眼
TC_Node_Stabilizer                 // 节点稳定器
TC_Node_Energizer                  // 节点充能器
// ...
```

---

## 完整列表

由于物品数量庞大(2716个)，建议直接查看源码文件：

**源文件**: `src/main/java/gregtech/api/enums/ItemList.java`  
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/enums/ItemList.java

---

## 使用技巧

### 1. 在代码中查找物品

```java
// 检查物品是否已注册
if (ItemList.Machine_LV_Macerator.hasBeenSet()) {
    // 使用该物品
}
```

### 2. 在配方中使用

```java
// 合成表配方
GTModHandler.addCraftingRecipe(
    ItemList.Machine_LV_Macerator.get(1),  // 输出
    new Object[] {
        "PPP",
        "WHW",
        "PPP",
        'P', OrePrefixes.plate.get(Materials.Steel),
        'W', OrePrefixes.wireGt01.get(Materials.Copper),
        'H', ItemList.Hull_LV.get(1)  // 使用ItemList物品
    }
);
```

### 3. 批量获取

```java
// 获取多个相同物品
ItemStack circuits = ItemList.Circuit_Integrated.get(64);
```

---

## 相关文档

- [Registry_README.md](./Registry_README.md) - 注册系统详细说明
- [Block.md](./Block.md) - 方块列表
- [Liquid.md](./Liquid.md) - 流体列表

---

**数据来源**: GT5-Unofficial master分支  
**最后更新**: 2026-02-19  
**物品总数**: 2,716个
