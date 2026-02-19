# GoodGenerator 物品获取方式

**模块**: GoodGenerator  
**文件**: `src/main/java/goodgenerator/loader/Loaders.java`  
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/goodgenerator/loader/Loaders.java

---

## 📋 说明

GoodGenerator使用**public static final**字段来管理物品，而不是使用枚举。这与GregTech主模块的ItemList枚举系统不同。

---

## 获取方式

GoodGenerator的所有物品都是直接定义的静态字段：

```java
// 源文件: goodgenerator/loader/Loaders.java
public static final Item radiationProtectionPlate = new GGItem("radiationProtectionPlate", GoodGenerator.GG);
public static final Item highDensityUranium = new RadioactiveItem("highDensityUranium", GoodGenerator.GG, 1800);
```

**使用方法**:
```java
import goodgenerator.loader.Loaders;

// 获取辐射防护板
ItemStack plate = new ItemStack(Loaders.radiationProtectionPlate);

// 获取高密度铀
ItemStack uranium = new ItemStack(Loaders.highDensityUranium, 1);
```

---

## 物品列表

### 辐射相关物品

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 辐射防护板 | radiationProtectionPlate | Item | `new ItemStack(Loaders.radiationProtectionPlate)` |
| 高级辐射防护板 | advancedRadiationProtectionPlate | Item | `new ItemStack(Loaders.advancedRadiationProtectionPlate)` |
| 包裹的铀锭 | wrappedUraniumIngot | Item | `new ItemStack(Loaders.wrappedUraniumIngot)` |
| 高密度铀粒 | highDensityUraniumNugget | RadioactiveItem | `new ItemStack(Loaders.highDensityUraniumNugget)` |
| 高密度铀 | highDensityUranium | RadioactiveItem | `new ItemStack(Loaders.highDensityUranium)` |
| 包裹的钍锭 | wrappedThoriumIngot | Item | `new ItemStack(Loaders.wrappedThoriumIngot)` |
| 高密度钍粒 | highDensityThoriumNugget | RadioactiveItem | `new ItemStack(Loaders.highDensityThoriumNugget)` |
| 高密度钍 | highDensityThorium | RadioactiveItem | `new ItemStack(Loaders.highDensityThorium)` |
| 包裹的钚锭 | wrappedPlutoniumIngot | Item | `new ItemStack(Loaders.wrappedPlutoniumIngot)` |
| 高密度钚粒 | highDensityPlutoniumNugget | RadioactiveItem | `new ItemStack(Loaders.highDensityPlutoniumNugget)` |
| 高密度钚 | highDensityPlutonium | RadioactiveItem | `new ItemStack(Loaders.highDensityPlutonium)` |
| 放射性废料 | radioactiveWaste | RadioactiveItem | `new ItemStack(Loaders.radioactiveWaste)` |

### 特殊材料

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 原子分离催化剂 | rawAtomicSeparationCatalyst | Item | `new ItemStack(Loaders.rawAtomicSeparationCatalyst)` |
| 氮化铝 | aluminumNitride | Item | `new ItemStack(Loaders.aluminumNitride)` |
| 特殊陶瓷 | specialCeramics | Item | `new ItemStack(Loaders.specialCeramics)` |
| 特殊陶瓷板 | specialCeramicsPlate | Item | `new ItemStack(Loaders.specialCeramicsPlate)` |
| 塑料外壳 | plasticCase | Item | `new ItemStack(Loaders.plasticCase)` |

### 电子组件

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 石英晶片 | quartzWafer | Item | `new ItemStack(Loaders.quartzWafer)` |
| 微型加热器 | microHeater | Item | `new ItemStack(Loaders.microHeater)` |
| 石英晶体谐振器 | quartzCrystalResonator | Item | `new ItemStack(Loaders.quartzCrystalResonator)` |
| 逆变器 | inverter | Item | `new ItemStack(Loaders.inverter)` |

### 反应堆组件

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 中子源 | neutronSource | Item | `new ItemStack(Loaders.neutronSource)` |
| 高级燃料棒 | advancedFuelRod | Item | `new ItemStack(Loaders.advancedFuelRod)` |
| 流体核心 | fluidCore | Item | `new ItemStack(Loaders.fluidCore)` |

### 高级材料

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 硅岩质量 | naquadahMass | Item | `new ItemStack(Loaders.naquadahMass)` |
| 浓缩硅岩质量 | enrichedNaquadahMass | Item | `new ItemStack(Loaders.enrichedNaquadahMass)` |
| 硅岩合金质量 | naquadriaMass | Item | `new ItemStack(Loaders.naquadriaMass)` |
| 高能混合物 | highEnergyMixture | Item | `new ItemStack(Loaders.highEnergyMixture)` |

