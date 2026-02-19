# GT5U翻译映射完整指南

**数据来源**: Translation-of-GTNH (https://github.com/Kiwi233/Translation-of-GTNH)  
**总翻译数**: 4621条  
**数据状态**: 100%真实，直接提取自lang文件

## 概述

本文档包含GT5-Unofficial所有子模块的中文翻译映射。所有翻译均从Translation-of-GTNH项目的lang文件中提取。

## 翻译模式分析

不同模块使用不同的命名模式：

### GREGTECH
发现的key前缀: GT5U, GTPP, GTPacketInfiniteSpraycan, achievement, channels, entity, fluid, for, gregtech, gt, gtpp, ic, item, itemGroup, key, mui, nei, tc, tile, tooltip

### BARTWORKS
发现的key前缀: BW, BW_GlasBlocks, BW_GlasBlocks2, BW_ItemBlocks, BW_Machinery_Casings, GT5U, GT_LESU_CASING, bw, chat, filled, gt, item, itemGroup, labModule, misc, moon, nei, planet, solarsystem, star, tile, tooltip

### MISCUTILS
发现的key前缀: tile

### TECTECH
发现的key前缀: item, tile

### KUBATECH
发现的key前缀: GT5U, KT, achievement, defc, item, kubablock, kubaitem, kubatech, tc

### GGFAB
发现的key前缀: ggfab

### GOODGENERATOR
发现的key前缀: CoolantTower, EssentiaOutputHatch, ExtremeHeatExchanger, FRF_Casing, FRF_Coil_1, FRF_Coil_2, FRF_Coil_3, FRF_Coil_4, FuelRefineFactory, GT5U, LargeEssentiaSmeltery, LargeFusion1, LargeFusion2, LargeFusion3, LargeFusion4, LargeFusion5, MAR_Casing, MultiNqGenerator, NeutronActivator, PreciseAssembler, UniversalChemicalFuelEngine, YOTTank, YOTTankCell, achievement, antimatterAnnihilationMatrix, antimatterContainmentCasing, batch_mode, compactFusionCoil, componentAssemblyLineCasing, crops, depletedfuelrod, enrichedNaquadahMass, essentiaCell, essentiaFilterCasing, essentiaOutputHatch, essentiaOutputHatch_ME, essentiaoutputhatch, fieldRestrictingGlass, fluid, fuelrod, fuelrodheat, gg, gravityStabilizationCasing, gt, gui, hatchTier, huiCircuit, impreciseUnitCasing, inverter, item, itemGroup, magicCasing, magneticFluxCasing, naquadahMass, naquadriaMass, preciseUnitCasing, preciseassembler, pressureResistantWalls, protomatterActivationCoil, radiationProtectionSteelFrame, rawCylinder, research, scanner, speedingPipe, supercriticalFluidTurbineCasing, tile, titaniumPlatedCylinder, value, yothatch, yottaFluidTankCasing, yottaFluidTankCell, yottank


## 如何使用本映射表

1. 找到你需要的模块章节
2. 在表格中搜索关键词
3. 使用Lang Key格式理解命名规则
4. 根据规则推断其他物品的翻译

## 按模块分类的完整翻译


### BARTWORKS (255条)


#### 前缀: `BW` (31条)

| Lang Key | 中文翻译 |
|----------|----------|
| `BW.NEI.display.radhatch.0` | 辐射剂量: %s Sv |
| `BW.NEI.display.radhatch.1` | 质量: %s kg |
| `BW.NEI.display.radhatch.2` | 时间: %s s |
| `BW.gui.text.lesu.amp_io` | A/t 输入/输出: %s |
| `BW.gui.text.lesu.eu` | EU： %s |
| `BW.gui.text.lesu.eu_out` | EU/t 输出：%s |
| `BW.gui.text.lesu.max` | 最大：%s |
| `BW.gui.text.lesu.max_in` | 最大EU/t输入：%s |
| `BW.gui.text.radio_hatch.tooltip.radiation_shutter` | 辐射闸门 |
| `BW.gui.text.radio_hatch.tooltip.radiation_shutter_control` | 辐射闸门控制 |
| `BW.infoData.BioVat.expectedProduction` | 预期产量 |
| `BW.infoData.BioVat.production` | 产量 |
| `BW.infoData.htgr.coolant` | 冷却液：%sL/s |
| `BW.infoData.htgr.fuel_amount` | 燃料数量：%s 个。 |
| `BW.infoData.htgr.fuel_type` | 燃料类型：%s |
| `BW.infoData.htgr.fuel_type.none` | 无 |
| `BW.infoData.htgr.fuel_type.triso` | TRISO (%s) |
| `BW.infoData.htgr.mode` | 模式：%s |
| `BW.infoData.htgr.mode.emptying` | 清空 |
| `BW.infoData.htgr.mode.normal` | 正常 |
| `BW.infoData.htgr.progress` | 进度：%ss / %ss |
| `BW.infoData.htr.helium_level` | 氦水平：%sL / %sL |
| `BW.infoData.htr.problems` | 问题：%s |
| `BW.infoData.mega_vacuum_freezer.subspace_cooling.active` | 亚空间冷却：§a激活中（%s） |
| `BW.infoData.mega_vacuum_freezer.subspace_cooling.inactive` | 亚空间冷却：§c未激活 |
| `BW.infoData.mega_vacuum_freezer.tier` | 等级: %d |
| `BW.infoData.thtr.coolant` | 冷却液/t: %s升/t |
| `BW.infoData.thtr.progress` | 进度：%ss/%ss |
| `BW.infoData.thtr.triso_pebbles` | TRISO燃料丸：%s个 / %s个 |
| `BW.infoData.wind_mill.grind_power` | 研磨功率：%dKU/t |

*...还有 1 条翻译*

#### 前缀: `BW_GlasBlocks` (17条)

| Lang Key | 中文翻译 |
|----------|----------|
| `BW_GlasBlocks.0.name` | 硼玻璃方块 |
| `BW_GlasBlocks.1.name` | 钛强化硼玻璃方块 |
| `BW_GlasBlocks.10.name` | 染色硼玻璃方块(淡绿) |
| `BW_GlasBlocks.11.name` | 染色硼玻璃方块(棕) |
| `BW_GlasBlocks.12.name` | 钍钇玻璃方块 |
| `BW_GlasBlocks.13.name` | 中子强化硼玻璃方块 |
| `BW_GlasBlocks.14.name` | 宇宙中子强化硼玻璃方块 |
| `BW_GlasBlocks.15.name` | 无尽强化硼玻璃方块 |
| `BW_GlasBlocks.2.name` | 钨钢强化硼玻璃方块 |
| `BW_GlasBlocks.3.name` | 镀铑钯强化硼玻璃方块 |
| `BW_GlasBlocks.4.name` | 铱强化硼玻璃方块 |
| `BW_GlasBlocks.5.name` | 锇强化硼玻璃方块 |
| `BW_GlasBlocks.6.name` | 染色硼玻璃方块(红) |
| `BW_GlasBlocks.7.name` | 染色硼玻璃方块(绿) |
| `BW_GlasBlocks.8.name` | 染色硼玻璃方块(紫) |
| `BW_GlasBlocks.9.name` | 染色硼玻璃方块(黄) |
| `BW_GlasBlocks.name` | 硼玻璃方块 |

#### 前缀: `BW_GlasBlocks2` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `BW_GlasBlocks2.0.name` | 超时空强化硼玻璃方块 |
| `BW_GlasBlocks2.name` | 硼玻璃方块 |

#### 前缀: `BW_ItemBlocks` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `BW_ItemBlocks.0.name` | 刻蚀青金石单元 |
| `BW_ItemBlocks.1.name` | 镀层青金石单元 |
| `BW_ItemBlocks.name` | 刻蚀青金石单元 |

#### 前缀: `BW_Machinery_Casings` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `BW_Machinery_Casings.0.name` | 镍锌铁氧体块 |
| `BW_Machinery_Casings.1.name` | 变压器绕组方块 |
| `BW_Machinery_Casings.name` | 机械方块 |

#### 前缀: `GT5U` (36条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GT5U.gui.config.general.crossmodinteractions` | 模组兼容 |
| `GT5U.gui.config.general.mixins` | Mixins |
| `GT5U.gui.config.general.multiblocks` | 多方块 |
| `GT5U.gui.config.general.pollution` | 污染 |
| `GT5U.gui.config.general.rossruinmetas` | Ross128B's Ruins MetaIDs |
| `GT5U.gui.config.general.rossruinmetas.ev` | EV |
| `GT5U.gui.config.general.rossruinmetas.ev.buffers` | 缓存 |
| `GT5U.gui.config.general.rossruinmetas.ev.cables` | 线缆 |
| `GT5U.gui.config.general.rossruinmetas.ev.generators` | 发电机 |
| `GT5U.gui.config.general.rossruinmetas.ev.machines` | 机器 |
| `GT5U.gui.config.general.rossruinmetas.highpressuresteam` | 高压蒸汽 |
| `GT5U.gui.config.general.rossruinmetas.highpressuresteam.buffers` | 缓存 |
| `GT5U.gui.config.general.rossruinmetas.highpressuresteam.cables` | 线缆 |
| `GT5U.gui.config.general.rossruinmetas.highpressuresteam.generators` | 发电机 |
| `GT5U.gui.config.general.rossruinmetas.highpressuresteam.machines` | 机器 |
| `GT5U.gui.config.general.rossruinmetas.hv` | HV |
| `GT5U.gui.config.general.rossruinmetas.hv.buffers` | 缓存 |
| `GT5U.gui.config.general.rossruinmetas.hv.cables` | 线缆 |
| `GT5U.gui.config.general.rossruinmetas.hv.generators` | 发电机 |
| `GT5U.gui.config.general.rossruinmetas.hv.machines` | 机器 |
| `GT5U.gui.config.general.rossruinmetas.lv` | LV |
| `GT5U.gui.config.general.rossruinmetas.lv.buffers` | 缓存 |
| `GT5U.gui.config.general.rossruinmetas.lv.cables` | 线缆 |
| `GT5U.gui.config.general.rossruinmetas.lv.generators` | 发电机 |
| `GT5U.gui.config.general.rossruinmetas.lv.machines` | 机器 |
| `GT5U.gui.config.general.rossruinmetas.mv` | MV |
| `GT5U.gui.config.general.rossruinmetas.mv.buffers` | 缓存 |
| `GT5U.gui.config.general.rossruinmetas.mv.cables` | 线缆 |
| `GT5U.gui.config.general.rossruinmetas.mv.generators` | 发电机 |
| `GT5U.gui.config.general.rossruinmetas.mv.machines` | 机器 |

*...还有 6 条翻译*

#### 前缀: `GT_LESU_CASING` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GT_LESU_CASING.0.name` | LESU机械方块 |
| `GT_LESU_CASING.name` | LESU机械方块 |

#### 前缀: `bw` (11条)

| Lang Key | 中文翻译 |
|----------|----------|
| `bw.blockores.01.name` | 矿石 |
| `bw.blockores.02.name` | 贫瘠矿石 |
| `bw.fuels.acidgens` | 酸性发电机 |
| `bw.recipe.BacteriaVat` | 细菌培养缸 |
| `bw.recipe.biolab` | 生物实验室 |
| `bw.recipe.cal` | 电路装配线 |
| `bw.recipe.htgr` | 高温气冷反应堆 |
| `bw.recipe.radhatch` | 放射仓材料列表 |
| `bw.werkstoffblocks.01.name` | 方块 |
| `bw.werkstoffblockscasing.01.name` | 螺栓机械方块 |
| `bw.werkstoffblockscasingadvanced.01.name` | 强化机械方块 |

#### 前缀: `chat` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `chat.cal.mode.0` | 电路装配线模式 |
| `chat.cal.mode.1` | 电路组装机模式 |

#### 前缀: `filled` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `filled.item.petriDish.name` | 培养皿 |

#### 前缀: `gt` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gt.blockmachines.creativeScanner.desc.1` | 立刻结束扫描。无需能量。 |
| `gt.recipe.electricimplosioncompressor` | 电动聚爆压缩机 |

#### 前缀: `item` (34条)

| Lang Key | 中文翻译 |
|----------|----------|
| `item.Agarose.name` | 琼脂糖 |
| `item.BISOPelletBall.name` | BISO燃料球 |
| `item.BISOPelletCompound.name` | BISO复合材料 |
| `item.BW_CombinedRotor.name` | 原始复合转子(风车专用) |
| `item.BW_LeatherRotor.name` | 原始皮革转子(风车专用) |
| `item.BW_PaperRotor.name` | 原始纸转子(风车专用) |
| `item.BW_SimpleWindMeter.name` | 简易风速计 |
| `item.BW_WoolRotor.name` | 原始羊毛转子(风车专用) |
| `item.BWmotor.name` | 简易斯特林马达 |
| `item.BWrawtube.name` | 加长玻璃管 |
| `item.BWstove.name` | 简易熔炉 |
| `item.BurnedOutTRISOPellet.name` | 枯竭TRISO燃料丸 |
| `item.BurnedOutTRISOPelletBall.name` | 枯竭TRISO燃料球 |
| `item.Cells.name` | 细菌细胞 |
| `item.DNASampleFlask.name` | DNA样品瓶 |
| `item.DetergentPowder.name` | 洗涤粉 |
| `item.GT_Rockcutter_Item_HV.name` | 岩石切割机HV |
| `item.GT_Rockcutter_Item_LV.name` | 岩石切割机LV |
| `item.GT_Rockcutter_Item_MV.name` | 岩石切割机MV |
| `item.GT_Teslastaff_Item.name` | 特斯拉权杖 |
| `item.IncubationModule.name` | 孵化模块 |
| `item.PlasmaMembrane.name` | 质膜 |
| `item.PlasmidCell.name` | 质粒样品瓶 |
| `item.TRISOPellet.name` | TRISO燃料丸 |
| `item.TRISOPelletBall.name` | TRISO燃料球 |
| `item.TRISOPelletCompound.name` | TRISO复合材料 |
| `item.completed_grindstone.name` | 磨石 |
| `item.grindstone_bottom.name` | 磨石底部件 |
| `item.grindstone_top.name` | 磨石顶部件 |
| `item.petriDish.name` | 无菌培养皿 |

*...还有 4 条翻译*

#### 前缀: `itemGroup` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `itemGroup.BioTab` | BartWorks生物工程 |
| `itemGroup.GT2C` | GT2兼容 |
| `itemGroup.bartworks` | BartWorks跨时代 |
| `itemGroup.bartworksMetaMaterials` | BartWorks超材料 |
| `itemGroup.bw.MetaItems.0` | BartWorks电路板改革 |

#### 前缀: `labModule` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `labModule.item.ClonalCellularSynthesisModule.name` | 细胞克隆模块 |
| `labModule.item.DNAExtractionModule.name` | DNA提取模块 |
| `labModule.item.PCRThermoclyclingModule.name` | 基因扩增模块 |
| `labModule.item.PlasmidSynthesisModule.name` | 质粒合成模块 |
| `labModule.item.TransformationModule.name` | 基因转化模块 |

#### 前缀: `misc` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `misc.BatchModeTextOff` | 关闭批量处理 |
| `misc.BatchModeTextOn` | 开启批量处理 |

#### 前缀: `moon` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `moon.Ross128ba` | 罗斯128ba |

#### 前缀: `nei` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `nei.biovat.0.name` | 需要玻璃等级: %s |
| `nei.biovat.1.name` | 精确剂量: %s Sv |
| `nei.biovat.2.name` | 最小剂量 %s Sv |
| `nei.biovat.input.tooltip` | 基于输出率，消耗至多1001倍的NEI流体原料 |
| `nei.biovat.output.tooltip` | 基于输出仓中的流体储量，输出至多1001倍的NEI流体产物 |

#### 前缀: `planet` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `planet.Ross128b` | 罗斯128b |

#### 前缀: `solarsystem` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `solarsystem.Ross128System` | 罗斯128星系 |

#### 前缀: `star` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `star.Ross128` | 罗斯128 |

#### 前缀: `tile` (15条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tile.BWHeatedWaterPump.0.name` | 简易斯特林水泵 |
| `tile.BWHeatedWaterPump.name` | 简易斯特林水泵 |
| `tile.BWRotorBlock.0.name` | 原始动力轴箱 |
| `tile.BWRotorBlock.name` | 原始动力轴箱 |
| `tile.BioFluidBlock.name` | 生物流质方块 |
| `tile.acidgenerator.name` | 酸性发电机 |
| `tile.biolab.name` | 生物实验室 |
| `tile.biovat.name` | 细菌培养缸 |
| `tile.bw.mbf.name` | 巨型工业高炉 |
| `tile.bw.mvf.name` | 巨型真空冷冻机 |
| `tile.bw.windmill.name` | 风车 |
| `tile.diode.name` | 线缆二极管 |
| `tile.energydistributor.name` | 能量分配器 |
| `tile.manutrafo.name` | 可调变压器 |
| `tile.radiohatch.name` | 放射仓 |

#### 前缀: `tooltip` (75条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tooltip.LESU.0.name` | 最大容量! |
| `tooltip.LESU.1.name` | 多个控制器! |
| `tooltip.bw.0.name` | 添加者: |
| `tooltip.bw.1.name` | 添加者：bartimaeusnek,模组： |
| `tooltip.bw.empty.name` | 空 |
| `tooltip.bw.high_temp_gas_cooled_reactor.material` | 供高温气冷反应堆使用 |
| `tooltip.bw.item.circuit.imprint` | 一个压印电路 |
| `tooltip.bw.item.circuit.sliced` | 一个切片电路 |
| `tooltip.bw.item.circuit.tagged` | 电路 |
| `tooltip.bw.item.circuit.tagged.imprint` | 一个压印%s |
| `tooltip.bw.item.circuit.tagged.sliced` | 一个切片%s |
| `tooltip.bw.mb_via.name` | %s§7 via §2BartWorks |
| `tooltip.bw.no.name` | 否 |
| `tooltip.bw.structure.glass` | 玻璃 |
| `tooltip.bw.structure.radio_hatch` | 放射仓 |
| `tooltip.bw.structure.tier_glass` | %s+玻璃 |
| `tooltip.bw.tier.name` | 等级: |
| `tooltip.bw.yes.name` | 是 |
| `tooltip.cal.imprintedWith` | 已压印： |
| `tooltip.cp.0.name` | 内部是否有编程电路? |
| `tooltip.glass_tier.0.name` | 玻璃等级: |
| `tooltip.labmodule.0.name` | 用于改变生物实验室工作模式的模块 |
| `tooltip.labparts.0.name` | 一个空的无菌培养皿 |
| `tooltip.labparts.1.name` | 一个空的DNA样品瓶 |
| `tooltip.labparts.2.name` | 一个空的质粒样品瓶 |
| `tooltip.labparts.3.name` | 生物工程专用洗涤粉 |
| `tooltip.labparts.4.name` | 用于辅助电泳分离DNA的粉末 |
| `tooltip.labparts.5.name` | 一个培养皿,内含: |
| `tooltip.labparts.6.name` | 这是一种很弱的培养菌,不能在细菌培养缸中繁殖! |
| `tooltip.labparts.7.name` | 一个DNA样品瓶,内含: |

*...还有 45 条翻译*

### GGFAB (30条)


#### 前缀: `ggfab` (30条)

| Lang Key | 中文翻译 |
|----------|----------|
| `ggfab.gui.advassline.shutdown` | §4上次异常关机原因： |
| `ggfab.gui.advassline.shutdown.energy` | §4功率不足 |
| `ggfab.gui.advassline.shutdown.fluid_null` | §4流体获取失败（检查你的ME流体存储） |
| `ggfab.gui.advassline.shutdown.input_busses` | §4输入总线数量过少，无法支持当前配方 |
| `ggfab.gui.advassline.shutdown.load.energy` | §4载入了无效的电力信息 |
| `ggfab.gui.advassline.shutdown.load.recipe` | §4不兼容的配方切换 |
| `ggfab.gui.advassline.shutdown.recipe_null` | §4配方为 null （报告给作者） |
| `ggfab.gui.advassline.shutdown.structure` | §4不兼容的结构变化 |
| `ggfab.gui.advassline.shutdown_clear` | §6清除 |
| `ggfab.gui.advassline.slice.idle` | 片#%s：待机 |
| `ggfab.gui.advassline.slice.stuck` | 片#%s：§4堵塞 |
| `ggfab.gui.advassline.slice.unknown` | 片#%s：? |
| `ggfab.gui.linked_input_bus.channel` | 频道 |
| `ggfab.gui.linked_input_bus.private` | 私人 |
| `ggfab.info.biome` | 生物群系： |
| `ggfab.info.linked_input_bus.data_copied` | §2已复制频道 ("%s§2") 与编程电路设置! |
| `ggfab.info.linked_input_bus.data_pasted` | §2已粘贴频道 ("%s§2") 与编程电路设置! |
| `ggfab.info.linked_input_bus.invalid_circuit` | §6配置数据存在但包含对这个总线无效的电路板! |
| `ggfab.info.linked_input_bus.invalid_data` | §6配置数据存在但已失效! |
| `ggfab.info.linked_input_bus.no_channel` | §6尚未指定频道! |
| `ggfab.info.linked_input_bus.no_data` | §6找不到配置数据! |
| `ggfab.info.linked_input_bus.not_owned` | §6该配置是从其他所有者处复制的! |
| `ggfab.recipe.toolcast` | 工具铸造机 |
| `ggfab.tooltip.linked_input_bus.change_freq_warn` | 修改一个频道上最后一个总线的频道，将导致剩余物品全部掉出来! |
| `ggfab.tooltip.linked_input_bus.private` | 私人频道不与他人共享. |
| `ggfab.tooltip.linked_input_bus.private.1` | 修改一个频道上最后一个总线的频道，将导致剩余物品全部掉出来! |
| `ggfab.waila.advassline.slice` | 片#%s：%s s / %s s |
| `ggfab.waila.advassline.slice.idle` | 片#%s：待机 |
| `ggfab.waila.advassline.slice.small` | 片#%s：%s t / %s t |
| `ggfab.waila.advassline.slice.stuck` | 片#%s：§4堵塞 |

### GOODGENERATOR (520条)


#### 前缀: `CoolantTower` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `CoolantTower.hint.0` | 任意GT混凝土 |
| `CoolantTower.hint.1` | 28x碳化钨框架 |
| `CoolantTower.hint.2` | 1 - 输入仓/输出仓 |

#### 前缀: `EssentiaOutputHatch` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `EssentiaOutputHatch.tooltip.0` | 空手Shift+右键以清空容器. |
| `EssentiaOutputHatch.tooltip.1` | 容量： |

#### 前缀: `ExtremeHeatExchanger` (6条)

| Lang Key | 中文翻译 |
|----------|----------|
| `ExtremeHeatExchanger.hint.0` | 25x强化钨钢机械方块(至少！) |
| `ExtremeHeatExchanger.hint.1` | 1 - 输入仓(蒸馏水) |
| `ExtremeHeatExchanger.hint.2` | 2 - 输出仓(超临界蒸汽/过热蒸汽/蒸汽) |
| `ExtremeHeatExchanger.hint.3` | 3 - 输入仓(热流体) |
| `ExtremeHeatExchanger.hint.4` | 4 - 输出仓(冷流体) |
| `ExtremeHeatExchanger.hint.5` | 任意机械方块 - 维护仓 |

#### 前缀: `FRF_Casing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FRF_Casing.0.name` | 硅岩燃料精炼机械方块 |
| `FRF_Casing.name` | 硅岩燃料精炼机械方块 |

#### 前缀: `FRF_Coil_1` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FRF_Coil_1.0.name` | 力场约束线圈 |
| `FRF_Coil_1.name` | 力场约束线圈 |

#### 前缀: `FRF_Coil_2` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FRF_Coil_2.0.name` | 进阶力场约束线圈 |
| `FRF_Coil_2.name` | 进阶力场约束线圈 |

#### 前缀: `FRF_Coil_3` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FRF_Coil_3.0.name` | 终极力场约束线圈 |
| `FRF_Coil_3.name` | 终极力场约束线圈 |

#### 前缀: `FRF_Coil_4` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FRF_Coil_4.0.name` | 时空力场约束线圈 |
| `FRF_Coil_4.name` | 时空力场约束线圈 |

#### 前缀: `FuelRefineFactory` (8条)

| Lang Key | 中文翻译 |
|----------|----------|
| `FuelRefineFactory.hint.0` | 8x力场约束玻璃 |
| `FuelRefineFactory.hint.1` | 32x力场约束线圈(任意等级) |
| `FuelRefineFactory.hint.2` | 104x硅岩燃料精炼机械方块(至少！) |
| `FuelRefineFactory.hint.3` | 1~16x输入仓 |
| `FuelRefineFactory.hint.4` | 1~16x输出仓 |
| `FuelRefineFactory.hint.5` | 1~16x输入总线 |
| `FuelRefineFactory.hint.6` | 1~16x能源仓 |
| `FuelRefineFactory.hint.7` | 所有仓室必须与力场约束玻璃相邻 |

#### 前缀: `GT5U` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GT5U.gui.text.node_too_small` | §7节点过小 |

#### 前缀: `LargeEssentiaSmeltery` (8条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeEssentiaSmeltery.hint.0` | 24x魔法机械方块(至少！) |
| `LargeEssentiaSmeltery.hint.1` | 12x源质扩散单元(至少！) |
| `LargeEssentiaSmeltery.hint.2` | 3x高级炼金炉(至少！) |
| `LargeEssentiaSmeltery.hint.3` | 3x源质过滤机械方块(至少！) |
| `LargeEssentiaSmeltery.hint.4` | 0 - 空气 |
| `LargeEssentiaSmeltery.hint.5` | 1 - 基础仓室/魔法机械方块 |
| `LargeEssentiaSmeltery.hint.6` | 2 - 消声仓 |
| `LargeEssentiaSmeltery.hint.7` | 支持TecTech能源仓. |

#### 前缀: `LargeFusion1` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeFusion1.hint.0` | 1666xLuV机械方块(至少！) |
| `LargeFusion1.hint.1` | 63x 镀铑钯强化硼玻璃方块(LuV)（至少！) |
| `LargeFusion1.hint.2` | 558x改良型超导线圈方块 |
| `LargeFusion1.hint.3` | 128x硅岩合金框架 |
| `LargeFusion1.hint.4` | 1 - 输入仓 |
| `LargeFusion1.hint.5` | 1 - 输出仓 |
| `LargeFusion1.hint.6` | 2 - 能源仓 |
| `LargeFusion1.hint.7` | 所有仓室必须为LuV以上 |
| `LargeFusion1.hint.8` | 支持TecTech能源仓. |

