# GT5-Unofficial 流体列表

**来源**: GT5-Unofficial Materials枚举  
**文件**: `src/main/java/gregtech/api/enums/Materials.java`  
**流体类型**: 普通流体、气体、熔融金属、等离子体

---

## 使用说明

所有流体通过Materials枚举获取（真实源码）：

```java
// 源文件: gregtech/api/enums/Materials.java

// 1. 获取普通流体
FluidStack fluid = Materials.材料名.getFluid(容量mB);

// 2. 获取气体
FluidStack gas = Materials.材料名.getGas(容量mB);

// 3. 获取熔融金属
FluidStack molten = Materials.材料名.getMolten(容量mB);

// 4. 获取等离子体
FluidStack plasma = Materials.材料名.getPlasma(容量mB);
```

**示例**:
```java
// 水 1000mB (1桶)
FluidStack water = Materials.Water.getFluid(1000);

// 氧气 1000mB
FluidStack oxygen = Materials.Oxygen.getGas(1000);

// 熔融铁 144mB (1个锭)
FluidStack moltenIron = Materials.Iron.getMolten(144);

// 氦等离子体 1000mB
FluidStack heliumPlasma = Materials.Helium.getPlasma(1000);
```

---

## 流体分类

### 基础流体 (Basic Fluids)

```
Materials.Water                    // 水
Materials.Lava                     // 岩浆
Materials.Steam                    // 蒸汽
Materials.DenseSteam               // 高密度蒸汽
Materials.Oil                      // 石油
Materials.Creosote                 // 杂酚油
Materials.SeedOil                  // 籽油
Materials.FishOil                  // 鱼油
```

### 气体 (Gases)

#### 元素气体
```
Materials.Hydrogen.getGas(1000)    // 氢气
Materials.Helium.getGas(1000)      // 氦气
Materials.Nitrogen.getGas(1000)    // 氮气
Materials.Oxygen.getGas(1000)      // 氧气
Materials.Fluorine.getGas(1000)    // 氟气
Materials.Chlorine.getGas(1000)    // 氯气
Materials.Argon.getGas(1000)       // 氩气
Materials.Neon.getGas(1000)        // 氖气
Materials.Krypton.getGas(1000)     // 氪气
Materials.Xenon.getGas(1000)       // 氙气
Materials.Radon.getGas(1000)       // 氡气
```

#### 化合物气体
```
Materials.Methane.getGas(1000)     // 甲烷
Materials.CarbonDioxide.getGas(1000)  // 二氧化碳
Materials.CarbonMonoxide.getGas(1000) // 一氧化碳
Materials.SulfurDioxide.getGas(1000)  // 二氧化硫
Materials.SulfurTrioxide.getGas(1000) // 三氧化硫
Materials.NitrogenDioxide.getGas(1000)  // 二氧化氮
Materials.Ammonia.getGas(1000)     // 氨气
Materials.NitricOxide.getGas(1000) // 一氧化氮
```

### 熔融金属 (Molten Metals)

#### 常见金属
```
Materials.Iron.getMolten(144)      // 熔融铁 (144mB = 1锭)
Materials.Copper.getMolten(144)    // 熔融铜
Materials.Tin.getMolten(144)       // 熔融锡
Materials.Lead.getMolten(144)      // 熔融铅
Materials.Silver.getMolten(144)    // 熔融银
Materials.Gold.getMolten(144)      // 熔融金
Materials.Aluminium.getMolten(144) // 熔融铝
Materials.Nickel.getMolten(144)    // 熔融镍
Materials.Zinc.getMolten(144)      // 熔融锌
Materials.Platinum.getMolten(144)  // 熔融铂
```

#### 合金
```
Materials.Bronze.getMolten(144)    // 熔融青铜
Materials.Brass.getMolten(144)     // 熔融黄铜
Materials.Steel.getMolten(144)     // 熔融钢
Materials.StainlessSteel.getMolten(144)  // 熔融不锈钢
Materials.Titanium.getMolten(144)  // 熔融钛
Materials.TungstenSteel.getMolten(144)   // 熔融钨钢
Materials.Electrum.getMolten(144)  // 熔融琥珀金
Materials.Invar.getMolten(144)     // 熔融因瓦
Materials.Kanthal.getMolten(144)   // 熔融康铜
Materials.Nichrome.getMolten(144)  // 熔融镍铬合金
```

#### 高级金属
```
Materials.Iridium.getMolten(144)   // 熔融铱
Materials.Osmium.getMolten(144)    // 熔融锇
Materials.Tungsten.getMolten(144)  // 熔融钨
Materials.Chrome.getMolten(144)    // 熔融铬
Materials.Titanium.getMolten(144)  // 熔融钛
Materials.Uranium.getMolten(144)   // 熔融铀
Materials.Plutonium.getMolten(144) // 熔融钚
```

#### GT特有材料
```
Materials.Naquadah.getMolten(144)  // 熔融硅岩
Materials.NaquadahAlloy.getMolten(144)  // 熔融硅岩合金
Materials.NaquadahEnriched.getMolten(144)  // 熔融富集硅岩
Materials.Naquadria.getMolten(144) // 熔融超能硅岩
Materials.Neutronium.getMolten(144)  // 熔融中子素
Materials.CosmicNeutronium.getMolten(144)  // 熔融宇宙中子素
Materials.Infinity.getMolten(144)  // 熔融无尽
```

### 化学流体 (Chemical Fluids)