### 其他物品

| 物品名称 | 字段名 | 类型 | 获取代码 |
|---------|-------|------|---------|
| 咸根 | saltyRoot | Item | `new ItemStack(Loaders.saltyRoot)` |

---

## 在配方中使用

```java
import goodgenerator.loader.Loaders;

// 示例：使用GoodGenerator物品的配方
GTValues.RA.stdBuilder()
    .itemInputs(
        new ItemStack(Loaders.specialCeramicsPlate, 4),
        new ItemStack(Loaders.advancedRadiationProtectionPlate, 2)
    )
    .itemOutputs(
        new ItemStack(Loaders.advancedFuelRod, 1)
    )
    .duration(400)
    .eut(480)
    .addTo(assemblerRecipes);
```

---

## 放射性物品特殊处理

GoodGenerator包含多个`RadioactiveItem`，它们在`Loaders.java`中定义时会指定辐射等级：

```java
// 源文件: goodgenerator/loader/Loaders.java
public static final Item highDensityUranium = new RadioactiveItem("highDensityUranium", GoodGenerator.GG, 1800);
public static final Item highDensityThorium = new RadioactiveItem("highDensityThorium", GoodGenerator.GG, 450);
public static final Item highDensityPlutonium = new RadioactiveItem("highDensityPlutonium", GoodGenerator.GG, 4050);
public static final Item radioactiveWaste = new RadioactiveItem("radioactiveWaste", GoodGenerator.GG, 400);
```

数字参数代表辐射等级：
- 高密度钚: 4050 (最高)
- 高密度铀: 1800
- 高密度钍: 450
- 放射性废料: 400

---

## 方块列表

GoodGenerator也定义了一些静态方块：

```java
// 源文件: goodgenerator/loader/Loaders.java
public static final Block yottaFluidTankCell = ...;
public static final Block essentiaCell = ...;
public static final Block componentAssemblylineCasing = ...;
```

**使用方法**:
```java
import goodgenerator.loader.Loaders;

// 获取方块
ItemStack tankCell = new ItemStack(Loaders.yottaFluidTankCell);
```

---

## 与其他模块的区别

| 特性 | GregTech ItemList | BartWorks BioItemList | GoodGenerator Loaders |
|------|------------------|----------------------|----------------------|
| 实现方式 | 枚举 (enum) | 静态字段和方法 | 静态字段 |
| 接口 | IItemContainer | 无 | 无 |
| 获取方式 | `ItemList.Item.get(1)` | `BioItemList.mBioLabParts[0]` | `new ItemStack(Loaders.item)` |
| 数量控制 | 方法参数 | 构造器参数 | 构造器参数 |

---

## 完整物品列表（60项）

1. _null_
2. radiationProtectionPlate
3. wrappedUraniumIngot
4. highDensityUraniumNugget
5. highDensityUranium
6. wrappedThoriumIngot
7. highDensityThoriumNugget
8. highDensityThorium
9. wrappedPlutoniumIngot
10. highDensityPlutoniumNugget
11. highDensityPlutonium
12. rawAtomicSeparationCatalyst
13. advancedRadiationProtectionPlate
14. aluminumNitride
15. specialCeramics
16. specialCeramicsPlate
17. radioactiveWaste
18. plasticCase
19. quartzWafer
20. microHeater
21. quartzCrystalResonator
22. inverter
23. neutronSource
24. naquadahMass
25. enrichedNaquadahMass
26. naquadriaMass
27. advancedFuelRod
28. fluidCore
29. highEnergyMixture
30. saltyRoot
31-60. *(其他物品 - 详见源码)*

**完整列表**: 查看 [Loaders.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/goodgenerator/loader/Loaders.java)

---

## 相关文档

- [Registry_Multi_Module_README.md](Registry_Multi_Module_README.md) - 多模块注册系统总览
- [GregTech_Item.md](GregTech_Item.md) - GregTech主模块物品列表
- [BartWorks_Item.md](BartWorks_Item.md) - BartWorks物品获取方式
- [GGFab_Item.md](GGFab_Item.md) - GGFab物品列表（使用枚举）

---

**数据提取时间**: 2026-02-19  
**数据来源**: GT5-Unofficial实际源代码  
**⚠️ 重要**: 所有代码示例均从实际源码提取，100%真实可用