#### 前缀: `LargeFusion2` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeFusion2.hint.0` | 1666x聚变机械方块(至少！) |
| `LargeFusion2.hint.1` | 63x铱强化硼玻璃方块(至少！) |
| `LargeFusion2.hint.2` | 558x压缩聚变线圈方块 |
| `LargeFusion2.hint.3` | 128x铿铀框架 |
| `LargeFusion2.hint.4` | 1 - 输入仓 |
| `LargeFusion2.hint.5` | 1 - 输出仓 |
| `LargeFusion2.hint.6` | 2 - 能源仓 |
| `LargeFusion2.hint.7` | 所有仓室必须为ZPM以上 |
| `LargeFusion2.hint.8` | 支持TecTech能源仓. |

#### 前缀: `LargeFusion3` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeFusion3.hint.0` | 1666x聚变机械方块MK II(至少！) |
| `LargeFusion3.hint.1` | 63x锇强化硼玻璃方块(至少！) |
| `LargeFusion3.hint.2` | 558x进阶压缩聚变线圈方块 |
| `LargeFusion3.hint.3` | 128x中子框架 |
| `LargeFusion3.hint.4` | 1 - 输入仓 |
| `LargeFusion3.hint.5` | 1 - 输出仓 |
| `LargeFusion3.hint.6` | 2 - 能源仓 |
| `LargeFusion3.hint.7` | 所有仓室必须为UV以上 |
| `LargeFusion3.hint.8` | 支持TecTech能源仓. |

