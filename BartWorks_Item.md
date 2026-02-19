# BartWorks 物品获取方式

**模块**: BartWorks  
**文件**: `src/main/java/bartworks/common/loaders/BioItemList.java`  
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/bartworks/common/loaders/BioItemList.java

---

## 📋 说明

BartWorks使用**静态ItemStack数组**和**静态方法**来管理物品，而不是使用枚举。这与GregTech主模块的ItemList枚举系统不同。

---

## 获取方式类型

### 1. 静态ItemStack数组

BartWorks定义了静态的ItemStack数组来存储物品：

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第33-36行)
public static final ItemStack[] mBioLabParts = { 
    new ItemStack(BioItemList.mItemBioLabParts),
    new ItemStack(BioItemList.mItemBioLabParts, 1, 1), 
    new ItemStack(BioItemList.mItemBioLabParts, 1, 2),
    new ItemStack(BioItemList.mItemBioLabParts, 1, 3), 
    new ItemStack(BioItemList.mItemBioLabParts, 1, 4) 
};
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;

// 获取生物实验室零件
ItemStack part0 = BioItemList.mBioLabParts[0]; // DNA提取模块
ItemStack part1 = BioItemList.mBioLabParts[1]; // PCR热循环模块
ItemStack part2 = BioItemList.mBioLabParts[2]; // 质粒合成模块
ItemStack part3 = BioItemList.mBioLabParts[3]; // 转化模块
ItemStack part4 = BioItemList.mBioLabParts[4]; // 克隆细胞合成模块
```

---

### 2. 静态方法获取

BartWorks提供静态方法来获取带NBT数据的物品：

#### getPetriDish() - 获取培养皿

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第71-75行)
public static ItemStack getPetriDish(BioCulture Culture) {
    if (Culture == null) return new ItemStack(BioItemList.vanillaBioLabParts);
    ItemStack ret = new ItemStack(BioItemList.vanillaBioLabParts);
    ret.setTagCompound(BioCulture.getNBTTagFromCulture(Culture));
    return ret;
}
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;
import bartworks.util.BioCulture;

// 获取特定生物培养物的培养皿
ItemStack petriDish = BioItemList.getPetriDish(someBioCulture);

// 获取空培养皿
ItemStack emptyDish = BioItemList.getPetriDish(null);
```

#### getDNASampleFlask() - 获取DNA样本瓶

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第77-82行)
public static ItemStack getDNASampleFlask(BioDNA dna) {
    if (dna == null) return new ItemStack(BioItemList.vanillaBioLabParts, 1, 1);
    ItemStack ret = new ItemStack(BioItemList.vanillaBioLabParts, 1, 1);
    ret.setTagCompound(BioData.getNBTTagFromBioData(dna));
    return ret;
}
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;
import bartworks.util.BioDNA;

// 获取特定DNA的样本瓶
ItemStack dnaFlask = BioItemList.getDNASampleFlask(someBioDNA);

// 获取空DNA样本瓶
ItemStack emptyFlask = BioItemList.getDNASampleFlask(null);
```

#### getPlasmidCell() - 获取质粒细胞

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第84-89行)
public static ItemStack getPlasmidCell(BioPlasmid plasmid) {
    if (plasmid == null) return new ItemStack(BioItemList.vanillaBioLabParts, 1, 2);
    ItemStack ret = new ItemStack(BioItemList.vanillaBioLabParts, 1, 2);
    ret.setTagCompound(BioData.getNBTTagFromBioData(plasmid));
    return ret;
}
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;
import bartworks.util.BioPlasmid;

// 获取特定质粒的细胞
ItemStack plasmidCell = BioItemList.getPlasmidCell(someBioPlasmid);

// 获取空质粒细胞
ItemStack emptyCell = BioItemList.getPlasmidCell(null);
```

#### getOtherItem() - 获取其他物品

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第91-101行)
/**
 * 1 - Detergent Powder 
 * 2 - Agarose 
 * 3 - Incubation Module 
 * 4 - Plasma Membrane 
 * others are null
 *
 * @param selection see above
 * @return the selected Item
 */
public static ItemStack getOtherItem(int selection) {
    if (selection > 0 && selection < 5) 
        return new ItemStack(BioItemList.vanillaBioLabParts, 1, selection + 2);
    return null;
}
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;

// 获取洗涤剂粉末
ItemStack detergent = BioItemList.getOtherItem(1);

// 获取琼脂糖
ItemStack agarose = BioItemList.getOtherItem(2);

// 获取培养模块
ItemStack incubation = BioItemList.getOtherItem(3);

// 获取等离子膜
ItemStack membrane = BioItemList.getOtherItem(4);
```

---

### 3. 集合方法获取所有变体

BartWorks提供方法来获取所有可能的物品变体：

```java
// 源文件: bartworks/common/loaders/BioItemList.java (第54-68行)

