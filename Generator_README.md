# GT5-Unofficial 发电机完全指南

> **代码库路径**：`/tmp/GT5-Unofficial/src/main/java/`（已完整克隆）  
> **覆盖模块**：gregtech · gtPlusPlus · goodgenerator · bartworks · kekztech · gtnhintergalactic  
> **共计**：~20 种单方块发电机 + ~25 种多方块发电机

---

## 0. 发电机 vs 耗电机器：核心区别

### 0.1 单方块发电机能量输出机制

所有单方块发电机继承 `MTEBasicGenerator`。其能量输出核心在 `onPostTick` 中通过
`increaseStoredEnergyUnits` 将 EU 写入自身内部缓存，再由能量网络框架从输出面抽走：

```java
// gregtech/api/metatileentity/implementations/MTEBasicGenerator.java:188-226
@Override
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    if (mFluid != null) {
        long tFuelValue = getFuelValue(mFluid), tConsumed = consumedFluidPerOperation(mFluid);
        if (tFuelValue > 0 && tConsumed > 0 && mFluid.amount >= tConsumed) {
            long tFluidAmountToUse = Math.min(
                mFluid.amount / tConsumed,
                (maxEUStore() - aBaseMetaTileEntity.getUniversalEnergyStored()) / tFuelValue);
            if (tFluidAmountToUse > 0L
                && aBaseMetaTileEntity.increaseStoredEnergyUnits(tFluidAmountToUse * tFuelValue, true)) {
                mFluid.amount -= tFluidAmountToUse * tConsumed; // 消耗流体
            }
        }
    }
    // 固体燃料处理（省略）...
    aBaseMetaTileEntity.setActive(
        aBaseMetaTileEntity.isAllowedToWork()
            && aBaseMetaTileEntity.getUniversalEnergyStored() >= maxEUOutput() + getMinimumStoredEU());
}

// 声明为电能输出设备（不是消费者）
@Override
public boolean isEnetOutput() { return true; }  // :136

// 输出电压 = 对应 tier 的基础电压
@Override
public long maxEUOutput() { return V[mTier]; }  // :146
```

**与耗电机器的对比**：

| 特性 | 发电机 | 耗电机器 |
|------|--------|----------|
| `isEnetOutput()` | `true` | `false` |
| `isEnetInput()` | `false` | `true` |
| 能量方向 | 向外推送 | 从外拉取 |
| `maxEUOutput()` | 返回 tier 电压 | 返回 0 |
| `maxEUInput()` | 返回 0 | 返回 tier 电压 |

### 0.2 多方块发电机能量输出机制

多方块发电机通过 **动力仓（`MTEHatchDynamo`）** 向外输出：

```java
// gregtech/api/metatileentity/implementations/MTEHatchDynamo.java:49-69
@Override
public boolean isEnetOutput() { return true; }

@Override
public boolean isOutputFacing(ForgeDirection side) {
    return side == getBaseMetaTileEntity().getFrontFacing();
}

@Override
public long maxEUOutput() { return V[mTier]; }  // :64

@Override
public long maxEUStore() { return 512L + V[mTier + 1] * 2L; }  // :69
```

多方块控制器在 `onRunningTick` 中调用 `addEnergyOutput`，最终通过 `addEnergyOutputMultipleDynamos`
将 EU 写入动力仓的内部缓存：

```java
// gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java:1015-1022
public boolean onRunningTick(ItemStack aStack) {
    if (mEUt > 0) {
        // mEUt > 0 表示发电机模式，乘以效率后输出
        addEnergyOutput(((long) mEUt * mEfficiency) / 10000);
        return true;
    }
    if (mEUt < 0) {
        // mEUt < 0 表示耗电机器模式
        if (!drainEnergyInput(getActualEnergyUsage())) { stopMachine(...); }
    }
}

// :1501-1575（简化）
public boolean addEnergyOutputMultipleDynamos(long aEU, boolean aAllowMixedVoltageDynamos) {
    // 验证总容量是否足够
    if (totalOutput < aEU) { explodeMultiblock(); return false; }
    // 按电压分包写入每个动力仓
    for (MTEHatch aDynamo : validMTEList(mDynamoHatches)) {
        long aVoltage = aDynamo.maxEUOutput();
        int aAmpsToInject = (int)(leftToInject / aVoltage);
        for (int i = 0; i < ampsOnCurrentHatch; i++) {
            aDynamo.getBaseMetaTileEntity().increaseStoredEnergyUnits(aVoltage, false); // 写入EU
        }
    }
}
```

**关键规则**：若 `mEUt > 0` → 发电；若 `mEUt < 0` → 耗电。多方块通过 `checkProcessing()` 返回
`CheckRecipeResultRegistry.GENERATING` 来设置正的 `mEUt`。

---

## 1. gregtech 模块单方块发电机

### 1.1 太阳能发电机 `MTESolarGenerator`

**代码路径**：`gregtech/common/tileentities/generators/MTESolarGenerator.java`  
**中文名**：太阳能板（LV～UV 各等级）

**工作方式**：每 20 tick（1秒）检查以下条件，全部满足则充电：
1. 白天（`world.isDaytime()`）
2. 不在下雨（或生物群系不受雨影响）
3. 能看到天空（`getSkyAtSide(UP)`）

```java
// MTESolarGenerator.java:189-199
@Override
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    if (aBaseMetaTileEntity.isServerSide()) {
        if (aTick % 100 == 0) { doWorldChecks(aBaseMetaTileEntity.getWorld(), aBaseMetaTileEntity); }
        if (aTick % 20 == 0 && valid) {
            // 每秒充入 maxEUOutput() * 20 EU
            aBaseMetaTileEntity.increaseStoredEnergyUnits(maxEUOutput() * 20, false);
        }
    }
    super.onPostTick(aBaseMetaTileEntity, aTick);
}

@Override
public boolean isEnetOutput() { return true; }  // :261

@Override
public long maxEUOutput() { return GTValues.V[mTier]; }  // :256

@Override
public boolean isOutputFacing(ForgeDirection side) {
    return side == getBaseMetaTileEntity().getFrontFacing();  // :271（前面输出）
}
```

**输出**：每 tick 输出 `V[mTier]` EU/t，无污染，无燃料消耗。

---

### 1.2 柴油发电机 `MTEDieselGenerator`

**代码路径**：`gregtech/common/tileentities/generators/MTEDieselGenerator.java`  
**中文名**：柴油发电机（LV～IV）  
**配方图**：`RecipeMaps.dieselFuels`

```java
// MTEDieselGenerator.java:86-87
@Override
public int getEfficiency() { return this.efficiency; }  // 由构造函数传入

// 输出面 = 前面
@Override
public boolean isOutputFacing(ForgeDirection side) {
    return side == getBaseMetaTileEntity().getFrontFacing();
}
```

**工作方式**：继承 `MTEBasicGenerator`，每 tick 调用 `onPostTick`（参见 0.1 节），
计算 `tFuelValue / tConsumed` 后通过 `increaseStoredEnergyUnits` 充入内部缓存。

---

### 1.3 燃气轮机 `MTEGasTurbine`（单方块）

**代码路径**：`gregtech/common/tileentities/generators/MTEGasTurbine.java`  
**中文名**：燃气轮机（LV～IV）  
**配方图**：`RecipeMaps.gasTurbineFuels`

```java
// MTEGasTurbine.java:70-76
@Override
public RecipeMap<?> getRecipeMap() { return RecipeMaps.gasTurbineFuels; }

@Override
public int getEfficiency() { return this.efficiency; }
```

工作机制与柴油发电机相同，区别在于燃料类型不同（使用气态燃料）。

---

### 1.4 蒸汽轮机 `MTESteamTurbine`（单方块）