#### 前缀: `LargeFusion4` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeFusion4.hint.0` | 1666x聚变机械方块MK III(至少！) |
| `LargeFusion4.hint.1` | 63x 中子强化硼玻璃方块(UHV)（至少！) |
| `LargeFusion4.hint.2` | 558x压缩聚变线圈方块MK-II原型 |
| `LargeFusion4.hint.3` | 128x无尽催化剂框架 |
| `LargeFusion4.hint.4` | 1 - 输入仓 |
| `LargeFusion4.hint.5` | 1 - 输出仓 |
| `LargeFusion4.hint.6` | 2 - 能源仓 |
| `LargeFusion4.hint.7` | 所有仓室必须为UHV以上 |
| `LargeFusion4.hint.8` | 支持TecTech能源仓. |

#### 前缀: `LargeFusion5` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `LargeFusion5.hint.0` | 1666x聚变机械方块MK IV(至少！) |
| `LargeFusion5.hint.1` | 63x 宇宙中子强化硼玻璃方块(UEV)（至少！) |
| `LargeFusion5.hint.2` | 558x压缩聚变线圈方块MK-II |
| `LargeFusion5.hint.3` | 128x无尽框架 |
| `LargeFusion5.hint.4` | 1 - 输入仓 |
| `LargeFusion5.hint.5` | 1 - 输出仓 |
| `LargeFusion5.hint.6` | 2 - 能源仓 |
| `LargeFusion5.hint.7` | 所有仓室必须为UEV以上 |
| `LargeFusion5.hint.8` | 支持TecTech能源仓. |

#### 前缀: `MAR_Casing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `MAR_Casing.0.name` | 力场约束机械方块 |
| `MAR_Casing.name` | 力场约束机械方块 |

#### 前缀: `MultiNqGenerator` (8条)

| Lang Key | 中文翻译 |
|----------|----------|
| `MultiNqGenerator.hint.0` | 6x钨钢管道方块 |
| `MultiNqGenerator.hint.1` | 48x力场约束机械方块 |
| `MultiNqGenerator.hint.2` | 36x防辐射钢框架 |
| `MultiNqGenerator.hint.3` | 77x防辐射机械方块(至少！) |
| `MultiNqGenerator.hint.4` | 1~4x输入仓 |
| `MultiNqGenerator.hint.5` | 0~1x输出仓 |
| `MultiNqGenerator.hint.6` | 1x维护仓 |
| `MultiNqGenerator.hint.7` | 1x动力仓 |

#### 前缀: `NeutronActivator` (7条)

| Lang Key | 中文翻译 |
|----------|----------|
| `NeutronActivator.hint.0` | 16x钢框架 |
| `NeutronActivator.hint.1` | 18x处理器机械方块 |
| `NeutronActivator.hint.2` | 4 x高速管道方块 |
| `NeutronActivator.hint.3` | 7 x洁净不锈钢机械方块(至少！) |
| `NeutronActivator.hint.4` | 1 - 输入仓/输入总线/洁净不锈钢机械方块 |
| `NeutronActivator.hint.5` | 2 - 输出仓/输出总线/维护仓/中子加速器/中子传感器/洁净不锈钢机械方块 |
| `NeutronActivator.hint.6` | 3 - EV+玻璃 |

#### 前缀: `PreciseAssembler` (7条)

| Lang Key | 中文翻译 |
|----------|----------|
| `PreciseAssembler.hint.0` | 42x精密电子单元机械方块(至少！) |
| `PreciseAssembler.hint.1` | 12x钨钢框架 |
| `PreciseAssembler.hint.2` | 42x防爆玻璃 |
| `PreciseAssembler.hint.3` | 21x机械方块(不是机器外壳!) |
| `PreciseAssembler.hint.4` | 1 - 输入仓/输入总线/输出总线/精密电子单元机械方块 |
| `PreciseAssembler.hint.5` | 2 - EV+玻璃 |
| `PreciseAssembler.hint.6` | 支持TecTech能源仓! |

#### 前缀: `UniversalChemicalFuelEngine` (11条)

| Lang Key | 中文翻译 |
|----------|----------|
| `UniversalChemicalFuelEngine.hint.0` | 93x加强钛机械方块 |
| `UniversalChemicalFuelEngine.hint.1` | 14x钛管道方块 |
| `UniversalChemicalFuelEngine.hint.10` | 支持TecTech动力仓/激光仓 |
| `UniversalChemicalFuelEngine.hint.2` | 14x钛齿轮箱机械方块 |
| `UniversalChemicalFuelEngine.hint.3` | 14x镀钛气缸 |
| `UniversalChemicalFuelEngine.hint.4` | 14x引擎进气机械方块 |
| `UniversalChemicalFuelEngine.hint.5` | 0 - 空气 |
| `UniversalChemicalFuelEngine.hint.6` | 1 - 维护仓 |
| `UniversalChemicalFuelEngine.hint.7` | 2 - 消声仓 |
| `UniversalChemicalFuelEngine.hint.8` | 3 - 输入仓 |
| `UniversalChemicalFuelEngine.hint.9` | 4 - 动力仓 |

#### 前缀: `YOTTank` (8条)

| Lang Key | 中文翻译 |
|----------|----------|
| `YOTTank.hint.0` | 47xYOT机械方块(至少！) |
| `YOTTank.hint.1` | 16x钢框架 |
| `YOTTank.hint.2` | 16x 相同等级玻璃 (每层) |
| `YOTTank.hint.3` | 9x流体单元方块(每层) |
| `YOTTank.hint.4` | 1 - 输入仓/YOT机械方块 |
| `YOTTank.hint.5` | 2 - 维护仓/YOT机械方块 |
| `YOTTank.hint.6` | 3 - 输出仓/YOT仓/YOT机械方块 |
| `YOTTank.hint.7` | 每台YOT储罐只接受一个YOT仓. |

#### 前缀: `YOTTankCell` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `YOTTankCell.tooltip.0` | 容量： |
| `YOTTankCell.tooltip.1` | 用于YOT储罐的流体单元 |

#### 前缀: `achievement` (52条)

| Lang Key | 中文翻译 |
|----------|----------|
| `achievement.FRF_Casing.0` | 硅岩燃料精炼机械方块 |
| `achievement.FRF_Casing.0.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.FRF_Coil_1.0` | 力场约束线圈 |
| `achievement.FRF_Coil_1.0.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.FRF_Coil_2.0` | 进阶力场约束线圈 |
| `achievement.FRF_Coil_2.0.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.FRF_Coil_3.0` | 终极力场约束线圈 |
| `achievement.FRF_Coil_3.0.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.FRF_Coil_4.0` | 时空力场约束线圈 |
| `achievement.FRF_Coil_4.0.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.frf` | 硅岩燃料精炼厂 |
| `achievement.gt.blockmachines.frf.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.largefusioncomputer2` | 聚变不嫌多 |
| `achievement.gt.blockmachines.largefusioncomputer2.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.largefusioncomputer3` | PROJECT MOISS |
| `achievement.gt.blockmachines.largefusioncomputer3.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.largefusioncomputer4` | イワシがつちからはえてくるんだ |
| `achievement.gt.blockmachines.largefusioncomputer4.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.largefusioncomputer5` | XXXX |
| `achievement.gt.blockmachines.largefusioncomputer5.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.nag` | 大型硅岩反应堆 |
| `achievement.gt.blockmachines.nag.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.gt.blockmachines.neutron_accelerator_luv` | Luv中子加速器 |
| `achievement.gt.blockmachines.neutron_accelerator_luv.desc` | 你真的想要它吗? |
| `achievement.item.advancedRadiationProtectionPlate` | 进阶防辐射板 |
| `achievement.item.advancedRadiationProtectionPlate.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.item.fluidCore.1` | 流体存储核心T2 |
| `achievement.item.fluidCore.1.desc` | 捡起此物品以在NEI内解锁该合成表 |
| `achievement.item.fluidCore.2` | 流体存储核心T3 |
| `achievement.item.fluidCore.2.desc` | 捡起此物品以在NEI内解锁该合成表 |

*...还有 22 条翻译*

#### 前缀: `antimatterAnnihilationMatrix` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `antimatterAnnihilationMatrix.0.name` | 反物质湮灭矩阵 |
| `antimatterAnnihilationMatrix.name` | 反物质湮灭矩阵 |

#### 前缀: `antimatterContainmentCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `antimatterContainmentCasing.0.name` | 反物质隔离机械方块 |
| `antimatterContainmentCasing.name` | 反物质隔离机械方块 |

#### 前缀: `batch_mode` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `batch_mode.cfgi.0` | 批处理大小 |

#### 前缀: `compactFusionCoil` (6条)

| Lang Key | 中文翻译 |
|----------|----------|
| `compactFusionCoil.0.name` | 改良型超导线圈方块 |
| `compactFusionCoil.1.name` | 压缩聚变线圈方块 |
| `compactFusionCoil.2.name` | 进阶压缩聚变线圈方块 |
| `compactFusionCoil.3.name` | 压缩聚变线圈方块MK-II原型 |
| `compactFusionCoil.4.name` | 压缩聚变线圈方块MK-II |
| `compactFusionCoil.name` | 压缩聚变线圈方块 |

