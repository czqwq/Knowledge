# GT5-Unofficial Mixin 与 ASM 字节码注入完全指南

> **代码来源**: 本文档所有代码示例均直接摘自 GT5-Unofficial 本地克隆  
> **上游仓库**: https://github.com/GTNewHorizons/GT5-Unofficial  
> **Commit SHA**: 96f51372a1f38513a4ddbb4819a5ac864bac858f  
> **框架**: [GTNHMixins](https://github.com/GTNewHorizons/GTNHMixins) + [SpongePowered Mixin](https://github.com/SpongePowered/Mixin) + [MixinExtras](https://github.com/LlamaLad7/MixinExtras)

---

## 📚 目录

1. [什么是 Mixin](#一什么是-mixin)
2. [GT5U 目录结构](#二gt5u-目录结构)
3. [EarlyMixin — GTCorePlugin](#三earlymixin--gtcoreplugin)
4. [LateMixin — LateMixinPlugin](#四latemixin--latemixinplugin)
5. [Mixin 枚举注册中心](#五mixin-枚举注册中心)
6. [TargetedMod — 条件目标 Mod](#六targetedmod--条件目标-mod)
7. [JSON 配置文件](#七json-配置文件)
8. [Access Transformer (AT)](#八access-transformer-at)
9. [注入注解详解](#九注入注解详解)
   - [@Mixin](#1-mixin--目标类声明)
   - [@Inject](#2-inject--注入代码)
   - [@Redirect](#3-redirect--重定向方法调用)
   - [@ModifyArg](#4-modifyarg--修改方法参数)
   - [@ModifyReturnValue](#5-modifyreturnvalue--修改返回值mixinextras)
   - [@WrapOperation](#6-wrapoperation--包装方法调用mixinextras)
   - [@WrapWithCondition](#7-wrapwithcondition--条件执行mixinextras)
   - [@Overwrite](#8-overwrite--完全替换方法)
   - [@Shadow / @Final / @Unique](#9-shadow--final--unique--访问目标类成员)
10. [注入点 @At 详解](#十注入点-at-详解)
11. [Accessor 接口模式](#十一accessor-接口模式)
12. [共享状态 Helper 模式](#十二共享状态-helper-模式)
13. [污染系统完整示例](#十三污染系统完整示例)
14. [数量统计总览](#十四数量统计总览)

---

## 一、什么是 Mixin

**Mixin** 是一种在运行时（类加载阶段）向已有 Java 类注入字节码的技术，无需修改目标类的源代码。它由 SpongePowered 为 Minecraft Mod 开发设计，GT5U 使用 GTNHMixins 框架对其进行了封装。

**工作原理**:
```
JVM 加载 Target.class
      ↓
MixinPlugin 拦截类加载
      ↓
ASM 字节码转换器将 Mixin 类的字节码合并进 Target.class
      ↓
最终 Target.class 包含原始代码 + 注入代码
```

**GT5U 中的两个加载阶段**:
- **EARLY** — 在所有 Mod 的 CoreMod 加载后立即执行，只能安全引用 Minecraft / Forge 原版类
- **LATE** — 在所有 CoreMod 均已加载后执行，可以引用其他 Mod 的类（如 IC2、Railcraft 等）

---

## 二、GT5U 目录结构

```
GT5-Unofficial/
└── src/
    ├── main/
    │   ├── java/
    │   │   └── gregtech/
    │   │       ├── asm/
    │   │       │   └── GTCorePlugin.java          ← EarlyMixin 加载器 (IFMLLoadingPlugin + IEarlyMixinLoader)
    │   │       └── mixin/
    │   │           ├── Mixin.java                 ← 中央 Mixin 注册枚举 (IMixins)
    │   │           ├── LateMixinPlugin.java        ← LateMixin 加载器 (@LateMixin + ILateMixinLoader)
    │   │           ├── TargetedMod.java            ← 目标 Mod 枚举 (ITargetMod)
    │   │           ├── hooks/
    │   │           │   └── MixinsVariablesHelper.java  ← 跨 Mixin 共享状态
    │   │           └── interfaces/
    │   │               └── accessors/             ← Accessor 接口定义
    │   │                   ├── AbstractClientPlayerAccessor.java
    │   │                   ├── ChunkCacheAccessor.java
    │   │                   ├── EntityAccessor.java
    │   │                   ├── IRecipeMutableAccess.java
    │   │                   ├── LanguageRegistryAccessor.java
    │   │                   ├── TesselatorAccessor.java
    │   │                   └── ... (共 14 个)
    │   └── resources/
    │       ├── META-INF/
    │       │   └── gregtech_at.cfg                ← Access Transformer 配置
    │       ├── mixins.gregtech.early.json          ← Early Mixin JSON 配置
    │       └── mixins.gregtech.late.json           ← Late Mixin JSON 配置
    └── mixin/
        └── java/
            └── gregtech/mixin/mixins/
                ├── early/                          ← Phase.EARLY 的实现类
                │   ├── forge/
                │   │   ├── ForgeHooksMixin.java
                │   │   └── GameRegistryMixin.java
                │   └── minecraft/
                │       ├── AbstractClientPlayerMixin.java
                │       ├── ItemMixin.java
                │       ├── ItemStackMixin_MetaItemRemover.java
                │       ├── WorldMixin.java
                │       ├── SoundManagerMixin.java
                │       ├── ...
                │       ├── accessors/              ← Accessor 实现类
                │       │   ├── ChunkCacheMixin.java
                │       │   ├── PotionMixin.java
                │       │   ├── VanillaShapedRecipeMixin.java
                │       │   └── ... (共 13 个)
                │       └── pollution/              ← 污染系统 Mixin
                │           ├── MixinExplosionPollution.java
                │           ├── MixinTileEntityFurnacePollution.java
                │           └── ...
                └── late/                           ← Phase.LATE 的实现类
                    ├── advanced_solar_panels/
                    ├── biomesoplenty/
                    ├── efr/
                    ├── galacticraftcore/
                    ├── hee/
                    ├── ic2/
                    │   ├── MixinDamageDropped.java
                    │   ├── MixinHarvestTool.java
                    │   ├── MixinIc2Hazmat.java
                    │   └── ...
                    ├── natura/
                    ├── railcraft/
                    ├── thaumcraft/
                    └── tinkersconstruct/
```

> **注意**: `src/mixin/java` 是独立的 Gradle sourceSet，与 `src/main/java` 分开编译，专门存放 Mixin 实现类。

---

## 三、EarlyMixin — GTCorePlugin

**文件路径**: `src/main/java/gregtech/asm/GTCorePlugin.java`

EarlyMixin 通过实现 `IFMLLoadingPlugin`（FML CoreMod 接口）和 `IEarlyMixinLoader`（GTNHMixins 接口）来注册。它在游戏最早期（CoreMod 阶段）加载，此时其他 Mod 的类尚未初始化。

```java
// src/main/java/gregtech/asm/GTCorePlugin.java (第 1-76 行)
package gregtech.asm;

import java.util.List;
import java.util.Map;
import java.util.Set;

import com.gtnewhorizon.gtnhlib.config.ConfigException;
import com.gtnewhorizon.gtnhlib.config.ConfigurationManager;
import com.gtnewhorizon.gtnhmixins.IEarlyMixinLoader;
import com.gtnewhorizon.gtnhmixins.builders.IMixins;

import bartworks.common.configs.Configuration;
import cpw.mods.fml.relauncher.IFMLLoadingPlugin;
import gregtech.api.util.scanner.ScannerConfig;
import gregtech.common.pollution.PollutionConfig;
import gregtech.mixin.Mixin;
import gtPlusPlus.core.config.ASMConfiguration;

@IFMLLoadingPlugin.MCVersion("1.7.10")
@IFMLLoadingPlugin.TransformerExclusions({ "gregtech.asm" })   // 排除自身包，避免被转换
@IFMLLoadingPlugin.Name("GregTech 5 Unofficial core plugin")
public class GTCorePlugin implements IFMLLoadingPlugin, IEarlyMixinLoader {

    static {
        // 在最早阶段注册配置文件（此时 @Config 注解还未处理）
        try {
            ConfigurationManager.registerConfig(ASMConfiguration.class);
            ConfigurationManager.registerConfig(Configuration.class);
            ConfigurationManager.registerConfig(PollutionConfig.class);
            ConfigurationManager.registerConfig(ScannerConfig.class);
        } catch (ConfigException e) {
            throw new RuntimeException(e);
        }
    }

    private static boolean DEV_ENVIRONMENT;

    @Override
    public String[] getASMTransformerClass() {
        return null;  // GT5U 不使用自定义 ASM Transformer（改用 Mixin）
    }

    @Override
    public String getModContainerClass() { return null; }

    @Override
    public String getSetupClass() { return null; }

    @Override
    public void injectData(Map<String, Object> data) {
        // 判断是否为开发环境（影响是否进行运行时反混淆）
        DEV_ENVIRONMENT = !(boolean) data.get("runtimeDeobfuscationEnabled");
    }

    @Override
    public String getAccessTransformerClass() { return null; }

    // ---- IEarlyMixinLoader 接口方法 ----

    @Override
    public String getMixinConfig() {
        return "mixins.gregtech.early.json";  // 对应 src/main/resources/mixins.gregtech.early.json
    }

    @Override
    public List<String> getMixins(Set<String> loadedCoreMods) {
        // IMixins.getEarlyMixins 根据 loadedCoreMods 过滤 Mixin 枚举，只返回 Phase.EARLY 且满足条件的类名
        return IMixins.getEarlyMixins(Mixin.class, loadedCoreMods);
    }

    public static boolean isDevEnv() {
        return DEV_ENVIRONMENT;
    }
}
```

**必须在 `META-INF/MANIFEST.MF` 中声明**（Gradle 构建时自动生成）:
```
FMLCorePlugin: gregtech.asm.GTCorePlugin
FMLCorePluginContainsFMLMod: true
```

---

## 四、LateMixin — LateMixinPlugin

**文件路径**: `src/main/java/gregtech/mixin/LateMixinPlugin.java`

LateMixin 通过 GTNHMixins 的 `@LateMixin` 注解标记，实现 `ILateMixinLoader` 接口。它在所有 CoreMod 加载完毕后执行，因此可以安全引用 IC2、Railcraft、Thaumcraft 等第三方 Mod 的类。

```java
// src/main/java/gregtech/mixin/LateMixinPlugin.java (第 1-22 行)
package gregtech.mixin;

import java.util.List;
import java.util.Set;

import com.gtnewhorizon.gtnhmixins.ILateMixinLoader;
import com.gtnewhorizon.gtnhmixins.LateMixin;
import com.gtnewhorizon.gtnhmixins.builders.IMixins;

@LateMixin  // GTNHMixins 注解，标记此类为 LateMixin 加载器
public class LateMixinPlugin implements ILateMixinLoader {

    @Override
    public String getMixinConfig() {
        return "mixins.gregtech.late.json";  // 对应 src/main/resources/mixins.gregtech.late.json
    }

    @Override
    public List<String> getMixins(Set<String> loadedMods) {
        // IMixins.getLateMixins 根据 loadedMods 过滤 Mixin 枚举，只返回 Phase.LATE 且满足条件的类名
        return IMixins.getLateMixins(Mixin.class, loadedMods);
    }
}
```

### EarlyMixin vs LateMixin 对比

| 特性 | EarlyMixin (Phase.EARLY) | LateMixin (Phase.LATE) |
|------|--------------------------|------------------------|
| 加载时机 | CoreMod 阶段，最早 | 所有 CoreMod 加载后 |
| 实现接口 | `IEarlyMixinLoader` | `ILateMixinLoader` |
| 注解标记 | `@IFMLLoadingPlugin` | `@LateMixin` |
| 可引用的类 | Minecraft / Forge 原版类 | 任意已加载 Mod 的类 |
| 配置文件 | `mixins.gregtech.early.json` | `mixins.gregtech.late.json` |
| getMixins 参数 | `Set<String> loadedCoreMods` | `Set<String> loadedMods` |
| IMixins 方法 | `getEarlyMixins()` | `getLateMixins()` |
| 典型用途 | 修改 Minecraft 核心逻辑 | 修改 IC2/RC/TC 等 Mod 行为 |

---

## 五、Mixin 枚举注册中心

**文件路径**: `src/main/java/gregtech/mixin/Mixin.java`

GT5U 使用一个 `enum Mixin implements IMixins` 作为所有 Mixin 的统一注册中心。每个枚举项代表一组相关的 Mixin 类，通过 `MixinBuilder` 定义其属性。

```java
// src/main/java/gregtech/mixin/Mixin.java (第 1-196 行，节选关键部分)
package gregtech.mixin;

import com.gtnewhorizon.gtnhmixins.builders.IMixins;
import com.gtnewhorizon.gtnhmixins.builders.MixinBuilder;
import gregtech.common.config.Gregtech;
import gregtech.common.pollution.PollutionConfig;

public enum Mixin implements IMixins {

    // ---- Phase.EARLY: 只能引用 Minecraft/Forge 类 ----

    // addClientMixins: 仅客户端加载
    GregtechCapes(new MixinBuilder()
        .addClientMixins("minecraft.AbstractClientPlayerMixin")
        .setPhase(Phase.EARLY)),

    // addCommonMixins: 客户端和服务端均加载，同时注册多个 Mixin
    SoundManagerMixin(new MixinBuilder("Seeking sound playback")
        .addClientMixins(
            "minecraft.SoundManagerMixin",
            "minecraft.SoundManagerInnerMixin")
        .setPhase(Phase.EARLY)),

    WorldMixin(new MixinBuilder("Block update detection")
        .addCommonMixins("minecraft.WorldMixin")
        .setPhase(Phase.EARLY)),

    // 一次注册多个 Accessor Mixin（common + client 分别列）
    VANILLA_ACCESSORS(new MixinBuilder()
        .addCommonMixins(
            "minecraft.accessors.BlockStemMixin",
            "minecraft.accessors.ChunkCacheMixin",
            "minecraft.accessors.VanillaShapedRecipeMixin",
            "minecraft.accessors.VanillaShapelessRecipeMixin",
            "minecraft.accessors.ForgeShapedRecipeMixin",
            "minecraft.accessors.ForgeShapelessRecipeMixin",
            "minecraft.accessors.ItemArmorMixin",
            "minecraft.accessors.PotionMixin",
            "minecraft.accessors.EntityPlayerMPMixin",
            "minecraft.accessors.WeightedRandomFishableMixin",
            "minecraft.accessors.EntityMixin",
            "minecraft.accessors.LanguageRegistryMixin",
            "minecraft.accessors.EntityItemMixin")
        .addClientMixins(
            "minecraft.accessors.GuiTextFieldMixin",
            "minecraft.accessors.TessellatorMixin")
        .setPhase(Phase.EARLY)),

    // setApplyIf: 运行时条件判断（读取配置）
    VanillaToolChanges(
        new MixinBuilder("Changes wooden tools to be a little faster")
            .addCommonMixins("minecraft.ItemToolMaterialMixin")
            .setApplyIf(() -> Gregtech.general.changedWoodenVanillaTools)
            .setPhase(Phase.EARLY)),

    // ---- Phase.LATE: 可引用第三方 Mod 类 ----

    // addRequiredMod: 仅当目标 Mod 已加载时才应用此 Mixin
    HEEAccessors(new MixinBuilder("Various accessors for Hardcore Ender Expansion")
        .addCommonMixins("hee.ChunkProviderHardcoreEndMixin", "hee.MapGenIslandMixin")
        .addRequiredMod(TargetedMod.HEE)
        .setPhase(Phase.LATE)),

    IC2_MACHINE_WRENCHING(new MixinBuilder("Changes the behavior of the wrenching mechanic for IC2 machines")
        .addCommonMixins(
            "ic2.MixinDamageDropped",
            "ic2.MixinHarvestTool",
            "ic2.MixinItemDropped")
        .addRequiredMod(TargetedMod.IC2)
        .setPhase(Phase.LATE)),

    // addExcludedMod: 排除某个 Mod 存在时不应用
    IC2_HAZMAT(new MixinBuilder()
        .setPhase(Phase.LATE)
        .addCommonMixins(
            "ic2.MixinIc2Hazmat",
            "ic2.MixinIc2Nano",
            "ic2.MixinIc2Quantum")
        .addRequiredMod(TargetedMod.IC2)
        .addExcludedMod(TargetedMod.GT6)),  // GT6 存在时不应用（避免冲突）

    // RequiredMod + ExcludedMod + ApplyIf 可组合使用
    POLLUTION_RENDER_BLOCKS_OPTIFINE(new MixinBuilder()
        .addClientMixins("minecraft.pollution.MixinRenderBlocks_PollutionWithOptifine")
        .addRequiredMod(TargetedMod.OPTIFINE)
        .addExcludedMod(TargetedMod.ANGELICA)
        .setApplyIf(() -> PollutionConfig.pollution && PollutionConfig.pollutionBlockRecolor)
        .setPhase(Phase.EARLY));

    private final MixinBuilder builder;

    Mixin(MixinBuilder builder) {
        this.builder = builder;
    }

    @Override
    public MixinBuilder getBuilder() {
        return this.builder;
    }
}
```

### MixinBuilder API 速查

| 方法 | 说明 |
|------|------|
| `new MixinBuilder()` | 创建 Builder，无描述 |
| `new MixinBuilder("描述")` | 创建 Builder，带描述（用于日志） |
| `.addCommonMixins("pkg.ClassName", ...)` | 注册 common（客户端+服务端）Mixin |
| `.addClientMixins("pkg.ClassName", ...)` | 注册 client-only Mixin |
| `.setPhase(Phase.EARLY)` | 设为 EarlyMixin |
| `.setPhase(Phase.LATE)` | 设为 LateMixin |
| `.addRequiredMod(TargetedMod.X)` | 仅当 Mod X 已加载时应用 |
| `.addExcludedMod(TargetedMod.X)` | 当 Mod X 存在时不应用 |
| `.setApplyIf(() -> condition)` | 运行时 boolean 条件（支持读取配置） |

> **类名说明**: `addCommonMixins` / `addClientMixins` 的字符串是相对于 JSON 配置的 `package` 字段的短类名。  
> - Early: `package = "gregtech.mixin.mixins.early"`，故 `"minecraft.WorldMixin"` → `gregtech.mixin.mixins.early.minecraft.WorldMixin`  
> - Late: `package = "gregtech.mixin.mixins.late"`，故 `"ic2.MixinHarvestTool"` → `gregtech.mixin.mixins.late.ic2.MixinHarvestTool`

---

## 六、TargetedMod — 条件目标 Mod

**文件路径**: `src/main/java/gregtech/mixin/TargetedMod.java`

```java
// src/main/java/gregtech/mixin/TargetedMod.java (第 1-36 行)
package gregtech.mixin;

import com.gtnewhorizon.gtnhmixins.builders.ITargetMod;
import com.gtnewhorizon.gtnhmixins.builders.TargetModBuilder;

public enum TargetedMod implements ITargetMod {

    // 参数1: CoreMod 类名（有 CoreMod 的 Mod），null 表示无 CoreMod
    // 参数2: Mod ID（FML modId）
    ADVANCED_SOLAR_PANELS(null, "AdvancedSolarPanel"),
    ANGELICA("com.gtnewhorizons.angelica.loading.AngelicaTweaker", "angelica"),
    BIOMESOPLENTY(null, "BiomesOPlenty"),
    EFR(null, "etfuturum"),
    GALACTICRAFT_CORE("micdoodle8.mods.galacticraft.core.asm.GCLoadingPlugin", "GalacticraftCore"),
    GT6("gregtech.asm.GT_ASM", "gregapi"),
    HEE("chylex.hee.HEECore", "HardcoreEnderExpansion"),
    IC2("ic2.core.coremod.IC2core", "IC2"),
    NATURA(null, "Natura"),
    OPTIFINE("optifine.OptiFineForgeTweaker", "Optifine"),
    RAILCRAFT(null, "Railcraft"),
    THAUMCRAFT(null, "Thaumcraft"),
    TINKERSCONSTRUCT(null, "TConstruct");

    private final TargetModBuilder builder;

    TargetedMod(String coreModClass, String modId) {
        this.builder = new TargetModBuilder()
            .setCoreModClass(coreModClass)
            .setModId(modId);
    }

    @Override
    public TargetModBuilder getBuilder() {
        return builder;
    }
}
```

**检测逻辑说明**:
- 对于 **Early** 阶段（`loadedCoreMods` 是 CoreMod 类名集合），若 `coreModClass != null`，则用 `coreModClass` 判断是否已加载；若 `coreModClass == null`，则该 Mod 无法在 Early 阶段检测（不应在 Early 阶段用 `addRequiredMod` 引用它）
- 对于 **Late** 阶段（`loadedMods` 是 modId 集合），用 `modId` 判断是否已加载

---

## 七、JSON 配置文件

GT5U 有三个 Mixin 配置 JSON，实际的 `mixins` 列表为空（由 `MixinPlugin` 动态注入），但 `package`、`refmap`、`compatibilityLevel` 等元数据必须正确。

### `mixins.gregtech.early.json`

**路径**: `src/main/resources/mixins.gregtech.early.json`

```json
{
  "required": true,
  "minVersion": "0.8.5-GTNH",
  "package": "gregtech.mixin.mixins.early",
  "refmap": "mixins.gregtech.refmap.json",
  "target": "@env(DEFAULT)",
  "compatibilityLevel": "JAVA_8",
  "mixins": [],
  "client": [],
  "server": []
}
```

### `mixins.gregtech.late.json`

**路径**: `src/main/resources/mixins.gregtech.late.json`

```json
{
  "required": true,
  "minVersion": "0.8.5-GTNH",
  "package": "gregtech.mixin.mixins.late",
  "refmap": "mixins.gregtech.refmap.json",
  "target": "@env(DEFAULT)",
  "compatibilityLevel": "JAVA_8",
  "mixins": [],
  "client": [],
  "server": []
}
```

**字段说明**:
| 字段 | 说明 |
|------|------|
| `required` | `true` 表示若 Mixin 应用失败则报错崩溃 |
| `minVersion` | 最低 Mixin 框架版本 |
| `package` | 此配置下所有 Mixin 类的包前缀 |
| `refmap` | 编译产物，记录混淆名到 MCP 名的映射 |
| `target` | 目标环境，`@env(DEFAULT)` 表示当前环境 |
| `compatibilityLevel` | Java 语言级别 |
| `mixins` | common Mixin 类名列表（此处动态注入，为空） |
| `client` | client-only Mixin 类名列表 |
| `server` | server-only Mixin 类名列表 |

---

## 八、Access Transformer (AT)

**路径**: `src/main/resources/META-INF/gregtech_at.cfg`

AT 用于将目标类的 `private`/`protected` 字段或方法提升为 `public`，使 Mixin 或其他代码可以直接访问。

```cfg
# src/main/resources/META-INF/gregtech_at.cfg

# GT - 将 SoundHandler 的私有字段提升为 public
public net.minecraft.client.audio.SoundHandler field_147697_e # sndRegistry
public net.minecraft.client.audio.SoundHandler field_147694_f # sndManager
public net.minecraft.item.ItemRecord field_150928_b # field_150928_b / all registered records
# GGFab
public net.minecraft.nbt.NBTTagList field_74747_a # tagList
public net.minecraft.nbt.NBTTagCompound field_74784_a # tagMap
# TecTech
public net.minecraft.block.Block field_149781_w # blockResistance
public net.minecraft.block.Block field_149782_v # blockHardness
```

**格式**: `<访问级别> <完全限定类名> <SRG字段名/方法签名>`  
`public`、`protected`、`private` 均可，常用 `public` 将字段开放。

**AT 与 @Shadow 的区别**:
- `@Shadow` 在 Mixin 类内部访问字段，仅在 Mixin 代码中生效
- AT 全局提升访问级别，整个 Mod 代码均可直接访问

---

## 九、注入注解详解

所有 Mixin 实现类位于 `src/mixin/java/gregtech/mixin/mixins/` 下，分 `early/` 和 `late/` 两个子目录。

### 1. `@Mixin` — 目标类声明

声明当前类是哪个目标类的 Mixin。

```java
// 方式一: 直接引用 Class（常用于已知类）
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/WorldMixin.java
@Mixin(value = World.class)
public class WorldMixin { ... }

// 方式二: 多目标同时 Mixin（合并多个类的相同修改）
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinHarvestTool.java
@Mixin(
    value = { ic2.core.block.BlockTileEntity.class,
               ic2.core.block.machine.BlockMachine.class,
               ic2.core.block.machine.BlockMachine2.class,
               ic2.core.block.machine.BlockMachine3.class,
               /* ... 共 16 个 IC2 方块类 */ })
public class MixinHarvestTool extends Block { ... }

// 方式三: 用字符串引用内部类或无法直接 import 的类（remap=false 时不做混淆映射）
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/SoundManagerInnerMixin.java
@Mixin(targets = "net.minecraft.client.audio.SoundManager$2$1")
public abstract class SoundManagerInnerMixin { ... }

// 方式四: remap=false — 目标类不做混淆映射（针对非 Minecraft 原版类）
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinIc2Hazmat.java
@Mixin(value = ItemArmorHazmat.class, remap = false)
public class MixinIc2Hazmat implements IHazardProtector { ... }
```

---

### 2. `@Inject` — 注入代码

在目标方法的指定位置插入代码。是最常用的注解。

**示例 1: 在方法头部注入，并取消原方法执行 (`cancellable = true`)**
```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/ItemStackMixin_MetaItemRemover.java
@Mixin(ItemStack.class)
public class ItemStackMixin_MetaItemRemover {

    @Inject(method = "loadItemStackFromNBT", at = @At("HEAD"), cancellable = true)
    @SuppressWarnings("unused")
    private static void gt5u$RemoveInvalidMetaItems(NBTTagCompound p_77949_0_,
                                                     CallbackInfoReturnable<ItemStack> cir) {
        var id = p_77949_0_.getShort("id");
        var meta = p_77949_0_.getInteger("Damage");

        if (RemovedMetaRegistry.contains(id, meta)) {
            cir.setReturnValue(null);  // 设置返回值并取消原方法
        }
    }
}
```

**示例 2: 在方法头部注入，修改配置（无返回值方法用 `CallbackInfo`）**
```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/LanguageRegistryMixin.java
@Mixin(value = LanguageRegistry.class)
public class LanguageRegistryMixin {

    // 方法头注入：记录当前翻译的 Mod
    @Inject(method = "loadLanguagesFor", at = @At(value = "HEAD"), remap = false, require = 1)
    private void gt5u$loadLanguagesForHEAD(ModContainer container, Side side, CallbackInfo callbackInfo) {
        MixinsVariablesHelper.currentlyTranslating = container.getModId();
    }

    // 方法返回时注入：清除记录
    @Inject(method = "loadLanguagesFor", at = @At(value = "RETURN"), remap = false, require = 1)
    private void gt5u$loadLanguagesForRETURN(ModContainer container, Side side, CallbackInfo callbackInfo) {
        MixinsVariablesHelper.currentlyTranslating = null;
    }
}
```

**示例 3: 在特定字段访问处注入（`FIELD` + `opcode`）**
```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/pollution/MixinTileEntityFurnacePollution.java
@Mixin(TileEntityFurnace.class)
public abstract class MixinTileEntityFurnacePollution extends TileEntity {

    @Inject(
        method = "updateEntity",
        at = @At(
            value = "FIELD",
            target = "net/minecraft/tileentity/TileEntityFurnace.furnaceBurnTime:I",
            opcode = Opcodes.GETFIELD,   // 指定字段读操作
            ordinal = 2))               // 第三次（index=2）访问该字段时注入
    private void gt5u$addPollution(CallbackInfo ci) {
        furnaceAddPollutionOnUpdate(this.worldObj, this.xCoord, this.zCoord,
                                   FurnacePollution.FURNACE.getPollution());
    }
}
```

**示例 4: 捕获局部变量 (`LocalCapture.CAPTURE_FAILHARD`) 并取消**
```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/VanillaTradingMixin.java
@Mixin(EntityVillager.class)
public class VanillaTradingMixin {

    @Inject(method = "func_146089_b", at = @At("HEAD"),
            locals = LocalCapture.CAPTURE_FAILHARD,
            cancellable = true)
    private static void gt5u$removeEyeOfEnder(MerchantRecipeList p_146089_0_,
                                               Item p_146089_1_,
                                               Random p_146089_2_,
                                               float p_146089_3_,
                                               CallbackInfo ci) {
        if (p_146089_1_.equals(Items.ender_eye)) {
            ci.cancel();  // 禁止村民出售末影之眼
        }
    }
}
```

**示例 5: 在 INVOKE 前后各注入一次（`shift = At.Shift.BEFORE/AFTER`）**
```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/MinecraftMixin_MouseOver.java
@Mixin(Minecraft.class)
public class MinecraftMixin_MouseOver {

    @Inject(
        method = "runTick",
        at = @At(
            value = "INVOKE",
            shift = At.Shift.BEFORE,
            target = "Lnet/minecraft/client/renderer/EntityRenderer;getMouseOver(F)V"))
    private void gt5u$before$getMouseOver(CallbackInfo ci) {
        if (GTMod.proxy != null) GTMod.clientProxy().setComputingPickBlock(true);
    }

    @Inject(
        method = "runTick",
        at = @At(
            value = "INVOKE",
            shift = At.Shift.AFTER,
            target = "Lnet/minecraft/client/renderer/EntityRenderer;getMouseOver(F)V"))
    private void gt5u$after$getMouseOver(CallbackInfo ci) {
        if (GTMod.proxy != null) GTMod.clientProxy().setComputingPickBlock(false);
    }
}
```

**`@Inject` 常用参数**:
| 参数 | 类型 | 说明 |
|------|------|------|
| `method` | `String` | 目标方法名，可加参数描述符 |
| `at` | `@At` | 注入点 |
| `cancellable` | `boolean` | 允许调用 `ci.cancel()` 取消原方法 |
| `require` | `int` | 必须匹配的注入点数量（`1` 表示必须找到，否则报错） |
| `remap` | `boolean` | 是否对方法名做混淆映射（非 MC 原版方法设 `false`） |
| `locals` | `LocalCapture` | 局部变量捕获策略 |

---

### 3. `@Redirect` — 重定向方法调用

将目标方法中的某个方法调用完全替换为 Mixin 中的代码。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/StringTranslateMixin.java
@Mixin(value = StringTranslate.class)
public class StringTranslateMixin {

    // 将 parseLangFile 方法中调用 Matcher.replaceAll 的地方重定向到此方法
    @Redirect(
        method = "parseLangFile",
        at = @At(
            value = "INVOKE",
            target = "Ljava/util/regex/Matcher;replaceAll(Ljava/lang/String;)Ljava/lang/String;",
            remap = false),
        remap = false,
        require = 1)
    private static String gt5u$replaceAll(Matcher matcher, String replace) {
        // 对 kubatech 模组的翻译文件只做 replaceFirst 而非 replaceAll
        if (MixinsVariablesHelper.currentlyTranslating != null
            && MixinsVariablesHelper.currentlyTranslating.equals(Tags.MODID)
            && matcher.find()) {
            return matcher.replaceFirst(matcher.group());
        }
        return matcher.replaceAll(replace);
    }
}
```

---

### 4. `@ModifyArg` — 修改方法参数

修改调用某个方法时传入的某个参数，其他参数不变。

```java
// src/mixin/java/gregtech/mixin/mixins/early/forge/GameRegistryMixin.java
@Mixin(GameRegistry.class)
public class GameRegistryMixin {

    // 修改 computeSortedGeneratorList 中传给 ImmutableList.copyOf 的 Collection 参数
    @ModifyArg(
        method = "computeSortedGeneratorList",
        at = @At(
            value = "INVOKE",
            target = "Lcom/google/common/collect/ImmutableList;copyOf(Ljava/util/Collection;)Lcom/google/common/collect/ImmutableList;",
            remap = false),
        remap = false)
    private static Collection<IWorldGenerator> gt5u$worldgenOrderFix(Collection<IWorldGenerator> elements) {
        // 将 GTWorldgenerator 移到列表末尾，确保最后运行
        List<IWorldGenerator> gtWorldgens = new ArrayList<>();
        for (Iterator<IWorldGenerator> iterator = elements.iterator(); iterator.hasNext();) {
            IWorldGenerator worldgen = iterator.next();
            if (worldgen instanceof GTWorldgenerator) {
                gtWorldgens.add(worldgen);
                iterator.remove();
            }
        }
        elements.addAll(gtWorldgens);
        return elements;
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/LocaleMixin.java (节选)
@Mixin(value = Locale.class)
public class LocaleMixin {

    // 修改 loadLocaleDataFiles 调用 getAllResources 时传入的 ResourceLocation 参数（index=0）
    @ModifyArg(
        method = "loadLocaleDataFiles",
        at = @At(
            value = "INVOKE",
            target = "Lnet/minecraft/client/resources/IResourceManager;getAllResources(Lnet/minecraft/util/ResourceLocation;)Ljava/util/List;"),
        index = 0,   // 第 0 个参数
        require = 1)
    private ResourceLocation gt5u$loadLocaleDataFiles(ResourceLocation resourceLocation) {
        // 记录当前正在翻译的 domain
        MixinsVariablesHelper.currentlyTranslating = resourceLocation.getResourceDomain();
        return resourceLocation;
    }
}
```

---

### 5. `@ModifyReturnValue` — 修改返回值（MixinExtras）

来自 MixinExtras 库，在方法 RETURN 时修改其返回值，比 `@Inject + CallbackInfoReturnable` 更简洁。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/WorldMixin.java
@Mixin(value = World.class)
public class WorldMixin {

    // 修改 getBlock 方法的返回值
    @ModifyReturnValue(method = "getBlock", at = @At("RETURN"), require = 1)
    private Block gt5u$getBlockDetector(Block block, int x, int y, int z) {
        if (block == BlockLoader.kubaBlock)
            BlockLoader.kubaBlock.setLastBlockAccess((World) (Object) this, x, y, z);
        return block;  // 返回原 block，同时触发了 setLastBlockAccess 副作用
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/AbstractClientPlayerMixin.java (节选)
@Mixin(AbstractClientPlayer.class)
public class AbstractClientPlayerMixin implements AbstractClientPlayerAccessor {

    @Unique
    private ResourceLocation gt$locationCape;

    // 修改 hasCape 检查的返回值
    @ModifyReturnValue(method = "func_152122_n", at = @At(value = "RETURN"))
    private boolean gt5u$hasCape(boolean original) {
        return gt$locationCape != null || original;  // 有 GT 斗篷时也返回 true
    }

    // 修改 getLocationCape 的返回值
    @ModifyReturnValue(method = "getLocationCape", at = @At(value = "RETURN"))
    private ResourceLocation gt5u$getCape(ResourceLocation original) {
        return gt$locationCape != null ? gt$locationCape : original;  // 优先返回 GT 斗篷
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/early/forge/ForgeHooksMixin.java
@Mixin(value = ForgeHooks.class, remap = false)
public class ForgeHooksMixin {

    // 修改 blockStrength 的返回值（用于 GT 工具特殊挖掘速度逻辑）
    @ModifyReturnValue(method = "blockStrength", at = @At("RETURN"))
    private static float gt$blockStrengthHack(float original, Block block, EntityPlayer player,
                                               World world, int x, int y, int z) {
        ItemStack stack = player.getCurrentEquippedItem();
        if (stack != null && stack.getItem() instanceof MetaGeneratedTool tool) {
            return tool.getBlockStrength(stack, block, player, world, x, y, z, original);
        }
        return original;
    }
}
```

---

### 6. `@WrapOperation` — 包装方法调用（MixinExtras）

将目标方法中某次方法调用包装，可在调用前后添加逻辑，或完全替换该调用。通过 `Operation<T>` 参数调用原始操作。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/SoundManagerMixin.java (节选)
@Mixin(SoundManager.class)
public class SoundManagerMixin {

    // 包装 SoundPoolEntry.getSoundPoolEntryLocation() 调用
    @WrapOperation(
        method = "playSound",
        at = @At(
            value = "INVOKE",
            target = "Lnet/minecraft/client/audio/SoundPoolEntry;getSoundPoolEntryLocation()Lnet/minecraft/util/ResourceLocation;"))
    ResourceLocation gt5u$wrap(SoundPoolEntry instance, Operation<ResourceLocation> original,
                                @Local(argsOnly = true) ISound sound) {
        ResourceLocation result = original.call(instance);  // 调用原方法
        if (sound instanceof ISeekingSound seekingSound) {
            // 如果是 seeking 音效，修改 ResourceLocation
            result = SeekingOggCodec.seekResource(result, seekingSound.getSeekMillisecondOffset());
        }
        return result;
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/SoundManagerInnerMixin.java
@Mixin(targets = "net.minecraft.client.audio.SoundManager$2$1")
public abstract class SoundManagerInnerMixin {

    // 包装 IResourceManager.getResource 调用，在调用前剥离 Seek 元数据
    @WrapOperation(
        method = "getInputStream",
        at = @At(
            value = "INVOKE",
            target = "Lnet/minecraft/client/resources/IResourceManager;getResource(Lnet/minecraft/util/ResourceLocation;)Lnet/minecraft/client/resources/IResource;"))
    IResource gt5u$stripSeekParams(IResourceManager instance, ResourceLocation location,
                                    Operation<IResource> original) {
        if (location.getResourcePath().endsWith(SeekingOggCodec.EXTENSION)) {
            location = new ResourceLocation(
                location.getResourceDomain(),
                SeekingOggCodec.stripSeekMetadata(location.getResourcePath()));
        }
        return original.call(instance, location);  // 调用原方法（传入修改后的参数）
    }
}
```

---

### 7. `@WrapWithCondition` — 条件执行（MixinExtras）

包装某个 void 方法调用，返回 `boolean` 决定是否执行原调用。`true` → 执行原调用，`false` → 跳过。

```java
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinIc2FissionFuelRemoval.java
@Mixin(value = ItemIC2.class, remap = false)
public class MixinIc2FissionFuelRemoval {

    // 包装 GameRegistry.registerItem 调用，阻止某些 IC2 核燃料物品注册
    @WrapWithCondition(
        method = "<init>",
        at = @At(
            value = "INVOKE",
            target = "Lcpw/mods/fml/common/registry/GameRegistry;registerItem(Lnet/minecraft/item/Item;Ljava/lang/String;)V"))
    private boolean gt5u$wrapRegister(Item item, String name) {
        switch (name) {
            case "reactorMOXSimpledepleted":
            case "reactorMOXDualdepleted":
            case "reactorMOXQuaddepleted":
            case "reactorUraniumSimpledepleted":
            case "reactorUraniumDualdepleted":
            case "reactorUraniumQuaddepleted":
            case "reactorLithiumCell":
            case "itemTritiumCell":
                return false;  // 返回 false：跳过这些物品的注册
            default:
                return true;   // 返回 true：正常注册
        }
    }
}
```

---

### 8. `@Overwrite` — 完全替换方法

完全覆盖目标类的某个方法，需要加 Javadoc 说明 `@author` 和 `@reason`（强制规范，缺少会有警告）。

```java
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinIc2Hazmat.java
@Mixin(value = ItemArmorHazmat.class, remap = false)
public class MixinIc2Hazmat implements IHazardProtector {

    /**
     * @author Sphyix
     * @reason Hazmat - IC2 logic superseded by GT check
     */
    @Overwrite
    public static boolean hasCompleteHazmat(EntityLivingBase entity) {
        // 完全替换 IC2 的防化服检测，改用 GT 自己的 API
        return HazardProtection.isWearingFullRadioHazmat(entity);
    }

    @Override
    public boolean protectsAgainst(ItemStack itemStack, Hazard hazard) {
        return true;
    }
}
```

> ⚠️ **注意**: `@Overwrite` 与其他 Mixin 可能发生冲突，且会在目标方法变化时静默失效，**应尽量避免使用**，优先用 `@Inject(cancellable=true)` 代替。

---

### 9. `@Shadow` / `@Final` / `@Unique` — 访问目标类成员

**`@Shadow`**: 声明一个与目标类成员同名的"幽灵"字段/方法，实际指向目标类中的对应成员，使 Mixin 代码可以访问它。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/pollution/MixinExplosionPollution.java
@Mixin(Explosion.class)
public class MixinExplosionPollution {

    @Shadow public float explosionSize;   // 引用目标类的 explosionSize 字段
    @Shadow private World worldObj;        // 引用目标类的 worldObj 字段
    @Shadow public double explosionX;
    @Shadow public double explosionZ;

    @Inject(method = "doExplosionA", at = @At(value = "TAIL"))
    public void gt5u$addExplosionPollution(CallbackInfo ci) {
        if (!this.worldObj.isRemote) {
            Pollution.addPollution(
                this.worldObj.getChunkFromBlockCoords((int) this.explosionX, (int) this.explosionZ),
                (int) Math.ceil(explosionSize * PollutionConfig.explosionPollutionAmount));
        }
    }
}
```

**`@Final`**: 与 `@Shadow` 配合使用，标记该字段在目标类中是 `final` 的（用于文档性标注，有些 Mixin 工具依赖它来防止意外写入）。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/accessors/PotionMixin.java
@Mixin(Potion.class)
public class PotionMixin implements PotionAccessor {

    @Shadow
    @Final              // 告知 Mixin 框架这是 final 字段
    private boolean isBadEffect;

    @Override
    public boolean gt5u$isBadEffect() {
        return this.isBadEffect;
    }
}
```

**`@Unique`**: 在 Mixin 中声明一个全新字段（不存在于目标类），会被直接注入到目标类中。命名需要唯一，通常加 Mod 前缀。

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/AbstractClientPlayerMixin.java
@Mixin(AbstractClientPlayer.class)
public class AbstractClientPlayerMixin implements AbstractClientPlayerAccessor {

    @Unique
    private ResourceLocation gt$locationCape;  // 向目标类注入一个全新字段

    @Override
    public void gt5u$setCape(ResourceLocation gtCape) {
        gt$locationCape = gtCape;
    }
}
```

---

## 十、注入点 `@At` 详解

`@At` 注解指定注入代码在目标方法的哪个位置生效。

| `value` 值 | 说明 | 常用场景 |
|-----------|------|---------|
| `"HEAD"` | 方法最开始（第一条指令前） | 前置拦截、参数检查 |
| `"RETURN"` | 每个 `return` 语句处 | 修改返回值、后置处理 |
| `"TAIL"` | 方法最后一个 `return` 前（等价于 `RETURN` 的最后一次） | 方法末尾后置处理 |
| `"INVOKE"` | 指定方法被调用处 | 拦截特定调用 |
| `"FIELD"` | 字段访问处（配合 `opcode`） | 拦截字段读/写 |
| `"NEW"` | `new` 实例化处 | 拦截对象创建 |

**`target` 描述符格式（用于 `INVOKE` / `FIELD`）**:
```
方法: L<类名(斜杠分隔)>;<方法名>(<参数描述符>)<返回描述符>
字段: L<类名>;<字段名>:<类型描述符>

示例:
  "Lnet/minecraft/client/audio/SoundPoolEntry;getSoundPoolEntryLocation()Lnet/minecraft/util/ResourceLocation;"
  "Lnet/minecraft/tileentity/TileEntityFurnace.furnaceBurnTime:I"
```

**`shift` 参数**: 调整注入位置相对于目标的偏移
```java
At.Shift.BEFORE  // 在目标点之前注入
At.Shift.AFTER   // 在目标点之后注入
At.Shift.BY      // 偏移指定条指令数
```

**`ordinal` 参数**: 当同一方法中有多次匹配时，指定第几次（从 0 开始）
```java
// 第 3 次（ordinal=2）读取 furnaceBurnTime 字段时注入
at = @At(value = "FIELD",
         target = "net/minecraft/tileentity/TileEntityFurnace.furnaceBurnTime:I",
         opcode = Opcodes.GETFIELD,
         ordinal = 2)
```

**FIELD 的 `opcode` 值**:
- `Opcodes.GETFIELD` — 读取实例字段
- `Opcodes.PUTFIELD` — 写入实例字段
- `Opcodes.GETSTATIC` — 读取静态字段
- `Opcodes.PUTSTATIC` — 写入静态字段

---

## 十一、Accessor 接口模式

Accessor 模式用于安全地暴露目标类的私有字段或方法，供 Mixin 之外的代码调用。

**三步结构**:

**第 1 步**: 定义 Accessor 接口（放在 `src/main/java/gregtech/mixin/interfaces/accessors/`）

```java
// src/main/java/gregtech/mixin/interfaces/accessors/IRecipeMutableAccess.java
package gregtech.mixin.interfaces.accessors;

import net.minecraft.item.ItemStack;

/**
 * Mixed-in interface for recipe classes in Forge and Vanilla that allows mutating the input and output items.
 */
public interface IRecipeMutableAccess {

    /** @return Gets the current output item of the recipe */
    ItemStack gt5u$getRecipeOutputItem();

    /** Sets a new output item on the recipe */
    void gt5u$setRecipeOutputItem(ItemStack newItem);

    /** @return The raw list or array of recipe inputs */
    Object gt5u$getRecipeInputs();
}
```

**第 2 步**: 实现 Accessor Mixin（放在 `src/mixin/java/.../accessors/`，并在 `Mixin.java` 中注册）

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/accessors/VanillaShapedRecipeMixin.java
@Mixin(ShapedRecipes.class)
public class VanillaShapedRecipeMixin implements IRecipeMutableAccess {

    @Shadow
    private ItemStack recipeOutput;

    @Shadow
    @Final
    public ItemStack[] recipeItems;

    @Override
    public ItemStack gt5u$getRecipeOutputItem() {
        return this.recipeOutput;
    }

    @Override
    public void gt5u$setRecipeOutputItem(ItemStack newItem) {
        this.recipeOutput = newItem;  // @Shadow 字段允许写入（除非加了 @Final）
    }

    @Override
    public Object gt5u$getRecipeInputs() {
        return this.recipeItems;
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/accessors/ChunkCacheMixin.java
@Mixin(ChunkCache.class)
public class ChunkCacheMixin implements ChunkCacheAccessor {

    @Shadow
    private World worldObj;

    @Override
    public World getWorld() {
        return worldObj;
    }
}
```

**第 3 步**: 在业务代码中使用

```java
// 通过强制类型转换到 Accessor 接口即可访问私有字段
IRecipeMutableAccess recipe = (IRecipeMutableAccess) someShapedRecipes;
ItemStack output = recipe.gt5u$getRecipeOutputItem();
recipe.gt5u$setRecipeOutputItem(newStack);
```

### 接口实现 Mixin（Implement Interface via Mixin）

通过 Mixin 为目标类添加接口实现，使目标类满足某个 GT 自定义接口：

```java
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinIc2Nano.java
@Mixin(value = ItemArmorNanoSuit.class, remap = false)
public class MixinIc2Nano implements IHazardProtector {  // 让 IC2 纳米盔甲实现 GT 的防护接口

    @Override
    public boolean protectsAgainst(ItemStack itemStack, Hazard hazard) {
        return true;
    }
}
```

```java
// src/mixin/java/gregtech/mixin/mixins/late/advanced_solar_panels/MixinAdvancedSolarHelmet.java
@Mixin(ItemAdvancedSolarHelmet.class)
public class MixinAdvancedSolarHelmet implements IHazardProtector {

    @Override
    public boolean protectsAgainst(ItemStack itemStack, Hazard hazard) {
        return true;  // 高级太阳能头盔也提供辐射防护
    }
}
```

---

## 十二、共享状态 Helper 模式

当多个 Mixin 需要共享状态（例如当前正在处理的 Mod 名），使用 `hooks/` 下的静态 Helper 类传递数据。

```java
// src/main/java/gregtech/mixin/hooks/MixinsVariablesHelper.java
package gregtech.mixin.hooks;

public class MixinsVariablesHelper {

    public static String currentlyTranslating = null;  // 当前正在翻译的 modId
}
```

**使用方式**: 在 `LanguageRegistryMixin` 中写入，在 `StringTranslateMixin` / `LocaleMixin` 中读取：

```java
// LanguageRegistryMixin 写入
@Inject(method = "loadLanguagesFor", at = @At(value = "HEAD"), remap = false, require = 1)
private void gt5u$loadLanguagesForHEAD(ModContainer container, Side side, CallbackInfo ci) {
    MixinsVariablesHelper.currentlyTranslating = container.getModId();
}

// StringTranslateMixin 读取
@Redirect(method = "parseLangFile", at = @At(value = "INVOKE",
    target = "Ljava/util/regex/Matcher;replaceAll(Ljava/lang/String;)Ljava/lang/String;",
    remap = false), remap = false, require = 1)
private static String gt5u$replaceAll(Matcher matcher, String replace) {
    if (MixinsVariablesHelper.currentlyTranslating != null
        && MixinsVariablesHelper.currentlyTranslating.equals(Tags.MODID)
        && matcher.find()) {
        return matcher.replaceFirst(matcher.group());  // kubatech 翻译只做 replaceFirst
    }
    return matcher.replaceAll(replace);
}
```

---

## 十三、污染系统完整示例

GT5U 的 Pollution（污染）系统是同时使用 Early 和 Late Mixin 的典型案例，用于让各种炉子和设备在运行时产生污染值。

### Early Mixin: 原版熔炉污染

```java
// src/mixin/java/gregtech/mixin/mixins/early/minecraft/pollution/MixinTileEntityFurnacePollution.java
// 注册: Mixin.java 中 POLLUTION_MINECRAFT_FURNACE 条目，Phase.EARLY
// 条件: PollutionConfig.pollution && PollutionConfig.furnacesPollute
@Mixin(TileEntityFurnace.class)
public abstract class MixinTileEntityFurnacePollution extends TileEntity {

    @Inject(
        method = "updateEntity",
        at = @At(
            value = "FIELD",
            target = "net/minecraft/tileentity/TileEntityFurnace.furnaceBurnTime:I",
            opcode = Opcodes.GETFIELD,
            ordinal = 2))
    private void gt5u$addPollution(CallbackInfo ci) {
        furnaceAddPollutionOnUpdate(this.worldObj, this.xCoord, this.zCoord,
                                   FurnacePollution.FURNACE.getPollution());
    }
}
```

### Late Mixin: IC2 铁炉污染

```java
// src/mixin/java/gregtech/mixin/mixins/late/ic2/MixinIC2IronFurnacePollution.java
// 注册: Mixin.java 中 POLLUTION_IC2_IRON_FURNACE 条目，Phase.LATE，需要 IC2
@Mixin(value = TileEntityIronFurnace.class, remap = false)
public abstract class MixinIC2IronFurnacePollution extends TileEntity {

    @Shadow
    public abstract boolean isBurning();

    @Inject(method = "updateEntityServer", at = @At("RETURN"))
    private void gt5u$updateEntityServer(CallbackInfo ci) {
        if (isBurning()) {
            furnaceAddPollutionOnUpdate(this.worldObj, this.xCoord, this.zCoord,
                                       FurnacePollution.IRON_FURNACE.getPollution());
        }
    }
}
```

### Late Mixin: Railcraft 锅炉污染

```java
// src/mixin/java/gregtech/mixin/mixins/late/railcraft/MixinRailcraftBoilerPollution.java
// 注册: Mixin.java 中 POLLUTION_RAILCRAFT 条目，Phase.LATE，需要 RAILCRAFT
@Mixin(value = SteamBoiler.class, remap = false)
public class MixinRailcraftBoilerPollution {

    @Shadow private RailcraftTileEntity tile;
    @Shadow protected boolean isBurning;

    @Inject(method = "tick", at = @At(value = "HEAD"))
    private void gt5u$tick(int x, CallbackInfo ci) {
        if (!this.isBurning || this.tile == null || this.tile.getWorld() == null) return;
        final World world = this.tile.getWorldObj();
        if ((world.getTotalWorldTime() % 20) == 0) {
            int pollutionAmount;
            if (this.tile instanceof TileMultiBlock) {
                pollutionAmount = (((TileMultiBlock) this.tile).getComponents().size() - x)
                                  * PollutionConfig.fireboxPollutionAmount;
            } else if (this.tile instanceof TileEngineSteamHobby) {
                pollutionAmount = PollutionConfig.hobbyistEnginePollutionAmount;
            } else {
                pollutionAmount = 40;
            }
            Pollution.addPollution(
                world.getChunkFromBlockCoords(this.tile.getX(), this.tile.getZ()),
                pollutionAmount);
        }
    }
}
```

### 在 Mixin.java 中注册污染 Mixin

```java
// Mixin.java 中对应的注册条目
POLLUTION_MINECRAFT_FURNACE(new MixinBuilder()
    .setPhase(Phase.EARLY)
    .addCommonMixins("minecraft.pollution.MixinTileEntityFurnacePollution")
    .setApplyIf(() -> PollutionConfig.pollution && PollutionConfig.furnacesPollute)),

POLLUTION_IC2_IRON_FURNACE(new MixinBuilder()
    .addCommonMixins("ic2.MixinIC2IronFurnacePollution")
    .setPhase(Phase.LATE)
    .setApplyIf(() -> PollutionConfig.pollution && PollutionConfig.furnacesPollute)
    .addRequiredMod(TargetedMod.IC2)),

POLLUTION_RAILCRAFT(new MixinBuilder("Make Railcraft Pollute")
    .addCommonMixins(
        "railcraft.MixinRailcraftBoilerPollution",
        "railcraft.MixinRailcraftCokeOvenPollution",
        "railcraft.MixinRailcraftTunnelBorePollution")
    .setPhase(Phase.LATE)
    .setApplyIf(() -> PollutionConfig.pollution && PollutionConfig.railcraftPollutes)
    .addRequiredMod(TargetedMod.RAILCRAFT)),
```

---

## 十四、数量统计总览

| 类别 | 数量 |
|------|------|
| Early Mixin 实现类 | 33 个 |
| Late Mixin 实现类 | 22 个 |
| Mixin 实现类总计 | 55 个 |
| Mixin 枚举条目 | 31 个（一条可包含多个类） |
| Accessor 接口 | 14 个 |
| 目标 Mod (TargetedMod) | 13 个 |

### 各注入注解使用频次（基于本地克隆统计）

| 注解 | 使用次数 | 来源 |
|------|---------|------|
| `@Inject` | 最多 | SpongePowered Mixin |
| `@ModifyReturnValue` | 较多 | MixinExtras |
| `@WrapOperation` | 中等 | MixinExtras |
| `@Shadow` | 中等 | SpongePowered Mixin |
| `@Redirect` | 少量 | SpongePowered Mixin |
| `@ModifyArg` | 少量 | SpongePowered Mixin |
| `@WrapWithCondition` | 少量 | MixinExtras |
| `@Overwrite` | 1 处 | SpongePowered Mixin |
| `@Unique` | 少量 | SpongePowered Mixin |
| `@Final` | 少量 | SpongePowered Mixin |

---

## 快速参考

### 新增 Mixin 的完整步骤

1. **创建 Mixin 实现类**（根据阶段放入对应目录）:
   - Early: `src/mixin/java/gregtech/mixin/mixins/early/<子包>/<类名>.java`
   - Late: `src/mixin/java/gregtech/mixin/mixins/late/<mod名>/<类名>.java`

2. **在 `Mixin.java` 中注册**:
   ```java
   MY_NEW_MIXIN(new MixinBuilder("描述（可选）")
       .addCommonMixins("minecraft.MyNewMixin")   // 类名相对于包前缀
       .setPhase(Phase.EARLY)),
   ```

3. **若需要 Accessor，定义接口**:
   - 接口放入 `src/main/java/gregtech/mixin/interfaces/accessors/`
   - 在 Mixin 类中 `implements` 该接口，用 `@Shadow` 引用私有字段

4. **若需要开放私有字段，添加 AT 条目**:
   - 在 `src/main/resources/META-INF/gregtech_at.cfg` 中添加 `public <类名> <SRG字段名>`

5. **JSON 文件无需修改**（类名由 `IMixins.getEarlyMixins/getLateMixins` 动态注入）

---

**文档版本**: 2026-02-21  
**数据来源**: GT5-Unofficial 本地克隆，commit `96f51372`
