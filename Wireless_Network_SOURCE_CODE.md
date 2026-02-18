# GT5-Unofficial 无线能量网络 - 真实源代码参考

**⚠️ 重要**: 本文档包含从GT5-Unofficial实际源代码中提取的代码片段。
**来源**: https://github.com/GTNewHorizons/GT5-Unofficial

---

## 核心类文件

### 1. WirelessNetworkManager.java

**文件路径**: `src/main/java/gregtech/common/misc/WirelessNetworkManager.java`

这是无线能量网络的核心管理类。

```java
package gregtech.common.misc;

import static gregtech.common.misc.GlobalVariableStorage.GlobalEnergy;

import java.math.BigInteger;
import java.util.UUID;

import gregtech.api.interfaces.tileentity.IGregTechTileEntity;
import gregtech.common.misc.spaceprojects.SpaceProjectManager;

public class WirelessNetworkManager {

    private WirelessNetworkManager() {}

    public static void strongCheckOrAddUser(UUID user_uuid) {
        SpaceProjectManager.checkOrCreateTeam(user_uuid);
        user_uuid = SpaceProjectManager.getLeader(user_uuid);
        if (!GlobalEnergy.containsKey(user_uuid)) {
            GlobalEnergy.put(user_uuid, BigInteger.ZERO);
        }
    }

    // ------------------------------------------------------------------------------------
    // Add EU to the users global energy. You can enter a negative number to subtract it.
    // If the value goes below 0 it will return false and not perform the operation.
    // BigIntegers have much slower operations than longs/ints. You should call these methods
    // as infrequently as possible and bulk store values to add to the global map.
    public static boolean addEUToGlobalEnergyMap(UUID user_uuid, BigInteger EU) {
        // Mark the data as dirty and in need of saving.
        try {
            GlobalEnergyWorldSavedData.INSTANCE.markDirty();
        } catch (Exception exception) {
            System.out.println("COULD NOT MARK GLOBAL ENERGY AS DIRTY IN ADD EU");
            exception.printStackTrace();
        }

        // Get the team UUID. Users are by default in a team with a UUID equal to their player UUID.
        UUID teamUUID = SpaceProjectManager.getLeader(user_uuid);

        // Get the teams total energy stored. If they are not in the map, return 0 EU.
        BigInteger totalEU = GlobalEnergy.getOrDefault(teamUUID, BigInteger.ZERO);
        totalEU = totalEU.add(EU);

        // If there is sufficient EU then complete the operation and return true.
        if (totalEU.signum() >= 0) {
            GlobalEnergy.put(teamUUID, totalEU);
            return true;
        }

        // There is insufficient EU so cancel the operation and return false.
        return false;
    }

    public static boolean addEUToGlobalEnergyMap(UUID user_uuid, long EU) {
        return addEUToGlobalEnergyMap(user_uuid, BigInteger.valueOf(EU));
    }

    public static boolean addEUToGlobalEnergyMap(UUID user_uuid, int EU) {
        return addEUToGlobalEnergyMap(user_uuid, BigInteger.valueOf(EU));
    }

    // Ticks between energy additions to the hatch. For a dynamo this is how many ticks between energy being consumed
    // and added to the global energy map.
    public static long ticks_between_energy_addition = 100L * 20L;

    // Total number of energy additions this multi can store before it is full.
    public static long number_of_energy_additions = 4L;

    public static long totalStorage(long tier_eu_per_tick) {
        return tier_eu_per_tick * ticks_between_energy_addition * number_of_energy_additions;
    }

    // ------------------------------------------------------------------------------------

    public static BigInteger getUserEU(UUID user_uuid) {
        return GlobalEnergy.getOrDefault(SpaceProjectManager.getLeader(user_uuid), BigInteger.ZERO);
    }

    // This overwrites the EU in the network. Only use this if you are absolutely sure you know what you are doing.
    public static void setUserEU(UUID user_uuid, BigInteger EU) {
        // Mark the data as dirty and in need of saving.
        try {
            GlobalEnergyWorldSavedData.INSTANCE.markDirty();
        } catch (Exception exception) {
            System.out.println("COULD NOT MARK GLOBAL ENERGY AS DIRTY IN SET EU");
            exception.printStackTrace();
        }

        GlobalEnergy.put(SpaceProjectManager.getLeader(user_uuid), EU);
    }

    public static void clearGlobalEnergyInformationMaps() {
        // Do not use this unless you are 100% certain you know what you are doing.
        GlobalEnergy.clear();
    }

    public static UUID processInitialSettings(final IGregTechTileEntity machine) {
        // UUID and username of the owner.
        final UUID UUID = machine.getOwnerUuid();
        SpaceProjectManager.checkOrCreateTeam(UUID);
        return UUID;
    }
}
```