#### 前缀: `componentAssemblyLineCasing` (15条)

| Lang Key | 中文翻译 |
|----------|----------|
| `componentAssemblyLineCasing.0.name` | 部件装配线外壳(LV) |
| `componentAssemblyLineCasing.1.name` | 部件装配线外壳(MV) |
| `componentAssemblyLineCasing.10.name` | 部件装配线外壳(UIV) |
| `componentAssemblyLineCasing.11.name` | 部件装配线外壳(UMV) |
| `componentAssemblyLineCasing.12.name` | 部件装配线外壳(UXV) |
| `componentAssemblyLineCasing.13.name` | 部件装配线外壳(MAX) |
| `componentAssemblyLineCasing.2.name` | 部件装配线外壳(HV) |
| `componentAssemblyLineCasing.3.name` | 部件装配线外壳(EV) |
| `componentAssemblyLineCasing.4.name` | 部件装配线外壳(IV) |
| `componentAssemblyLineCasing.5.name` | 部件装配线外壳(LuV) |
| `componentAssemblyLineCasing.6.name` | 部件装配线外壳(ZPM) |
| `componentAssemblyLineCasing.7.name` | 部件装配线外壳(UV) |
| `componentAssemblyLineCasing.8.name` | 部件装配线外壳(UHV) |
| `componentAssemblyLineCasing.9.name` | 部件装配线外壳(UEV) |
| `componentAssemblyLineCasing.name` | 部件装配线外壳 |

#### 前缀: `crops` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `crops.saltroot` | 盐根 |

#### 前缀: `depletedfuelrod` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `depletedfuelrod.tooltip.0` | 枯竭 |

#### 前缀: `enrichedNaquadahMass` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `enrichedNaquadahMass.tooltip.0` | 一种强烈的满足感. |

#### 前缀: `essentiaCell` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `essentiaCell.0.name` | 新手源质扩散单元 |
| `essentiaCell.1.name` | 学徒源质扩散单元 |
| `essentiaCell.2.name` | 大师源质扩散单元 |
| `essentiaCell.3.name` | 宗师源质扩散单元 |
| `essentiaCell.name` | 源质扩散单元 |

#### 前缀: `essentiaFilterCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `essentiaFilterCasing.0.name` | 源质过滤机械方块 |
| `essentiaFilterCasing.name` | 源质过滤机械方块 |

#### 前缀: `essentiaOutputHatch` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `essentiaOutputHatch.0.name` | 源质输出仓 |
| `essentiaOutputHatch.name` | 源质输出仓 |

#### 前缀: `essentiaOutputHatch_ME` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `essentiaOutputHatch_ME.0.name` | 源质输出仓(ME) |
| `essentiaOutputHatch_ME.name` | 源质输出仓(ME) |

#### 前缀: `essentiaoutputhatch` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `essentiaoutputhatch.chat.0` | 已清空. |

#### 前缀: `fieldRestrictingGlass` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `fieldRestrictingGlass.0.name` | 力场约束玻璃 |
| `fieldRestrictingGlass.name` | 力场约束玻璃 |

#### 前缀: `fluid` (76条)

| Lang Key | 中文翻译 |
|----------|----------|
| `fluid.2-Ethyl-1-Hexanol` | 2-乙基己醇 |
| `fluid.Acid Naquadah Emulsion` | 酸性硅岩乳液 |
| `fluid.Antimony Pentachloride` | 五氯化锑 |
| `fluid.Antimony Pentachloride Solution` | 五氯化锑溶液 |
| `fluid.Antimony Pentafluoride` | 五氟化锑 |
| `fluid.Antimony Trichloride Solution` | 三氯化锑溶液 |
| `fluid.Cyclopentadiene` | 环戊二烯 |
| `fluid.Diethylamine` | 二乙胺 |
| `fluid.Enriched Naquadah Goo` | 富集硅岩黏浆 |
| `fluid.Enriched-Naquadah-Rich Solution` | 高纯富集硅岩溶液 |
| `fluid.Ethanol Gasoline` | 乙醇汽油 |
| `fluid.Ether` | 乙醚 |
| `fluid.Ferrocene Solution` | 二茂铁溶液 |
| `fluid.Ferrocene Waste` | 二茂铁废水 |
| `fluid.Fluorine-Rich Waste Liquid` | 富氟废液 |
| `fluid.Fluoroantimonic Acid` | 氟锑酸 |
| `fluid.Heavy Naquadah Fuel` | 重质硅岩燃料 |
| `fluid.Impure Ferrocene Mixture` | 含杂二茂铁混合物 |
| `fluid.Iron II Chloride` | 氯化亚铁 |
| `fluid.Jet Fuel A` | 航空煤油A |
| `fluid.Jet Fuel No.3` | 航空煤油#3 |
| `fluid.Light Naquadah Fuel` | 轻质硅岩燃料 |
| `fluid.Low Quality Naquadah Emulsion` | 低纯硅岩乳液 |
| `fluid.Low Quality Naquadah Solution` | 低纯硅岩溶液 |
| `fluid.Low Quality Naquadria Sulphate` | 低纯硫酸超能硅岩 |
| `fluid.Naquadah Asphalt` | 硅岩沥青 |
| `fluid.Naquadah Based Liquid Fuel MkI` | 硅岩基流体燃料-MkI |
| `fluid.Naquadah Based Liquid Fuel MkI (Depleted)` | 硅岩基流体燃料-MkI(枯竭的) |
| `fluid.Naquadah Based Liquid Fuel MkII` | 硅岩基流体燃料-MkII |
| `fluid.Naquadah Based Liquid Fuel MkII (Depleted)` | 硅岩基流体燃料-MkII(枯竭的) |

*...还有 46 条翻译*

#### 前缀: `fuelrod` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `fuelrod.tooltip.0` | 耐久：%s/%s |

#### 前缀: `fuelrodheat` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `fuelrodheat.tooltip.0` | 具有与铀相同的发热量 |
| `fuelrodheat.tooltip.1` | 发热量是铀的%s倍 |
| `fuelrodheat.tooltip.2` | 具有MOX特性 |

#### 前缀: `gg` (23条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gg.gui.text.large_essentia_smeltery.requires` | 需要总计%s的§bAqua§f与§cIgnis§f才能运作。 |
| `gg.recipe.componentassemblyline` | 部件装配线 |
| `gg.recipe.extreme_heat_exchanger` | 超级热交换机 |
| `gg.recipe.naquadah_fuel_refine_factory` | 硅岩燃料精炼厂 |
| `gg.recipe.naquadah_reactor` | 大型硅岩反应堆 |
| `gg.recipe.neutron_activator` | 中子活化器 |
| `gg.recipe.precise_assembler` | 精密组装机 |
| `gg.scanner.info.antimatter_forge` | 反物质熔炉 |
| `gg.scanner.info.antimatter_generator` | 反物质发电机 |
| `gg.scanner.info.fusion_reactor_mk` | 聚变反应堆 MK |
| `gg.scanner.info.generator.efficiency` | 效率： |
| `gg.scanner.info.generator.generates` | 当前发电：%s EU/t |
| `gg.scanner.info.generator.problems` | 问题： |
| `gg.scanner.info.les.node_power` | 节点能量： |
| `gg.scanner.info.les.parallel` | 并行： |
| `gg.scanner.info.les.purification_efficiency` | 净化效率： |
| `gg.scanner.info.les.speed_up` | 加速： |
| `gg.scanner.info.neutron_activator.input` | 当前中子动能输入：%sev |
| `gg.scanner.info.neutron_activator.progress` | 进度：%s s / %s s |
| `gg.structure.tooltip.antimatter_hatch` | 反物质仓 |
| `gg.structure.tooltip.input_hatch` | 输入仓 |
| `gg.structure.tooltip.laser_source_hatch` | 激光源仓 |
| `gg.structure.tooltip.output_hatch` | 输出仓 |

#### 前缀: `gravityStabilizationCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gravityStabilizationCasing.0.name` | 重力稳定机械方块 |
| `gravityStabilizationCasing.name` | 重力稳定机械方块 |

#### 前缀: `gt` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gt.blockmachines.YottaFluidTank.cfgi.0` | 更新速度(每x个tick更新一次I/O) |

#### 前缀: `gui` (21条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gui.AntimatterForge.0` | 反物质存量 |
| `gui.AntimatterForge.1` | 被动电力消耗 |
| `gui.AntimatterForge.2` | 主动电力消耗 |
| `gui.AntimatterForge.3` | 反物质变化量 |
| `gui.AntimatterGenerator.0` | 已生产的EU |
| `gui.AntimatterGenerator.1` | 效率 |
| `gui.LargeFusion.0` | 能量容量： |
| `gui.LargeFusion.1` | 储存能量： |
| `gui.NeutronActivator.0` | 当前中子动能： |
| `gui.NeutronActivator.1` | 输入： |
| `gui.NeutronSensor.0` | 输入中子动能值. |
| `gui.NeutronSensor.1` | 例如 >5000KeV，<=30MeV…… |
| `gui.NeutronSensor.2` | 有效 |
| `gui.NeutronSensor.3` | 无效 |
| `gui.NeutronSensor.4` | eV阈值 |
| `gui.YOTTank.0` | 容量： |
| `gui.YOTTank.1` | 流体： |
| `gui.YOTTank.2` | 已存储： |
| `gui.YOTTank.3` | 锁定为: |
| `gui.YOTTank.button.locking` | 锁定流体 |
| `gui.YOTTank.button.void` | 溢出销毁 |

#### 前缀: `hatchTier` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `hatchTier.tooltip.0` | 仓室等级： |

#### 前缀: `huiCircuit` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `huiCircuit.tooltip.0` | §b93015-T浮点运算/秒§r |
| `huiCircuit.tooltip.1` | §e76M处理单元§r |
| `huiCircuit.tooltip.2` | §a无效RSA算法§r |
| `huiCircuit.tooltip.3` | §c第56梅森素数§r |
| `huiCircuit.tooltip.4` | §5佯谬§r |

#### 前缀: `impreciseUnitCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `impreciseUnitCasing.0.name` | 不精密的电子单元机械方块 |
| `impreciseUnitCasing.name` | 不精密的电子单元机械方块 |

#### 前缀: `inverter` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `inverter.tooltip.0` | 将直流电转化为交流电. |

#### 前缀: `item` (65条)

| Lang Key | 中文翻译 |
|----------|----------|
| `item.advancedFuelRod.name` | 高级燃料棒(空) |
| `item.advancedRadiationProtectionPlate.name` | 进阶防辐射板 |
| `item.aluminumNitride.name` | 氮化铝粉 |
| `item.chromaticGem.name` | 彩色宝石 |
| `item.circuitWrap.0.name` | 封装ULV电路板 |
| `item.circuitWrap.1.name` | 封装LV电路板 |
| `item.circuitWrap.10.name` | 封装UEV电路板 |
| `item.circuitWrap.11.name` | 封装UIV电路板 |
| `item.circuitWrap.12.name` | 封装UMV电路板 |
| `item.circuitWrap.13.name` | 封装UXV电路板 |
| `item.circuitWrap.14.name` | 封装MAX电路板 |
| `item.circuitWrap.2.name` | 封装MV电路板 |
| `item.circuitWrap.3.name` | 封装HV电路板 |
| `item.circuitWrap.4.name` | 封装EV电路板 |
| `item.circuitWrap.5.name` | 封装IV电路板 |
| `item.circuitWrap.6.name` | 封装LuV电路板 |
| `item.circuitWrap.7.name` | 封装ZPM电路板 |
| `item.circuitWrap.8.name` | 封装UV电路板 |
| `item.circuitWrap.9.name` | 封装UHV电路板 |
| `item.circuitWrap.name` | 封装电路板 |
| `item.enrichedNaquadahMass.name` | 富集硅岩团 |
| `item.fluidCore.0.name` | 流体存储核心T1 |
| `item.fluidCore.1.name` | 流体存储核心T2 |
| `item.fluidCore.2.name` | 流体存储核心T3 |
| `item.fluidCore.3.name` | 流体存储核心T4 |
| `item.fluidCore.4.name` | 流体存储核心T5 |
| `item.fluidCore.5.name` | 流体存储核心T6 |
| `item.fluidCore.6.name` | 流体存储核心T7 |
| `item.fluidCore.7.name` | 流体存储核心T8 |
| `item.fluidCore.8.name` | 流体存储核心T9 |

*...还有 35 条翻译*

#### 前缀: `itemGroup` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `itemGroup.Good Generator` | 更多发电机 |
| `itemGroup.Nuclear Items` | [GG]多方块核反应堆 |