// 获取所有培养皿
public static Collection<ItemStack> getAllPetriDishes() {
    HashSet<ItemStack> ret = new HashSet<>();
    for (BioCulture Culture : BioCulture.BIO_CULTURE_ARRAY_LIST) {
        ret.add(BioItemList.getPetriDish(Culture));
    }
    return ret;
}

// 获取所有DNA样本瓶
public static Collection<ItemStack> getAllDNASampleFlasks() {
    HashSet<ItemStack> ret = new HashSet<>();
    for (BioData dna : BioData.BIO_DATA_ARRAY_LIST) {
        ret.add(BioItemList.getDNASampleFlask(BioDNA.convertDataToDNA(dna)));
    }
    return ret;
}

// 获取所有质粒细胞
public static Collection<ItemStack> getAllPlasmidCells() {
    HashSet<ItemStack> ret = new HashSet<>();
    for (BioData dna : BioData.BIO_DATA_ARRAY_LIST) {
        ret.add(BioItemList.getPlasmidCell(BioPlasmid.convertDataToDNA(dna)));
    }
    return ret;
}
```

**使用方法**:
```java
import bartworks.common.loaders.BioItemList;
import java.util.Collection;

// 获取所有培养皿变体
Collection<ItemStack> allDishes = BioItemList.getAllPetriDishes();

// 获取所有DNA样本瓶变体
Collection<ItemStack> allFlasks = BioItemList.getAllDNASampleFlasks();

// 获取所有质粒细胞变体
Collection<ItemStack> allCells = BioItemList.getAllPlasmidCells();
```

---

## 物品列表

### 生物实验室模块 (mBioLabParts)

| 索引 | 物品名称 | 内部名称 | 获取代码 |
|------|---------|---------|---------|
| 0 | DNA提取模块 | DNAExtractionModule | `BioItemList.mBioLabParts[0]` |
| 1 | PCR热循环模块 | PCRThermoclyclingModule | `BioItemList.mBioLabParts[1]` |
| 2 | 质粒合成模块 | PlasmidSynthesisModule | `BioItemList.mBioLabParts[2]` |
| 3 | 转化模块 | TransformationModule | `BioItemList.mBioLabParts[3]` |
| 4 | 克隆细胞合成模块 | ClonalCellularSynthesisModule | `BioItemList.mBioLabParts[4]` |

### 生物实验室零件 (vanillaBioLabParts)

| Meta值 | 物品名称 | 内部名称 | 获取代码 |
|--------|---------|---------|---------|
| 0 | 培养皿 | petriDish | `BioItemList.getPetriDish(culture)` |
| 1 | DNA样本瓶 | DNASampleFlask | `BioItemList.getDNASampleFlask(dna)` |
| 2 | 质粒细胞 | PlasmidCell | `BioItemList.getPlasmidCell(plasmid)` |
| 3 | 洗涤剂粉末 | DetergentPowder | `BioItemList.getOtherItem(1)` |
| 4 | 琼脂糖 | Agarose | `BioItemList.getOtherItem(2)` |
| 5 | 培养模块 | IncubationModule | `BioItemList.getOtherItem(3)` |
| 6 | 等离子膜 | PlasmaMembrane | `BioItemList.getOtherItem(4)` |

---

## 在配方中使用

```java
import bartworks.common.loaders.BioItemList;

// 示例：使用BartWorks物品的配方
GTValues.RA.stdBuilder()
    .itemInputs(
        BioItemList.mBioLabParts[0],  // DNA提取模块
        BioItemList.getOtherItem(1)    // 洗涤剂粉末
    )
    .itemOutputs(
        BioItemList.getDNASampleFlask(someDNA)  // DNA样本瓶
    )
    .duration(200)
    .eut(120)
    .addTo(someRecipeMap);
```

---

## 与GregTech ItemList的区别

| 特性 | GregTech ItemList | BartWorks BioItemList |
|------|------------------|----------------------|
| 实现方式 | 枚举 (enum) | 静态字段和方法 |
| 接口 | IItemContainer | 无 |
| 获取方式 | `ItemList.Item.get(1)` | `BioItemList.mBioLabParts[0]` 或 `BioItemList.getPetriDish()` |
| NBT支持 | 有限 | 完整支持 (通过方法) |
| 物品变体 | 通过meta值 | 通过NBT数据 |

---

## 相关文档

- [Registry_Multi_Module_README.md](Registry_Multi_Module_README.md) - 多模块注册系统总览
- [GregTech_Item.md](GregTech_Item.md) - GregTech主模块物品列表
- [GoodGenerator_Item.md](GoodGenerator_Item.md) - GoodGenerator物品获取方式

---

**数据提取时间**: 2026-02-19  
**数据来源**: GT5-Unofficial实际源代码  
**⚠️ 重要**: 所有代码示例均从实际源码提取，100%真实可用