**代码路径**：`gregtech/common/tileentities/generators/MTESteamTurbine.java`  
**中文名**：蒸汽轮机（LV～IV）  
**配方图**：`RecipeMaps.steamTurbineFuels`

```java
// MTESteamTurbine.java:80-86
@Override
public int getCapacity() { return 24000 * this.mTier; }  // 流体容量

@Override
public int getEfficiency() { return 6 + this.mTier; }  // tier 1=7, tier 2=8...
```

效率随 tier 提升：tier 1 → 7%（相对），tier 2 → 8% 等。

---

### 1.5 等离子体发电机 `MTEPlasmaGenerator`

**代码路径**：`gregtech/common/tileentities/generators/MTEPlasmaGenerator.java`  
**中文名**：等离子体发电机（LV～UV）  
**配方图**：`RecipeMaps.plasmaFuels`

```java
// MTEPlasmaGenerator.java:106-112
@Override
public RecipeMap<?> getRecipeMap() { return RecipeMaps.plasmaFuels; }

@Override
public int getEfficiency() {
    return Math.max(10, 10 + Math.min(90, this.mTier * 10));
    // tier 1 → 20%, tier 5 → 60%, tier 9 → 100%
}
```

**输出面**：仅前面（`side == getFrontFacing()`）。

---

### 1.6 钠克达反应堆 `MTENaquadahReactor`（单方块）

**代码路径**：`gregtech/common/tileentities/generators/MTENaquadahReactor.java`  
**中文名**：钠克达反应堆（HV～UV+，tier 4~8）  
**配方图**：按 tier 选择 `smallNaquadahReactorFuels` / `largeNaquadahReactorFuels` / `hugeNaquadahReactorFuels` / `extremeNaquadahReactorFuels` / `ultraHugeNaquadahReactorFuels`

```java
// MTENaquadahReactor.java:66-85
@Override
public RecipeMap<?> getRecipeMap() {
    return switch (mTier) {
        case 4 -> RecipeMaps.smallNaquadahReactorFuels;
        case 5 -> RecipeMaps.largeNaquadahReactorFuels;
        case 6 -> RecipeMaps.hugeNaquadahReactorFuels;
        case 7 -> RecipeMaps.extremeNaquadahReactorFuels;
        case 8 -> RecipeMaps.ultraHugeNaquadahReactorFuels;
        default -> null;
    };
}

@Override
public int getEfficiency() {
    return mTier == 4 ? 80 : 100 + (50 * (mTier - 5));
    // tier 4: 80%, tier 5: 100%, tier 6: 150%, tier 7: 200%, tier 8: 250%
}

// 输出面：两侧面（不包括顶面底面、不包括前面后面）
@Override
public boolean isOutputFacing(ForgeDirection side) {
    return ((side.flag & (ForgeDirection.UP.flag | ForgeDirection.DOWN.flag)) == 0)
        && side != getBaseMetaTileEntity().getFrontFacing()
        && side != getBaseMetaTileEntity().getBackFacing();
}
```

---

### 1.7 魔法能源转换器 `MTEMagicEnergyConverter`

**代码路径**：`gregtech/common/tileentities/generators/MTEMagicEnergyConverter.java`  
**中文名**：魔法能源转换器（LV～IV）  
**配方图**：`RecipeMaps.magicFuels`

```java
// MTEMagicEnergyConverter.java:44-50
@Override
public RecipeMap<?> getRecipeMap() { return RecipeMaps.magicFuels; }

@Override
public int getEfficiency() { return 100 - this.mTier * 5; }
// tier 1: 95%, tier 2: 90%, tier 3: 85%, tier 4: 80%
```

---

### 1.8 魔法能量吸收器 `MTEMagicalEnergyAbsorber`

**代码路径**：`gregtech/common/tileentities/generators/MTEMagicalEnergyAbsorber.java`  
**中文名**：魔法能量吸收器（LV～IV）  
依赖：Thaumcraft，通过吸收 Vis（魔力）和 Essentia（精华）及末影水晶产生 EU。

```java
// MTEMagicalEnergyAbsorber.java:434-435
@Override
public int getEfficiency() { return 100; }

// 从 Vis 产生 EU 的核心
// :561
tEU = Math.min(maxEUOutput(), (long) drained * drained * sEnergyFromVis * getEfficiency() / 10000);
```

---

### 1.9 雷电棒 `MTELightningRod`

**代码路径**：`gregtech/common/tileentities/generators/MTELightningRod.java`  
**中文名**：雷电收集棒

**工作方式**：在雷雨天气随机触发闪电，将满量 EU 充入内部缓存，同时在世界中产生闪电效果。
需要在上方堆叠铁栅栏作为"导体"，高度越高概率越大。

```java
// MTELightningRod.java:63-96（精简）
public void onPostTick(IGregTechTileEntity aBaseMetaTileEntity, long aTick) {
    if (aTick % 256 == 0 && (aWorld.isThundering() || (aWorld.isRaining() && XSTR_INSTANCE.nextInt(10) == 0))) {
        // 计算上方铁栅栏高度 aRodValue
        if (XSTR_INSTANCE.nextInt(4 * aWorld.getHeight()) < (aRodValue * (aY + aRodValue))) {
            // 一次性充满
            aBaseMetaTileEntity.increaseStoredEnergyUnits(maxEUStore() - aBaseMetaTileEntity.getStoredEU(), false);
            aWorld.addWeatherEffect(new EntityLightningBolt(aWorld, aX, aY + aRodValue, aZ));
        }
    }
}

@Override
public boolean isEnetOutput() { return true; }   // :130

@Override
public long maxEUOutput() { ... }  // :140
```

---

## 2. gregtech 模块多方块发电机

### 2.1 大型锅炉系列 `MTELargeBoiler`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeBoiler.java`  
**子类**：`MTELargeBoilerBronze` / `MTELargeBoilerSteel` / `MTELargeBoilerTitanium` / `MTELargeBoilerTungstenSteel`  
**注意**：大型锅炉**不直接产生 EU**，而是将燃料能量转换为**蒸汽（Steam）或超热蒸汽（Superheated Steam）**输出，蒸汽再由蒸汽轮机或锅炉外的机器使用。

| 型号 | Steam 产量 | EUt 等效 | 是否 SH Steam |
|------|-----------|---------|--------------|
| 铜制 Bronze | 400 EUt equiv | 400 | 否 |
| 钢铁 Steel | 1000 EUt equiv | 1000 | 否 |
| 钛金 Titanium | 4000 EUt equiv | 4000 | 是 |
| 钨钢 TungstenSteel | 16000 EUt equiv | 16000 | 是 |

```java
// MTELargeBoilerBronze.java:22
public static final int EUT_GENERATED = 400;

// MTELargeBoilerTitanium.java:22
public static final int EUT_GENERATED = 4000;

// MTELargeBoilerTungstenSteel.java:22
public static final int EUT_GENERATED = 16000;
```

**蒸汽输出机制**（`MTELargeBoiler.java:377-409`）：

```java
// 将 tGeneratedEU（即 getEUt() * 实际运行时间）转换为蒸汽量
long amount = (tGeneratedEU + STEAM_PER_WATER) / STEAM_PER_WATER;
// 1L 水 = STEAM_PER_WATER L 蒸汽（默认 160）

if (isSuperheated()) {
    // 钛/钨钢锅炉：输出 1/3 超热蒸汽（等效热量相同）
    if (depleteInput(Materials.Water.getFluid(amount / superToNormalSteam))
        || depleteInput(GTModHandler.getDistilledWater(amount / superToNormalSteam))) {
        addOutput(FluidRegistry.getFluidStack("ic2superheatedsteam", tGeneratedEU / superToNormalSteam));
    }
} else {
    // 铜/钢锅炉：输出普通蒸汽
    addOutput(Materials.Steam.getGas(tGeneratedEU));
}
```