#### 前缀: `magicCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `magicCasing.0.name` | 魔法机械方块 |
| `magicCasing.name` | 魔法机械方块 |

#### 前缀: `magneticFluxCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `magneticFluxCasing.0.name` | 磁通量机械方块 |
| `magneticFluxCasing.name` | 磁通量机械方块 |

#### 前缀: `naquadahMass` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `naquadahMass.tooltip.0` | 远不够纯. |

#### 前缀: `naquadriaMass` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `naquadriaMass.tooltip.0` | 什么? |

#### 前缀: `preciseUnitCasing` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `preciseUnitCasing.0.name` | 精密电子单元机械方块 MK-I |
| `preciseUnitCasing.1.name` | 精密电子单元机械方块 MK-II |
| `preciseUnitCasing.2.name` | 精密电子单元机械方块 MK-III |
| `preciseUnitCasing.3.name` | 精密电子单元机械方块 MK-IV |
| `preciseUnitCasing.name` | 精密电子单元机械方块 |

#### 前缀: `preciseassembler` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `preciseassembler.chat.0` | 精密模式 |
| `preciseassembler.chat.1` | 常规模式 |

#### 前缀: `pressureResistantWalls` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `pressureResistantWalls.0.name` | 耐压墙 |
| `pressureResistantWalls.name` | 耐压墙 |

#### 前缀: `protomatterActivationCoil` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `protomatterActivationCoil.0.name` | 元始物质活化线圈 |
| `protomatterActivationCoil.name` | 元始物质活化线圈 |

#### 前缀: `radiationProtectionSteelFrame` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `radiationProtectionSteelFrame.0.name` | 防辐射钢框架 |
| `radiationProtectionSteelFrame.name` | 防辐射钢框架 |

#### 前缀: `rawCylinder` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `rawCylinder.0.name` | 粗制气缸 |
| `rawCylinder.name` | 粗制气缸 |

#### 前缀: `research` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `research.ESSENTIA_CELL.page.0` | 新手源质扩散单元的效率实在太低,你完全不能忍受. 所以你研发了一些新的源质扩散单元<BR><BR>新手源质扩散单元只提供1稳定点,学徒级的单元可以提供2稳定点,大师级的单元可以提供5稳定点,而宗师级的单元可以提供足足10稳定点!<BR><BR>随着稳定点越高,每点源质在发电机中产生的能量就越多.<BR><BR>同时也可以解锁更好的仓室. |
| `research.ESSENTIA_OUTPUT_HATCH_ME.page.0` | 总有一天你会用到它...<BR><BR>请务必连接网络使用,它没有缓存！ |
| `research.ESSENTIA_SMELTERY.page.0` | 荒古炼金炉已经不足以支撑你的源质生产了...<BR><BR>大型源质冶炼厂(LES)是荒古炼金炉的进阶版,消耗EU和Centivis,用以冶炼源质. |
| `research.ESSENTIA_SMELTERY.page.1` | Ignis与Aqua是LES运行的基本条件,最低需求约为最高能源仓等级^2*1.15CV/每次工作,满足后机器才能运行.<BR><BR>Ordo影响污染、咒波瓦斯生成概率(冶炼源质时随机在消声仓仓口排出咒波瓦斯).<BR><BR>Perditio可以加速机器工作,最高200%(100CV/5t). |
| `research.ESSENTIA_SMELTERY.page.2` | 扩散单元等级及结构大小仅影响机器并行,最大并行为64x.<BR><BR>不含源质的物品会冶炼出1点perditio. |

#### 前缀: `scanner` (14条)

| Lang Key | 中文翻译 |
|----------|----------|
| `scanner.info.CASS.tier` | 外壳等级： |
| `scanner.info.CASS.tier.none` | 无！ |
| `scanner.info.FRF` | 线圈等级： |
| `scanner.info.NA` | 当前中子动能： |
| `scanner.info.UX.0` | 并行运行： |
| `scanner.info.XHE.0` | 输出蒸汽量： |
| `scanner.info.XHE.1` | 超临界阈值： |
| `scanner.info.YOTTank.0` | 当前容量： |
| `scanner.info.YOTTank.1` | 流体名： |
| `scanner.info.YOTTank.2` | 当前已用： |
| `scanner.info.YOTTank.3` | 锁定为: |
| `scanner.info.YOTTank.empty` | 空 |
| `scanner.info.YOTTank.next` | 无. 将锁定为进入容器的下一种流体 |
| `scanner.info.YOTTank.none` | 无 |

#### 前缀: `speedingPipe` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `speedingPipe.0.name` | 高速管道方块 |
| `speedingPipe.name` | 高速管道方块 |

#### 前缀: `supercriticalFluidTurbineCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `supercriticalFluidTurbineCasing.0.name` | 超临界蒸汽涡轮机械方块 |
| `supercriticalFluidTurbineCasing.name` | 超临界蒸汽涡轮机械方块 |

#### 前缀: `tile` (16条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tile.coalTar.name` | 煤焦 |
| `tile.combustionPromotor.name` | 助燃剂 |
| `tile.gg.antimatterRender.name` | 反物质渲染 |
| `tile.heavilyCrackedHeavyNaquadahFuel.name` | 重度裂化重质硅岩燃料 |
| `tile.heavilyCrackedLightNaquadahFuel.name` | 重度裂化轻质硅岩燃料 |
| `tile.heavilyCrackedNaquadahAsphalt.name` | 重度裂化硅岩沥青 |
| `tile.heavilyCrackedNaquadahGas.name` | 重度裂化硅岩气 |
| `tile.lightlyCrackedHeavyNaquadahFuel.name` | 轻度裂化重质硅岩燃料 |
| `tile.lightlyCrackedLightNaquadahFuel.name` | 轻度裂化轻质硅岩燃料 |
| `tile.lightlyCrackedNaquadahAsphalt.name` | 轻度裂化硅岩沥青 |
| `tile.lightlyCrackedNaquadahGas.name` | 轻度裂化硅岩气 |
| `tile.moderatelyCrackedHeavyNaquadahFuel.name` | 中度裂化重质硅岩燃料 |
| `tile.moderatelyCrackedLightNaquadahFuel.name` | 中度裂化轻质硅岩燃料 |
| `tile.moderatelyCrackedNaquadahAsphalt.name` | 中度裂化硅岩沥青 |
| `tile.moderatelyCrackedNaquadahGas.name` | 中度裂化硅岩气 |
| `tile.supercriticalSteam.name` | 超临界蒸汽 |

#### 前缀: `titaniumPlatedCylinder` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `titaniumPlatedCylinder.0.name` | 镀钛气缸 |
| `titaniumPlatedCylinder.name` | 镀钛气缸 |

#### 前缀: `value` (10条)

| Lang Key | 中文翻译 |
|----------|----------|
| `value.component_assembly_line` | 外壳等级: %s |
| `value.extreme_heat_exchanger.0` | 最大热流体输入： |
| `value.extreme_heat_exchanger.1` | 最大蒸馏水输入: |
| `value.extreme_heat_exchanger.4` | 阈值： |
| `value.naquadah_fuel_refine_factory` | 需要 %s 级线圈 |
| `value.naquadah_reactor` | 基础输出电压: %s EU/t |
| `value.neutron_activator.0` | 最低中子动能： |
| `value.neutron_activator.1` | 最高中子动能： |
| `value.neutron_activator.2` | MeV |
| `value.precise_assembler` | 需要MK-%s机械方块 |

#### 前缀: `yothatch` (4条)

| Lang Key | 中文翻译 |
|----------|----------|
| `yothatch.chat.0` | 存储优先级设为 %s. |
| `yothatch.chat.1` | 设置为 %s 模式 |
| `yothatch.chat.2` | 启用黏滞模式 |
| `yothatch.chat.3` | 禁用黏滞模式 |

#### 前缀: `yottaFluidTankCasing` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `yottaFluidTankCasing.0.name` | YOT机械方块 |
| `yottaFluidTankCasing.name` | YOT机械方块 |

#### 前缀: `yottaFluidTankCell` (11条)

| Lang Key | 中文翻译 |
|----------|----------|
| `yottaFluidTankCell.0.name` | 流体单元方块T1 |
| `yottaFluidTankCell.1.name` | 流体单元方块T2 |
| `yottaFluidTankCell.2.name` | 流体单元方块T3 |
| `yottaFluidTankCell.3.name` | 流体单元方块T4 |
| `yottaFluidTankCell.4.name` | 流体单元方块T5 |
| `yottaFluidTankCell.5.name` | 流体单元方块T6 |
| `yottaFluidTankCell.6.name` | 流体单元方块T7 |
| `yottaFluidTankCell.7.name` | 流体单元方块T8 |
| `yottaFluidTankCell.8.name` | 流体单元方块T9 |
| `yottaFluidTankCell.9.name` | 流体单元方块T10 |
| `yottaFluidTankCell.name` | 流体单元方块 |

#### 前缀: `yottank` (5条)

| Lang Key | 中文翻译 |
|----------|----------|
| `yottank.chat.0` | 流体锁定已清除 |
| `yottank.chat.1` | 锁定为 %s |
| `yottank.chat.2` | 将锁定为进入容器的下一种流体 |
| `yottank.chat.voidExcessDisabled` | 启用溢出停机 |
| `yottank.chat.voidExcessEnabled` | 禁用溢出停机 |

### GREGTECH (3590条)


#### 前缀: `GT5U` (1217条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GT5U.BLACKHOLE.mode.0` | 压缩机 |
| `GT5U.BLACKHOLE.mode.1` | 奇点压缩机 |
| `GT5U.DEHP.mode.0` | 直出蒸汽 |
| `GT5U.DEHP.mode.1` | 加热冷却液 |
| `GT5U.DTPF.catalystinfotooltip` | 为不消耗催化剂的配方指定额外消耗的催化剂等级,粗制为1级，恒星为5级 |
| `GT5U.DTPF.catalysttier` | 催化剂等级 |
| `GT5U.DTPF.convergencebutton` | 允许维度收敛 |
| `GT5U.DTPF.convergencebuttontooltip.0` | 需要在控制器的插槽中放入超维校准矩阵 |
| `GT5U.DTPF.convergencebuttontooltip.1` | 右键打开催化剂选择菜单 |
| `GT5U.EBF.heat` | 热容 |
| `GT5U.GTPP_MULTI_ADV_DISTILLATION_TOWER.mode.0` | 蒸馏塔 |
| `GT5U.GTPP_MULTI_ADV_DISTILLATION_TOWER.mode.1` | 蒸馏室 |
| `GT5U.GTPP_MULTI_ARC_FURNACE.mode.0` | 电力电弧炉 |
| `GT5U.GTPP_MULTI_ARC_FURNACE.mode.1` | 等离子电弧炉 |
| `GT5U.GTPP_MULTI_CUTTING_MACHINE.mode.0` | 切割机 |
| `GT5U.GTPP_MULTI_CUTTING_MACHINE.mode.1` | 切片机 |
| `GT5U.GTPP_MULTI_INDUSTRIAL_DEHYDRATOR.mode.0` | 真空干燥炉 |
| `GT5U.GTPP_MULTI_INDUSTRIAL_DEHYDRATOR.mode.1` | 脱水机 |
| `GT5U.GTPP_MULTI_INDUSTRIAL_PLATE_PRESS.mode.0` | 卷板机 |
| `GT5U.GTPP_MULTI_INDUSTRIAL_PLATE_PRESS.mode.1` | 冲压机床 |
| `GT5U.GTPP_MULTI_MASS_FABRICATOR.mode.0` | 质量发生器 |
| `GT5U.GTPP_MULTI_MASS_FABRICATOR.mode.1` | 回收机 |
| `GT5U.GTPP_MULTI_PACKAGER.mode.0` | 打包机 |
| `GT5U.GTPP_MULTI_PACKAGER.mode.1` | 解包器 |
| `GT5U.GTPP_MULTI_PRECISE_ASSEMBLER.mode.0` | 精密模式 |
| `GT5U.GTPP_MULTI_PRECISE_ASSEMBLER.mode.1` | 常规模式 |
| `GT5U.GTPP_MULTI_WASH_PLANT.mode.0` | 洗矿机 |
| `GT5U.GTPP_MULTI_WASH_PLANT.mode.1` | 简易洗矿池 |
| `GT5U.GTPP_MULTI_WASH_PLANT.mode.2` | 化学浸洗机 |
| `GT5U.INDUSTRIAL_ELECTROMAGNETIC_SEPARATOR.mode.0` | 电磁离析机 |

