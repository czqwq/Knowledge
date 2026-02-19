# GT5-Unofficial 已注册机器完整文档

> 数据来源：GT5-Unofficial 真实源代码（/src/main/java/gregtech/ 及 /src/main/java/tectech/）  
> 代码路径：https://github.com/GTNewHorizons/GT5-Unofficial  
> **严禁伪造代码，所有描述均依照真实源文件**

---

## 目录

1. [GT5U 多方块机器（Multiblock Machines）](#一gt5u-多方块机器)
2. [GT5U 基础单方块机器（Basic Machines）](#二gt5u-基础单方块机器)
3. [TecTech（TT）模块机器](#三tectech-tt-模块机器)
   - [量子计算机 / DataBank / 研究站](#31-量子计算机--databank--研究站)
   - [主动变压器 / 微波炉 / 网络交换机](#32-主动变压器--微波炉--网络交换机)
   - [特斯拉塔 / 能量注入机](#33-特斯拉塔--能量注入机)
   - [神锻炉（Forge of Gods）体系](#34-神锻炉forge-of-gods体系)
   - [鸿蒙之眼（Eye of Harmony）详细分析](#35-鸿蒙之眼eye-of-harmony-详细分析)

---

## 一、GT5U 多方块机器

### 1.1 电弧炉（Electric Blast Furnace，EBF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java`  
**继承**：`MTEAbstractMultiFurnace<MTEElectricBlastFurnace>`

**功能**：  
高温电弧冶炼炉，可将矿石/材料冶炼为更高级合金或化合物，是 GregTech 科技线中最核心的多方块机器之一。需要线圈方块决定最高可处理温度。

**工作原理**：  
- 通过 `addMachineType("Blast Furnace, EBF")` 注册机器类型
- 使用流体（如氧气）可以缩短配方时间
- 支持电路板调整（电路放入输入总线）
- 线圈温度决定可处理配方等级；高于配方要求时可额外获得效率加成（每级减少配方时间）
- 每 2 个线圈等级超出 = 相当于 1 次完美超频（4x EU、0.25x 时间）

**代码摘要**（tooltip 来自源文件 line 110-139）：
```java
tt.addMachineType("Blast Furnace, EBF")
    .addInfo("You can use some fluids to reduce recipe time. Place the circuit in the Input Bus")
    .addInfo("That means the EBF will reduce recipe time by a factor 4 instead of 2 (giving 100% efficiency)")
```

---

### 1.2 装配线（Assembly Line，AL）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEAssemblyLine.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEAssemblyLine>`

**功能**：  
制作 LuV+ 等级复杂机器部件，每个输入仓位（切片）对应 NEI 配方中的一个输入槽位，物品和流体按 NEI 顺序逐槽插入，不兼容合成台配方。

**代码摘要**（line 136-139）：
```java
tt.addMachineType("Assembly Line, Assline, AL")
    .addInfo("Used to craft complex machine parts (LuV+)")
    .addInfo("Items & Fluids are inserted in NEI order, one per slice")
    .addInfo("Does not run Assembler recipes")
```

---

### 1.3 聚变反应堆（Fusion Computer，MK1/2/3）
**类文件**：  
- `MTEFusionComputer.java`（抽象基类）  
- `MTEFusionComputer1.java`、`MTEFusionComputer2.java`、`MTEFusionComputer3.java`（具体实现）

**功能**：  
核聚变反应堆，消耗大量 EU 启动并持续运行，将等离子体/特殊材料聚变为更高级材料或能量。

**代码摘要**（MTEFusionComputer1 line 79-83）：
```java
tt.addMachineType("Fusion Reactor")
    .addInfo("It's over 9000!!!")
    .addInfo("§b2,048§7 EU/t and §b10M§7 EU capacity per Energy Hatch")
    .addInfo("If the recipe has a startup cost greater than the")
    .addInfo("number of energy hatches * cap, you can't do it")
```

**工作原理**：  
- 需要大量能量仓，每个仓提供 2048 EU/t 输入和 10M EU 容量
- 启动费用 = 能量仓数量 × 容量，必须满足才能开启配方
- MK1/2/3 的区分在于可用线圈等级和最大启动能量

---

### 1.4 蒸馏塔（Distillation Tower，DT）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEDistillationTower.java`  
**继承**：`MTEEnhancedMultiBlockBase<MTEDistillationTower>`

**功能**：  
将复杂流体蒸馏为多种产品，每个输出流体对应结构中特定高度的输出舱，高度等于 NEI 配方中的槽位编号。

**代码摘要**（line 138-140）：
```java
tt.addMachineType("Distillery, DT")
    .addInfo("Fluids are only put out at the correct height")
    .addInfo("The correct height equals the slot number in the NEI recipe")
```

---

### 1.5 大型锅炉（Large Boiler，Bronze/Steel/Titanium/TungstenSteel）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeBoiler.java`（抽象基类）+ 四个子类

**功能**：  
消耗固体燃料或液体燃料产生蒸汽。编程电路可以节流（每档减少 1000L/s 产量）。

**代码摘要**（line 126-136）：
```java
tt.addMachineType("Boiler");
// ...
.addInfo("A programmed circuit in the main block throttles the boiler (-1000L/s per config)")
.addInfo("Only some solid fuels are allowed (check the NEI Large Boiler tab for details)")
.addInfo("If there are any disallowed fuels in the input bus, the boiler won't run!")
```

---

### 1.6 爆炸压缩机（Implosion Compressor）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEImplosionCompressor.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEImplosionCompressor>`

**功能**：  
利用炸药/TNT爆炸压力将材料压缩为致密材料（如宝石质地材料）。

**代码摘要**（line 98-99）：
```java
tt.addMachineType("Implosion Compressor")
    .addInfo("Explosions are fun")
```

---

### 1.7 大型内燃机（Large Combustion Engine，LCE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEDieselEngine.java`  
**继承**：`MTEEnhancedMultiBlockBase<MTEDieselEngine>`

**功能**：  
消耗柴油等高热值液体燃料发电，发动机进气舱正面不能有阻挡（必须是空气）。可注入液氧提高效率。

**代码摘要**（line 99-133）：
```java
tt.addMachineType("Combustion Generator, LCE")
    .addInfo("Engine Intake Casings must not be obstructed in front (only air blocks)")
```

---

### 1.8 超大型内燃机（Extreme Combustion Engine，ECE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEExtremeDieselEngine.java`  
**继承**：`MTEDieselEngine`

**功能**：  
大型内燃机升级版，需要高等级燃料 + 润滑油，可选注液氧提升产量。

**代码摘要**（line 43-47）：
```java
tt.addMachineType("Combustion Generator, ECE")
    .addInfo("Supply high rating fuel and 8000L of Lubricant per hour to run")
    .addInfo("Supply 40L/s of Liquid Oxygen to boost output (optional)")
    .addInfo("Default: Produces 10900EU/t at 100% fuel efficiency")
    .addInfo("Boosted: Produces 32700EU/t at 150% fuel efficiency")
```

---

### 1.9 洁净室（Cleanroom）
**类文件**：`gregtech/common/tileentities/machines/multi/MTECleanroom.java`  
**继承**：`MTETooltipMultiBlockBase`

**功能**：  
为高级芯片等精密材料的制造提供洁净环境。启动时消耗 40 EU/t，效率满后降至 4 EU/t；每个维护问题降低 10% 最大效率；内部污染会强制关机。

**代码摘要**（line 126-133）：
```java
tt.addMachineType("Cleanroom")
    .addInfo("Consumes 40 EU/t when first turned on, and 4 EU/t once at 100% efficiency")
    .addInfo("Can accept 2A from an LV energy hatch")
    .addInfo("Will overclock and gain efficiency faster starting from HV")
    .addInfo("Each maintenance issues reduces maximum efficiency by 10%")
    .addInfo("Generating any pollution inside causes the cleanroom to shut down")
```

---

### 1.10 炭坑（Charcoal Pit）
**类文件**：`gregtech/common/tileentities/machines/multi/MTECharcoalPit.java`  
**继承**：`MTETooltipMultiBlockBase`

**功能**：  
将原木转化为易碎木炭方块，无需电力，成型后自动开始运行。

**代码摘要**（line 227-229）：
```java
tt.addMachineType("Charcoal Pile Igniter, CPI")
    .addInfo("Converts Logs into Brittle Charcoal blocks")
    .addInfo("Automatically starts when formed")
```

---

### 1.11 焦炭炉（Coke Oven）
**类文件**：`gregtech/common/tileentities/machines/multi/MTECokeOven.java`  
**继承**：`MTEEnhancedMultiBlockBase<MTECokeOven>`

**功能**：  
将煤炭转化为焦炭并产出杂酚油（Creosote Oil）。

**代码摘要**（line 81-82）：
```java
return new MultiblockTooltipBuilder().addMachineType("Coke Oven")
    .addInfo("Turns coal into coke and produces creosote oil")
```

---

### 1.12 砖砌高炉（Bricked Blast Furnace，BBF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEBrickedBlastFurnace.java`  
**继承**：`MetaTileEntity`

**功能**：  
用于钢铁和通用火法冶金，是最早期的多方块冶炼机器，具有实用界面。

**代码摘要**（line 138-140）：
```java
tooltipBuilder.addMachineType("Blast Furnace, BBF")
    .addInfo("Usable for Steel and general Pyrometallurgy")
    .addInfo("Has a useful interface, unlike other gregtech multis")
```

---

### 1.13 热交换器（Large Heat Exchanger，LHE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEHeatExchanger.java`  
**继承**：`MTEEnhancedMultiBlockBase<MTEHeatExchanger>`

**功能**：  
通过热流体（超热蒸汽/各种蒸汽）驱动涡轮发电，或对流体进行加热/冷却处理，实现热能转换。

**代码摘要**（line 116）：
```java
tt.addMachineType("Heat Exchanger, LHE")
```

---

### 1.14 大型化学反应器（Large Chemical Reactor，LCR）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeChemicalReactor.java`

**功能**：  
多方块化学反应器，可直接接受流体输入（而非流体胶囊），比单方块化学反应器更高效。

**代码摘要**（line 107-108）：
```java
tt.addMachineType("Chemical Reactor, LCR")
    .addInfo("Accepts fluids instead of fluid cells")
```

---

### 1.15 真空冷冻机（Vacuum Freezer，VF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEVacuumFreezer.java`

**功能**：  
冷却热锭和热单元，将高温材料冷却为可用材料（如冷却热铂棒）。

**代码摘要**（line 98-99）：
```java
tt.addMachineType("Vacuum Freezer, VF")
    .addInfo("Cools hot ingots and cells")
```

---

### 1.16 石油裂解装置（Oil Cracker，OCU）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEOilCracker.java`

**功能**：  
热裂解重烃，比化学反应器更高效。支持氢裂解（减少 20% 氢耗，增加 25% 产出）和蒸汽裂解（不同效果），最大 50% EU 折扣。

**代码摘要**（line 126-132）：
```java
tt.addMachineType("Cracker, OCU")
    .addInfo("Maximum of " + TooltipHelper.effText(0.5f) + " EU discount")
    .addInfo("Thermally cracks heavy hydrocarbons into lighter fractions")
    .addInfo("More efficient than the Chemical Reactor")
    .addInfo("Hydro - Consumes 20% less Hydrogen and outputs 25% more cracked fluid")
```

---

### 1.17 焦化炉（Pyrolyse Oven）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEPyrolyseOven.java`

**功能**：  
工业级炭化生产机器，EU/t 不受线圈等级影响。

**代码摘要**（line 97-100）：
```java
tt.addMachineType("Coke Oven")
    .addInfo("Industrial Charcoal producer")
    .addInfo("EU/t is not affected by Coil tier")
```

---

### 1.18 大型流体提取机（Large Fluid Extractor，LFE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeFluidExtractor.java`

**功能**：  
大规模提取流体，可并行运行多个提取配方。玻璃等级限制能量仓等级（UEV玻璃解锁所有等级）。

**代码摘要**（line 286-302）：
```java
tt.addMachineType("Fluid Extractor, LFE")
    .addInfo("The energy hatch tier is limited by the glass tier. UEV glass unlocks all tiers")
```

---

### 1.19 超大型化学反应器（Mega Chemical Reactor，MCR）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEMegaChemicalReactor.java`

**功能**：  
LCR 的超大版，支持更大量的并行化学反应。

**代码摘要**（line 101）：
```java
tt.addMachineType("Chemical Reactor, MCR")
```

---

### 1.20 纳米锻造炉（Nano Forge）
**类文件**：`gregtech/common/tileentities/machines/multi/MTENanoForge.java`

**功能**：  
利用纳米技术制造纳米机器人。机器等级取决于控制器槽位中的纳米机器人类型，每个等级可能需要结构更改。

**代码摘要**（line 746-754）：
```java
tt.addMachineType("Nanite Fabricator")
    .addInfo("Requires insane amounts of power to create nanites")
    .addInfo("Each tier requires some structural changes")
    .addInfo("Machine tier depends on Nanite in controller slot")
    .addInfo("Requires a Carbon Nanite to use tier 1")
```

---

### 1.21 等离子体锻造炉（Plasma Forge，DTPF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEPlasmaForge.java`

**功能**：  
超维度等离子体处理机器，可储存一定运行时间。

**代码摘要**（line 576-593）：
```java
tt.addMachineType("Plasma Forge, DTPF")
    .addInfo("Transcending Dimensional Boundaries.")
    .addInfo("the total amount of stored runtime")
```

---

### 1.22 超维等离子混合机（Transcendent Plasma Mixer，TPM）
**类文件**：`gregtech/common/tileentities/machines/multi/MTETranscendentPlasmaMixer.java`

**功能**：  
DTPF 的辅助机器，根据并行菜单中设定的数量并行运行，所有 EU 从无线能量网络扣除。

**代码摘要**（line 108-112）：
```java
tt.addMachineType("Transcendent Mixer, TPM")
    .addInfo("Assisting in all your DTPF needs!")
    .addInfo("This multiblock will run in parallel according to the amount set in the parallel menu")
    .addInfo("All inputs will scale, except time...")
    .addInfo("All EU is deducted from wireless EU networks only")
```

---

### 1.23 蒸汽大型涡轮（Large Steam Turbine，LST）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeTurbineSteam.java`  
**继承**：`MTELargeTurbine`

**功能**：  
消耗蒸汽发电，输出蒸馏水，产电量取决于涡轮叶片和配合度。可用螺丝刀调节配合度。

**代码摘要**（line 61-65）：
```java
tt.addMachineType("Steam Turbine, LST")
    .addInfo("Needs a Turbine, place inside controller")
    .addInfo("Outputs Distilled Water as well as producing power")
    .addInfo("Power output depends on turbine and fitting")
    .addInfo("Use screwdriver to adjust fitting of turbine")
```

---

### 1.24 气体涡轮（Large Gas Turbine，LGT）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeTurbineGas.java`  
**继承**：`MTELargeTurbine`

**功能**：  
消耗燃气（天然气等）驱动涡轮发电。

**代码摘要**（line 58-59）：
```java
tt.addMachineType("Gas Turbine, LGT")
    .addInfo("Needs a Turbine, place inside controller")
```

---

### 1.25 等离子体涡轮（Large Plasma Turbine，LPT）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeTurbinePlasma.java`  
**继承**：`MTELargeTurbine`

**功能**：  
消耗来自聚变反应堆的等离子体发电，产量极高。

**代码摘要**（line 61-63）：
```java
tt.addMachineType("Plasma Turbine, LPT")
    .addInfo("Needs a Turbine, place inside controller")
    .addInfo("Use your Fusion Reactor to produce the Plasma")
```

---

### 1.26 石油钻井机（Oil Drill 1-4 & Infinite，FDR）
**类文件**：`MTEOilDrill1~4.java`、`MTEOilDrillInfinite.java`（均继承 `MTEOilDrillBase`）

**功能**：  
在指定范围内抽取石油，工作范围可用螺丝刀调整。有限版最终会耗尽油田，无限版基础循环时间为 1 tick，可用剪线钳启用批量模式（16x 时间、16x 产出）。

**代码摘要**（MTEOilDrillBase line 123-130、MTEOilDrillInfinite line 38-42）：
```java
tt.addMachineType("Pump, FDR")
    .addInfo("Works on " + getRangeInChunks() + "x" + getRangeInChunks() + " chunks")
    .addInfo("Use a Screwdriver to configure range")
// MTEOilDrillInfinite:
    .addInfo("Base cycle time: 1 tick")
    .addInfo("You can enable batch mode with wire cutters. 16x Time 16x Output")
```

---

### 1.27 矿石钻井机（Ore Drilling Plant 1-4，MBM）
**类文件**：`MTEOreDrillingPlant1~4.java`（均继承 `MTEOreDrillingPlantBase`）

**功能**：  
大范围矿石开采，可以区块模式工作，产出约 3 倍破碎矿石。

**代码摘要**（MTEOreDrillingPlantBase line 633-640）：
```java
tt.addMachineType("Miner, MBM")
    .addInfo("Use a Screwdriver to configure working area")
    .addInfo("Maximum area is " + side + "x" + side + " blocks")
    .addInfo("In chunk mode, working area center is the chunk corner nearest to the drill")
    .addInfo("Gives ~3x as much crushed ore vs normal processing")
    .addInfo("Fortune bonus of " + formatNumber(mTier + 3) + ". Only works on small ores")
```

---

### 1.28 空气过滤器（Air Filter 1/2/3，EAF）
**类文件**：`MTEAirFilter1.java`、`MTEAirFilter2.java`、`MTEAirFilter3.java`（均继承 `MTEAirFilterBase`）

**功能**：  
过滤区块内污染，消耗涡轮叶片。每个消音舱降低工作区域一个区块的污染，工作区域随等级增大。

**代码摘要**（MTEAirFilterBase line 191-202）：
```java
tt.addMachineType("Air Filter, EAF")
    .addInfo("Needs a Turbine in the controller")
    .addInfo("Can process " + (2 * multiTier + 1) + "x" + (2 * multiTier + 1) + " chunks")
    .addInfo("Each muffler hatch reduces pollution in one chunk of the working area by:")
```

---

### 1.29 混凝土回填机（Concrete Backfiller 1/2）
**类文件**：`MTEConcreteBackfiller1.java`、`MTEConcreteBackfiller2.java`（均继承 `MTEConcreteBackfillerBase`）

**功能**：  
向下方区域填充轻混凝土方块，防止敌怪生成，可减少游戏延迟。填满一层后自动收回管道。

**代码摘要**（MTEConcreteBackfillerBase line 99-105）：
```java
tt.addMachineType("Concrete Backfiller")
    .addInfo("Will fill in areas below it with light concrete. This goes through walls")
    .addInfo("Use it to remove any spawning locations beneath your base to reduce lag")
    .addInfo("Will pull back the pipes after it finishes that layer")
    .addInfo("Range is " + getRadius() + "x" + getRadius() + " blocks horizontally")
```

---

### 1.30 衰变仓库（Decay Warehouse）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEDecayWarehouse.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEDecayWarehouse>`

**功能**：  
存储单一放射性同位素并让其自然衰变。衰变速度取决于半衰期（半衰期越短越快），无论是否通电均会衰变。EU 输入决定每秒可存入/取出的物品数量。

**代码摘要**（line 223-234）：
```java
tt.addMachineType("Decay Warehouse")
    .addInfo("Stores a single type of radioactive isotope and allows it to decay over time")
    .addInfo("Decay speed is dependent on the isotopes' half-lives (lower is faster)")
    .addInfo("Isotopes decay regardless of whether the warehouse is on or powered")
    .addInfo("The warehouse will pull in up to N / EU_PER_IO items per second,")
    .addInfo("where N is the warehouse's EU input (standard energy hatch rules)")
```

---

### 1.31 工业离心机（Industrial Centrifuge）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialCentrifuge.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEIndustrialCentrifuge>`

**功能**：  
大型工业离心机，用于离心分离材料，可用螺丝刀禁用动画。

**代码摘要**（line 150-152）：
```java
tt.addMachineType("Centrifuge")
    .addInfo("Disable animations with a screwdriver")
```

---

### 1.32 工业酿造机（Industrial Brewery，BBB）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialBrewery.java`

**功能**：  
大规模酿造机器，并行处理酿造配方。

**代码摘要**（line 144）：
```java
tt.addMachineType("Brewery, BBB")
```

---

### 1.33 流体成型机（Fluid Shaper / Mass Solidifier）
**类文件**：`MTEFluidShaper.java`、`MTEMassSolidifier.java`（均继承 `MTEExtendedPowerMultiBlockBase`）

**功能**：  
将流体固化为固体物品。运行速度会随时间增加（最快 3x），但衰减速度是加速速度的两倍。

**代码摘要**（MTEFluidShaper line 184-199）：
```java
tt.addMachineType("Fluid Solidifier")
    .addInfo("Speeds up to a maximum of " + TooltipHelper.speedText(3f))
    .addInfo("Decays at double the rate that it speeds up at")
```

---

### 1.34 工业电磁分离机（Industrial EM Separator/Polarizer，MFE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialElectromagneticSeparator.java`

**功能**：  
同时支持电磁分离和极化两种模式（螺丝刀切换），需要电磁铁插入专用槽位。

**代码摘要**（line 210-214）：
```java
tt.addMachineType("Electromagnetic Separator/Polarizer, MFE")
    .addInfo("Use screwdriver to switch mode")
    .addInfo("Insert an electromagnet into the electromagnet housing to use")
    .addInfo("Better electromagnets give further bonuses")
    .addInfo("With Tengam electromagnet, multi-amp (NOT laser) hatches are allowed")
```

---

### 1.35 工业拉丝机（Wire Mill，IWF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialWireMill.java`

**功能**：  
大规模拉丝作业。

**代码摘要**（line 137）：
```java
tt.addMachineType("Wiremill, IWF")
```

---

### 1.36 工业激光雕刻机（High Intensity Laser Engraver，HILE）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialLaserEngraver.java`

**功能**：  
高强度激光雕刻，激光源舱决定最大配方等级和并行数量（并行 = 激光安培数立方根）。

**代码摘要**（line 228-235）：
```java
tt.addMachineType("Laser Engraver, HILE")
    .addInfo("Laser source hatch determines maximum recipe tier and parallels")
    .addInfo("Recipe tier and overclocks limited to laser source tier + 1")
    .addInfo("Parallels equal to the cube root of laser source amperage input")
```

---

### 1.37 工业打包/拆包机（Packager/Unpackager，AWD）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialPackager.java`

**功能**：  
极端打包需求的多方块机器，可在控制器中配置为拆包模式。

**代码摘要**（line 158-160）：
```java
tt.addMachineType("Packager, Unpackager, AWD")
    .addInfo("This Multiblock is used for EXTREME packaging requirements")
    .addInfo("Can be configured to work as an Unpackager in controller")
```

---

### 1.38 大型分子装配机（Large Molecular Assembler）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELargeMolecularAssembler.java`

**功能**：  
需要数据球（Data Orb）放入控制器槽位，前两次超频为完美超频。

**代码摘要**（line 276-296）：
```java
return new MultiblockTooltipBuilder().addMachineType(MACHINE_TYPE)
    .addInfo("Needs a Data Orb to be placed in the controller")
    .addInfo("The first two Overclocks:")
```

---

### 1.39 多功能熔炉（Multi Furnace）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEMultiFurnace.java`

**功能**：  
多方块熔炉，并行处理熔炉配方。

**代码摘要**（line 107）：
```java
tt.addMachineType("Furnace")
```

---

### 1.40 多功能罐装机（Multi Canner）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEMultiCanner.java`

**功能**：  
并行罐装作业。

**代码摘要**（line 117-119）：
```java
tt.addMachineType("Canner")
    .addInfo("It's uncanny!")
```

---

### 1.41 多功能车床（Multi Lathe，IPL）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEMultiLathe.java`

**功能**：  
工业多方块车床。

**代码摘要**（line 193）：
```java
tt.addMachineType("Lathe, IPL")
```

---

### 1.42 多功能压热器（Multi Autoclave）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEMultiAutoclave.java`

**功能**：  
多方块高压蒸汽作业机。

**代码摘要**（line 207）：
```java
tt.addMachineType("Autoclave")
```

---

### 1.43 橡胶树提取机（Latex Extractor，LATEX）
**类文件**：`gregtech/common/tileentities/machines/multi/MTELatex.java`

**功能**：  
大规模橡胶提取。可插入弹性奇点（Elastic Singularity）获得额外加成（电缆涂层）。

**代码摘要**（line 264-273）：
```java
tt.addMachineType("Cable Coater, LATEX")
    .addInfo("An Elastic Singularity can be inserted into the controller to gain the following bonuses")
```

---

### 1.44 工业提取机（Industrial Extractor）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIndustrialExtractor.java`

**功能**：  
大规模提取作业。

**代码摘要**（line 157）：
```java
tt.addMachineType("Extractor")
```

---

### 1.45 旋转磁控管（Spinmatron）
**类文件**：`gregtech/common/tileentities/machines/multi/MTESpinmatron.java`

**功能**：  
改进型离心机，超频上限为能量仓等级 + 1，非巨型涡轮有效果降低。

**代码摘要**（line 386-408）：
```java
tt.addMachineType("Centrifuge")
    .addInfo("Overclocks limited to Hatch Tier + 1")
    .addInfo("Non-Huge Turbines have reduced effectiveness...")
```

---

### 1.46 太阳能电池板工厂（Solar Factory）
**类文件**：`gregtech/common/tileentities/machines/multi/MTESolarFactory.java`

**功能**：  
批量生产太阳能电池板，有三个等级结构，各自允许更高产量。

**代码摘要**（line 380-384）：
```java
tt.addMachineType("Solar Factory")
    .addInfo("Produces solar panels in bulk")
    .addInfo("The structure has 3 tiers, each allowing greater production than the last")
```

---

### 1.47 虫洞发生器（Wormhole Generator，MWG）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEWormholeGenerator.java`

**功能**：  
通过两台虫洞发生器传输 EU，两台必须用 AE2 纠缠奇点（Entangled Singularity）链接。传输效率在速率完全稳定时为固定百分比（常量 `TRANSFER_EFFICIENCY`）。

**代码摘要**（line 969-973）：
```java
tt.addMachineType("Wormhole Generator, MWG")
    .addInfo("Transfers EU between two wormhole generators")
    .addInfo("Wormholes are linked by placing an AE2 Entangled Singularity in each controller slot")
    .addInfo("The transfer rate is limited by the wormhole size, and the wormhole size is governed by the transfer rate")
```

---

### 1.48 研究补全机（Research Completer）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEResearchCompleter.java`

**功能**：  
利用 EU 和神秘学节点（Thaumcraft Nodes）完成研究笔记，节点放在中间排。

**代码摘要**（line 348-350）：
```java
tt.addMachineType("Research Completer")
    .addInfo("Completes Thaumcraft research notes using EU and Thaumcraft nodes")
    .addInfo("Place nodes in the center row")
```

---

### 1.49 综合矿石处理机（Integrated Ore Factory，IOF）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEIntegratedOreFactory.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEIntegratedOreFactory>`

**功能**：  
一步完成所有矿石处理流程。每种矿石消耗 30 EU/t + 2L 润滑油 + 200L 蒸馏水，支持多种处理模式（螺丝刀切换），可按住潜行螺丝刀清除石粉输出。

**代码摘要**（line 203-210）：
```java
tt.addMachineType("Ore Processor, IOF")
    .addInfo("Does all ore processing in one step")
    .addInfo("Every ore costs 30EU/t, 2L lubricant, 200L distilled water")
    .addInfo("Processing time is dependent on mode")
    .addInfo("Use a screwdriver to switch mode")
    .addInfo("Sneak click with screwdriver to void the stone dust")
```

---

### 1.50 熵增处理机（Entropic Processor）
**类文件**：`gregtech/common/tileentities/machines/multi/MTEEntropicProcessor.java`  
**继承**：`MTEExtendedPowerMultiBlockBase<MTEEntropicProcessor>`

**功能**：  
通过增大或降低物质熵来处理物质。默认 8 并行，催化剂由配方消耗后在完成时返还，每个外壳等级提供 1 次完美超频（奥金 = 1 次）。

**代码摘要**（line 213-224）：
```java
tt.addMachineType("Entropic Processor")
    .addInfo("Processes substances by increasing or decreasing their entropy")
    .addInfo("Has " + TooltipHelper.parallelText(8) + " parallels by default")
    .addInfo("Mixes fluids or solids with a magical catalyst")
    .addInfo("Catalyst is consumed by the recipe, then returned upon completion")
    .addInfo("Performs one perfect overclock per casing tier (Thaumium = 1 perfect OC)")
```

---

## 二、GT5U 基础单方块机器

基础机器实现在 `gregtech/common/tileentities/machines/basic/` 和 `gregtech/common/tileentities/machines/` 目录中，主要通过 `MetaTileEntityBasicMachine` 及其子类实现。

| 机器 | 类名 | 功能 |
|------|------|------|
| 物质复制机 | `MTEReplicator` | 从 UU-Matter 复制材料 |
| 物质制造机 | `MTEMassfabricator` | 消耗大量 EU 将物品分解为 UU-Matter |
| 扫描仪 | `MTEScanner` | 扫描物品/生物/方块，产出数据卡 |
| 微波能量发射器 | `MTEMicrowaveEnergyTransmitter` | 无线传输 EU，无需电缆 |
| 矿脉探测器（高级）| `MTEAdvSeismicProspector` | 探测地底矿脉信息 |
| 炸箱机 | `MTEBoxinator` | 往箱子里装东西 |
| 充电器 | `MTECharger` | 为可充电物品充电 |
| 磁悬浮柱 | `MTEMagLevPylon` | 磁悬浮传输相关 |
| 工业蜂巢 | `MTEIndustrialApiary` | 大规模养蜂 |
| 岩石破碎机 | `MTERockBreaker` | 破碎岩石 |
| 传送机 | `MTETeleporter` | 消耗 EU 传送玩家/物品 |
| 水泵 | `MTEPump` | 抽水 |
| 药水酿造机 | `MTEPotionBrewer` | 酿造药水 |
| 涡轮增压机 | `MTETurboCharger` | 加速机器运行 |
| 世界加速器 | `MTEWorldAccelerator` | 加速周围 TileEntity |
| 名称移除器 | `MTENameRemover` | 移除物品自定义名称 |
| 怪物驱逐装置 | `MTEMonsterRepellent` | 防怪物生成 |
| 更好的点唱机 | `MTEBetterJukebox` | 播放音乐 |
| 矿工 | `MTEMiner` | 向下挖矿 |
| 抽屉成型机 | `MTEDrawerFramer` | 制作抽屉框架 |

---

## 三、TecTech（TT）模块机器

TecTech 模块位于 `src/main/java/tectech/`，是 GT5U 的高级科技扩展，主要面向 UV+ 科技树。

### 3.1 量子计算机（Quantum Computer）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEQuantumComputer.java`

**功能**：  
生成计算能力（Computation），为需要计算资源的机器（如研究站）提供算力。可用螺丝刀切换模式。

**代码摘要**（line 358-365）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.em.computer.machinetype"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.computer.desc.0"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.computer.desc.1")) // Used to generate
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.computer.desc.2")) // Use screwdriver to
```

---

### 3.2 数据银行（Data Bank）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEDataBank.java`

**功能**：  
为多个研究站/量子计算机提供数据存储/分发服务，通过 DATA 管道连接，可用螺丝刀切换配置。

**代码摘要**（line 123-134）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.em.databank.type"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.databank.desc.0")) // Controller block of
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.databank.desc.1")) // Used to supply
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.databank.desc.2")) // and give multiple
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.databank.desc.3")) // Use screwdriver to
```

---

### 3.3 研究站（Research Station）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEResearchStation.java`

**功能**：  
使用计算资源研究高级科技。

**代码摘要**（line 330-340）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.em.research.type"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.research.desc.1"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.research.desc.2"))
```

---

### 3.4 主动变压器（Active Transformer）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEActiveTransformer.java`

**功能**：  
在不同电压等级间转换 EU，只有 0.004% 的损耗。

**代码摘要**（line 174-179）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.em.transformer.machinetype"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.transformer.desc.1")) // Can transform to
    .addInfo(translateToLocal("gt.blockmachines.multimachine.em.transformer.desc.2")) // Only 0.004% power
```

---

### 3.5 微波炉（Microwave）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEMicrowave.java`

**功能**：  
计时加热机器，启动计时器后在计时期间可对附近机器/方块产生效果。可配置行为。

**代码摘要**（line 232-248）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.tm.microwave.name"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.microwave.desc.1")) // Starts a timer when
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.microwave.desc.2")) // While the timer is
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.microwave.desc.4")) // Can be configured
```

---

### 3.6 网络交换机（Network Switch / Network Switch Adv）
**类文件**：`MTENetworkSwitch.java`、`MTENetworkSwitchAdv.java`

**功能**：  
连接多个量子计算机/数据银行网络节点，路由计算资源。高级版支持更复杂的路由规则。

**代码摘要**（MTENetworkSwitch line 140-148）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.em.switch.type"));
tt.addInfo(translateToLocal("gt.blockmachines.multimachine.em.switch.desc.0"));
tt.addInfo(translateToLocal("gt.blockmachines.multimachine.em.switch.desc.1"));
```

---

### 3.7 特斯拉塔（Tesla Tower）
**类文件**：`tectech/thing/metaTileEntity/multi/MTETeslaTower.java`

**功能**：  
无线传输 EU，向附近特斯拉线圈单方块机器输电。传输电压取决于塔的等级。

**代码摘要**（line 600-614）：
```java
tt.addMachineType(translateToLocal("gt.blockmachines.multimachine.tm.teslaCoil.name"))
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.teslaCoil.desc.1")) // Used to transmit
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.teslaCoil.desc.2")) // Can be fed with
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.teslaCoil.desc.3")) // Transmitted voltage
    .addInfo(translateToLocal("gt.blockmachines.multimachine.tm.teslaCoil.desc.4")) // Primary Tesla
```

---

### 3.8 能量注入机（Energy Infuser）
**类文件**：`tectech/thing/metaTileEntity/multi/MTEEnergyInfuser.java`

**功能**：  
同时充电和修复装备，不支持储货输入总线，充电无最大速度或能量损耗。

**代码摘要**（line 240-244）：
```java
tt.addMachineType("Restorer")
    .addInfo("Simultaneously recharges and repairs equipment")
    .addInfo("Stocking input buses are not supported")
    .addInfo("Recharging: No max speed or energy loss")
```

---

### 3.9 神锻炉体系（Forge of Gods / Godforge）

#### 3.9.1 神锻炉主体（Forge of Gods）
**类文件**：`tectech/thing/metaTileEntity/multi/godforge/MTEForgeOfGods.java`

**功能**：  
超级多方块机器，利用稳定中子星的热能、引力和动能进行材料处理，是游戏中最先进的冶炼系统。其四个模块的功能从基础冶炼到物质降维逐级提升。

**代码摘要**（line 773-783）：
```java
tt.addMachineType("Stellar Forge")
    .addInfo("A massive structure harnessing the thermal, gravitational and")
    .addInfo("kinetic energy of a stabilised neutron star for material processing")
    .addInfo("to varying degrees, ranging from regular smelting to matter degeneration")
```

#### 3.9.2 熔融模块（Molten Module）
**类文件**：`tectech/thing/metaTileEntity/multi/godforge/MTEMoltenModule.java`

**功能**：  
神锻炉第二模块，直接将材料熔融为液态。如果输出材料没有液态形式，则以固态输出。

**代码摘要**（line 172-178）：
```java
tt.addMachineType("Blast Smelter")
    .addInfo("This is a module of the Godforge")
    .addInfo("Used for high temperature material liquefaction")
    .addInfo("The second module of the Godforge, this module melts materials directly into their liquid form.")
```

#### 3.9.3 等离子模块（Plasma Module）
**类文件**：`tectech/thing/metaTileEntity/multi/godforge/MTEPlasmaModule.java`

**功能**：  
神锻炉第三模块，用极端高温将材料离子化为等离子体。不是所有等离子体都能生产。

**代码摘要**（line 167-173）：
```java
tt.addMachineType("Plasma Fabricator")
    .addInfo("Used for extreme temperature matter ionization")
    .addInfo("The third module of the Godforge, this module infuses materials with extreme amounts")
    .addInfo("of heat, ionizing and turning them into plasma directly.")
```

#### 3.9.4 冶炼模块（Smelting Module）
**类文件**：`tectech/thing/metaTileEntity/multi/godforge/MTESmeltingModule.java`

**功能**：  
神锻炉第一模块，执行最基础的热处理（与熔炉/高炉相同的冶炼操作）。

**代码摘要**（line 209-215）：
```java
tt.addMachineType("Blast Furnace, Furnace")
    .addInfo("Used for basic smelting operations at various temperatures")
    .addInfo("As the first of the Godforge modules, this module performs the most basic")
    .addInfo("thermal processing, namely smelting materials identically to a furnace or blast furnace")
```

#### 3.9.5 奇异物质模块（Exotic Module）
**类文件**：`tectech/thing/metaTileEntity/multi/godforge/MTEExoticModule.java`

**功能**：  
神锻炉第四也是最后一个模块，打破物质的基本构成单元，产生奇异混合物，包括夸克-胶子等离子体（QGP）。

**代码摘要**（line 499-505）：
```java
tt.addMachineType("Exotic Matter Producer")
    .addInfo("Used for ultra high temperature matter degeneration")
    .addInfo("The fourth and final module of the Godforge, this module breaks apart the very")
    .addInfo("building blocks of matter, producing exotic mixtures in the process. Quark-Gluon Plasma")
```

---

## 3.10 鸿蒙之眼（Eye of Harmony）详细分析

**类文件**：`tectech/thing/metaTileEntity/multi/MTEEyeOfHarmony.java`  
**行数**：1,898 行  
**关联文件**：
- `tectech/recipe/EyeOfHarmonyRecipe.java` — 配方数据类  
- `tectech/recipe/EyeOfHarmonyRecipeStorage.java` — 配方存储/查找  
- `tectech/thing/block/TileEntityEyeOfHarmony.java` — 渲染方块实体  
- `tectech/recipe/TecTechRecipeMaps.java` — 配方图谱（用于 NEI 显示）

---

### 机器概述

鸿蒙之眼（Eye of Harmony，EOH）是一个**时空操控机器**，通过超维度工程创造一个内部比外部更大的时空泡。由于其 EU 需求过于庞大，无法通过传统能量仓处理——**所有 EU 直接从玩家的无线 EU 网络中扣除和输出**，不使用任何能量仓。

**代码证明**（line 977-979）：
```java
.addInfo("to be handled with conventional means. All EU requirements are handled directly by")
.addInfo("your wireless EU network")
```

**结构验证代码**（line 900-912）：
```java
// Make sure there are no energy hatches.
{
    if (!mEnergyHatches.isEmpty()) {
        return false;
    }
    if (!mExoticEnergyHatches.isEmpty()) {
        return false;
    }
}
// Make sure there are 2 input hatches.
return mInputHatches.size() == 2;
```

---

### 结构组成

EOH 是一个巨大的多方块结构（33x33x33 左右），需要（来自 tooltip，line 1090-1118）：
- **534** 块 Reinforced Temporal Structure Casing（加固时间结构外壳）
- **31** 块 Infinite SpaceTime Energy Boundary Casing（无限时空能量边界外壳）
- **168** 块 Time Dilation Field Generator（时间膨胀场发生器，**D 字符**）
- **48** 块 Stabilisation Field Generator（稳定场发生器）
- **138** 块 Spacetime Compression Field Generator（时空压缩场发生器）
- 2 个普通输入舱（氢气和氦气输入）
- 1 个 ME 输出舱
- 1 个普通输入总线
- 1 个 ME 输出总线
- **无能量仓**（拒绝所有能量仓）

---

### 三大可分级方块

EOH 有三种可升级（0-8 级）的特殊结构方块，对机器行为有决定性影响：

#### ① 时空压缩场发生器（Spacetime Compression Field Generator）
- 决定可运行的配方等级（`spacetimeCompressionFieldMetadata`）
- 超出配方要求的等级越多，处理时间越短（每超出一级，时间乘以 `(1 - SPACETIME_CASING_DIFFERENCE_DISCOUNT_PERCENTAGE)`，即折扣 3%）

**常量**（line 107）：
```java
private static final double SPACETIME_CASING_DIFFERENCE_DISCOUNT_PERCENTAGE = 0.03;
```

#### ② 时间膨胀场发生器（Time Dilation Field Generator）
- 每级别使配方时间减少 50%（乘法，`timeAccelerationFieldMetadata`）
- 同时降低配方成功概率（每级降低 `TIME_ACCEL_DECREASE_CHANCE_PER_TIER = 0.0925`，约 9.25%）

**常量**（line 109）：
```java
private static final double TIME_ACCEL_DECREASE_CHANCE_PER_TIER = 0.0925;
```

#### ③ 稳定场发生器（Stabilisation Field Generator）
- 提高配方成功概率（`stabilisationFieldMetadata`）
- 但降低产出（每级 5%）
- 低等级稳定场会有**产电惩罚**（power output penalty）

**常量**（line 111）：
```java
private static final double STABILITY_INCREASE_PROBABILITY_DECREASE_YIELD_PER_TIER = 0.05;
```

---

### 工作流程（从源代码精确还原）

#### Step 1：初始化（onPreTick，每 tick）

**代码**（line 1514-1527）：
```java
@Override
public void onPreTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    super.onPreTick(aBaseMetaTileEntity, aTick);

    if (aTick == 1) {
        userUUID = getBaseMetaTileEntity().getOwnerUuid();
        strongCheckOrAddUser(userUUID);
    }

    if (!recipeRunning && mMachine) {
        if ((aTick % TICKS_BETWEEN_HATCH_DRAIN) == 0) {
            drainFluidFromHatchesAndStoreInternally();
        }
    }
}
```

- 第 1 tick：获取机器所有者 UUID，注册到无线网络（`strongCheckOrAddUser`）
- 非配方运行时，每 **20 tick（1 秒）** 从输入舱抽取流体存入内部存储（`TICKS_BETWEEN_HATCH_DRAIN = 20`）
- 存储的流体：氢气、氦气、原始星尘物质（RawStarMatter）

---

#### Step 2：检查配方（checkProcessing_EM）

**代码**（line 1192-1212）：
```java
@Override
@NotNull
protected CheckRecipeResult checkProcessing_EM() {
    ItemStack controllerStack = getControllerSlot();
    if (controllerStack == null) {
        return SimpleCheckRecipeResult.ofFailure("no_planet_block");
    }

    lagPreventer++;
    if (lagPreventer < RECIPE_CHECK_INTERVAL) {
        lagPreventer = 0;
        // No item in multi gui slot.
        currentRecipe = TecTech.eyeOfHarmonyRecipeStorage.recipeLookUp(controllerStack);
        if (currentRecipe == null) {
            return CheckRecipeResultRegistry.NO_RECIPE;
        }
        CheckRecipeResult result = processRecipe(currentRecipe);
        if (!result.wasSuccessful()) currentRecipe = null;
        return result;
    }
    return CheckRecipeResultRegistry.NO_RECIPE;
}
```

**关键逻辑**：
1. 控制器槽位中必须有**行星方块**（`BlockDimensionDisplay`，由 gtneioreplugin 提供）——不同星球对应不同配方
2. 每 **60 tick（3 秒）** 才检查一次配方（`RECIPE_CHECK_INTERVAL = 3 * 20`），防卡顿

---

#### Step 3：处理配方（processRecipe）

**代码**（line 1226-1387，精简关键部分）：

##### 3.1 读取电路倍增器（OC 倍数）
```java
// Get circuit damage, clamp it and then use it later for overclocking.
currentCircuitMultiplier = 0;
for (ItemStack itemStack : mInputBusses.get(0).getRealInventory()) {
    if (GTUtility.isAnyIntegratedCircuit(itemStack)) {
        currentCircuitMultiplier = MathHelper.clamp_int(itemStack.getItemDamage(), 0, 24);
        break;
    }
}
```

- 输入总线中的集成电路决定超频次数（0-24），电路编号 = OC 次数

##### 3.2 读取星列阵（Astral Array）数量（决定并行）
```java
for (ItemStack itemStack : mInputBusses.get(0).getRealInventory()) {
    if (astralArrayAmount >= ASTRAL_ARRAY_LIMIT) break;
    if (itemStack != null && itemStack.isItemEqual(CustomItemList.astralArrayFabricator.get(1))) {
        long insertAmount = Math.min(itemStack.stackSize, ASTRAL_ARRAY_LIMIT - astralArrayAmount);
        astralArrayAmount += insertAmount;
        itemStack.stackSize -= insertAmount;
    }
}
```

- 星列阵制造机（`astralArrayFabricator`）被放入输入总线后消耗，提供并行能力
- 并行数公式（line 1250-1254）：
```java
parallelExponent = (long) Math.floor(
    Math.log(PARALLEL_FOR_FIRST_ASTRAL_ARRAY * Math.min(astralArrayAmount, ASTRAL_ARRAY_LIMIT))
        / LOG_CONSTANT);
parallelAmount = (long) GTUtility.powInt(2, parallelExponent);
```
其中：
- `PARALLEL_FOR_FIRST_ASTRAL_ARRAY = 8`
- `ASTRAL_ARRAY_LIMIT = 8637`（精确可达到 2^21 并行）
- `LOG_CONSTANT = Math.log(1.7)`

---

##### 3.3 流体检查
```java
// 单并行：需要氢气和氦气
if (parallelAmount == 1) {
    if (getHydrogenStored() < currentRecipe.getHydrogenRequirement())
        return SimpleCheckRecipeResult.ofFailure("no_hydrogen");
    if (getHeliumStored() < currentRecipe.getHeliumRequirement())
        return SimpleCheckRecipeResult.ofFailure("no_helium");
}
// 多并行：需要原始星尘物质（Stellar Plasma）
if (parallelAmount > 1) {
    if (getStellarPlasmaStored() < currentRecipe.getHeliumRequirement() * (12.4 / 1_000_000f) * parallelAmount)
        return SimpleCheckRecipeResult.ofFailure("no_stellar_plasma");
}
```

---

##### 3.4 时空外壳等级检查
```java
if (spacetimeCompressionFieldMetadata < recipeObject.getSpacetimeCasingTierRequired()) {
    return CheckRecipeResultRegistry.insufficientMachineTier(
        (int) recipeObject.getSpacetimeCasingTierRequired());
}
```

---

### 耗电机制（最核心部分）

EOH **不使用能量仓**，所有 EU 通过**无线网络**处理。

#### 耗电计算（line 1290-1318）

```java
// Calculate multipliers used in power calculations
double powerMultiplier = Math.max(1, GTUtility.powInt(POWER_INCREASE_CONSTANT, parallelExponent));

// Determine EU recipe input
startEU = recipeObject.getEUStartCost();

// Calculate normal EU values
double outputEUPenalty = (TOTAL_CASING_TIERS_WITH_POWER_PENALTY - stabilisationFieldMetadata)
    * STABILITY_INCREASE_PROBABILITY_DECREASE_YIELD_PER_TIER;
outputEU_BigInt = BigInteger.valueOf((long) (recipeObject.getEUOutput() * (1 - outputEUPenalty)));
usedEU = BigInteger.valueOf(-startEU)
    .multiply(BigInteger.valueOf((long) GTUtility.powInt(4, currentCircuitMultiplier)));

// Calculate parallel EU values
if (parallelAmount > 1) {
    outputEU_BigInt = outputEU_BigInt
        .multiply(BigInteger.valueOf((long) (powerMultiplier * PRECISION_MULTIPLIER)))
        .divide(BigInteger.valueOf((long) (PRECISION_MULTIPLIER * POWER_DIVISION_CONSTANT)));

    usedEU = usedEU
        .multiply(BigInteger.valueOf((long) (powerMultiplier * PARALLEL_MULTIPLIER_CONSTANT * PRECISION_MULTIPLIER)))
        .divide(BigInteger.valueOf((long) (PRECISION_MULTIPLIER * POWER_DIVISION_CONSTANT)));
}

// Remove EU from the users network.
if (!addEUToGlobalEnergyMap(userUUID, usedEU)) {
    return CheckRecipeResultRegistry.insufficientStartupPower(usedEU.abs());
}
```

**各常量含义**（均来自源文件 line 102-131）：
| 常量 | 值 | 含义 |
|------|----|------|
| `POWER_DIVISION_CONSTANT` | `20.7` | 并行时功率除数 |
| `POWER_INCREASE_CONSTANT` | `2.3` | 并行时功率增长底数 |
| `PARALLEL_MULTIPLIER_CONSTANT` | `1.63` | 并行 EU 输入额外倍数 |
| `TOTAL_CASING_TIERS_WITH_POWER_PENALTY` | `8` | 产电惩罚计算用的总层数 |
| `PRECISION_MULTIPLIER` | `1_000_000` | BigInteger 精度倍数 |

**功率计算公式总结**：
1. **基础 EU 输入**（启动成本）：`usedEU = -startEU × 4^currentCircuitMultiplier`（负数，从网络扣除）
2. **基础 EU 输出**：`outputEU = recipeEUOutput × (1 - (8 - stabilisationTier) × 0.05)`
3. **并行时 EU 输入**：`usedEU × powerMultiplier × 1.63 / 20.7`
4. **并行时 EU 输出**：`outputEU × powerMultiplier / 20.7`
5. **其中**：`powerMultiplier = max(1, 2.3^parallelExponent)`

#### 扣电（消耗无线网络 EU）
```java
// usedEU 是负数，调用 addEUToGlobalEnergyMap 向玩家无线网络添加负值 = 扣电
if (!addEUToGlobalEnergyMap(userUUID, usedEU)) {
    return CheckRecipeResultRegistry.insufficientStartupPower(usedEU.abs());
}
```

- `addEUToGlobalEnergyMap` 来自 `gregtech.common.misc.WirelessNetworkManager`
- `usedEU` 是 `BigInteger`（支持超大数值），且为**负数**
- 如果无线网络余额不足，返回 `insufficientStartupPower` 失败，**不开始配方**

---

### 配方完成后的产电（outputAfterRecipe_EM）

**代码**（line 1481-1511）：
```java
public void outputAfterRecipe_EM() {
    recipeRunning = false;
    eRequiredData = 0L;

    destroyRenderBlock();

    // Output EU
    addEUToGlobalEnergyMap(userUUID, outputEU_BigInt);

    startEU = 0;
    outputEU_BigInt = BigInteger.ZERO;

    outputFailedChance();

    if (successfulParallelAmount > 0) {
        for (ItemStackLong itemStack : outputItems) {
            outputItemToAENetwork(itemStack.itemStack, itemStack.stackSize);
        }
        for (FluidStackLong fluidStack : outputFluids) {
            outputFluidToAENetwork(fluidStack.fluidStack, fluidStack.amount);
        }
    }
    // ...
}
```

- 配方完成后，向无线网络注入 `outputEU_BigInt`（正数，充电）
- 所有物品/流体输出到 ME 输出总线/输出舱（通过 `ItemEjectionHelper`）

---

### 配方成功率系统

EOH 配方有成功概率机制（line 1332-1340）：

```java
// If pityChance needs to be reset, it will be set to Double.MIN_Value at the end of the recipe.
if (pityChance == Double.MIN_VALUE) {
    pityChance = currentRecipe.getBaseRecipeSuccessChance()
        - timeAccelerationFieldMetadata * TIME_ACCEL_DECREASE_CHANCE_PER_TIER
        + stabilisationFieldMetadata * STABILITY_INCREASE_PROBABILITY_DECREASE_YIELD_PER_TIER;
}
previousRecipeChance = successChance;
successChance = recipeChanceCalculator();
```

**pity 系统**（line 1428-1448）：
```java
private void outputFailedChance() {
    // ...
    if (parallelAmount == 1) {
        // Add chance to pity if previous recipe is equal to current one, else reset pity
        if (previousRecipeChance == successChance) {
            pityChance += (1 - successChance) * successChance;
        } else {
            pityChance = successChance;
        }
    }
    // ...
    } else if (parallelAmount == 1) {
        // Recipe succeeded, reset pity
        pityChance = Double.MIN_VALUE;
    }
}
```

- 配方失败时，下次成功概率增加（pity 机制），直到成功
- 多并行模式下不计算 pity

---

### 失败处理：时空物质输出

配方失败时输出熔融时空（Molten SpaceTime）（line 1428-1435）：
```java
private void outputFailedChance() {
    long failedParallelAmount = parallelAmount - successfulParallelAmount;
    if (failedParallelAmount > 0) {
        // 2^Tier spacetime released upon recipe failure.
        outputFluidToAENetwork(
            Materials.SpaceTime.getMolten(1),
            (long) ((successChance * MOLTEN_SPACETIME_PER_FAILURE_TIER
                * GTUtility.powInt(SPACETIME_FAILURE_BASE, currentRecipeRocketTier + 1)) * failedParallelAmount));
```

- `MOLTEN_SPACETIME_PER_FAILURE_TIER = 14_400`
- `SPACETIME_FAILURE_BASE = 2`（即 2^(火箭等级+1) 倍量）

---

### 渲染系统

配方运行时在机器后方 16 格处生成一个渲染方块（`BlockEOHRender`），模拟星体外观（line 1389-1421）：

```java
private void createRenderBlock(final EyeOfHarmonyRecipe currentRecipe) {
    // ...
    this.getBaseMetaTileEntity().getWorld()
        .setBlock((int)(x + xOffset), (int)(y + yOffset), (int)(z + zOffset),
            TTCasingsContainer.eyeOfHarmonyRenderBlock);
    TileEntityEyeOfHarmony rendererTileEntity = ...;
    rendererTileEntity.setTier(currentRecipe.getRocketTier());
    // Star is a larger size depending on the spacetime tier of the recipe.
    rendererTileEntity.setStarSize(0.4 + recipeSpacetimeTier / 8.0);
}
```

---

### 鸿蒙之眼工作流程总图

```
[每 tick]
  └─ onPreTick()
       ├─ tick==1: 获取 UUID, 注册无线网络
       └─ 每20tick(非运行时): drainFluidFromHatchesAndStoreInternally()
            └─ 存储 H₂、He、RawStarMatter 到内部 Map

[每60tick] checkProcessing_EM()
  ├─ 读取控制器槽位行星方块
  ├─ 查找配方 eyeOfHarmonyRecipeStorage.recipeLookUp(controllerStack)
  └─ processRecipe(currentRecipe)
       ├─ 读取电路编号 → currentCircuitMultiplier (OC次数)
       ├─ 读取/消耗 astralArrayFabricator → 计算 parallelAmount = 2^parallelExponent
       ├─ 检查流体存量 (H₂/He 或 RawStarMatter)
       ├─ 检查 spacetimeCompressionFieldMetadata >= recipe要求
       ├─ 计算 EU:
       │    usedEU = -startEU × 4^OC × (并行因子)  ← 负数
       │    outputEU = recipeOutput × (1 - 稳定惩罚) × (并行因子)
       ├─ addEUToGlobalEnergyMap(userUUID, usedEU) → 从无线网络扣电
       │    └─ 失败? → 返回 insufficientStartupPower
       ├─ 计算处理时间 recipeProcessTimeCalculator(...)
       ├─ 计算成功率和产出率
       ├─ createRenderBlock() → 在机器后16格生成星体
       └─ 返回 SUCCESSFUL

[配方运行中] mMaxProgresstime 倒计时

[配方完成] outputAfterRecipe_EM()
  ├─ destroyRenderBlock()
  ├─ addEUToGlobalEnergyMap(userUUID, outputEU_BigInt) → 向无线网络充电
  ├─ outputFailedChance():
  │    ├─ 输出熔融时空 (失败的并行份数)
  │    └─ 更新 pityChance
  └─ 输出物品/流体到 ME 输出总线/舱
```

---

## 附录：关键常量速查表（MTEEyeOfHarmony.java）

| 常量名 | 值 | 用途 |
|--------|----|----|
| `MOLTEN_SPACETIME_PER_FAILURE_TIER` | `14_400` | 每失败层级输出的熔融时空量 |
| `SPACETIME_FAILURE_BASE` | `2` | 失败时空输出底数 |
| `SPACETIME_CASING_DIFFERENCE_DISCOUNT_PERCENTAGE` | `0.03` | 时空外壳每超出要求1级的时间折扣 |
| `TIME_ACCEL_DECREASE_CHANCE_PER_TIER` | `0.0925` | 时间膨胀每级降低的成功率 |
| `STABILITY_INCREASE_PROBABILITY_DECREASE_YIELD_PER_TIER` | `0.05` | 稳定场每级提升成功率/降低产出 |
| `PARALLEL_FOR_FIRST_ASTRAL_ARRAY` | `8` | 第一个星列阵对应的并行基础值 |
| `CONSTANT_FOR_LOG` | `1.7` | 对数计算常量 |
| `PARALLEL_MULTIPLIER_CONSTANT` | `1.63` | 并行 EU 输入倍数 |
| `POWER_DIVISION_CONSTANT` | `20.7` | 并行功率除数 |
| `POWER_INCREASE_CONSTANT` | `2.3` | 并行功率增长底数 |
| `TOTAL_CASING_TIERS_WITH_POWER_PENALTY` | `8` | 计算产电惩罚的基准等级 |
| `ASTRAL_ARRAY_LIMIT` | `8637` | 星列阵最大数量（对应 2^21 并行） |
| `TICKS_BETWEEN_HATCH_DRAIN` | `20` | 每次从输入舱抽取流体的间隔 tick |
| `RECIPE_CHECK_INTERVAL` | `60` (3×20) | 每次检查配方的间隔 tick |

---

*本文档基于 GT5-Unofficial 真实源代码编写，所有代码均来自 `/src/main/java/` 目录下的实际 Java 源文件。*