`mEUt` 在 `checkProcessing` 中被正值设置（等同于 `getEUt()`），触发 `onRunningTick → addEnergyOutput`，
**但大型锅炉不连接动力仓，而是将能量用于驱动蒸汽输出运算**。实际上它在 `onRunningTick` 中不产生 EU，
而是在 `onRunningTick` 调用到的特殊流体处理逻辑里直接 `addOutput(steam)`。

---

### 2.2 大型燃油引擎 `MTEDieselEngine`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTEDieselEngine.java`  
**中文名**：大型柴油引擎  
**结构尺寸**：3×3×4

```java
// MTEDieselEngine.java:199-219
protected int getNominalOutput() { return 2048; }   // 基础输出 2048 EU/t

protected int getBoostFactor() { return 2; }        // 氧气加速倍数（3倍输出）

protected int getAdditiveFactor() { return 1; }     // 添加剂系数
```

**工作方式**（`checkProcessing` 第 231-291 行）：
1. 遍历输入仓中的柴油类燃料（`RecipeMaps.dieselFuels`）
2. 计算燃料消耗量：`fuelConsumption = getNominalOutput() / fuelValue`
3. 检测是否提供 2L 氧气（`Materials.Oxygen.getGas(2L)`），有则进入 **Boost 模式**（3× 输出）
4. 每 72 tick 消耗 1L 润滑油（不满足则停机）
5. 设置 `this.mEUt = getNominalOutput()`（正值 → 发电）

```java
// :282,286
this.mEUt = mEfficiency < 2000 ? 0 : getNominalOutput(); // 效率低于 20% 时不输出
return CheckRecipeResultRegistry.GENERATING;
```

**输出机制**：`mEUt > 0` → `onRunningTick` 调用 `addEnergyOutput((long)mEUt * mEfficiency / 10000)` →
`addEnergyOutputMultipleDynamos` → 写入后方动力仓缓存。

---

### 2.3 极限柴油引擎 `MTEExtremeDieselEngine`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTEExtremeDieselEngine.java`  
**中文名**：极限柴油引擎（Combustion Generator, ECE）  
继承自 `MTEDieselEngine`，覆写以下参数：

```java
// MTEExtremeDieselEngine.java:67-138（关键覆写）
@Override
public RecipeMap<FuelBackend> getRecipeMap() {
    return RecipeMaps.extremeDieselFuels;  // 使用极限柴油燃料
}

@Override
protected int getNominalOutput() {
    // 默认 10900 EU/t，Boost 后 32700 EU/t
    return ...; // 约 10900
}
```

**Default**：10900 EU/t；**Boosted**（液氧）：32700 EU/t。  
需要 8000L/h 润滑油，40L/s 液氧（可选 boost）。

---

### 2.4 大型涡轮基类 `MTELargeTurbine`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeTurbine.java`  
**结构尺寸**：3×3×4

大型涡轮通过 `checkProcessing` 调用 `fluidIntoPower` 方法计算输出功率，然后设置 `mEUt`：

```java
// MTELargeTurbine.java（checkProcessing 精简版）
@Override
public CheckRecipeResult checkProcessing() {
    int newPower = fluidIntoPower(getStoredFluids(), new TurbineStatCalculator(turbine));
    if (newPower > 0) {
        this.mEUt = newPower;              // 正值 → 发电
        this.mMaxProgresstime = 20;
        this.mEfficiencyIncrease = 200;
        return CheckRecipeResultRegistry.GENERATING;
    }
    return CheckRecipeResultRegistry.NO_FUEL_FOUND;
}
```

每种涡轮子类实现自己的 `fluidIntoPower`，根据转子参数（`TurbineStatCalculator`）和流量计算 EU/t。

---

### 2.5 蒸汽大型涡轮 `MTELargeTurbineSteam`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeTurbineSteam.java`  
**机型代号**：LST  
**燃料**：蒸汽（Steam）  
**副产品**：蒸馏水（Distilled Water）

```java
// MTELargeTurbineSteam.java:fluidIntoPower（精简）
int fluidIntoPower(ArrayList<FluidStack> aFluids, TurbineStatCalculator turbine) {
    this.realOptFlow = looseFit ? turbine.getOptimalLooseSteamFlow() : turbine.getOptimalSteamFlow();
    // 允许使用最多 (1 + 0.5 * overflowMultiplier) 倍最优流量
    int remainingFlow = GTUtility.safeInt((long)(realOptFlow * (0.5f * turbine.getOverflowEfficiency() + 1)));

    for (FluidStack aFluidStack : aFluids) {
        if (GTModHandler.isAnySteam(aFluidStack)) {
            flow = Math.min(aFluidStack.amount, remainingFlow);
            depleteInput(new FluidStack(aFluidStack, flow)); // 消耗蒸汽
            totalFlow += flow;
        }
    }

    int waterToOutput = condenseSteam(totalFlow);
    addOutput(GTModHandler.getDistilledWater(waterToOutput)); // 输出蒸馏水

    // 计算最终 EU/t，乘以效率系数
    tEU = GTUtility.safeInt((long)(tEU * turbine.getSteamEfficiency() * 0.5f));
    if (tEU > getMaximumOutput()) tEU = GTUtility.safeInt(getMaximumOutput());
    return tEU;
}

// 蒸汽冷凝为蒸馏水（有精度累计）
private int condenseSteam(int steam) {
    excessWater += steam;
    int water = excessWater / STEAM_PER_WATER;
    excessWater %= STEAM_PER_WATER;
    return water;
}
```

---

### 2.6 超热蒸汽大型涡轮 `MTELargeTurbineHPSteam`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeTurbineHPSteam.java`  
**燃料**：超热蒸汽（Superheated Steam）  
**副产品**：普通蒸汽（Steam）  
**机壳**：钛金涡轮机壳（`getCasingMeta() = 11`）

```java
// MTELargeTurbineHPSteam.java:fluidIntoPower（精简）
int fluidIntoPower(ArrayList<FluidStack> aFluids, TurbineStatCalculator turbine) {
    // 允许 (1.5 + 0.5 * overflowMultiplier) 倍最优流量
    int remainingFlow = GTUtility.safeInt((long)(realOptFlow * (0.5f * turbine.getOverflowEfficiency() + 1.5)));

    for (FluidStack aFluidStack : aFluids) {
        if (GTModHandler.isSuperHeatedSteam(aFluidStack)) {
            flow = Math.min(aFluidStack.amount, remainingFlow);
            depleteInput(new FluidStack(aFluidStack, flow));
            totalFlow += flow;
        } else if (GTModHandler.isAnySteam(aFluidStack)) {
            depleteInput(new FluidStack(aFluidStack, aFluidStack.amount)); // 丢弃普通蒸汽
        }
    }

    addOutput(Materials.Steam.getGas(totalFlow)); // 输出等量普通蒸汽

    // overflowEfficiency 公式（超热蒸汽溢出惩罚比普通蒸汽更宽松）
    // efficiency = 1.0f - abs(totalFlow - optFlow) / (optFlow * (overflowMultiplier + 2))
    return tEU;
}
```

---

### 2.7 燃气大型涡轮 `MTELargeTurbineGas`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeTurbineGas.java`  
**机型代号**：LGT  
**燃料**：气态燃料（`RecipeMaps.gasTurbineFuels`）  
**机壳**：不锈钢涡轮机壳（`getCasingMeta() = 10`）  
**特殊**：需要空气进气区域（控制器前方 3×3 空旷区域）

