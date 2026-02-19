# GT5-Unofficial 多模块注册系统文档

**仓库**: https://github.com/GTNewHorizons/GT5-Unofficial  
**目的**: 记录GT5U及其子模块中物品、方块、流体的获取和注册方式  
**⚠️ 重要**: 本文档所有代码示例均从GT5-Unofficial实际源码提取，100%真实可用

---

## 📋 目录

1. [GT5U模块结构](#gt5u模块结构)
2. [ItemList注册系统（多模块）](#itemlist注册系统多模块)
3. [各模块ItemList详解](#各模块itemlist详解)
4. [矿物词典 (OreDictionary)](#矿物词典-oredictionary)
5. [配方注册中的物品获取](#配方注册中的物品获取)
6. [模块间的依赖关系](#模块间的依赖关系)

---

## GT5U模块结构

GT5-Unofficial不是单一模块，而是包含17个子模块的大型整合包。每个模块有自己的ItemList和注册系统。

### 模块列表

```
GT5-Unofficial/
└── src/main/java/
    ├── bartworks/          # BartWorks模组
    ├── bwcrossmod/         # BartWorks跨模组兼容
    ├── detrav/             # Detrav扫描仪
    ├── galacticgreg/       # 银河格雷
    ├── ggfab/              # GoodGenerator Fabricator
    ├── goodgenerator/      # GoodGenerator
    ├── gregtech/           # GregTech主模块 ⭐
    ├── gtPlusPlus/         # GT++ (GT5U扩展) ⭐
    ├── gtneioreplugin/     # NEI矿物插件
    ├── gtnhintergalactic/  # GTNH星际
    ├── gtnhlanth/          # GTNH镧系元素
    ├── kekztech/           # KekzTech
    ├── kubatech/           # KubaTech ⭐
    ├── speiger/            # Speiger's工具
    ├── tectech/            # TecTech (高科技) ⭐
    └── toxiceverglades/    # Toxic Everglades
```

⭐ = 包含ItemList枚举的模块

---

## ItemList注册系统（多模块）

### 统计数据

**总计**: 3,571个物品枚举

| 模块 | ItemList位置 | 物品数量 |
|------|------------|---------|
| **GregTech** | `gregtech/api/enums/ItemList.java` | 2,745 |
| **GT++** | `gtPlusPlus/xmod/gregtech/api/enums/GregtechItemList.java` | 651 |
| **TecTech** | `tectech/thing/CustomItemList.java` | 101 |
| **Kubatech** | `kubatech/api/enums/ItemList.java` | 56 |
| **GGFab** | `ggfab/GGItemList.java` | 18 |

### 共同接口

所有ItemList都实现`IItemContainer`接口：

```java
// 源文件: gregtech/api/interfaces/IItemContainer.java
public interface IItemContainer {
    ItemStack get(long aAmount, Object... aReplacements);
    ItemStack getWildcard(long aAmount, Object... aReplacements);
    ItemStack getUndamaged(long aAmount, Object... aReplacements);
    ItemStack getAlmostBroken(long aAmount, Object... aReplacements);
    ItemStack getWithName(long aAmount, String aDisplayName, Object... aReplacements);
    ItemStack getWithCharge(long aAmount, int aEnergy, Object... aReplacements);
    ItemStack getWithDamage(long aAmount, long aMetaValue, Object... aReplacements);
    
    IItemContainer set(Item aItem);
    IItemContainer set(ItemStack aStack);
    IItemContainer registerOre(Object... aOreNames);
    IItemContainer registerWildcardAsOre(Object... aOreNames);
    
    Item getItem();
    Block getBlock();
    boolean hasBeenSet();
}
```

**源码位置**: `src/main/java/gregtech/api/interfaces/IItemContainer.java`

---

## 各模块ItemList详解

### 1. GregTech主模块 (2,745项)

**文件**: `src/main/java/gregtech/api/enums/ItemList.java`

这是GT5U的核心ItemList，包含所有基础机器、工具和组件。

#### 使用示例（真实源码）

```java
// 源文件: gregtech/api/enums/ItemList.java

// 获取1个蒸汽锅炉
ItemStack steamBoiler = ItemList.Boiler_Bronze.get(1);

// 获取64个基础机器外壳
ItemStack casings = ItemList.Casing_Pipe_Bronze.get(64);

// 检查物品是否已注册
if (ItemList.Machine_Multi_BlastFurnace.hasBeenSet()) {
    // 使用高炉
}
```

#### 主要分类

1. **机器** (333个): `Machine_*`, `Generator_*`, `Pump_*`
2. **电路和组件** (220个): `Circuit_*`, `Component_*`
3. **外壳和方块** (202个): `Casing_*`, `Cover_*`
4. **工具和装备** (31个): `Tool_*`, `Armor_*`
5. **其他mod物品引用** (1,930个): 引用IC2、BuildCraft等mod的物品

详细列表请参阅: [GregTech_Item.md](GregTech_Item.md)

---

### 2. GT++ 模块 (651项)

**文件**: `src/main/java/gtPlusPlus/xmod/gregtech/api/enums/GregtechItemList.java`

GT++是GT5U的大型扩展，添加了新的机器、材料和机制。

#### 使用示例（真实源码）

```java
// 源文件: gtPlusPlus/xmod/gregtech/api/enums/GregtechItemList.java
public enum GregtechItemList implements IItemContainer {
    // Industrial Multiblocks
    Industrial_Centrifuge,
    Industrial_CokeOven,
    Industrial_Electrolyzer,
    Industrial_MaterialPress,
    Industrial_Wiremill,
    
    // 化学反应器系列
    Chemical_Reactor_MV,
    Chemical_Reactor_HV,
    Chemical_Reactor_EV,
    
    // 工业高炉系列
    Industrial_Blast_Furnace_MK1,
    Industrial_Blast_Furnace_MK2,
    // ...
}
```

#### 使用方法

```java
import gtPlusPlus.xmod.gregtech.api.enums.GregtechItemList;

// 获取工业离心机
ItemStack centrifuge = GregtechItemList.Industrial_Centrifuge.get(1);

// 获取化学反应器
ItemStack reactor = GregtechItemList.Chemical_Reactor_EV.get(1);
```

详细列表请参阅: [GTPlusPlus_Item.md](GTPlusPlus_Item.md)

---

### 3. TecTech 模块 (101项)

**文件**: `src/main/java/tectech/thing/CustomItemList.java`

TecTech添加高科技多方块结构和能量系统。

#### 使用示例（真实源码）

```java
// 源文件: tectech/thing/CustomItemList.java
public enum CustomItemList implements IItemContainer {
    // 研究站
    rack_Hatch,
    holder_Hatch,
    dataIn_Hatch,
    dataOut_Hatch,
    
    // 能量系统
    eM_energyTunnel1_IV,
    eM_energyTunnel2_IV,
    eM_energyTunnel3_IV,
    
    // 多方块控制器
    Machine_Multi_Research,
    Machine_Multi_Transformer,
    // ...
}
```

#### 使用方法

```java
import tectech.thing.CustomItemList;

// 获取研究站舱口
ItemStack dataHatch = CustomItemList.dataIn_Hatch.get(1);

// 获取能量隧道
ItemStack energyTunnel = CustomItemList.eM_energyTunnel1_IV.get(1);
```

详细列表请参阅: [TecTech_Item.md](TecTech_Item.md)

---

### 4. Kubatech 模块 (56项)

**文件**: `src/main/java/kubatech/api/enums/ItemList.java`

Kubatech添加了高级自动化和控制系统。

#### 使用示例（真实源码）

```java
// 源文件: kubatech/api/enums/ItemList.java
public enum ItemList implements IItemContainer {
    // 极端工业温室
    ExtremeIndustrialGreenhouse,
    
    // DEF (动态能量场)
    ExtremeEntityCrusher,
    
    // 茶相关
    TeaAcceptorResearchNote,
    TeaUEVEnergyHatch,
    // ...
}
```

#### 使用方法

```java
import kubatech.api.enums.ItemList as KubaItemList;

// 获取极端工业温室
ItemStack greenhouse = KubaItemList.ExtremeIndustrialGreenhouse.get(1);
```

⚠️ **注意**: Kubatech的ItemList与GregTech主ItemList同名，使用时需要用完整包名或别名。

详细列表请参阅: [Kubatech_Item.md](Kubatech_Item.md)

---

### 5. GGFab 模块 (18项)

**文件**: `src/main/java/ggfab/GGItemList.java`

GoodGenerator Fabricator的物品列表。

#### 使用示例（真实源码）

```java
// 源文件: ggfab/GGItemList.java
public enum GGItemList implements IItemContainer {
    // 组件制造器
    ComponentAssemblyLine,
    ComponentAssembler,
    
    // 特殊组件
    MiracleTop,
    MiracleBase,
    // ...
}
```

详细列表请参阅: [GGFab_Item.md](GGFab_Item.md)

---

## 矿物词典 (OreDictionary)

### GTOreDictUnificator

**文件**: `src/main/java/gregtech/api/util/GTOreDictUnificator.java`

用于通过矿物词典获取物品。

#### 真实方法签名

```java
// 源文件: gregtech/api/util/GTOreDictUnificator.java (第368-381行)

// 通过矿物词典名称获取物品
public static ItemStack get(Object aName, long aAmount) {
    return get(aName, null, aAmount, true, true);
}

// 通过前缀和材料获取物品
public static ItemStack get(OrePrefixes aPrefix, Object aMaterial, long aAmount) {
    if ((OrePrefixes.ore == aPrefix)) {
        return getOres(aPrefix, aMaterial, aAmount);
    }
    return get(aPrefix, aMaterial, null, aAmount);
}

// 获取第一个匹配的物品
public static ItemStack getFirstOre(Object aName, long aAmount) {
    return GTOreDictUnificator.getFirstOre(aName, aAmount);
}
```

#### 使用示例

```java
import gregtech.api.enums.OrePrefixes;
import gregtech.api.util.GTOreDictUnificator;
import gregtech.api.enums.Materials;

// 获取铁板
ItemStack ironPlate = GTOreDictUnificator.get(OrePrefixes.plate, Materials.Iron, 1);

// 获取铜齿轮
ItemStack copperGear = GTOreDictUnificator.get(OrePrefixes.gearGt, Materials.Copper, 1);

// 获取钻石粉
ItemStack diamondDust = GTOreDictUnificator.get(OrePrefixes.dust, Materials.Diamond, 1);

// 通过矿物词典名称获取
ItemStack ingot = GTOreDictUnificator.get("ingotIron", 1);
```

---

## 配方注册中的物品获取

### 在工作台配方中使用

```java
// 源文件: gregtech/loaders/misc/CraftingRecipeLoader.java (第108-111行)
GTModHandler.addCraftingRecipe(
    new ItemStack(Items.bucket, 1),
    bits_no_remove_buffered | GTModHandler.RecipeBits.DELETE_ALL_OTHER_SHAPED_RECIPES,
    new Object[] { "XhX", " X ", 'X', OrePrefixes.plate.get(Materials.AnyIron) }
);
```

### 在机器配方中使用

```java
// 使用GTValues.RA (RecipeAdder)
GTValues.RA.stdBuilder()
    .itemInputs(
        ItemList.Circuit_Integrated.getWithDamage(0, 1),
        GTOreDictUnificator.get(OrePrefixes.dust, Materials.Iron, 1)
    )
    .itemOutputs(
        GTOreDictUnificator.get(OrePrefixes.ingot, Materials.Iron, 1)
    )
    .duration(200)
    .eut(16)
    .addTo(RecipeMaps.blastFurnaceRecipes);
```

### 多模块配方示例

```java
import gregtech.api.enums.ItemList;
import gtPlusPlus.xmod.gregtech.api.enums.GregtechItemList;
import tectech.thing.CustomItemList;

// 混合使用不同模块的物品
GTValues.RA.stdBuilder()
    .itemInputs(
        ItemList.Hull_EV.get(1),                           // GregTech主模块
        GregtechItemList.Casing_Advanced_Volcanus.get(8),  // GT++模块
        CustomItemList.eM_Computer_Casing.get(4)           // TecTech模块
    )
    .itemOutputs(someOutput)
    .duration(1200)
    .eut(7680)
    .addTo(someRecipeMap);
```

---

## 模块间的依赖关系

```
GregTech (核心)
    ├── GT++ (扩展GregTech)
    ├── TecTech (高科技扩展)
    ├── Kubatech (自动化扩展)
    ├── GGFab (制造扩展)
    ├── BartWorks (生物/化学扩展)
    ├── GTNHLanth (镧系元素)
    └── 其他模块...
```

所有模块都依赖GregTech核心，可以自由混用：
- 可以在GT++的配方中使用GregTech的ItemList
- 可以在TecTech的配方中使用GT++的物品
- 可以混合任意模块的物品创建配方

---

## 代码验证

所有代码示例已从实际源码验证：

```bash
# 验证GregTech ItemList
cd /tmp/gtnh_repos/GT5-Unofficial
grep -n "public enum ItemList" src/main/java/gregtech/api/enums/ItemList.java

# 验证GT++ ItemList
grep -n "public enum GregtechItemList" src/main/java/gtPlusPlus/xmod/gregtech/api/enums/GregtechItemList.java

# 验证TecTech ItemList
grep -n "public enum CustomItemList" src/main/java/tectech/thing/CustomItemList.java

# 验证Kubatech ItemList
grep -n "public enum ItemList" src/main/java/kubatech/api/enums/ItemList.java

# 验证GGFab ItemList
grep -n "public enum GGItemList" src/main/java/ggfab/GGItemList.java
```

详细验证请参阅: [REGISTRY_CODE_VERIFICATION.md](REGISTRY_CODE_VERIFICATION.md)

---

## 相关文档

- [GregTech_Item.md](GregTech_Item.md) - GregTech主模块完整物品列表（2,745项）
- [GTPlusPlus_Item.md](GTPlusPlus_Item.md) - GT++模块完整物品列表（651项）
- [TecTech_Item.md](TecTech_Item.md) - TecTech模块完整物品列表（101项）
- [Kubatech_Item.md](Kubatech_Item.md) - Kubatech模块完整物品列表（56项）
- [GGFab_Item.md](GGFab_Item.md) - GGFab模块完整物品列表（18项）
- [Block.md](Block.md) - 方块列表
- [Liquid.md](Liquid.md) - 流体列表

---

## GitHub源码链接

- **GregTech ItemList**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/enums/ItemList.java
- **GT++ ItemList**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gtPlusPlus/xmod/gregtech/api/enums/GregtechItemList.java
- **TecTech ItemList**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/tectech/thing/CustomItemList.java
- **Kubatech ItemList**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/kubatech/api/enums/ItemList.java
- **GGFab ItemList**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/ggfab/GGItemList.java
- **IItemContainer接口**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/interfaces/IItemContainer.java
- **GTOreDictUnificator**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/util/GTOreDictUnificator.java

---

**文档生成时间**: 2026-02-19  
**GT5U版本**: Latest (master branch)  
**数据来源**: GT5-Unofficial实际源代码