**关键点**:
- 使用`BigInteger`存储能量（支持巨大数值）
- 使用`SpaceProjectManager`管理团队
- 能量操作需要标记数据为dirty以触发保存
- `ticks_between_energy_addition = 100L * 20L` = 2000 ticks = 100秒

---

### 2. CoverEnergyWireless.java

**文件路径**: `src/main/java/gregtech/common/covers/CoverEnergyWireless.java`

这是无线能量覆盖物（Cover）的实现，用于从玩家全局网络提取能量。

```java
package gregtech.common.covers;

import static gregtech.common.misc.WirelessNetworkManager.addEUToGlobalEnergyMap;
import static gregtech.common.misc.WirelessNetworkManager.ticks_between_energy_addition;
import static java.lang.Long.min;

import java.util.UUID;

import gregtech.api.covers.CoverContext;
import gregtech.api.interfaces.tileentity.ICoverable;
import gregtech.api.metatileentity.BaseMetaTileEntity;

public class CoverEnergyWireless extends CoverLegacyData {

    private final long transferred_energy_per_operation;

    public CoverEnergyWireless(CoverContext context, int voltage) {
        super(context);
        this.transferred_energy_per_operation = 2 * voltage * ticks_between_energy_addition;
    }

    @Override
    public boolean isRedstoneSensitive(long aTimer) {
        return false;
    }

    @Override
    public boolean allowsCopyPasteTool() {
        return false;
    }

    @Override
    public boolean allowsTickRateAddition() {
        return false;
    }

    @Override
    public void doCoverThings(byte aInputRedstone, long aTimer) {
        if (coverData == 0 || aTimer % ticks_between_energy_addition == 0) {
            tryFetchingEnergy(coveredTile.get());
        }
        coverData = 1;
    }

    private static UUID getOwner(Object te) {
        if (te instanceof BaseMetaTileEntity igte) {
            return igte.getOwnerUuid();
        } else {
            return null;
        }
    }

    private void tryFetchingEnergy(ICoverable tileEntity) {
        if (tileEntity instanceof BaseMetaTileEntity bmte) {
            long currentEU = bmte.getStoredEUuncapped();
            long euToTransfer = min(transferred_energy_per_operation - currentEU, transferred_energy_per_operation);
            if (euToTransfer <= 0) return; // nothing to transfer
            if (!addEUToGlobalEnergyMap(getOwner(tileEntity), -euToTransfer)) return;
            bmte.increaseStoredEnergyUnits(euToTransfer, true);
        }
    }

    @Override
    public boolean alwaysLookConnected() {
        return true;
    }

    @Override
    public int getMinimumTickRate() {
        return 20;
    }
}
```

**工作原理**:
1. 每`ticks_between_energy_addition`（2000 ticks）执行一次
2. 计算需要传输的能量量
3. 调用`addEUToGlobalEnergyMap`并传入**负值**来扣除能量
4. 如果成功，则将能量注入机器

**传输量计算**:
```java
transferred_energy_per_operation = 2 * voltage * ticks_between_energy_addition
```
例如：IV等级(8192 EU/t) → 2 * 8192 * 2000 = 32,768,000 EU每次操作

---

### 3. GTMiscCommand.java - 命令实现