```java
// MTELargeTurbineGas.java:fluidIntoPower（精简）
int fluidIntoPower(ArrayList<FluidStack> aFluids, TurbineStatCalculator turbine) {
    FluidStack firstFuelType = new FluidStack(aFluids.get(0), 0); // 只处理第一种燃料
    int fuelValue = getFuelValue(firstFuelType);

    if (turbine.getOptimalGasEUt() < fuelValue) {
        // 转子太弱/燃料太强：仅消耗 1L，直接输出最优 EU/t
        this.realOptFlow = 1;
        depleteInput(new FluidStack(firstFuelType, 1));
        return GTUtility.safeInt((long)turbine.getOptimalGasEUt());
    }

    actualOptimalFlow = GTUtility.safeInt(
        (long)((looseFit ? turbine.getOptimalLooseGasFlow() : turbine.getOptimalGasFlow()) / fuelValue));

    // totalFlow 范围：允许最多 (1.5 * overflowMultiplier) 倍最优流量
    tEU = GTUtility.safeInt((long)totalFlow * fuelValue);
    tEU = GTUtility.safeInt((long)(tEU * turbine.getGasEfficiency()));
    return tEU;
}
```

---

### 2.8 等离子体大型涡轮 `MTELargeTurbinePlasma`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTELargeTurbinePlasma.java`  
**机型代号**：LPT  
**燃料**：等离子体（`RecipeMaps.plasmaFuels`）  
**副产品**：对应的熔融液体（如 `helium.plasma` → `molten.helium`）  
**机壳**：钨钢涡轮机壳（`getCasingMeta() = 12`）  
**特殊**：每 20 tick 运行一次（`mMaxProgresstime = 20`）

```java
// MTELargeTurbinePlasma.java:fluidIntoPower（精简）
int fluidIntoPower(ArrayList<FluidStack> aFluids, TurbineStatCalculator turbine) {
    FluidStack firstFuelType = new FluidStack(aFluids.get(0), 0);
    int fuelValue = getFuelValue(firstFuelType);  // 从 RecipeMaps.plasmaFuels 查找 mSpecialValue

    actualOptimalFlow = GTUtility.safeInt((long)Math.ceil(
        (double)(turbine.getOptimalPlasmaFlow()) * 20 / (double)fuelValue));
    this.realOptFlow = actualOptimalFlow;

    // 消耗等离子体后输出对应熔融液体
    String fn = FluidRegistry.getFluidName(firstFuelType);
    String[] nameSegments = fn.split("\\.", 2); // "plasma.helium" → ["plasma", "helium"]
    if (nameSegments.length == 2) {
        FluidStack output = FluidRegistry.getFluidStack(nameSegments[1], totalFlow);  // "helium"
        if (output == null) output = FluidRegistry.getFluidStack("molten." + nameSegments[1], totalFlow);
        if (output != null) addOutput(output);
    }

    tEU = GTUtility.safeInt((long)((fuelValue / 20D) * (double)totalFlow));
    tEU = GTUtility.safeInt((long)(turbine.getPlasmaEfficiency() * tEU));
    return tEU;
}

// 等离子体涡轮的溢流效率公式（最宽松）
// efficiency = 1.0f - abs(totalFlow - optFlow) / (optFlow * (overflowMultiplier * 3 + 1))

@Override
public CheckRecipeResult checkProcessing() {
    CheckRecipeResult status = super.checkProcessing();
    if (status == CheckRecipeResultRegistry.GENERATING) {
        this.mMaxProgresstime = 20;   // 20 tick 一次（1秒周期）
        this.mEfficiencyIncrease = 200;
    }
    return status;
}
```

---

### 2.9 虫洞发生器 `MTEWormholeGenerator`

**代码路径**：`gregtech/common/tileentities/machines/multi/MTEWormholeGenerator.java`  
**机型代号**：MWG  
**注意**：虫洞发生器**不是传统意义上的发电机**，它的功能是在两个配对的虫洞之间
**传输 EU**（效率约 99.5%），需要 AE2 纠缠奇点配对，通过激光能源仓输入/输出。

```java
// MTEWormholeGenerator.java:969-972（tooltip）
tt.addMachineType("Wormhole Generator, MWG")
    .addInfo("Transfers EU between two wormhole generators")  // 传输而非生产

// :660-661（传输逻辑）
inputHatch.setEUVar(inputHatch.getEUVar() - toSend);   // 从输入仓扣除
outputHatch.setEUVar(outputHatch.getEUVar() + toReceive); // 写入对端输出仓
// toReceive = toSend * TRANSFER_EFFICIENCY (0.995)
```

**结构**：7×9×7，需要 AE2 高能玻璃、融合线圈、激光源仓和激光目标仓。

---

## 3. gtPlusPlus 模块单方块发电机

### 3.1 地热发电机 `MTEGeothermalGenerator`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/generators/MTEGeothermalGenerator.java`  
**配方图**：`RecipeMaps.hotFuels`（包括 Pahoehoe 熔岩和普通熔岩）

```java
// MTEGeothermalGenerator.java:35-54
@Override
public int getCapacity() { return 5000 * this.mTier; }

@Override
public int getEfficiency() { return 100 - (this.mTier * 7); }
// tier 1: 93%, tier 2: 86%, tier 3: 79%...

@Override
public int getFuelValue(final ItemStack aStack) {
    // 燃料值 = max(GTModHandler 燃料值 * 1.2, 基类燃料值)
    int rValue = Math.max((GTModHandler.getFuelValue(aStack) * 6) / 5, super.getFuelValue(aStack));
    return rValue;
}

@Override
public RecipeMap<?> getRecipeMap() { return RecipeMaps.hotFuels; }
```

---

### 3.2 半流体发电机 `MTESemiFluidGenerator`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/generators/MTESemiFluidGenerator.java`  
**配方图**：`GTPPRecipeMaps.semiFluidFuels`（焦油、重油等半流体燃料）

```java
// MTESemiFluidGenerator.java:44-47
@Override
public RecipeMap<?> getRecipeMap() { return GTPPRecipeMaps.semiFluidFuels; }

@Override
public int getEfficiency() { return 100 - (this.mTier * 5); }
// 输出面：前面
@Override
public boolean isOutputFacing(ForgeDirection side) {
    return (side == getBaseMetaTileEntity().getFrontFacing());
}
```

---

### 3.3 火箭燃料发电机 `MTERocketFuelGenerator`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/generators/MTERocketFuelGenerator.java`  
**基类**：`MTERocketFuelGeneratorBase`  
**配方图**：`GTPPRecipeMaps.rocketFuels`

```java
// MTERocketFuelGenerator.java:37-40
@Override
public RecipeMap<?> getRecipeMap() { return GTPPRecipeMaps.rocketFuels; }

@Override
public int getEfficiency() {
    return 80 - (10 * (this.mTier - 4));
    // tier 4: 80%, tier 5: 70%, tier 6: 60%
}
```

---

### 3.4 RTG 发电机 `MTERTGenerator`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/generators/MTERTGenerator.java`  
**中文名**：放射性同位素热电发电机  
**配方图**：`GTPPRecipeMaps.rtgFuels`  
**燃料**：RTG 颗粒（Am-241、Pu-238、Po-210、Sr-90）

**工作方式**：RTG 燃料颗粒一次性放入后即被消耗，其携带的全部 EU 一次性写入发电机内部缓存，
再由 `maxEUOutput()` 以固定电压慢慢向外输出。电压由燃料配方的 `mEUt` 字段决定（非固定 tier）。