*...还有 1187 条翻译*

#### 前缀: `GTPP` (125条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GTPP.CC.discount` | EU损耗 |
| `GTPP.CC.machinetier` | 控制核心等级 |
| `GTPP.CC.parallel` | 最大并行 |
| `GTPP.EBF.heat` | 热容 |
| `GTPP.MBTT.SteamHatch` | 蒸汽仓 |
| `GTPP.MBTT.SteamInputBus` | 输入总线(蒸汽) |
| `GTPP.MBTT.SteamOutputBus` | 输出总线(蒸汽) |
| `GTPP.algae.brown_algae.name` | 褐藻 |
| `GTPP.algae.euglenoids.name` | 裸藻 |
| `GTPP.algae.fire_algae.name` | 火藻 |
| `GTPP.algae.golden-brown_algae.name` | 金褐藻 |
| `GTPP.algae.green_algae.name` | 绿藻 |
| `GTPP.algae.red_algae.name` | 红藻 |
| `GTPP.algae.tooltip.fresh_water` | 淡水：%s |
| `GTPP.algae.tooltip.generation` | 产生：%d |
| `GTPP.algae.tooltip.growth` | 生长：%d |
| `GTPP.algae.tooltip.lifespan` | 寿命：%d天 |
| `GTPP.algae.tooltip.production` | 生产进度：%d |
| `GTPP.algae.tooltip.requires_light` | 需要光照：%s |
| `GTPP.algae.tooltip.salt_water` | 盐水：%s |
| `GTPP.algae.tooltip.temp_tolerance` | 温度耐受：%d |
| `GTPP.algae.yellow-green_algae.name` | 黄藻 |
| `GTPP.battpack.tooltip.1` | 在Baubles的腰带栏内使用 |
| `GTPP.battpack.tooltip.2` | 消耗 |
| `GTPP.battpack.tooltip.3` | 给穿着的盔甲充能 |
| `GTPP.battpack.tooltip.4` | 同样给快捷栏内的物品充能 |
| `GTPP.chat.text.cover_overflow_valve_overflow_point` | 溢流点：%d升 |
| `GTPP.container.decaychest.name` | 可衰变 |
| `GTPP.gui.text.cover_overflow_valve_allow_fluid_input` | §8允许流体输入 |
| `GTPP.gui.text.cover_overflow_valve_allow_fluid_output` | §8允许流体输出 |

*...还有 95 条翻译*

#### 前缀: `GTPacketInfiniteSpraycan` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GTPacketInfiniteSpraycan.Action.TOGGLE_SHAKE_LOCK` | 无限喷漆罐：锁定颜色循环 |

#### 前缀: `achievement` (911条)

| Lang Key | 中文翻译 |
|----------|----------|
| `achievement.MU-metaitem.01.32066` | 质子遏制 |
| `achievement.MU-metaitem.01.32066.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32068` | 电子遏制 |
| `achievement.MU-metaitem.01.32068.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32070` | 夸克遏制 |
| `achievement.MU-metaitem.01.32070.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32106` | 初级物理学家 |
| `achievement.MU-metaitem.01.32106.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32107` | 研究生物理学家 |
| `achievement.MU-metaitem.01.32107.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32108` | 学术物理学家 |
| `achievement.MU-metaitem.01.32108.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32109` | 物理学硕士 |
| `achievement.MU-metaitem.01.32109.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.MU-metaitem.01.32110` | 引力遏制 |
| `achievement.MU-metaitem.01.32110.desc` | [AL]捡起此物品以在NEI内解锁该合成表 |
| `achievement.advancedsteam` | 替代蒸汽选项 |
| `achievement.advancedsteam.desc` | 智能油耗 |
| `achievement.advancing` | 超前 |
| `achievement.advancing.desc` | 制作铕 |
| `achievement.alienmetallurgy` | 异星冶金学 |
| `achievement.alienmetallurgy.desc` | 拾取一个硅岩合金锭 |
| `achievement.alienpower` | 外星能量 |
| `achievement.alienpower.desc` | 制造一台硅岩反应堆Mk.I |
| `achievement.alloysmelter` | 合金熔炼 |
| `achievement.alloysmelter.desc` | 制造一台蒸汽合金炉 |
| `achievement.amplifier` | 增幅器 |
| `achievement.amplifier.desc` | 制造一台UU增幅液产生器 |
| `achievement.antimatterAnnihilationMatrix.0` | 反物质湮灭矩阵 |
| `achievement.antimatterAnnihilationMatrix.0.desc` | 捡起此物品以在NEI内解锁该合成表 |

*...还有 881 条翻译*

#### 前缀: `channels` (20条)

| Lang Key | 中文翻译 |
|----------|----------|
| `channels.gregtech.antenna` | 决定天线机械方块等级。最低为§6T1§r等级1，最高为§6T2§r等级2。 |
| `channels.gregtech.capacitor` | 决定兰博顿电容等级。最低为§6空电容§r等级1，最高为§6终极电容UMV§r等级10。 |
| `channels.gregtech.casing` | 决定金属机械方块等级。 |
| `channels.gregtech.cell` | 决定钒氧化还原能量单元等级。最低为§6EV§r等级1，最高为§6UHV§r等级6。 |
| `channels.gregtech.coil` | 决定线圈方块等级。最低为§6白铜线圈§r等级1，最高为§6永恒线圈§r等级14。 |
| `channels.gregtech.field` | 决定T.F.F.T.储库方块等级。 |
| `channels.gregtech.glass` | 决定玻璃的等级。玻璃等级繁多，且不同等级各有多种可替代玻璃方块。具体请参考各个玻璃方块的物品描述 |
| `channels.gregtech.gt_no_hatch` | 当设置时，禁用自动放置仓室 |
| `channels.gregtech.height` | 决定可重复片的高度。其有效范围根据多方块结构不同而有所差异。 |
| `channels.gregtech.item_pipe` | 决定物品管道方块等级。最低为§6锡物品管道方块§r等级1，最高为§6黑钚物品管道方块§r等级8。 |
| `channels.gregtech.length` | 决定可重复片的宽度。其有效范围根据多方块结构不同而有所差异。 |
| `channels.gregtech.machine_casing` | 决定机械方块等级。最低为§6ULV机械方块§r等级1，最高为§6UHV机械方块§r等级10。 |
| `channels.gregtech.manipulator` | 决定量子操纵者的脉冲控制方块等级。最低为§6中子脉冲控制方块§r等级1，最高为§6时空连续体撕裂方块§r等级4。 |
| `channels.gregtech.pipe` | 决定管道方块等级。最低为§6青铜管道方块§r等级1，最高为§6钨钢管道方块§r等级4。 |
| `channels.gregtech.shielding` | 决定量子操纵者的屏蔽核心方块等级。最低为§6中子屏蔽核心方块§r等级1，最高为§6时时空扭曲核心方块§r等级4。 |
| `channels.gregtech.solenoid` | 决定螺线管超导线圈等级。最低为§6MV螺线管超导线圈§r等级1，最高为§6UMV螺线管超导线圈§r等级11。 |
| `channels.gregtech.spacetime_compression` | 决定压缩时空场发生器等级。最低为§6粗制压缩时空场发生器§r等级1，最高为§6鸿蒙压缩时空场发生器§r等级9。 |
| `channels.gregtech.stabilisation` | 决定稳定力场发生器等级。最低为§6粗制稳定力场发生器§r等级1，最高为§6鸿蒙稳定力场发生器§r等级9。 |
| `channels.gregtech.time_dilation` | 决定时间膨胀场发生器等级。最低为§6粗制时间膨胀场发生器§r等级1，最高为§6鸿蒙时间膨胀场发生器§r等级9。 |
| `channels.gregtech.unit_casing` | 决定电子单元机械方块等级。最低为§6不精密的电子单元机械方块§r等级1，最高为§6精密电子单元机械方块 MK-IV§r等级5。 |

#### 前缀: `entity` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `entity.gregtech.GT_Entity_Arrow.name` | GT箭头 |
| `entity.gregtech.PowderBarrelPrimed.name` | 点燃的火药桶 |

#### 前缀: `fluid` (80条)

| Lang Key | 中文翻译 |
|----------|----------|
| `fluid.2-tert-butyl-anthrahydroquinone` | 2-叔丁基蒽氢醌 |
| `fluid.2-tert-butyl-anthraquinone` | 2-叔丁基蒽醌 |
| `fluid.Acetylhydrazine` | 乙酰肼 |
| `fluid.Acidic Iridium Solution` | 酸性铱溶液 |
| `fluid.Acidic Osmium Solution` | 酸性锇溶液 |
| `fluid.Ammonia` | 氨气 |
| `fluid.Ammonia Boronfluoride Solution` | 氟化硼氨溶液 |
| `fluid.Ammonium Chloride` | 氯化铵 |
| `fluid.Ammonium Dinitramide` | 二硝酰胺铵 |
| `fluid.Ammonium N-nitrourethane` | N-硝氨基甲酸乙酯-铵 |
| `fluid.Aqua Regia` | 王水 |
| `fluid.Boron Trifluoride` | 三氟化硼 |
| `fluid.Calcium Chloride` | 氯化钙 |
| `fluid.CompressedNitrogen` | 压缩氮气 |
| `fluid.CompressedOxygen` | 压缩氧气 |
| `fluid.Concrete` | 混凝土 |
| `fluid.Dimethyl Sulfate` | 硫酸二甲酯 |
| `fluid.EnrichedBacterialSludge` | 放射性细菌污泥 |
| `fluid.EnzymesSollution` | 酶溶液 |
| `fluid.Ethyl Acetate` | 乙酸乙酯 |
| `fluid.Ethyl Carbamate` | 氨基甲酸乙酯 |
| `fluid.Ethyl Chloroformate` | 氯基甲酸乙酯 |
| `fluid.Ethyl Dinitrocarbamate` | 二硝氨基甲酸乙酯 |
| `fluid.Ethyl N-nitrocarbamate` | N-硝氨基甲酸乙酯 |
| `fluid.FermentedBacterialSludge` | 发酵的细菌污泥 |
| `fluid.FluorecentdDNA` | 荧光DNA |
| `fluid.Formaldehyde` | 甲醛 |
| `fluid.Formic Acid` | 甲酸 |
| `fluid.GelatinMixture` | 明胶混合物 |
| `fluid.Hot Ruthenium Tetroxide Solution` | 热四氧化钌溶液 |

*...还有 50 条翻译*

#### 前缀: `for` (158条)

| Lang Key | 中文翻译 |
|----------|----------|
| `for.bees.authority.machinist` | Aditya & Noila |
| `for.bees.species.acentauri` | 半人马α |
| `for.bees.species.aluminium` | 铝 |
| `for.bees.species.amber` | 琥珀 |
| `for.bees.species.americium` | 镅 |
| `for.bees.species.apatite` | 磷灰石 |
| `for.bees.species.arcaneshards` | 奥术碎片 |
| `for.bees.species.arsenic` | 砷 |
| `for.bees.species.ash` | 灰烬 |
| `for.bees.species.astralsilver` | 星辰银 |
| `for.bees.species.barnarda` | 巴纳德 |
| `for.bees.species.barnardac` | 巴纳德C |
| `for.bees.species.barnardae` | 巴纳德E |
| `for.bees.species.barnardaf` | 巴纳德F |
| `for.bees.species.bauxite` | 铝土 |
| `for.bees.species.blackplutonium` | 黑钚 |
| `for.bees.species.callisto` | 木卫四 |
| `for.bees.species.callistoice` | 木卫四冰 |
| `for.bees.species.centauri` | 半人马 |
| `for.bees.species.ceres` | 谷神星 |
| `for.bees.species.certus` | 赛特斯 |
| `for.bees.species.chrome` | 铬 |
| `for.bees.species.clay` | 黏土 |
| `for.bees.species.coal` | 煤 |
| `for.bees.species.conductiveiron` | 导电铁 |
| `for.bees.species.coolant` | 冷却液 |
| `for.bees.species.copper` | 铜 |
| `for.bees.species.cosmicneutronium` | 宇宙中子态素 |
| `for.bees.species.cryolite` | 冰晶石 |
| `for.bees.species.cryotheum` | 极寒之凛冰 |

*...还有 128 条翻译*

