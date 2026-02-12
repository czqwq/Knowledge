# GTNH ExampleMod 与 Gradle 构建系统文档

**仓库地址**: https://github.com/GTNewHorizons/ExampleMod1.7.10  
**目的**: GTNH模组开发的标准模板和构建系统参考

---

## 目录

1. [项目概览](#项目概览)
2. [Gradle构建系统](#gradle构建系统)
3. [GTNH特定配置](#gtnh特定配置)
4. [项目结构](#项目结构)
5. [依赖管理](#依赖管理)
6. [Mixins支持](#mixins支持)
7. [发布流程](#发布流程)
8. [最佳实践](#最佳实践)

---

## 项目概览

### 基本信息

| 项目 | 信息 |
|------|------|
| **模板名称** | GTNH ExampleMod |
| **目标MC版本** | 1.7.10 |
| **Forge版本** | 10.13.4.1614+ |
| **Gradle版本** | 9.2.1 (Wrapper) |
| **Java目标** | JVM 8 (支持Java 17语法) |
| **构建系统** | RetroFuturaGradle (RFG) |

### 核心特性

- ✅ **最小化build.gradle.kts**: 仅3行，所有配置由插件提供
- ✅ **Kotlin DSL**: 类型安全的Gradle配置
- ✅ **现代Java语法**: Jabel支持Java 17编译到JVM 8
- ✅ **自动泛型注入**: 反编译代码自动添加泛型
- ✅ **Spotless格式化**: 统一代码风格
- ✅ **自动版本管理**: Tags类自动生成
- ✅ **Mixins可选支持**: 开箱即用的Mixin配置
- ✅ **多平台发布**: Maven、Modrinth、CurseForge

---

## Gradle构建系统

### A. 核心文件

#### 1. build.gradle.kts

**完整内容**:
```kotlin
plugins {
    id("com.gtnewhorizons.gtnhconvention")
}
```

**设计理念**:
- **最小化**: 仅引入一个约定插件
- **可更新**: 所有复杂配置由插件提供，便于后续升级
- **不要修改**: 保持原样以获得最佳兼容性

#### 2. settings.gradle.kts

```kotlin
pluginManagement {
    repositories {
        maven {
            name = "GTNH Maven"
            url = uri("https://nexus.gtnewhorizons.com/repository/public/")
            mavenContent {
                includeGroup("com.gtnewhorizons")
                includeGroupByRegex("com\\.gtnewhorizons\\..+")
            }
        }
        gradlePluginPortal()
        mavenCentral()
        mavenLocal()
    }
}

plugins {
    id("com.gtnewhorizons.gtnhsettingsconvention") version "2.0.7"
}
```

**功能**:
- 配置插件仓库（GTNH Maven优先）
- 引入设置约定插件
- 固定版本号（2.0.7）

#### 3. gradle.properties

**核心配置项**:

##### 基本信息
```properties
# 模组信息
modName = MyMod
modId = mymodid
modGroup = com.myname.mymodid

# 版本信息
minecraftVersion = 1.7.10
forgeVersion = 10.13.4.1614
channel = stable
mappingsVersion = 12
```

##### 构建特性
```properties
# 现代Java语法支持
enableModernJavaSyntax = true
jabelJavaVersion = 17

# 泛型注入
enableGenericInjection = true

# 自动版本类生成
generateGradleTokenClass = com.myname.mymodid.Tags
gradleTokenModId = MODID
gradleTokenModName = MODNAME
gradleTokenVersion = VERSION
gradleTokenGroupId = GROUPID
gradleTokenGroupName = GROUPNAME
```

##### 发布配置
```properties
# Maven发布
usesMavenPublishing = true
useModGroupForPublishing = true

# Modrinth/CurseForge
modrinthProjectId = 
curseForgeProjectId = 
```

##### Mixins配置
```properties
# Mixins支持（默认关闭）
usesMixins = false
separateMixinSourceSet = 
mixinPlugin = 
mixinsPackage = 
```

### B. Gradle Wrapper

**gradle-wrapper.properties**:
```properties
distributionUrl=https://services.gradle.org/distributions/gradle-9.2.1-bin.zip
```

**自动JVM管理** (`gradle/gradle-daemon-jvm.properties`):
```properties
# Gradle将自动安装JDK 25
daemon-jvm-version=25
```

---

## GTNH特定配置

### A. gtnhconvention 插件

**提供的功能**:

| 功能 | 说明 |
|------|------|
| **RetroFuturaGradle** | MC 1.7.10反编译和Forge集成 |
| **Jabel支持** | Java 17语法 → JVM 8字节码 |
| **泛型注入** | 自动添加泛型参数 |
| **Spotless** | 代码格式化 |
| **Maven发布** | 自动化发布流程 |
| **TOKEN生成** | 自动生成Tags.java |
| **依赖管理** | 知名仓库自动包含 |

### B. Spotless代码格式化

**配置文件**: `gtnhShared/spotless.gradle`

**支持的语言**:

#### Java
```gradle
java {
    importOrderFile(Blowdryer.file('spotless.importorder'))
    eclipse('4.19').configFile(Blowdryer.file('spotless.eclipseformat.xml'))
    toggleOffOn()  // 支持 spotless:off/on 注释
}
```

#### Kotlin
```gradle
kotlin {
    ktlint('1.7.1').editorConfigOverride([
        'ktlint_code_style': 'intellij_idea'
    ])
}
```

#### Scala
```gradle
scala {
    scalafmt('3.7.15')
}
```

#### JSON
```gradle
json {
    ratchetFrom 'origin/master'  // 增量格式化
    prettier().config([
        printWidth: 100,
        tabWidth: 2
    ])
}
```

**Gradle任务**:
```bash
./gradlew spotlessCheck   # 检查格式
./gradlew spotlessApply   # 应用格式化
```

---

## 项目结构

### 完整目录树

```
ExampleMod/
├── build.gradle.kts              # 构建脚本（3行）
├── settings.gradle.kts           # 项目设置
├── gradle.properties             # 核心配置（210行）
├── dependencies.gradle           # 依赖声明
├── repositories.gradle           # 仓库配置
│
├── gradle/                       # Gradle配置
│   ├── wrapper/
│   │   ├── gradle-wrapper.properties
│   │   └── gradle-wrapper.jar
│   └── gradle-daemon-jvm.properties
│
├── gtnhShared/                   # GTNH共享配置
│   ├── spotless.gradle
│   ├── spotless.eclipseformat.xml
│   └── spotless.importorder
│
├── src/                          # 源代码
│   └── main/
│       ├── java/
│       │   └── com/myname/mymodid/
│       │       ├── MyMod.java
│       │       ├── CommonProxy.java
│       │       ├── ClientProxy.java
│       │       └── Config.java
│       └── resources/
│           ├── mcmod.info
│           └── LICENSE
│
├── docs/                         # 文档
│   ├── FAQ.md
│   ├── migration.md
│   └── porting.md
│
├── .github/                      # GitHub配置
│   └── workflows/
│
├── .editorconfig                 # 编辑器配置
├── .gitignore
├── .gitattributes
├── CODEOWNERS
├── LICENSE
├── LICENSE-template
├── jitpack.yml                   # JitPack配置
└── README.md
```

### 源代码结构

#### MyMod.java - 模组主类

```java
package com.myname.mymodid;

import cpw.mods.fml.common.Mod;
import cpw.mods.fml.common.SidedProxy;
import cpw.mods.fml.common.event.*;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

@Mod(
    modid = MyMod.MODID,
    version = Tags.VERSION,  // ← 自动生成
    name = MyMod.NAME,
    acceptedMinecraftVersions = "[1.7.10]"
)
public class MyMod {
    public static final String MODID = "mymodid";
    public static final String NAME = "My Mod";
    public static final Logger LOG = LogManager.getLogger(MODID);

    @SidedProxy(
        clientSide = "com.myname.mymodid.ClientProxy",
        serverSide = "com.myname.mymodid.CommonProxy"
    )
    public static CommonProxy proxy;

    @Mod.EventHandler
    public void preInit(FMLPreInitializationEvent event) {
        proxy.preInit(event);
        LOG.info("I am " + MODID + " at version " + Tags.VERSION);
    }

    @Mod.EventHandler
    public void init(FMLInitializationEvent event) {
        proxy.init(event);
    }

    @Mod.EventHandler
    public void postInit(FMLPostInitializationEvent event) {
        proxy.postInit(event);
    }

    @Mod.EventHandler
    public void serverStarting(FMLServerStartingEvent event) {
        proxy.serverStarting(event);
    }
}
```

#### Tags.java - 自动生成的版本类

**由Gradle自动生成**:
```java
package com.myname.mymodid;

public class Tags {
    public static final String MODID = "mymodid";
    public static final String MODNAME = "MyMod";
    public static final String VERSION = "0.1.0";
    public static final String GROUPID = "com.myname.mymodid";
    public static final String GROUPNAME = "mymodid";
}
```

**生成位置**: `build/generated/sources/`  
**配置**: `gradle.properties` 中的 `generateGradleTokenClass`

#### mcmod.info - 模组元数据

```json
{
  "modListVersion": 2,
  "modList": [{
    "modid": "${modId}",
    "name": "${modName}",
    "description": "Example mod",
    "version": "${modVersion}",
    "mcversion": "${minecraftVersion}",
    "url": "https://github.com/GTNewHorizons/ExampleMod1.7.10",
    "updateUrl": "",
    "authorList": ["Author Name"],
    "credits": "",
    "logoFile": "",
    "screenshots": [],
    "parent": "",
    "requiredMods": [],
    "dependencies": [],
    "dependants": [],
    "useDependencyInformation": false
  }]
}
```

**变量替换**:
- `${modId}` → `gradle.properties` 中的 `modId`
- `${modName}` → `gradle.properties` 中的 `modName`
- `${modVersion}` → Git标签版本
- `${minecraftVersion}` → `gradle.properties` 中的值

---

## 依赖管理

### A. dependencies.gradle

```gradle
dependencies {
    // 示例：NEI依赖
    // runtimeOnlyNonPublishable("com.github.GTNewHorizons:NotEnoughItems:2.7.69-GTNH:dev")
    
    // API依赖（编译+运行，暴露给依赖方）
    // api("com.github.GTNewHorizons:YourAPI:1.0.0:dev")
    
    // 实现依赖（仅运行时，不暴露）
    // implementation("com.github.GTNewHorizons:SomeLib:1.0.0:dev")
    
    // 编译依赖（仅编译时）
    // compileOnly("com.github.GTNewHorizons:CompileOnly:1.0.0:dev")
    
    // 开发依赖（开发时可用，不发布）
    // devOnlyNonPublishable("com.github.GTNewHorizons:DevTool:1.0.0:dev")
}
```

### B. 依赖配置类型

| 配置 | 编译时 | 运行时 | 发布 | 用途 |
|------|--------|--------|------|------|
| **api** | ✅ | ✅ | ✅ | 公开API |
| **implementation** | ✅ | ✅ | ✅ | 内部实现 |
| **compileOnly** | ✅ | ❌ | ❌ | 编译依赖 |
| **compileOnlyApi** | ✅ | ❌ | ✅ | 暴露编译依赖 |
| **runtimeOnly** | ❌ | ✅ | ✅ | 运行时依赖 |
| **runtimeOnlyNonPublishable** | ❌ | ✅ | ❌ | 运行时不发布 |
| **devOnlyNonPublishable** | ✅ | ✅ | ❌ | 开发专用 |

### C. repositories.gradle

```gradle
repositories {
    // 自定义仓库在此添加
    // maven {
    //     name = "Custom Maven"
    //     url = "https://maven.example.com/releases"
    // }
}
```

**默认已包含的仓库** (通过 `includeWellKnownRepositories = true`):
- GTNH Maven
- CurseForge Maven
- Modrinth Maven
- 1.7.10特定仓库
- Maven Central
- Gradle Plugin Portal

---

## Mixins支持

### A. 启用Mixins

**步骤1**: 修改 `gradle.properties`
```properties
usesMixins = true
mixinPlugin = com.myname.mymodid.mixins.MixinPlugin
mixinsPackage = com.myname.mymodid.mixins
```

**步骤2**: 创建Mixin配置文件

**src/main/resources/mixins.mymodid.json**:
```json
{
  "required": true,
  "minVersion": "0.8",
  "package": "com.myname.mymodid.mixins",
  "refmap": "mixins.mymodid.refmap.json",
  "plugin": "com.myname.mymodid.mixins.MixinPlugin",
  "mixins": [
    "MixinEntityPlayer"
  ],
  "client": [
    "MixinGuiMainMenu"
  ],
  "server": []
}
```

**步骤3**: 实现IMixinConfigPlugin（可选）

```java
package com.myname.mymodid.mixins;

import org.spongepowered.asm.mixin.extensibility.IMixinConfigPlugin;
import org.spongepowered.asm.mixin.extensibility.IMixinInfo;

import java.util.List;
import java.util.Set;

public class MixinPlugin implements IMixinConfigPlugin {
    @Override
    public void onLoad(String mixinPackage) { }

    @Override
    public String getRefMapperConfig() {
        return null;
    }

    @Override
    public boolean shouldApplyMixin(String targetClassName, String mixinClassName) {
        return true;  // 条件加载
    }

    @Override
    public void acceptTargets(Set<String> myTargets, Set<String> otherTargets) { }

    @Override
    public List<String> getMixins() {
        return null;
    }

    @Override
    public void preApply(String targetClassName, ClassNode targetClass, 
                        String mixinClassName, IMixinInfo mixinInfo) { }

    @Override
    public void postApply(String targetClassName, ClassNode targetClass, 
                         String mixinClassName, IMixinInfo mixinInfo) { }
}
```

### B. 单独Mixin源集（可选）

**提升编译速度**:
```properties
separateMixinSourceSet = java  # 或 kotlin/scala
```

**目录结构**:
```
src/
├── main/
│   └── java/...
└── mixin/
    └── java/
        └── com/myname/mymodid/mixins/
            └── MixinEntityPlayer.java
```

---

## 发布流程

### A. Maven发布

**配置**:
```properties
usesMavenPublishing = true
useModGroupForPublishing = true
mavenPublishUrl = https://nexus.gtnewhorizons.com/repository/releases/
```

**环境变量**:
```bash
export MAVEN_USER=your_username
export MAVEN_PASSWORD=your_password
```

**发布命令**:
```bash
./gradlew publish
```

**发布到的坐标**:
```
groupId: com.myname.mymodid
artifactId: MyMod
version: 0.1.0
```

### B. Modrinth发布

**配置**:
```properties
modrinthProjectId = abc123def
modrinthRelations = required-project:fplib;optional-project:gasstation
```

**环境变量**:
```bash
export MODRINTH_TOKEN=your_modrinth_token
```

**发布命令**:
```bash
./gradlew modrinth
```

### C. CurseForge发布

**配置**:
```properties
curseForgeProjectId = 123456
curseForgeRelations = requiredDependency:railcraft;optionalDependency:forestry
```

**环境变量**:
```bash
export CURSEFORGE_API_KEY=your_api_key
```

**发布命令**:
```bash
./gradlew curseforge
```

### D. 版本管理

**Git标签**:
```bash
git tag v0.1.0
git push --tags
```

**自动化发布** (GitHub Actions):
```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build
        run: ./gradlew build
      - name: Publish
        env:
          MAVEN_USER: ${{ secrets.MAVEN_USER }}
          MAVEN_PASSWORD: ${{ secrets.MAVEN_PASSWORD }}
        run: ./gradlew publish
```

---

## 最佳实践

### 1. 项目设置

#### ✅ DO
- 保持 `build.gradle.kts` 最小化
- 在 `dependencies.gradle` 管理依赖
- 在 `repositories.gradle` 添加仓库
- 使用 `gradle.properties` 集中配置
- 遵循Spotless格式规范

#### ❌ DON'T
- 不要修改 `build.gradle.kts`
- 不要在 `build.gradle.kts` 中声明依赖
- 不要硬编码版本号（使用 `gradle.properties`）
- 不要提交生成的代码（`build/`、`.gradle/`）

### 2. 依赖管理

#### API vs Implementation

```gradle
// ✅ 正确：对外暴露的接口
api("com.github.GTNewHorizons:YourAPI:1.0.0:dev")

// ✅ 正确：内部实现细节
implementation("com.github.GTNewHorizons:InternalLib:1.0.0:dev")

// ❌ 错误：所有依赖都用api
api("com.github.GTNewHorizons:Everything:1.0.0:dev")
```

### 3. Mixin最佳实践

```java
// ✅ 正确：使用@Inject
@Mixin(EntityPlayer.class)
public class MixinEntityPlayer {
    @Inject(method = "onUpdate", at = @At("HEAD"))
    private void onUpdateHead(CallbackInfo ci) {
        // 逻辑
    }
}

// ❌ 避免：过度使用@Overwrite
@Mixin(EntityPlayer.class)
public class BadMixin {
    @Overwrite  // 可能与其他模组冲突
    public void onUpdate() {
        // ...
    }
}
```

### 4. 版本控制

```properties
# ✅ 正确：使用Git标签
# Git: git tag v0.1.0

# ✅ 正确：自动版本号
generateGradleTokenClass = com.myname.mymodid.Tags

# ❌ 错误：硬编码版本
@Mod(version = "0.1.0")  // 使用 Tags.VERSION
```

### 5. 构建优化

```properties
# ✅ 启用并行构建
org.gradle.parallel=true

# ✅ 增加内存
org.gradle.jvmargs=-Xmx3G

# ✅ 使用缓存
org.gradle.caching=true

# ✅ 分离Mixin源集（大项目）
separateMixinSourceSet = java
```

---

## Gradle任务参考

### 常用任务

| 任务 | 描述 |
|------|------|
| `./gradlew build` | 完整构建 |
| `./gradlew runClient` | 运行客户端 |
| `./gradlew runServer` | 运行服务器 |
| `./gradlew jar` | 仅打包JAR |
| `./gradlew clean` | 清理构建 |

### 开发任务

| 任务 | 描述 |
|------|------|
| `./gradlew setupDecompWorkspace` | 反编译工作区 |
| `./gradlew genSrgs` | 生成SRG映射 |
| `./gradlew decompile` | 反编译Minecraft |

### 代码质量

| 任务 | 描述 |
|------|------|
| `./gradlew spotlessCheck` | 检查格式 |
| `./gradlew spotlessApply` | 应用格式化 |
| `./gradlew check` | 运行所有检查 |

### 发布任务

| 任务 | 描述 |
|------|------|
| `./gradlew publish` | Maven发布 |
| `./gradlew modrinth` | Modrinth发布 |
| `./gradlew curseforge` | CurseForge发布 |

---

## 相关文档

- [Core_Infrastructure_README.md](./Core_Infrastructure_README.md) - 核心基础设施
- [ModularUI_README.md](./ModularUI_README.md) - GUI框架
- [Modpack_README.md](./Modpack_README.md) - 整合包配置
- [GTNH_Repos_Index.md](./GTNH_Repos_Index.md) - 仓库总索引

---

## 外部资源

- **RetroFuturaGradle**: https://github.com/GTNewHorizons/RetroFuturaGradle
- **gtnhconvention**: https://github.com/GTNewHorizons/gradle-buildconfig
- **Spotless**: https://github.com/diffplug/spotless
- **Gradle文档**: https://docs.gradle.org/

---

**最后更新**: 2026-02-12  
**Gradle版本**: 9.2.1  
**RFG版本**: Latest  
**维护者**: AI Knowledge Base Team  
**版本**: 1.0