```java
// MTERTGenerator.java:49-51
// 注：公式使用 20（tick/秒）× 86400（秒/真实日），即按真实世界天换算 tick 数
// mDayTick < 24000 则跟踪游戏内天（1 MC日 = 24000 tick），两者单位不同
// （源码注释 "// Generates fuel value based on MC days"，但公式实为真实日刻度）
public static int convertDaysToTicks(float days) {
    return MathUtils.roundToClosestInt(20 * 86400 * days);
}

// :323-329（getFuelValue 核心）
@Override
public int getFuelValue(ItemStack aStack) {
    GTRecipe tFuel = getRecipeMap().findRecipeQuery().items(aStack).find();
    if (tFuel != null) {
        int voltage = tFuel.mEUt;                           // 从配方读取输出电压
        this.mVoltage = voltage;                             // 动态设置输出电压
        this.mTicksToBurnFor = getTotalEUGenerated(convertDaysToTicks(tFuel.mSpecialValue), voltage);
        this.mDaysRemaining = MathUtils.roundToClosestInt(mTicksToBurnFor / 20 / 60 / 3); // 剩余天数计数器
        return (int)(mTicksToBurnFor * getEfficiency() / 100L); // 返回值 = 一次性写入缓存的总 EU
    }
}

// 输出电压由燃料配方决定（动态），而非固定 tier
@Override
public long maxEUOutput() {
    return (getBaseMetaTileEntity().isAllowedToWork()) ? this.mVoltage : 0L;
}
```

**RTG 燃料颗粒参数**（来源：`MetaGeneratedGregtechItems.java:329-363`）：

| 颗粒 | `mSpecialValue` | 电压（`mEUt`） |
|------|----------------|-------------|
| Pu-238 RTG Pellet | 87.7 | MV (512 EU/t) |
| Sr-90 RTG Pellet | 28.8 | LV (32 EU/t) |
| Po-210 RTG Pellet | 1 | HV (2048 EU/t) |
| Am-241 RTG Pellet | 216 | LV/2 (16 EU/t) |

**输出面**：两侧面（左右），不包括前后面和顶底面：
```java
// :155-158
@Override
public boolean isOutputFacing(ForgeDirection side) {
    return (side.offsetY == 0)
        && (side != getBaseMetaTileEntity().getFrontFacing())
        && (side != getBaseMetaTileEntity().getBackFacing());
}
```

---

### 3.5 GT++ 高级锅炉系列 `MTEAdvancedBoilerBase`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/generators/MTEAdvancedBoilerBase.java`  
**子类**：`MTEAdvancedBoilerLV`（tier 1）/ `MTEAdvancedBoilerMV`（tier 2）/ `MTEAdvancedBoilerHV`（tier 3）  
**特点**：使用固体燃料（非流体），**不会因缺水而爆炸**，burn time > 500 时有额外温度加成。

```java
// MTEAdvancedBoilerBase.java:33
private static final int STEAM_PER_SECOND = 750;

// 每秒蒸汽产量 = 750 × tier
@Override
protected int getProductionPerSecond() { return steamPerSecond; } // = 750 * tier

// 最大温度 = 进度条最大值
@Override
protected int getMaxTemperature() { return maxProgresstime(); } // = 1000 + 250 * tier

// 不会因缺水而爆炸
@Override
protected void onDangerousWaterLack(IGregTechTileEntity tile, long ticks) {
    // Smart boilers don't explode!
}

// 燃料更新（温度 ≤ 101 才消耗燃料）
@Override
protected void updateFuel(IGregTechTileEntity tile, long ticks) {
    ItemStack fuelStack = this.mInventory[2];
    int burnTime = getBurnTime(fuelStack);
    if (burnTime > 0 && this.mTemperature <= 101) {
        this.mProcessingEnergy += burnTime / 10;
        this.mTemperature += burnTime / 500; // 高热值燃料额外加温
        tile.decrStackSize(2, 1);
    }
}
```

---

## 4. gtPlusPlus 模块多方块发电机

### 4.1 大型半流体发电机 `MTELargeSemifluidGenerator`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/MTELargeSemifluidGenerator.java`  
**机型代号**：LSB  
**结构**：3×3×4  
**配方**：`GTPPRecipeMaps.semiFluidFuels`

```java
// MTELargeSemifluidGenerator.java:checkProcessing（精简）
@Override
public CheckRecipeResult checkProcessing() {
    ArrayList<FluidStack> tFluids = getStoredFluids();
    // 检查润滑油（每小时 2000L）和氧气（可选，每 tick 4L）
    boostEu = oxygen.amount >= 4L;
    long lubricantCost = boostEu ? 2L : 1L;

    for (FluidStack hatchFluid : tFluids) {
        GTRecipe aFuel = GTPPRecipeMaps.semiFluidFuels.getBackend().findFuel(hatchFluid);
        int newEUt = boostEu ? 4096 : 2048;              // 默认 2048, 氧气加速 4096
        fuelConsumption = newEUt / aFuel.mSpecialValue;   // 消耗量
        if (depleteInput(new FluidStack(hatchFluid.getFluid(), fuelConsumption))) {
            // 消耗润滑油（每 72 tick 一次）
            if (mRuntime % 72 == 0) depleteInput(Materials.Lubricant.getFluid(lubricantCost));
            this.lEUt = mEfficiency < 2000 ? 0 : newEUt; // 使用 lEUt（long 版本）
            this.mMaxProgresstime = 1;
            this.mEfficiencyIncrease = 15;
            return CheckRecipeResultRegistry.GENERATING;
        }
    }
}
```

**使用 `lEUt`（long 型）而非 `mEUt`（int 型）**，支持更大功率输出。

---

### 4.2 大型火箭引擎 `MTELargeRocketEngine`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/MTELargeRocketEngine.java`  
**结构**：3×3×10

```java
// MTELargeRocketEngine.java:checkProcessing（精简）
// 需要：GT++ 火箭燃料 + CO2 润滑 + 空气（防止过热）+ 液氢（可选 boost）
@Override
public CheckRecipeResult checkProcessing() {
    int aAirToConsume = this.euProduction / 100;
    if (getAirAmount() < aAirToConsume) return SimpleCheckRecipeResult.ofFailure("no_air");

    for (FluidStack hatchFluid : tFluids) {
        GTRecipe aFuel = GTPPRecipeMaps.rocketFuels.getBackend().findFuel(hatchFluid);
        this.boostEu = consumeLOH(); // 消耗液氢
        if (boostEu) {
            this.fuelValue = aFuel.mSpecialValue * 3;
            this.lEUt = GTValues.V[5] << 1; // ~65536 EU/t boost 模式
        } else {
            this.lEUt = GTValues.V[5] << 1; // 约 32768 EU/t
        }
        this.mEfficiencyIncrease = this.euProduction / 2000;
        return CheckRecipeResultRegistry.GENERATING;
    }
}

// 消耗 CO2 作为润滑剂
private boolean consumeCO2() {
    return this.depleteInput(Materials.CarbonDioxide.getGas(this.boostEu ? 3 : 1));
}
```

---

### 4.3 太阳能塔 `MTESolarTower`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/MTESolarTower.java`  
**特点**：不消耗燃料，利用太阳光加热冷熔盐，冷熔盐转热熔盐，热熔盐可被后续机器用于发电。  
本质上是**流体转换器**，不直接产生 EU。

```java
// MTESolarTower.java:418
@Override
public RecipeMap<?> getRecipeMap() { return GTPPRecipeMaps.solarTowerRecipes; }

// 输入：Cold Solar Salt → 输出：Hot Solar Salt
// 不设置 mEUt/lEUt 为正值，不直接发电
```

**热量机制**：每 10 秒（200 tick）根据太阳反射器环数计算热量增益，
达到 30000 热量才开始转换熔盐。公式：  
`效率 = (7000 - |currentHeat - 50000|^0.8) / 7000`