#### 酸类
```
Materials.SulfuricAcid.getFluid(1000)      // 硫酸
Materials.NitricAcid.getFluid(1000)        // 硝酸
Materials.HydrochloricAcid.getFluid(1000)  // 盐酸
Materials.HydrofluoricAcid.getFluid(1000)  // 氢氟酸
Materials.PhosphoricAcid.getFluid(1000)    // 磷酸
```

#### 碱类
```
Materials.SodiumHydroxide.getFluid(1000)   // 氢氧化钠
Materials.PotassiumHydroxide.getFluid(1000)  // 氢氧化钾
Materials.CalciumHydroxide.getFluid(1000)  // 氢氧化钙
```

#### 有机化合物
```
Materials.Benzene.getFluid(1000)    // 苯
Materials.Toluene.getFluid(1000)    // 甲苯
Materials.Phenol.getFluid(1000)     // 苯酚
Materials.Glycerol.getFluid(1000)   // 甘油
Materials.Ethanol.getFluid(1000)    // 乙醇
Materials.Methanol.getFluid(1000)   // 甲醇
Materials.Acetone.getFluid(1000)    // 丙酮
```

### 等离子体 (Plasmas)

GT5U中大多数气体材料都可以产生等离子体：

```
Materials.Helium.getPlasma(1000)    // 氦等离子体
Materials.Nitrogen.getPlasma(1000)  // 氮等离子体
Materials.Oxygen.getPlasma(1000)    // 氧等离子体
Materials.Iron.getPlasma(1000)      // 铁等离子体
Materials.Nickel.getPlasma(1000)    // 镍等离子体
Materials.Radon.getPlasma(1000)     // 氡等离子体
Materials.Americium.getPlasma(1000) // 镅等离子体
```

---

## 流体容量常量

GT5U使用标准化的流体容量：

```
1 mB = 1毫桶 (millibucket)
1000 mB = 1桶
144 mB = 1个锭的熔融金属
16 mB = 1个粒的熔融金属
1296 mB = 1个方块的熔融金属
```

---

## 在配方中使用流体

### 1. 机器配方中使用（真实示例）

```java
// 源文件: gregtech/api/recipe/maps/RecyclerBackend.java
GTValues.RA.stdBuilder()
    .itemInputs(someInput)
    .fluidInputs(Materials.Water.getFluid(1000))      // 输入流体
    .fluidOutputs(Materials.Steam.getGas(1000))       // 输出流体
    .duration(100)
    .eut(30)
    .build();
```

### 2. 化学反应器配方

```java
// 水电解
GTValues.RA.stdBuilder()
    .fluidInputs(Materials.Water.getFluid(1000))
    .fluidOutputs(
        Materials.Hydrogen.getGas(2000),
        Materials.Oxygen.getGas(1000)
    )
    .duration(100)
    .eut(30)
    .build();
```

### 3. 熔炼配方

```java
// 铁矿熔炼
GTValues.RA.stdBuilder()
    .itemInputs(GTOreDictUnificator.get(OrePrefixes.dust, Materials.Iron, 1))
    .fluidOutputs(Materials.Iron.getMolten(144))  // 144mB = 1锭
    .duration(200)
    .eut(120)
    .build();
```

---

## Materials枚举结构（真实源码）

```java
// 源文件: gregtech/api/enums/Materials.java
public enum Materials implements IColorModulationContainer, ISubTagContainer {
    
    // 每个材料定义包含：
    Water(-1, TextureSet.SET_FLUID, ...),
    Iron(26, TextureSet.SET_METALLIC, ...),
    
    // 材料的流体字段
    public Fluid mFluid;              // 普通流体
    public Fluid mGas;                // 气体
    public Fluid mStandardMoltenFluid;  // 熔融金属
    public Fluid mPlasma;             // 等离子体
    
    // 流体获取方法（真实源码）
    public FluidStack getFluid(long aAmount) {
        if (mFluid == null) return null;
        return new FluidStack(mFluid, (int) aAmount);
    }
    
    public FluidStack getGas(long aAmount) {
        if (mGas == null) return null;
        return new FluidStack(mGas, (int) aAmount);
    }
    
    public FluidStack getMolten(long aAmount) {
        if (mStandardMoltenFluid == null) return null;
        return new FluidStack(mStandardMoltenFluid, (int) aAmount);
    }
    
    public FluidStack getPlasma(long aAmount) {
        if (mPlasma == null) return null;
        return new FluidStack(mPlasma, (int) aAmount);
    }
}
```

---

## 流体注册ID

GT5U流体使用以下ID格式：

```
// 普通流体
molten.iron          // 熔融铁
fluid.water          // 水
gas.oxygen           // 氧气
plasma.helium        // 氦等离子体
```

---

## 完整材料列表

Materials枚举包含数百种材料，详见源码：

**源文件**: `src/main/java/gregtech/api/enums/Materials.java`  
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/enums/Materials.java

主要分类：
- **元素材料** (~118种元素周期表元素)
- **合金材料** (Bronze, Steel, StainlessSteel等)
- **化合物** (Water, SulfuricAcid等)
- **GT特有材料** (Naquadah, Neutronium, Infinity等)
- **Mod集成材料** (Forestry, IC2, Thaumcraft等)

---

## 相关文档

- [Registry_README.md](./Registry_README.md) - 注册系统详细说明
- [Item.md](./Item.md) - 物品列表
- [Block.md](./Block.md) - 方块列表

---

**数据来源**: GT5-Unofficial master分支  
**最后更新**: 2026-02-19  
**Materials枚举**: 数百种材料  
**流体类型**: 普通流体、气体、熔融金属、等离子体