#### 前缀: `gregtech` (12条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gregtech.areaExploratory` | 探索 |
| `gregtech.areaLethargic` | 摸鱼 |
| `gregtech.effectMachineBoost` | 机器助推器 |
| `gregtech.effectTreetwister` | 树苗嬗变 |
| `gregtech.fertilityMultiply` | 繁殖 |
| `gregtech.fertilitySterile` | 不育 |
| `gregtech.floweringNaturalistic` | 顺其自然 |
| `gregtech.floweringNonpollinating` | 不授粉 |
| `gregtech.lifeBlink` | 瞬灭 |
| `gregtech.lifeEon` | 永生 |
| `gregtech.speedAccelerated` | 加速 |
| `gregtech.speedUnproductive` | 不生产 |

#### 前缀: `gt` (588条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gt.behaviour.paintspray.infinite.gui.header` | 选择一种颜色 |
| `gt.behaviour.paintspray.infinite.gui.lock_error` | §e喷漆罐已被§c锁定§e！§b潜行并鼠标中键单击以解锁。 |
| `gt.behaviour.paintspray.infinite.gui.shake_toggle` | 允许/禁止颜色切换 |
| `gt.behaviour.paintspray.infinite.gui.solvent` | 有机溶剂 |
| `gt.behaviour.paintspray.infinite.tooltip.gui` | 中键：打开颜色选择界面 |
| `gt.behaviour.paintspray.infinite.tooltip.infinite` | 无限使用 |
| `gt.behaviour.paintspray.infinite.tooltip.lock` | 潜行时中键单击：锁定或解锁喷漆罐 |
| `gt.behaviour.paintspray.infinite.tooltip.locked` | 已锁定 |
| `gt.behaviour.paintspray.infinite.tooltip.more_info` | 按住SHIFT查看详情 |
| `gt.behaviour.paintspray.infinite.tooltip.pick` | 中键单击方块：复制颜色至喷漆罐 |
| `gt.behaviour.paintspray.infinite.tooltip.prevent_shake` | %s-鼠标中键: 允许/阻止左键点击 |
| `gt.behaviour.paintspray.infinite.tooltip.preventing_shake` | 左键点击已禁用 |
| `gt.behaviour.paintspray.infinite.tooltip.switch` | 左键单击：切换颜色(潜行以反转切换方向) |
| `gt.behaviour.switch_mode.tooltip` | 按[%s]切换模式 |
| `gt.behaviour.trowel.tooltip1` | 右键随机放置一个物品栏中的方块 |
| `gt.behaviour.trowel.tooltip2` | §o“别忘了带上装饰铲！”§r -§cQuerns§r |
| `gt.blackholerenderer.name` | 黑洞渲染器 |
| `gt.block.longdistancepipe.name` | 长距离管道 |
| `gt.blockcasings.cyclotron_coils.name` | 螺线管超导线圈 |
| `gt.blockcasings.name` | 机械方块 |
| `gt.blockcasings10.name` | 机械方块 |
| `gt.blockcasings11.name` | 机械方块 |
| `gt.blockcasings2.name` | 机械方块 |
| `gt.blockcasings3.name` | 机械方块 |
| `gt.blockcasings4.name` | 机械方块 |
| `gt.blockcasings5.name` | 机械方块 |
| `gt.blockcasings6.name` | 机械方块 |
| `gt.blockcasings8.name` | 机械方块 |
| `gt.blockcasings9.name` | 机械方块 |
| `gt.blockcasingsNH.name` | 机械方块 |

*...还有 558 条翻译*

#### 前缀: `gtpp` (345条)

| Lang Key | 中文翻译 |
|----------|----------|
| `gtpp.material.AbyssalAlloy` | 深渊合金 |
| `gtpp.material.AceticAnhydride` | 乙酸酐 |
| `gtpp.material.AdvancedNitinol` | 高级镍钛诺 |
| `gtpp.material.AgarditeCd` | 钇砷铜矿(Cd) |
| `gtpp.material.AgarditeLa` | 钇砷铜矿(La) |
| `gtpp.material.AgarditeNd` | 钇砷铜矿(Nd) |
| `gtpp.material.AgarditeY` | 钇砷铜矿(Y) |
| `gtpp.material.Alburnite` | 硫碲金锗矿 |
| `gtpp.material.Almandine` | 铁铝榴石 |
| `gtpp.material.Alumina` | 氧化铝 |
| `gtpp.material.Aluminium` | 铝 |
| `gtpp.material.Americium` | 镅 |
| `gtpp.material.Ammonia` | 氨 |
| `gtpp.material.Ammonium` | 铵 |
| `gtpp.material.AmmoniumBifluoride` | 氟化氢铵 |
| `gtpp.material.AmmoniumNitrate` | 硝酸铵 |
| `gtpp.material.AmmoniumTetrafluoroberyllate` | 氟铍酸铵 |
| `gtpp.material.AncientGranite` | 远古花岗岩 |
| `gtpp.material.Antimony` | 锑 |
| `gtpp.material.Arcanite` | 奥金 |
| `gtpp.material.ArceusAlloy2B` | 阿尔宙斯合金2B |
| `gtpp.material.Argon` | 氩 |
| `gtpp.material.Arsenic` | 砷 |
| `gtpp.material.AstralTitanium` | 星体钛 |
| `gtpp.material.BabbitAlloy` | 巴氏合金 |
| `gtpp.material.BariteRa` | 重晶石(Ra) |
| `gtpp.material.Barium` | 钡 |
| `gtpp.material.Beryllium` | 铍 |
| `gtpp.material.BerylliumFluoride` | 氟化铍 |
| `gtpp.material.BerylliumHydroxide` | 氢氧化铍 |

*...还有 315 条翻译*

#### 前缀: `ic` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `ic.recipe.recycler` | 回收机 |
| `ic.recipe.recycler.description` | 压缩、焚烧、摧毁并过滤一切 |

#### 前缀: `item` (72条)

| Lang Key | 中文翻译 |
|----------|----------|
| `item.GT5U.infinite_spray_can.name.colored` | 无限喷漆罐%c%s%c |
| `item.GT5U.infinite_spray_can.name.solvent` | 无限喷漆罐%c溶剂%c |
| `item.GTPP.air_filter.name` | 空气滤网 |
| `item.GTPP.air_filter.name.t1` | 空气滤网 [一级] |
| `item.GTPP.air_filter.name.t2` | 空气滤网 [二级] |
| `item.GTPP.air_intake_hatch.name` | 进气仓 |
| `item.GTPP.catalyst_housing.name` | 催化剂仓 |
| `item.gt.advancedsensorcard.name` | 高级传感器卡片[GT] |
| `item.gt.comb.name` | 蜂窝 |
| `item.gt.depletedRodExcitedPlutonium.name` | 燃料棒（枯竭激发钚） |
| `item.gt.depletedRodExcitedPlutonium2.name` | 二联燃料棒（枯竭激发钚） |
| `item.gt.depletedRodExcitedPlutonium4.name` | 四联燃料棒（枯竭激发钚） |
| `item.gt.depletedRodExcitedUranium.name` | 燃料棒（枯竭激发铀） |
| `item.gt.depletedRodExcitedUranium2.name` | 二联燃料棒（枯竭激发铀） |
| `item.gt.depletedRodExcitedUranium4.name` | 四联燃料棒（枯竭激发铀） |
| `item.gt.depletedRodGlowstone.name` | 燃料棒（阳光化合物） |
| `item.gt.depletedRodHighDensityPlutonium.name` | 燃料棒（枯竭浓缩钚） |
| `item.gt.depletedRodHighDensityPlutonium2.name` | 二联燃料棒（枯竭浓缩钚） |
| `item.gt.depletedRodHighDensityPlutonium4.name` | 四联燃料棒（枯竭浓缩钚） |
| `item.gt.depletedRodHighDensityUranium.name` | 燃料棒（枯竭浓缩铀） |
| `item.gt.depletedRodHighDensityUranium2.name` | 二联燃料棒（枯竭浓缩铀） |
| `item.gt.depletedRodHighDensityUranium4.name` | 四联燃料棒（枯竭浓缩铀） |
| `item.gt.depletedRodLithium.name` | 燃料棒（氚） |
| `item.gt.depletedRodMOX.name` | 燃料棒（枯竭MOX） |
| `item.gt.depletedRodMOX2.name` | 二联燃料棒（枯竭MOX） |
| `item.gt.depletedRodMOX4.name` | 四联燃料棒（枯竭MOX） |
| `item.gt.depletedRodNaquadah.name` | 燃料棒（枯竭硅岩） |
| `item.gt.depletedRodNaquadah2.name` | 二联燃料棒（枯竭硅岩） |
| `item.gt.depletedRodNaquadah32.name` | “核心”（枯竭） |
| `item.gt.depletedRodNaquadah4.name` | 四联燃料棒（枯竭硅岩） |

*...还有 42 条翻译*

#### 前缀: `itemGroup` (10条)

| Lang Key | 中文翻译 |
|----------|----------|
| `itemGroup.GTtools` | GT预构工具 |
| `itemGroup.GregTech.GTPP_BLOCKS` | GT++方块 |
| `itemGroup.GregTech.GTPP_MACHINES` | GT++机器 |
| `itemGroup.GregTech.GTPP_MISC` | GT++杂项 |
| `itemGroup.GregTech.GTPP_OTHER` | GT++其他 |
| `itemGroup.GregTech.GTPP_OTHER_2` | GT++其他II |
| `itemGroup.GregTech.GTPP_TOOLS` | GT++工具 |
| `itemGroup.GregTech.Main` | 主体 |
| `itemGroup.GregTech.Materials` | 材料 |
| `itemGroup.GregTech.Ores` | 矿石 |

#### 前缀: `key` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `key.gt.tool_mode_switch` | 工具模式切换 |

#### 前缀: `mui` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `mui.button.close` | x |

#### 前缀: `nei` (16条)

| Lang Key | 中文翻译 |
|----------|----------|
| `nei.options.tools.dump.gt5u` | GT5u |
| `nei.options.tools.dump.gt5u.batch_mode` | 尚未支持批量处理模式的机器 |
| `nei.options.tools.dump.gt5u.batch_modes` | 尚未支持批量处理模式的机器 |
| `nei.options.tools.dump.gt5u.input_separation` | 不支持输入隔离 |
| `nei.options.tools.dump.gt5u.input_separations` | 不支持输入隔离 |
| `nei.options.tools.dump.gt5u.material` | Material |
| `nei.options.tools.dump.gt5u.materials` | 材料 |
| `nei.options.tools.dump.gt5u.metatileentity` | 元方块实体 |
| `nei.options.tools.dump.gt5u.metatileentitys` | MetaTileEntities |
| `nei.options.tools.dump.gt5u.mode.0` | 可用 |
| `nei.options.tools.dump.gt5u.mode.1` | 已使用 |
| `nei.options.tools.dump.gt5u.recipe_locking` | 尚未支持配方锁定的机器 |
| `nei.options.tools.dump.gt5u.recipe_lockings` | 尚未支持配方锁定的机器 |
| `nei.options.tools.dump.gt5u.void_protection` | 尚未支持溢出保护的机器 |
| `nei.options.tools.dump.gt5u.void_protections` | 尚未支持溢出保护的机器 |
| `nei.options.tools.dump.gt5u.warn_env` | You're outside of the pack. Some IDs present in the full pack might be missing in this dump. |

#### 前缀: `tc` (25条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tc.aspect.custom1` | 平等,平衡,均衡 |
| `tc.aspect.custom1.name` | Aequalitas |
| `tc.aspect.custom2` | 疯癫,癫狂,狂热 |
| `tc.aspect.custom2.name` | Vesania |
| `tc.aspect.custom3` | 起始,起源,源头 |
| `tc.aspect.custom3.name` | Primordium |
| `tc.aspect.custom4` | 星辰,星座,天国 |
| `tc.aspect.custom4.name` | Astrum |
| `tc.aspect.custom5` | 荣耀,荣誉,声誉 |
| `tc.aspect.custom5.name` | Gloria |
| `tc.aspect.electrum` | 电力，闪电 |
| `tc.aspect.help.custom1` | 平衡的事物 |
| `tc.aspect.help.custom2` | 扭曲的思想 |
| `tc.aspect.help.custom3` | 新事物的起始 |
| `tc.aspect.help.custom4` | 宇宙 |
| `tc.aspect.help.custom5` | 荣耀 |
| `tc.aspect.help.electrum` | 闪电的力量 |
| `tc.aspect.help.magneto` | 吸引的力量 |
| `tc.aspect.help.nebrisum` | 偷来的奖励 |
| `tc.aspect.help.radio` | 无形的腐化能量 |
| `tc.aspect.help.strontio` | 失误与过错 |
| `tc.aspect.magneto` | 磁力，吸引 |
| `tc.aspect.nebrisum` | 欺骗，偷袭 |
| `tc.aspect.radio` | 辐射 |
| `tc.aspect.strontio` | 愚蠢，无能 |