---

### 4.4 GT++ 大型等离子体涡轮 `MTELargerTurbinePlasma`

**代码路径**：`gtPlusPlus/xmod/gregtech/common/tileentities/machines/multi/production/turbines/MTELargerTurbinePlasma.java`  
**基类**：`MTELargerTurbineBase`  
**结构**：7×9×7（更大型，需要 Turbine Hatch 槽位安装多个转子）  
**配方图**：`RecipeMaps.plasmaFuels`

```java
// MTELargerTurbinePlasma.java:26-40
public class MTELargerTurbinePlasma extends MTELargerTurbineBase {

    @Override
    public int getCasingMeta() { return 4; }   // 钨钢涡轮机壳

    @Override
    public int getCasingTextureIndex() { return 60; }

    @Override
    public int getFuelValue(FluidStack aLiquid) {
        GTRecipe tFuel = getRecipeMap().getBackend().findFuel(aLiquid);
        return tFuel != null ? tFuel.mSpecialValue : 0;
    }

    @Override
    public RecipeMap<FuelBackend> getRecipeMap() { return RecipeMaps.plasmaFuels; }
}
```

---

## 5. goodgenerator 模块多方块发电机

### 5.1 大型钠克达反应堆 `MTEMultiNqGenerator`

**代码路径**：`goodgenerator/blocks/tileEntity/MTEMultiNqGenerator.java`  
**机型代号**：LNR  
**结构**：7×8×7  
**配方图**：`GoodGeneratorRecipeMaps.naquadahReactorFuels`  
**特殊**：需要持续消耗液态空气（Liquid Air）；可用冷却液和激励液调整效率/输出。

**冷却液效率加成**：

| 冷却液 | 消耗量 | 效率 |
|--------|--------|------|
| IC2 Coolant | 1000 L/s | 配置值 |
| Super Coolant | 1000 L/s | 配置值 |
| Cryotheum | 1000 L/s | 配置值 |
| Tachyon Temporal Fluid | 20 L/s | 配置值（最高） |

**激励液倍率**：

| 激励液 | 消耗量 | 倍率 |
|--------|--------|------|
| Molten Caesium | 180 L/s | 配置值 |
| Molten Uranium-235 | 180 L/s | 配置值 |
| Molten Naquadah | 20 L/s | 配置值 |
| Atomic Sep. Catalyst | 20 L/s | 配置值 |
| Spatially Enlarged Fluid | 20 L/s | 配置值 |

```java
// MTEMultiNqGenerator.java:checkProcessing_EM（精简）
@Override
public CheckRecipeResult checkProcessing_EM() {
    GTRecipe tRecipe = GoodGeneratorRecipeMaps.naquadahReactorFuels.findRecipeQuery()
        .fluids(tFluids.toArray(new FluidStack[0])).find();
    if (tRecipe != null) {
        Pair<FluidStack, Integer> excitedInfo = getExcited(tFluids.toArray(new FluidStack[0]), false);
        int pall = excitedInfo == null ? 1 : excitedInfo.getValue(); // 激励液倍率
        if (consumeFuel(copyFluidWithAmount(tRecipe.mFluidInputs[0], pall), tFluids)) {
            mOutputFluids = new FluidStack[]{ copyFluidWithAmount(tRecipe.mFluidOutputs[0], pall) };
            basicOutput = tRecipe.mSpecialValue;   // 基础 EU/t
            times = pall;
            mMaxProgresstime = tRecipe.mDuration;
            return CheckRecipeResultRegistry.GENERATING;
        }
    }
}

// 运行时每 20 tick（1秒）更新一次输出
@Override
public boolean onRunningTick(ItemStack stack) {
    if (mMaxProgresstime != 0 && mProgresstime % 20 == 0) {
        // 消耗液态空气（否则停止输出）
        if (!consumeFuel(Materials.LiquidAir.getFluid(LiquidAirConsumptionPerSecond), input)) {
            this.mEUt = 0; this.trueOutput = 0; return true;
        }
        int eff = consumeCoolant(input);   // 获取冷却液效率
        if (consumeFuel(lockedFluid, input)) time = times; // 激励液激活
        this.mEUt = basicOutput * eff * time / 100;
        this.trueOutput = (long)basicOutput * (long)eff * (long)time / 100;
    }
    addAutoEnergy(trueOutput); // 写入动力仓
    return true;
}

// 能量输出到动力仓
public void addAutoEnergy(long outputPower) {
    if (!this.mDynamoHatches.isEmpty()) {
        MTEHatchDynamo tHatch = this.mDynamoHatches.get(0);
        if (tHatch.maxEUOutput() * tHatch.maxAmperesOut() >= outputPower) {
            tHatch.setEUVar(Math.min(tHatch.maxEUStore(),
                tHatch.getBaseMetaTileEntity().getStoredEU() + outputPower));
        } else {
            stopMachine(ShutDownReasonRegistry.INSUFFICIENT_DYNAMO);
        }
    }
}
```

---

### 5.2 超临界流体涡轮 `MTESupercriticalFluidTurbine`

**代码路径**：`goodgenerator/blocks/tileEntity/MTESupercriticalFluidTurbine.java`  
**燃料**：超临界蒸汽（`supercriticalsteam`）  
**副产品**：超热蒸汽（`ic2superheatedsteam`）  
**结构**：3×3×4（与标准大型涡轮相同）

```java
// MTESupercriticalFluidTurbine.java:fluidIntoPower（精简）
@Override
public int fluidIntoPower(ArrayList<FluidStack> aFluids, TurbineStatCalculator turbine) {
    FluidStack tSCSteam = FluidRegistry.getFluidStack("supercriticalsteam", 1);
    // 允许最多 125% 最优流量
    int remainingFlow = GTUtility.safeInt((long)(realOptFlow * 1.25f));

    for (FluidStack aFluidStack : aFluids) {
        if (tSCSteam.isFluidEqual(aFluidStack)) {
            flow = Math.min(aFluidStack.amount, remainingFlow);
            depleteInput(new FluidStack(aFluidStack, flow));
            totalFlow += flow;
        } else if (GTModHandler.isAnySteam(aFluidStack)) {
            depleteInput(...); // 丢弃普通蒸汽
        }
    }

    // 1:1 输出超热蒸汽
    addOutput(FluidRegistry.getFluidStack("ic2superheatedsteam", totalFlow));

    // 与普通蒸汽涡轮相同效率公式（无额外 0.5 系数）
    tEU = GTUtility.safeInt((long)(tEU * turbine.getSteamEfficiency()));
    return tEU;
}

// 转子损耗 = 2x 普通涡轮
@Override
public int getDamageToComponent(ItemStack aStack) {
    return looseFit ? (XSTR.XSTR_INSTANCE.nextInt(2) == 0 ? 0 : 1) : 2;
}
```

---

### 5.3 通用化学燃料引擎 `MTEUniversalChemicalFuelEngine`

**代码路径**：`goodgenerator/blocks/tileEntity/MTEUniversalChemicalFuelEngine.java`  
**机型代号**：UCFE  
**结构**：5×4×9  
**支持燃料**：柴油（`RecipeMaps.dieselFuels`）、气态（`RecipeMaps.gasTurbineFuels`）、火箭燃料（`GTPPRecipeMaps.rocketFuels`）