**文件路径**: `src/main/java/gregtech/common/misc/GTMiscCommand.java`

#### global_energy_display命令实现

```java
private void processGlobalEnergyDisplayCommand(ICommandSender sender, String[] args) {
    // Usage is /gt global_energy_display username.

    String username = args[1];
    String formatted_username = EnumChatFormatting.BLUE + username + EnumChatFormatting.RESET;
    UUID userUUID = SpaceProjectManager.getPlayerUUIDFromName(username);

    if (!SpaceProjectManager.isInTeam(userUUID)) {
        sendChatToPlayer(sender, "User " + formatted_username + " has no global energy network.");
        return;
    }
    UUID teamUUID = SpaceProjectManager.getLeader(userUUID);

    sendChatToPlayer(
        sender,
        "User " + formatted_username
            + " has "
            + EnumChatFormatting.RED
            + formatNumber(getUserEU(userUUID))
            + EnumChatFormatting.RESET
            + "EU in their network.");
    if (!userUUID.equals(teamUUID)) sendChatToPlayer(
        sender,
        "User " + formatted_username
            + " is currently in network of "
            + EnumChatFormatting.BLUE
            + SpaceProjectManager.getPlayerNameFromUUID(teamUUID)
            + EnumChatFormatting.RESET
            + ".");
}
```

**功能**:
- 通过玩家名获取UUID
- 检查玩家是否有能量网络
- 显示能量数量（使用`getUserEU`）
- 如果在团队中，显示团队leader

#### global_energy_join命令实现

```java
private void processGlobalEnergyJoinCommand(ICommandSender sender, String[] args) {
    // Usage is /gt global_energy_join username_of_you username_to_join

    String usernameSubject = args[1];
    String usernameTeam = args[2];

    String formattedUsernameSubject = EnumChatFormatting.BLUE + usernameSubject + EnumChatFormatting.RESET;
    String formattedUsernameTeam = EnumChatFormatting.BLUE + usernameTeam + EnumChatFormatting.RESET;

    UUID uuidSubject = SpaceProjectManager.getPlayerUUIDFromName(usernameSubject);
    UUID uuidTeam = SpaceProjectManager.getPlayerUUIDFromName(usernameTeam);

    if (uuidSubject.equals(uuidTeam)) {
        // leave team
        SpaceProjectManager.putInTeam(uuidSubject, uuidSubject);
        sendChatToPlayer(
            sender,
            "User " + formattedUsernameSubject + " has rejoined their own global energy network.");
        return;
    }

    // join other's team

    if (SpaceProjectManager.getLeader(uuidSubject)
        .equals(SpaceProjectManager.getLeader(uuidTeam))) {
        sendChatToPlayer(sender, "They are already in the same network!");
        return;
    }

    SpaceProjectManager.putInTeam(uuidSubject, uuidTeam);

    sendChatToPlayer(sender, "Success! " + formattedUsernameSubject + " has joined " + formattedUsernameTeam + ".");
    sendChatToPlayer(
        sender,
        "To undo this simply join your own network again with /gt global_energy_join " + formattedUsernameSubject
            + " "
            + formattedUsernameSubject
            + ".");
}
```

**功能**:
- 如果两个参数相同，则离开团队（创建自己的网络）
- 如果不同，则加入另一个玩家的团队
- 使用`SpaceProjectManager.putInTeam`来管理团队关系
- **注意**: 能量不会在离队时分割，留在原团队

---

## 其他相关文件

### 无线相关的Covers

找到的无线相关覆盖物文件：
- `CoverEnergyWireless.java` - 能量无线覆盖物
- `CoverEnergyWirelessDebug.java` - 调试版本
- `CoverWirelessController.java` - 无线控制器
- `CoverRedstoneWirelessBase.java` - 红石无线基类
- `CoverRedstoneTransmitterInternal.java` - 红石发送器
- `CoverRedstoneTransmitterExternal.java` - 红石发送器（外部）
- `CoverRedstoneReceiverExternal.java` - 红石接收器
- `CoverWirelessDoesWorkDetector.java` - 工作检测器
- `CoverWirelessItemDetector.java` - 物品检测器
- `CoverWirelessMaintenanceDetector.java` - 维护检测器
- `CoverWirelessFluidDetector.java` - 流体检测器