#### 前缀: `tile` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tile.gt.dronerender.name` | 无人机渲染器 |

#### 前缀: `tooltip` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tooltip.flotationCell.lockedTo` | 锁定为： |
| `tooltip.large_distill_tower.upgraded` | §6已升级 |
| `tooltip.large_macerator.tier` | 等级：§6%s |

### KUBATECH (211条)


#### 前缀: `GT5U` (9条)

| Lang Key | 中文翻译 |
|----------|----------|
| `GT5U.gui.text.EEC_invalidspawner` | 无效的刷怪笼！ |
| `GT5U.gui.text.EEC_nospawner` | 未放入电动刷怪笼！ |
| `GT5U.gui.text.EEC_peaceful` | 此生物无法在和平模式生成！ |
| `GT5U.gui.text.EIG_ic2glass` | 玻璃等级不足! |
| `GT5U.gui.text.EIG_missingwater` | 没有水! |
| `GT5U.gui.text.EIG_seedOverflow` | 存储了太多种子! |
| `GT5U.gui.text.EIG_slotoverflow` | 内部作物数量过多！ |
| `GT5U.gui.text.MegaApiary_noflowers` | 缺少花朵！ |
| `GT5U.gui.text.MegaApiary_slotoverflow` | 内部蜜蜂数量过多！ |

#### 前缀: `KT` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `KT.research.ultimatetea` | 你找到一种方法,将这些茶转化为纯粹的能源并获得%s§6§l茶 |

#### 前缀: `achievement` (26条)

| Lang Key | 中文翻译 |
|----------|----------|
| `achievement.teacollection.black_tea` | §6§lKuba红茶 |
| `achievement.teacollection.black_tea.desc` | §6最常见也最受欢迎的茶 |
| `achievement.teacollection.butterfly_tea` | §1§lKuba蝶豆花茶 |
| `achievement.teacollection.butterfly_tea.desc` | §1甚至不是茶 |
| `achievement.teacollection.earl_gray_tea` | §6§lKuba格雷伯爵茶 |
| `achievement.teacollection.earl_gray_tea.desc` | §6为真正的英国人准备 |
| `achievement.teacollection.green_tea` | §2§lKuba绿茶 |
| `achievement.teacollection.green_tea.desc` | §2万茶之源 |
| `achievement.teacollection.lemon_tea` | §e§lKuba柠檬茶 |
| `achievement.teacollection.lemon_tea.desc` | §e带柠檬的红茶，你在期待什么？ |
| `achievement.teacollection.milk_tea` | §f§lKuba奶茶 |
| `achievement.teacollection.milk_tea.desc` | §f奶与红茶的结合，我的最爱 |
| `achievement.teacollection.oolong_tea` | §e§lKuba乌龙茶 |
| `achievement.teacollection.oolong_tea.desc` | §e對於真正的鑑賞家 |
| `achievement.teacollection.peppermint_tea` | §a§lKuba薄荷茶 |
| `achievement.teacollection.peppermint_tea.desc` | §a可以养胃 |
| `achievement.teacollection.pu-erh_tea` | §4§lKuba普洱茶 |
| `achievement.teacollection.pu-erh_tea.desc` | §4助消化，味道也像泥土 |
| `achievement.teacollection.red_tea` | §c§lKuba洛神花茶 |
| `achievement.teacollection.red_tea.desc` | §c为什么会有人喝这个？ |
| `achievement.teacollection.ultimate_tea` | §4§l§k?????? |
| `achievement.teacollection.ultimate_tea.desc` | §4§l一茶饮尽 |
| `achievement.teacollection.white_tea` | §e§lKuba白茶 |
| `achievement.teacollection.white_tea.desc` | §e最健康的一款 |
| `achievement.teacollection.yellow_tea` | §6§lKuba黄茶 |
| `achievement.teacollection.yellow_tea.desc` | §6青草味更浓的绿茶 |

#### 前缀: `defc` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `defc.casing.name` | 聚变方块 |
| `defc.casing.tip` | 龙研聚合装置外壳 T %d |

#### 前缀: `item` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `item.kubaitems.name` | 茶 / 茶叶 |

#### 前缀: `kubablock` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `kubablock.tea_acceptor.name` | §4§l茶接收器 |
| `kubablock.tea_storage.name` | §4§l茶叶存储扩展器 |

#### 前缀: `kubaitem` (46条)

| Lang Key | 中文翻译 |
|----------|----------|
| `kubaitem.defc_schematic_t1.name` | 龙之核心图纸 |
| `kubaitem.defc_schematic_t1.tip` | 可以在冥王星地牢找到这个图纸 |
| `kubaitem.defc_schematic_t2.name` | 双足飞龙核心图纸 |
| `kubaitem.defc_schematic_t3.name` | 觉醒核心图纸 |
| `kubaitem.defc_schematic_t4.name` | 混沌核心图纸 |
| `kubaitem.fromcollection` | 此物品来自 |
| `kubaitem.notyours` | 那东西好像不是你的 |
| `kubaitem.tea.black_tea.name` | 红茶 |
| `kubaitem.tea.earl_gray_tea.name` | 格雷伯爵茶 |
| `kubaitem.tea.green_tea.name` | 绿茶 |
| `kubaitem.tea.lemon_tea.name` | 柠檬茶 |
| `kubaitem.tea.milk_tea.name` | 奶茶 |
| `kubaitem.tea.oolong_tea.name` | 乌龙茶 |
| `kubaitem.tea.peppermint_tea.name` | 薄荷茶 |
| `kubaitem.tea.pu-erh_tea.name` | 普洱茶 |
| `kubaitem.tea.white_tea.name` | 白茶 |
| `kubaitem.tea.yellow_tea.name` | 黄茶 |
| `kubaitem.tea_acceptor_research_note.name` | 茶接收器研究笔记 |
| `kubaitem.teacollection` | 传奇秘制茶系列 |
| `kubaitem.teacollection.black_tea.name` | §6§lKuba红茶 |
| `kubaitem.teacollection.butterfly_tea.name` | §1§lKuba蝶豆花茶 |
| `kubaitem.teacollection.earl_gray_tea.name` | §6§lKuba格雷伯爵茶 |
| `kubaitem.teacollection.green_tea.name` | §2§lKuba绿茶 |
| `kubaitem.teacollection.lemon_tea.name` | §e§lKuba柠檬茶 |
| `kubaitem.teacollection.milk_tea.name` | §f§lKuba奶茶 |
| `kubaitem.teacollection.mmm` | Mmmm茶 |
| `kubaitem.teacollection.oolong_tea.name` | §e§lKuba乌龙茶 |
| `kubaitem.teacollection.peppermint_tea.name` | §a§lKuba薄荷茶 |
| `kubaitem.teacollection.pu-erh_tea.name` | §4§lKuba普洱茶 |
| `kubaitem.teacollection.red_tea.name` | §c§lKuba洛神花茶 |

*...还有 16 条翻译*

#### 前缀: `kubatech` (121条)

| Lang Key | 中文翻译 |
|----------|----------|
| `kubatech.chat.eec.infernal_drops_disabled` | 将尝试阻止生成精英怪 |
| `kubatech.chat.eec.infernal_drops_enabled` | 允许精英怪生成 |
| `kubatech.chat.eec.ritual_mode_connected` | 已成功连接到仪式 |
| `kubatech.chat.eec.ritual_mode_disabled` | 苦难之井模式已关闭 |
| `kubatech.chat.eec.ritual_mode_enabled` | 苦难之井模式已启用 |
| `kubatech.chat.eec.ritual_mode_error` | 无法连接到仪式！ |
| `kubatech.chat.forbidden_while_running` | 无法在运行时更改模式！ |
| `kubatech.command.config.invalid_option` | §c无效选项！可能的选项：reload |
| `kubatech.command.config.success` | §a成功重载配置文件 |
| `kubatech.command.config.usage` | <选项> |
| `kubatech.command.help.possible_commands` | 可选指令： |
| `kubatech.command.help.usage` | - 显示所有可选指令 |
| `kubatech.command.tea.invalid_option` | §c无效使用！ |
| `kubatech.command.tea.player_not_found` | §c未找到玩家！ |
| `kubatech.command.tea.success_add` | 玩家 %s 现在有%d杯茶 |
| `kubatech.command.tea.success_get` | 玩家 %s 有%d杯茶 |
| `kubatech.command.tea.success_set` | 玩家 %s 现在有%d杯茶 |
| `kubatech.command.tea.usage` | <玩家> get/set/add (<数量>) |
| `kubatech.commandhandler.cant_find` | §c找不到指令选项 %s |
| `kubatech.commandhandler.generic_help` | §c你也可以使用 "/kubatech help" 以查看可选指令 |
| `kubatech.commandhandler.invalid` | §c无效使用！该指令的可能使用为 /%s |
| `kubatech.commandhandler.usage` | <选项> |
| `kubatech.defusioncrafter` | 龙研聚合装置 |
| `kubatech.defusioncrafter.tier` | 外壳等级: %s |
| `kubatech.gui.text.configuration` | 配置 |
| `kubatech.gui.text.eec.cycle_weapons.info` | 如果启用了§f武器保护§r功能，当物品栏中有空间时，会将几乎损坏的武器从GUI移至输出总线。 |
| `kubatech.gui.text.eec.cycle_weapons_off` | 武器循环：关闭 |
| `kubatech.gui.text.eec.cycle_weapons_on` | 武器循环：开启 |
| `kubatech.gui.text.eec.infernal_drop_always` | 不会作用于始终为精英怪的怪物！ |
| `kubatech.gui.text.eec.infernal_drop_off` | 允许精英怪生成：关闭 |

*...还有 91 条翻译*

#### 前缀: `tc` (3条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tc.research_category.KUBATECH` | §l茶 |
| `tc.research_name.KT_UltimateTea` | %s §6§l茶 |
| `tc.research_text.KT_UltimateTea` | §4§l纯粹的能源 |

### MISCUTILS (1条)


#### 前缀: `tile` (1条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tile.dimensionAustraliaPortalBlock.name` | 澳大利亚传送门 |

### TECTECH (14条)


#### 前缀: `item` (12条)

| Lang Key | 中文翻译 |
|----------|----------|
| `item.itemBoltGermanium.name` | 锗螺栓 |
| `item.itemDustGermanium.name` | 锗粉 |
| `item.itemDustSmallGermanium.name` | 小堆锗粉 |
| `item.itemDustTinyGermanium.name` | 小搓锗粉 |
| `item.itemGearGermanium.name` | 锗齿轮 |
| `item.itemIngotGermanium.name` | 锗锭 |
| `item.itemNuggetGermanium.name` | 锗粒 |
| `item.itemPlateGermanium.name` | 锗板 |
| `item.itemRingGermanium.name` | 锗环 |
| `item.itemRodGermanium.name` | 锗杆 |
| `item.itemRotorGermanium.name` | 锗转子 |
| `item.itemScrewGermanium.name` | 锗螺丝 |

#### 前缀: `tile` (2条)

| Lang Key | 中文翻译 |
|----------|----------|
| `tile.Block of Germanium.name` | 锗块 |
| `tile.Germanium Frame Box.name` | 锗框架 |


## 特殊翻译模式

### GregTech组件翻译

GregTech使用模板化翻译：

```
gt.component.dust=%s粉
gt.component.ingot=%s锭
gt.component.plate=%s板
```

使用时，`%s`会被材料名替换。

### Kubatech茶物品

Kubatech的茶使用特定格式：

```
kubaitem.tea.black_tea.name=红茶
kubaitem.teacollection.black_tea.name=§6§lKuba红茶
```

### GT++物品

GT++（miscutils）使用`gtpp`或`item.GTPP`前缀。

## 验证方法

所有翻译都可以通过以下命令验证：

```bash
cd Translation-of-GTNH
grep "翻译文本" resources/*/lang/zh_CN.lang
```

## 注意事项

⚠️ **ItemList枚举名 ≠ Lang Key**

ItemList中的枚举名（如`Hull_LV`）通常需要转换才能找到对应的lang key。这个转换规则需要查看GT5U源码中的set()调用。

例如：
- 枚举名: `ItemList.Hull_LV`
- 可能的lang key: `gt.blockmachines.hull.tier.01.name`
- 中文翻译: 需要先找到正确的key

---

*本文档由自动化脚本生成，数据100%来自Translation-of-GTNH*