```java
// MTEUniversalChemicalFuelEngine.java:效率系数
protected final double DIESEL_EFFICIENCY_COEFFICIENT = 0.04D;
protected final double GAS_EFFICIENCY_COEFFICIENT = 0.04D;
protected final double ROCKET_EFFICIENCY_COEFFICIENT = 0.005D;
protected final double EFFICIENCY_CEILING = 1.5D; // 最高效率 150%

// 效率公式（指数曲线）：exp(-C/(促进剂/燃料)) * 1.5
public void calculateEfficiency(long aFuel, long aPromoter, double coefficient) {
    if (aPromoter == 0) { this.tEff = 0; return; }
    this.tEff = (int)(Math.exp(-coefficient * (double)aFuel / (double)aPromoter)
        * EFFICIENCY_CEILING * 10000);
}

// checkProcessing_EM（精简）
@Override
public CheckRecipeResult checkProcessing_EM() {
    long PromoterAmount = findLiquidAmount(getPromoter(), tFluids); // 燃烧促进剂

    // 依次尝试柴油 > 气态 > 火箭燃料
    result = processFuel(tFluids, RecipeMaps.dieselFuels, PromoterAmount, DIESEL_EFFICIENCY_COEFFICIENT, 1);
    if (result.wasSuccessful()) return result;
    result = processFuel(tFluids, RecipeMaps.gasTurbineFuels, PromoterAmount, GAS_EFFICIENCY_COEFFICIENT, 1);
    if (result.wasSuccessful()) return result;
    result = processFuel(tFluids, GTPPRecipeMaps.rocketFuels, PromoterAmount, ROCKET_EFFICIENCY_COEFFICIENT, 3);
    return result;
}

// 运行时每 tick 向动力仓写入 EU
void addAutoEnergy() {
    long exEU = this.getPowerFlow() * tEff / 10000;
    MTEHatchDynamo tHatch = mDynamoHatches.get(0);
    tHatch.setEUVar(Math.min(tHatch.maxEUStore(),
        tHatch.getBaseMetaTileEntity().getStoredEU() + exEU));
}
```

---

### 5.4 反物质发生器 `AntimatterGenerator`

**代码路径**：`goodgenerator/blocks/tileEntity/AntimatterGenerator.java`  
**机型代号**：SLAM  
**结构**：35×43×35（极大）  
**输出仓**：异域动力仓（Exotic Dynamo Hatch，激光源仓）

```java
// AntimatterGenerator.java
public static final long ANTIMATTER_FUEL_VALUE = 1_000_000_000_000L; // 1e12 EU/L

// 能量产生公式：Antimatter^exponent * 1e12 * efficiency
// exponent 由催化剂决定：铜=1.00, UIV超导=1.02, UMV超导=1.03

public void createEU(long antimatter, FluidStack catalyst) {
    float efficiency = Math.min(
        (float)antimatter / (float)catalystCount,
        (float)catalystCount / (float)antimatter); // 两者比值越接近1，效率越高

    generatedEU = (long)((Math.pow(antimatter, modifier) * ANTIMATTER_FUEL_VALUE) * efficiency);

    if (wirelessEnabled && modifier >= 1.03F) {
        // 无线模式：直接注入全局无线网络
        addEUToGlobalEnergyMap(owner_uuid, generatedEU);
    } else {
        // 有线模式：分配给所有异域动力仓
        float invHatchCount = 1.0F / (float)mExoticDynamoHatches.size();
        for (MTEHatch tHatch : getExoticDynamoHatches()) {
            tHatch.setEUVar(tHatch.getEUVar() + (long)(generatedEU * invHatchCount));
        }
    }
}
```

**周期**：每 5 秒（100 tick）一个处理周期，一次性消耗所有输入仓中的反物质和催化剂。  
**无线模式**：使用螺丝刀切换，需要 UMV 超导基底作为催化剂。

---

## 6. bartworks 模块单方块发电机

### 6.1 酸液发电机 `MTEAcidGenerator`

**代码路径**：`bartworks/common/tileentities/tiered/MTEAcidGenerator.java`  
**配方图**：`BartWorksRecipeMaps.acidGenFuels`  
**特点**：使用酸类液体作为燃料，无污染。

```java
// MTEAcidGenerator.java（完整核心代码）
public class MTEAcidGenerator extends MTEBasicGenerator {

    @Override
    public RecipeMap<?> getRecipeMap() {
        return BartWorksRecipeMaps.acidGenFuels; // 酸液燃料
    }

    @Override
    public int getEfficiency() { return efficiency; } // 由构造函数传入

    @Override
    public int getPollution() { return 0; } // 无污染
}
```

继承 `MTEBasicGenerator`，通过 `onPostTick` 的 `increaseStoredEnergyUnits` 机制输出 EU（参见 0.1 节）。

---

## 7. kekztech 模块多方块发电机

### 7.1 固体氧化物燃料电池 MK1 `MTESOFuelCellMK1`

**代码路径**：`kekztech/common/tileentities/MTESOFuelCellMK1.java`  
**机型**：Gas Turbine（气体涡轮类型）  
**结构**：3×3×5

```java
// MTESOFuelCellMK1.java:52-53
private final int OXYGEN_PER_SEC = 100;   // 每秒需要 100L 氧气
private final int EU_PER_TICK = 2048;     // 输出 2048 EU/t
private final int STEAM_PER_SEC = 20000;  // 输出 20000 L/s 普通蒸汽

// checkProcessing：遍历输入仓查找气态燃料
@Override
public CheckRecipeResult checkProcessing() {
    for (GTRecipe aFuel : RecipeMaps.gasTurbineFuels.getAllRecipes()) {
        FluidStack liquid = ...; // 找到燃料
        liquid.amount = (EU_PER_TICK * 20) / aFuel.mSpecialValue; // 计算消耗量

        if (super.depleteInput(liquid)) {
            if (!super.depleteInput(Materials.Oxygen.getGas(OXYGEN_PER_SEC))) {
                return CheckRecipeResultRegistry.NO_FUEL_FOUND; // 缺氧气则停机
            }
            super.mEUt = EU_PER_TICK;                       // 设置正的 mEUt → 发电
            super.mMaxProgresstime = 20;
            super.addOutput(Materials.Steam.getGas(STEAM_PER_SEC)); // 副产品蒸汽
            return CheckRecipeResultRegistry.GENERATING;
        }
    }
}
```

---

### 7.2 固体氧化物燃料电池 MK2 `MTESOFuelCellMK2`

**代码路径**：`kekztech/common/tileentities/MTESOFuelCellMK2.java`  
为 MK1 的升级版，参数更高：

```java
// MTESOFuelCellMK2.java:52-54
private final int OXYGEN_PER_SEC = 2000;  // 每秒需要 2000L 氧气
private final int EU_PER_TICK = 24576;    // 输出 24576 EU/t（约 3A IV）
private final int STEAM_PER_SEC = 96000;  // 输出 96000 L/s 超热蒸汽（SH Steam）

// 工作原理与 MK1 相同，但使用超热蒸汽作为副产品
super.addOutput(FluidRegistry.getFluidStack("ic2superheatedsteam", STEAM_PER_SEC));
```

---

## 8. gtnhintergalactic 模块多方块发电机

### 8.1 戴森球 `TileEntityDysonSwarm`

**代码路径**：`gtnhintergalactic/tile/multi/TileEntityDysonSwarm.java`  
**机型**：戴森球（Dyson Swarm）  
继承自 `TTMultiblockBase`（TecTech 多方块基类）

**工作原理**：在轨道部署太阳能模块，每 tick 根据模块数量和功率因子输出 EU，
支持普通动力仓和 TecTech 多路动力仓。