### 数据存储

相关的数据存储文件：
- `WirelessDataStore.java` - 无线数据存储
- `WirelessComputationPacket.java` - 无线计算数据包
- `GlobalVariableStorage.java` - 全局变量存储（包含GlobalEnergy map）
- `GlobalEnergyWorldSavedData.java` - 世界保存数据

---

## 关键设计要点

### 1. 能量存储使用BigInteger
```java
private static Map<UUID, BigInteger> GlobalEnergy;
```
- 原因：支持极大的能量值
- 缺点：操作比long/int慢
- 建议：批量操作，减少调用频率

### 2. 团队系统集成SpaceProjectManager
```java
UUID teamUUID = SpaceProjectManager.getLeader(user_uuid);
```
- 每个玩家默认在自己的团队（teamUUID = playerUUID）
- `putInTeam(subjectUUID, leaderUUID)`来加入团队
- 团队leader的UUID作为能量map的key

### 3. 能量操作是批量的
```java
public static long ticks_between_energy_addition = 100L * 20L; // 2000 ticks = 100秒
```
- 不是每tick传输能量
- 每2000 ticks（100秒）传输一次
- 每次传输大量能量以减少BigInteger操作

### 4. 数据持久化
```java
GlobalEnergyWorldSavedData.INSTANCE.markDirty();
```
- 每次修改能量都需要标记为dirty
- 数据保存在世界保存数据中
- 确保服务器重启后数据不丢失

---

## 使用示例

### 从玩家网络扣除能量（输入）
```java
UUID playerUUID = machine.getOwnerUuid();
long energyNeeded = 10000000L; // 10M EU

// 尝试扣除能量（传入负值）
if (WirelessNetworkManager.addEUToGlobalEnergyMap(playerUUID, -energyNeeded)) {
    // 成功扣除，可以给机器供能
    machine.increaseStoredEnergyUnits(energyNeeded, true);
} else {
    // 能量不足，无法扣除
}
```

### 向玩家网络存入能量（输出）
```java
UUID playerUUID = machine.getOwnerUuid();
long energyProduced = 5000000L; // 5M EU

// 从机器提取能量
machine.decreaseStoredEU(energyProduced, true);

// 存入玩家网络
WirelessNetworkManager.addEUToGlobalEnergyMap(playerUUID, energyProduced);
```

### 查询玩家能量
```java
UUID playerUUID = ...;
BigInteger currentEnergy = WirelessNetworkManager.getUserEU(playerUUID);
System.out.println("Player has: " + currentEnergy + " EU");
```

---

## 总结

GT5-Unofficial的无线能量网络系统：

1. **核心类**: `WirelessNetworkManager` 管理全局能量map
2. **覆盖物**: `CoverEnergyWireless` 实现能量提取/注入
3. **命令系统**: `GTMiscCommand` 提供管理命令
4. **团队系统**: 通过`SpaceProjectManager`实现玩家组队
5. **数据持久化**: 通过`GlobalEnergyWorldSavedData`保存数据

**与我之前虚构的代码对比**:
- ✅ 核心概念正确（UUID、全局能量、团队系统）
- ✅ 命令确实存在
- ❌ 我虚构的类名和方法名大部分是错的
- ❌ 实际使用的是`SpaceProjectManager`而非我编造的`GlobalEnergyManager`
- ❌ 实际方法是`addEUToGlobalEnergyMap`而非`decreaseEnergy`/`increaseEnergy`
- ❌ 能量map存储在`GlobalVariableStorage.GlobalEnergy`而非我编造的地方

**文档更新**: 2026-02-18
**源代码版本**: master分支最新版
**仓库**: https://github.com/GTNewHorizons/GT5-Unofficial
