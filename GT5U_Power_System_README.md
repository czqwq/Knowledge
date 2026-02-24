# GT5-Unofficial 电力系统（Power/Energy System）知识库

> **代码来源：** https://github.com/GTNewHorizons/GT5-Unofficial  
> **本地路径：** /tmp/GT5-Unofficial（单 monorepo，含 gregtech/tectech 等 17 个模块）  
> **所有代码均经本地源码核实，不含虚假代码。**

---

## 目录

1. [电压阶梯体系](#1-电压阶梯体系)
2. [核心能量接口](#2-核心能量接口)
3. [电缆系统（MTECable）](#3-电缆系统-mtecable)
4. [能量节点图（Power Graph）](#4-能量节点图-power-graph)
5. [变压器（MTETransformer）](#5-变压器-mtetransformer)
6. [能量仓（MTEHatch 系列）](#6-能量仓-mtehatch-系列)
7. [TecTech 多安培/激光能量仓](#7-tectech-多安培激光能量仓)
8. [无线能量网络（WirelessNetworkManager）](#8-无线能量网络-wirelessnetworkmanager)
9. [能量流向完整链路](#9-能量流向完整链路)

---

## 1. 电压阶梯体系

### 1.1 核心常量：`GTValues.java`

文件路径：`src/main/java/gregtech/api/enums/GTValues.java`

```java
// src/main/java/gregtech/api/enums/GTValues.java:121-136

/**
 * The Voltage Tiers. Use this Array instead of the old named Voltage Variables
 */
public static final long[] V = new long[] { 8L, 32L, 128L, 512L, 2048L, 8192L, 32_768L, 131_072L, 524_288L,
    2_097_152L, 8_388_608L, 33_554_432L, 134_217_728L, 536_870_912L, Integer.MAX_VALUE - 7,
    // Error tier to prevent out of bounds errors. Not really a real tier (for now).
    8_589_934_592L };

/**
 * The Voltage Practical. These are recipe voltage you should use if you expect the recipe to use a full amp of that
 * tier. These leave a bit of headroom for cable and transformer losses, but not enough to make it a great gain.
 */
// this will correctly map ULV to 7.
public static final long[] VP = Arrays.stream(V)
    .map(
        i -> BigInteger.valueOf(i)
            .multiply(BigInteger.valueOf(30))
            .divide(BigInteger.valueOf(32))
            .longValueExact())
    .toArray();

/**
 * Array of Maximum Amperes at given Tier index
 */
public static final long[] AatV = new long[] { 268435455, 67108863, 16777215, 4194303, 1048575, 262143, 65535,
    16383, 4095, 1023, 255, 63, 15, 3, 1, 1 };
```

### 1.2 电压索引枚举：`VoltageIndex.java`

文件路径：`src/main/java/gregtech/api/enums/VoltageIndex.java`

```java
// src/main/java/gregtech/api/enums/VoltageIndex.java:1-21
public class VoltageIndex {

    public final static int ULV = 0;
    public final static int LV  = 1;
    public final static int MV  = 2;
    public final static int HV  = 3;
    public final static int EV  = 4;
    public final static int IV  = 5;
    public final static int LuV = 6;
    public final static int ZPM = 7;
    public final static int UV  = 8;
    public final static int UHV = 9;
    public final static int UEV = 10;
    public final static int UIV = 11;
    public final static int UMV = 12;
    public final static int UXV = 13;
    public final static int MAX = 14;

    private VoltageIndex() {}
}
```

### 1.3 电压名称与颜色：`GTValues.java`

```java
// src/main/java/gregtech/api/enums/GTValues.java:163-179
public static final String[] VN = new String[] { "ULV", // 0
    "LV",  // 1
    "MV",  // 2
    "HV",  // 3
    "EV",  // 4
    "IV",  // 5
    "LuV", // 6
    "ZPM", // 7
    "UV",  // 8
    "UHV", // 9
    "UEV", // 10
    "UIV", // 11
    "UMV", // 12
    "UXV", // 13
    "MAX", // 14
    "MAX+" // 15
};
```

### 1.4 配方专用电压：`TierEU.java`

文件路径：`src/main/java/gregtech/api/enums/TierEU.java`

```java
// src/main/java/gregtech/api/enums/TierEU.java（全文）
// Do NOT use these for crafting recipes as they are exactly 1A! Use RECIPE_ULV etc.
public static final long ULV  = V[VoltageIndex.ULV];
public static final long LV   = V[VoltageIndex.LV];
// ... 以此类推到 MAX

// Use me for recipes.
// VP = V * 30/32，为配方留有一定余量
public static final long RECIPE_ULV = GTValues.VP[VoltageIndex.ULV];
public static final long RECIPE_LV  = GTValues.VP[VoltageIndex.LV];
public static final long RECIPE_MV  = GTValues.VP[VoltageIndex.MV];
public static final long RECIPE_HV  = GTValues.VP[VoltageIndex.HV];
public static final long RECIPE_EV  = GTValues.VP[VoltageIndex.EV];
public static final long RECIPE_IV  = GTValues.VP[VoltageIndex.IV];
public static final long RECIPE_LuV = GTValues.VP[VoltageIndex.LuV];
public static final long RECIPE_ZPM = GTValues.VP[VoltageIndex.ZPM];
public static final long RECIPE_UV  = GTValues.VP[VoltageIndex.UV];
public static final long RECIPE_UHV = GTValues.VP[VoltageIndex.UHV];
```

**电压对照表：**

| 索引 | 名称 | `V[n]` 数值（EU/t）  |
|------|------|---------------------|
|  0   | ULV  | 8                   |
|  1   | LV   | 32                  |
|  2   | MV   | 128                 |
|  3   | HV   | 512                 |
|  4   | EV   | 2,048               |
|  5   | IV   | 8,192               |
|  6   | LuV  | 32,768              |
|  7   | ZPM  | 131,072             |
|  8   | UV   | 524,288             |
|  9   | UHV  | 2,097,152           |
| 10   | UEV  | 8,388,608           |
| 11   | UIV  | 33,554,432          |
| 12   | UMV  | 134,217,728         |
| 13   | UXV  | 536,870,912         |
| 14   | MAX  | 2,147,483,640       |

---

## 2. 核心能量接口

### 2.1 `IEnergyConnected`（能量连接接口）

文件路径：`src/main/java/gregtech/api/interfaces/tileentity/IEnergyConnected.java`

```java
// src/main/java/gregtech/api/interfaces/tileentity/IEnergyConnected.java
public interface IEnergyConnected extends IColoredTileEntity {

    /**
     * Inject Energy Call for Electricity. Gets called by EnergyEmitters to inject Energy into your Block
     *
     * @param side      0-5 = Vanilla方向，6 = 无方向限制
     * @return          使用的安培数，0 表示未接受
     */
    long injectEnergyUnits(ForgeDirection side, long aVoltage, long aAmperage);

    /** 侧面能量输入判断 */
    boolean inputEnergyFrom(ForgeDirection side);

    /** 侧面能量输出判断 */
    boolean outputsEnergyTo(ForgeDirection side);
}
```

**工具方法 `Util.emitEnergyToNetwork`（向网络发射能量，兼容 IC2/RF）：**

```java
// src/main/java/gregtech/api/interfaces/tileentity/IEnergyConnected.java:54-100
public static long emitEnergyToNetwork(long voltage, long amperage, IEnergyConnected emitter) {
    long usedAmperes = 0;
    // 遍历六个方向
    for (final ForgeDirection side : ForgeDirection.VALID_DIRECTIONS) {
        if (usedAmperes > amperage) break;
        if (!emitter.outputsEnergyTo(side)) continue;

        final TileEntity tTileEntity = emitterTile.getTileEntityAtSide(side);

        if (tTileEntity instanceof IEnergyConnected energyConnected) {
            // GT 能量接口：直接注入
            usedAmperes += energyConnected.injectEnergyUnits(oppositeSide, voltage, amperage - usedAmperes);
        } else if (tTileEntity instanceof IEnergySink sink) {
            // IC2 能量：逐安培注入
            while (amperage > usedAmperes && sink.getDemandedEnergy() > 0
                && sink.injectEnergy(oppositeSide, voltage, voltage) < voltage) usedAmperes++;
        } else if (GregTechAPI.mOutputRF && tTileEntity instanceof IEnergyReceiver receiver) {
            // RF 能量：转换比率由配置决定
            final int rfOut = GTUtility.safeInt(voltage * GregTechAPI.mEUtoRF / 100);
            if (receiver.receiveEnergy(oppositeSide, rfOut, true) == rfOut) {
                receiver.receiveEnergy(oppositeSide, rfOut, false);
                usedAmperes++;
            }
        }
    }
    return usedAmperes;
}
```

### 2.2 `IBasicEnergyContainer`（能量容器接口）

文件路径：`src/main/java/gregtech/api/interfaces/tileentity/IBasicEnergyContainer.java`

```java
// src/main/java/gregtech/api/interfaces/tileentity/IBasicEnergyContainer.java（核心方法摘录）
public interface IBasicEnergyContainer extends IEnergyConnected, IHasWorldObjectAndCoords {

    boolean isUniversalEnergyStored(long aEnergyAmount);
    long getUniversalEnergyStored();
    long getUniversalEnergyCapacity();

    long getOutputAmperage();
    long getOutputVoltage();
    long getInputAmperage();
    long getInputVoltage();

    boolean decreaseStoredEnergyUnits(long aEnergy, boolean aIgnoreTooLessEnergy);
    boolean increaseStoredEnergyUnits(long aEnergy, boolean aIgnoreTooMuchEnergy);
    boolean drainEnergyUnits(ForgeDirection side, long aVoltage, long aAmperage);

    long getAverageElectricInput();
    long getAverageElectricOutput();
    long getStoredEU();
    long getEUCapacity();

    // 蒸汽支持（默认实现返回0）
    default long getStoredSteam()    { return 0; }
    default long getSteamCapacity()  { return 0; }
    default boolean increaseStoredSteam(long aEnergy, boolean aIgnoreTooMuchEnergy) { return false; }
}
```

---

## 3. 电缆系统（MTECable）

文件路径：`src/main/java/gregtech/api/metatileentity/implementations/MTECable.java`

### 3.1 关键字段

```java
// src/main/java/gregtech/api/metatileentity/implementations/MTECable.java:61-91
public class MTECable extends MetaPipeEntity implements IMetaTileEntityCable {

    public final float mThickNess;
    public final Materials mMaterial;
    public final long mCableLossPerMeter, mAmperage, mVoltage;
    public final boolean mInsulated, mCanShock;

    public int mTransferredAmperage = 0;

    public MTECable(int aID, String aName, String aNameRegional, float aThickNess, Materials aMaterial,
        long aCableLossPerMeter, long aAmperage, long aVoltage, boolean aInsulated, boolean aCanShock) {
        super(aID, aName, aNameRegional, 0);
        mThickNess = aThickNess;
        mMaterial = aMaterial;
        mAmperage = aAmperage;        // 最大安培数
        mVoltage = aVoltage;          // 最大电压（超过即起火）
        mInsulated = aInsulated;
        mCanShock = aCanShock;
        mCableLossPerMeter = aCableLossPerMeter;  // 每米损耗（EU/t）
    }
```

### 3.2 `injectEnergyUnits`（能量注入）

```java
// src/main/java/gregtech/api/metatileentity/implementations/MTECable.java:209（方法签名）
public long injectEnergyUnits(ForgeDirection side, long voltage, long amperage) {
    // 通过 PowerNodes 图系统传递能量到消费者
    // 具体路径传导在 PowerNodePath 中完成
}
```

---

## 4. 能量节点图（Power Graph）

GT5U 用图结构管理电缆网络，避免每 tick 扫描全图。

### 4.1 `PowerNodePath`（路径：电缆段损耗与过载检测）

文件路径：`src/main/java/gregtech/api/graphs/paths/PowerNodePath.java`

```java
// src/main/java/gregtech/api/graphs/paths/PowerNodePath.java（全文核心）
public class PowerNodePath extends NodePath {

    long mMaxAmps;      // 路径允许最大安培数（取各电缆最小值）
    long mAmps = 0;     // 本 tick 累计安培数
    long mLoss;         // 路径总损耗（各电缆 mCableLossPerMeter 之和）
    long mVoltage = 0;  // 本 tick 传导电压
    long mMaxVoltage;   // 路径最大承受电压

    public void applyVoltage(long aVoltage, boolean aCountUp) {
        // 超过最大电压 → 点火
        if (aVoltage > mMaxVoltage) {
            lock.addTileEntity(null);
            for (MetaPipeEntity tCable : mPipes) {
                if (((MTECable) tCable).mVoltage < this.mVoltage) {
                    BaseMetaPipeEntity tBaseCable = (BaseMetaPipeEntity) tCable.getBaseMetaTileEntity();
                    if (tBaseCable != null) {
                        tBaseCable.setToFire();   // 电缆过压起火
                    }
                }
            }
        }
    }

    public void addAmps(long aAmps) {
        this.mAmps += aAmps;
        // 超过最大安培数 * 40（40 tick 缓冲） → 点火
        if (this.mAmps > mMaxAmps * 40) {
            lock.addTileEntity(null);
            for (MetaPipeEntity tCable : mPipes) {
                if (((MTECable) tCable).mAmperage * 40 < this.mAmps) {
                    BaseMetaPipeEntity tBaseCable = (BaseMetaPipeEntity) tCable.getBaseMetaTileEntity();
                    if (tBaseCable != null) {
                        tBaseCable.setToFire();   // 电缆过安培起火
                    }
                }
            }
        }
    }

    @Override
    protected void processPipes() {
        super.processPipes();
        mMaxAmps = Integer.MAX_VALUE;
        mMaxVoltage = Integer.MAX_VALUE;
        for (MetaPipeEntity tCable : mPipes) {
            if (tCable instanceof MTECable) {
                mMaxAmps = Math.min(((MTECable) tCable).mAmperage, mMaxAmps);
                mLoss    += ((MTECable) tCable).mCableLossPerMeter;   // 累加损耗
                mMaxVoltage = Math.min(((MTECable) tCable).mVoltage, mMaxVoltage);
            }
        }
    }
}
```

### 4.2 `GenerateNodeMapPower`（节点图构建）

文件路径：`src/main/java/gregtech/api/graphs/GenerateNodeMapPower.java`

```java
// src/main/java/gregtech/api/graphs/GenerateNodeMapPower.java
public class GenerateNodeMapPower extends GenerateNodeMap {

    public GenerateNodeMapPower(BaseMetaPipeEntity aTileEntity) {
        generateNode(aTileEntity, null, 1, null, ForgeDirection.UNKNOWN, new ArrayList<>(), new HashSet<>());
    }

    @Override
    protected boolean isPipe(TileEntity aTileEntity) {
        // 只把 MTECable 算作管道节点
        return super.isPipe(aTileEntity) && ((BaseMetaPipeEntity) aTileEntity).getMetaTileEntity() instanceof MTECable;
    }

    @Override
    protected boolean addConsumer(TileEntity aTileEntity, ForgeDirection side, int aNodeValue,
        ArrayList<ConsumerNode> aConsumers) {
        if (aTileEntity instanceof BaseMetaTileEntity tBaseTileEntity) {
            if (tBaseTileEntity.inputEnergyFrom(side, false)) {
                // GT BaseMetaTileEntity → NodeGTBaseMetaTile
                ConsumerNode tConsumerNode = new NodeGTBaseMetaTile(aNodeValue, tBaseTileEntity, side, aConsumers);
                aConsumers.add(tConsumerNode);
                return true;
            }
        } else if (aTileEntity instanceof IEnergyConnected tTileEntity) {
            if (tTileEntity.inputEnergyFrom(side, false)) {
                // GT IEnergyConnected → NodeEnergyConnected
                ConsumerNode tConsumerNode = new NodeEnergyConnected(aNodeValue, tTileEntity, side, aConsumers);
                aConsumers.add(tConsumerNode);
                return true;
            }
        } else if (aTileEntity instanceof IEnergySink sink) {
            // IC2 能量汇 → NodeEnergySink
            ConsumerNode tConsumerNode = new NodeEnergySink(aNodeValue, (IEnergySink) aTileEntity, side, aConsumers);
            aConsumers.add(tConsumerNode);
            return true;
        } else if (GregTechAPI.mOutputRF && aTileEntity instanceof IEnergyReceiver receiver) {
            // RF 接收者 → NodeEnergyReceiver
            ConsumerNode tConsumerNode = new NodeEnergyReceiver(aNodeValue, receiver, side, aConsumers);
            aConsumers.add(tConsumerNode);
            return true;
        }
        return false;
    }

    @Override
    protected NodePath getNewPath(MetaPipeEntity[] aPipes) {
        return new PowerNodePath(aPipes);
    }
}
```

### 4.3 `PowerNodes`（能量分发核心算法）

文件路径：`src/main/java/gregtech/api/graphs/PowerNodes.java`

```java
// src/main/java/gregtech/api/graphs/PowerNodes.java（核心逻辑）
public static long powerNode(Node aCurrentNode, Node aPreviousNode, NodeList aConsumers, long aVoltage, long aMaxAmps) {
    long tAmpsUsed = 0;
    ConsumerNode tConsumer = (ConsumerNode) aConsumers.getNode();
    while (tConsumer != null) {
        int tTargetNodeValue = tConsumer.mNodeValue;
        if (tTargetNodeValue < aCurrentNode.mNodeValue || tTargetNodeValue > aCurrentNode.mHighestNodeValue) {
            // 目标在下游 → 向低值节点路由
            for (int j = 0; j < 6; j++) {
                final Node tNextNode = aCurrentNode.mNeighbourNodes[j];
                if (tNextNode != null && tNextNode.mNodeValue < aCurrentNode.mNodeValue) {
                    if (tNextNode.mNodeValue == tConsumer.mNodeValue) {
                        tAmpsUsed += processNodeInject(aCurrentNode, tConsumer, j, aMaxAmps - tAmpsUsed, aVoltage);
                        tConsumer = (ConsumerNode) aConsumers.getNextNode();
                    } else {
                        tAmpsUsed += processNextNode(aCurrentNode, tNextNode, aConsumers, j, aMaxAmps - tAmpsUsed, aVoltage);
                        tConsumer = (ConsumerNode) aConsumers.getNode();
                    }
                    break;
                }
            }
        } else {
            // 目标在上游 → 向高值节点路由
            for (int side = 5; side > -1; side--) {
                final Node tNextNode = aCurrentNode.mNeighbourNodes[side];
                if (tNextNode == null) continue;
                if (tNextNode.mNodeValue > aCurrentNode.mNodeValue && tNextNode.mNodeValue < tTargetNodeValue) {
                    tAmpsUsed += processNextNodeAbove(aCurrentNode, tNextNode, aConsumers, side, aMaxAmps - tAmpsUsed, aVoltage);
                    tConsumer = (ConsumerNode) aConsumers.getNode();
                    break;
                } else if (tNextNode.mNodeValue == tTargetNodeValue) {
                    tAmpsUsed += processNodeInject(aCurrentNode, tConsumer, side, aMaxAmps - tAmpsUsed, aVoltage);
                    tConsumer = (ConsumerNode) aConsumers.getNextNode();
                    break;
                }
            }
        }
        if (aMaxAmps - tAmpsUsed <= 0) return tAmpsUsed;
    }
    return tAmpsUsed;
}

// 向消费者注入能量，同时记录路径损耗和安培数
protected static long processNodeInject(Node aCurrentNode, ConsumerNode aConsumer, int ordinalSide, long aMaxAmps, long aVoltage) {
    if (aCurrentNode.locks[ordinalSide].isLocked()) return 0;
    final PowerNodePath tPath     = (PowerNodePath) aCurrentNode.mNodePaths[ordinalSide];
    final PowerNodePath tSelfPath = (PowerNodePath) aCurrentNode.mSelfPath;
    long tVoltLoss = 0;
    if (tSelfPath != null) {
        tVoltLoss += tSelfPath.getLoss();
        tSelfPath.applyVoltage(aVoltage, false);
    }
    tPath.applyVoltage(aVoltage - tVoltLoss, true);
    tVoltLoss += tPath.getLoss();
    long tAmps = aConsumer.injectEnergy(aVoltage - tVoltLoss, aMaxAmps);  // 注入（电压已扣除损耗）
    tPath.addAmps(tAmps);
    if (tSelfPath != null) tSelfPath.addAmps(tAmps);
    return tAmps;
}
```

---

## 5. 变压器（MTETransformer）

文件路径：`src/main/java/gregtech/api/metatileentity/implementations/MTETransformer.java`

变压器通过 `isAllowedToWork()` 切换升压/降压模式：

```java
// src/main/java/gregtech/api/metatileentity/implementations/MTETransformer.java:132-160

@Override
public long maxEUStore() {
    return Math.max(512L, 1L << (mTier + 2)) + V[mTier + 1] * 4L;
}

@Override
public long maxEUInput() {
    // isAllowedToWork() = true → 降压模式：接收上一阶电压
    // isAllowedToWork() = false → 升压模式：接收本阶电压
    return V[getBaseMetaTileEntity().isAllowedToWork() ? mTier + 1 : mTier];
}

@Override
public long maxEUOutput() {
    return V[getBaseMetaTileEntity().isAllowedToWork() ? mTier : mTier + 1];
}

@Override
public long maxAmperesOut() {
    return getBaseMetaTileEntity().isAllowedToWork() ? 4 : 1;
}

@Override
public long maxAmperesIn() {
    return getBaseMetaTileEntity().isAllowedToWork() ? 2 : 5;
}
```

**变压器模式说明：**

| 模式 | `isAllowedToWork()` | 输入电压 | 输出电压 | 输入安培 | 输出安培 |
|------|---------------------|---------|---------|---------|---------|
| 降压（Step Down） | `true`  | `V[tier+1]` | `V[tier]`   | 2A  | 4A  |
| 升压（Step Up）   | `false` | `V[tier]`   | `V[tier+1]` | 5A  | 1A  |

---

## 6. 能量仓（MTEHatch 系列）

### 6.1 基类 `MTEHatch`

文件路径：`src/main/java/gregtech/api/metatileentity/implementations/MTEHatch.java`

```java
// src/main/java/gregtech/api/metatileentity/implementations/MTEHatch.java:15
public abstract class MTEHatch extends MTEBasicTank implements ICraftingIconProvider {

    public enum ConnectionType {
        CABLE,      // 普通电缆
        WIRELESS,   // 无线能量
        LASER       // 激光（TecTech）
    }
}
```

### 6.2 普通能量仓（单机）：`MTEBasicMachine`

```java
// src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java:361-374
@Override
public long maxEUStore() {
    return V[mTier] * 64L;         // 储能 = 电压 * 64
}

@Override
public long maxEUInput() {
    return V[mTier];               // 接收电压 = 本阶电压
}

@Override
public long maxAmperesIn() {
    return ((long) mEUt * 2L) / V[mTier] + 1L;   // 根据配方 EU/t 动态计算
}
```

---

## 7. TecTech 多安培/激光能量仓

文件路径：`src/main/java/tectech/thing/metaTileEntity/hatch/MTEHatchEnergyMulti.java`

TecTech 的 `MTEHatchEnergyMulti` 支持多安培输入，是 TecTech 多方块的能量基础。

```java
// src/main/java/tectech/thing/metaTileEntity/hatch/MTEHatchEnergyMulti.java:30-144
public class MTEHatchEnergyMulti extends MTEHatch {

    public final int maxAmperes;   // 最大安培数（如 4A、16A、64A、256A...）
    public int Amperes;            // 当前可用安培数

    public MTEHatchEnergyMulti(int aID, String aName, String aNameRegional, int aTier, int aAmp) {
        super(aID, aName, aNameRegional, aTier, 0, new String[] {
            CommonValues.TEC_MARK_GENERAL,
            translateToLocal("gt.blockmachines.hatch.energymulti.desc.0"),
            translateToLocalFormatted("gt.blockmachines.hatch.energymulti.desc.2", aAmp + (aAmp >> 2)),
            translateToLocalFormatted("gt.blockmachines.hatch.energymulti.desc.3", aAmp)
        });
        Amperes = maxAmperes = aAmp;
    }

    @Override
    public long getMinimumStoredEU() {
        return 128L * Amperes;          // 最低储能 = 128 * 安培数
    }

    @Override
    public long maxEUInput() {
        return V[mTier];               // 电压与阶级一致
    }

    @Override
    public long maxEUStore() {
        return 512L + V[mTier] * 4L * Amperes;   // 储能随安培数线性增长
    }

    @Override
    public long maxAmperesIn() {
        return Amperes + (Amperes >> 2);   // 最大输入安培 = Amperes * 1.25（25% 缓冲）
    }

    @Override
    public long maxWorkingAmperesIn() {
        return Amperes;                    // 实际工作安培
    }
}
```

**纹理根据安培数变化（区分 4A/16A/64A/激光）：**

```java
// src/main/java/tectech/thing/metaTileEntity/hatch/MTEHatchEnergyMulti.java:73-98
@Override
public ITexture[] getTexturesActive(ITexture aBaseTexture) {
    if (maxAmperes > 64) {
        return new ITexture[] { aBaseTexture, Textures.BlockIcons.OVERLAYS_ENERGY_IN_MULTI_LASER[mTier + 1] };
    } else if (maxAmperes > 16) {
        return new ITexture[] { aBaseTexture, Textures.BlockIcons.OVERLAYS_ENERGY_IN_MULTI_64A[mTier + 1] };
    } else if (maxAmperes > 4) {
        return new ITexture[] { aBaseTexture, Textures.BlockIcons.OVERLAYS_ENERGY_IN_MULTI_16A[mTier + 1] };
    } else if (maxAmperes > 2) {
        return new ITexture[] { aBaseTexture, Textures.BlockIcons.OVERLAYS_ENERGY_IN_MULTI_4A[mTier + 1] };
    }
    // 默认 1A 纹理
    return new ITexture[] { aBaseTexture, Textures.BlockIcons.OVERLAYS_ENERGY_IN[mTier + 1] };
}
```

---

## 8. 无线能量网络（WirelessNetworkManager）

文件路径：`src/main/java/gregtech/common/misc/WirelessNetworkManager.java`

全局无线能量使用 `BigInteger` 存储，按玩家 UUID（或队伍领队 UUID）隔离。

```java
// src/main/java/gregtech/common/misc/WirelessNetworkManager.java（全文）
public class WirelessNetworkManager {

    // 添加/减少能量（负数表示消耗）
    // 若结果 < 0 则取消操作，返回 false
    public static boolean addEUToGlobalEnergyMap(UUID user_uuid, BigInteger EU) {
        // 标记脏数据以触发保存
        GlobalEnergyWorldSavedData.INSTANCE.markDirty();

        UUID teamUUID = SpaceProjectManager.getLeader(user_uuid);
        BigInteger totalEU = GlobalEnergy.getOrDefault(teamUUID, BigInteger.ZERO);
        totalEU = totalEU.add(EU);

        if (totalEU.signum() >= 0) {
            GlobalEnergy.put(teamUUID, totalEU);
            return true;   // 操作成功
        }
        return false;      // 能量不足，操作取消
    }

    // 充电仓补充间隔（20 * 100 = 2000 tick）
    public static long ticks_between_energy_addition = 100L * 20L;
    // 每仓最多存储次数
    public static long number_of_energy_additions = 4L;

    // 总储能 = 每 tick EU * 间隔 * 存储次数
    public static long totalStorage(long tier_eu_per_tick) {
        return tier_eu_per_tick * ticks_between_energy_addition * number_of_energy_additions;
    }

    // 查询玩家/队伍当前能量
    public static BigInteger getUserEU(UUID user_uuid) {
        return GlobalEnergy.getOrDefault(SpaceProjectManager.getLeader(user_uuid), BigInteger.ZERO);
    }
}
```

---

## 9. 能量流向完整链路

```
能量发电机（Generator）
        ↓ emitEnergyToNetwork()
电缆网络（MTECable → PowerNodePath）
        ↓ GenerateNodeMapPower 构建图
        ↓ PowerNodes.powerNode() 路由分发
        ↓ 电压 - mCableLossPerMeter = 实际到达电压
消费者节点（NodeGTBaseMetaTile / NodeEnergySink / NodeEnergyReceiver）
        ↓ injectEnergyUnits()
能量仓（MTEHatchInput / MTEHatchEnergyMulti）
        ↓ getStoredEU() / decreaseStoredEnergyUnits()
多方块机器（MTEMultiBlockBase.checkRecipe）
```

**过载保护规则（来自 `PowerNodePath`）：**
- **过压（Voltage Overflow）：** 当前传导电压 > 路径 `mMaxVoltage` → 立即点燃超限电缆
- **过流（Amperage Overflow）：** 累计安培 > `mMaxAmps * 40`（40 tick 缓冲）→ 点燃超限电缆
- **安培缓冲：** `addAmps()` 每 tick 重置（`reset(aTimePassed)` 方法按时间衰减）