```java
// TileEntityDysonSwarm.java:192-298（精简）
private long euPerTick = 0;

// 每运行周期根据模块数计算功率
euPerTick = (long)((long)moduleCount * IGConfig.dysonSwarm.euPerModule * powerFactor);

// 输出 EU 到动力仓
@Override
public boolean energyFlowOnRunningTick(ItemStack aStack, boolean allowProduction) {
    if (allowProduction && euPerTick > 0) {
        addEnergyOutput_EM(euPerTick, 1); // 调用 TecTech 基类的输出方法
    }
    return true;
}

// 内部实现（写入各动力仓）
public boolean addEnergyOutput_EM(long EU, long Amperes) {
    long euVar = EU * Amperes;
    for (MTEHatchDynamo tHatch : filterValidMTEs(mDynamoHatches)) {
        long diff = tHatch.maxEUStore() - tHatch.getBaseMetaTileEntity().getStoredEU();
        if (diff > 0) {
            tHatch.setEUVar(tHatch.getBaseMetaTileEntity().getStoredEU() + Math.min(euVar, diff));
        }
    }
    // 同理处理 TecTech 多路动力仓 eDynamoMulti
}
```

---

## 9. 能量输出机制总结对比

| 类型 | 能量方向 | 输出方法 | 涉及接口 |
|------|----------|----------|---------|
| **单方块发电机** | 自身缓存 → 能量网络 | `increaseStoredEnergyUnits` | `isEnetOutput()=true` |
| **多方块 (mEUt>0)** | 控制器 → 动力仓缓存 → 能量网络 | `addEnergyOutputMultipleDynamos` | `MTEHatchDynamo.isEnetOutput()=true` |
| **特殊多方块** | 控制器 → 直接写入动力仓 | `tHatch.setEUVar(...)` | 绕过标准流程 |
| **无线发电** | 控制器 → 全局无线网络 | `addEUToGlobalEnergyMap` | 需要 WirelessNetworkManager |
| **耗电机器** | 能量网络 → 自身缓存 | `drainEnergyInput` | `isEnetInput()=true`, `mEUt<0` |

### 关键区别：`mEUt` 符号决定运行模式

```java
// MTEMultiBlockBase.java:1015-1029
public boolean onRunningTick(ItemStack aStack) {
    if (mEUt > 0) {
        // 发电机模式：向外输出
        addEnergyOutput(((long)mEUt * mEfficiency) / 10000);
        return true;
    }
    if (mEUt < 0) {
        // 消耗机器模式：从外拉取
        if (!drainEnergyInput(getActualEnergyUsage())) {
            stopMachine(ShutDownReasonRegistry.POWER_LOSS);
            return false;
        }
    }
}
```

### 动力仓内部存储后的输出

`MTEHatchDynamo` 本身也是一个 `isEnetOutput()=true` 的方块。其 `increaseStoredEnergyUnits`
将 EU 写入 `BaseMetaTileEntity` 内部存储后，GT 能量网络框架会在每 tick 自动检查
`isOutputFacing(side)` 并将能量推送到相邻的电缆/机器：

```java
// MTEHatchDynamo.java:49-69
@Override
public boolean isEnetOutput() { return true; }

@Override
public boolean isOutputFacing(ForgeDirection side) {
    return side == getBaseMetaTileEntity().getFrontFacing(); // 仅前面输出
}

@Override
public long maxEUOutput() { return V[mTier]; }  // 输出电压限制

@Override
public long maxEUStore() { return 512L + V[mTier + 1] * 2L; } // 内部缓存容量
```

---

## 10. 完整发电机索引

### 单方块发电机

| 机器 | 模块 | 燃料类型 | 代码路径 |
|------|------|---------|---------|
| MTESolarGenerator | gregtech | 无（太阳光） | `gregtech/common/tileentities/generators/` |
| MTEDieselGenerator | gregtech | 液态柴油燃料 | `gregtech/common/tileentities/generators/` |
| MTEGasTurbine | gregtech | 气态燃料 | `gregtech/common/tileentities/generators/` |
| MTESteamTurbine | gregtech | 蒸汽 | `gregtech/common/tileentities/generators/` |
| MTEPlasmaGenerator | gregtech | 等离子体 | `gregtech/common/tileentities/generators/` |
| MTENaquadahReactor | gregtech | 钠克达燃料（固/液） | `gregtech/common/tileentities/generators/` |
| MTEMagicEnergyConverter | gregtech | 魔法燃料 | `gregtech/common/tileentities/generators/` |
| MTEMagicalEnergyAbsorber | gregtech | Vis/Essentia/末影水晶 | `gregtech/common/tileentities/generators/` |
| MTELightningRod | gregtech | 雷击（随机） | `gregtech/common/tileentities/generators/` |
| MTEAcidGenerator | bartworks | 酸液 | `bartworks/common/tileentities/tiered/` |
| MTEGeothermalGenerator | gtPlusPlus | 熔岩/Pahoehoe熔岩 | `gtPlusPlus/.../generators/` |
| MTESemiFluidGenerator | gtPlusPlus | 半流体燃料 | `gtPlusPlus/.../generators/` |
| MTERocketFuelGenerator | gtPlusPlus | 火箭燃料 | `gtPlusPlus/.../generators/` |
| MTERTGenerator | gtPlusPlus | RTG 颗粒（放射性） | `gtPlusPlus/.../generators/` |
| MTEAdvancedBoilerLV/MV/HV | gtPlusPlus | 固体燃料（产蒸汽） | `gtPlusPlus/.../generators/` |

### 多方块发电机

| 机器 | 模块 | 机型代号 | 输出类型 | 代码路径 |
|------|------|---------|---------|---------|
| MTELargeBoilerBronze/Steel/Ti/TuSt | gregtech | Boiler | 蒸汽/超热蒸汽 | `gregtech/.../machines/multi/` |
| MTELargeTurbineSteam | gregtech | LST | EU | `gregtech/.../machines/multi/` |
| MTELargeTurbineHPSteam | gregtech | LHT | EU | `gregtech/.../machines/multi/` |
| MTELargeTurbineGas | gregtech | LGT | EU | `gregtech/.../machines/multi/` |
| MTELargeTurbinePlasma | gregtech | LPT | EU | `gregtech/.../machines/multi/` |
| MTEDieselEngine | gregtech | LDE | EU | `gregtech/.../machines/multi/` |
| MTEExtremeDieselEngine | gregtech | ECE | EU | `gregtech/.../machines/multi/` |
| MTEWormholeGenerator | gregtech | MWG | EU（传输） | `gregtech/.../machines/multi/` |
| MTELargeSemifluidGenerator | gtPlusPlus | LSB | EU | `gtPlusPlus/.../production/` |
| MTELargeRocketEngine | gtPlusPlus | LRE | EU | `gtPlusPlus/.../production/` |
| MTESolarTower | gtPlusPlus | Solar Tower | 热熔盐 | `gtPlusPlus/.../production/` |
| MTELargerTurbinePlasma | gtPlusPlus | 大型等离子涡轮 | EU | `gtPlusPlus/.../turbines/` |
| MTEMultiNqGenerator | goodgenerator | LNR | EU | `goodgenerator/blocks/tileEntity/` |
| MTESupercriticalFluidTurbine | goodgenerator | SC Turbine | EU | `goodgenerator/blocks/tileEntity/` |
| MTEUniversalChemicalFuelEngine | goodgenerator | UCFE | EU | `goodgenerator/blocks/tileEntity/` |
| AntimatterGenerator | goodgenerator | SLAM | EU（超量） | `goodgenerator/blocks/tileEntity/` |
| MTESOFuelCellMK1 | kekztech | SOFC MK1 | EU + 蒸汽 | `kekztech/common/tileentities/` |
| MTESOFuelCellMK2 | kekztech | SOFC MK2 | EU + 超热蒸汽 | `kekztech/common/tileentities/` |
| TileEntityDysonSwarm | gtnhintergalactic | Dyson Swarm | EU | `gtnhintergalactic/tile/multi/` |
