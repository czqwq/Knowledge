# GTNH核心基础设施仓库分析

**分析仓库**: Angelica、UniMixins、StructureLib、Hodgepodge  
**目的**: 为AI提供GTNH核心基础设施的完整知识库

---

## 📚 目录

1. [仓库概览](#仓库概览)
2. [Angelica - 渲染引擎](#angelica---渲染引擎)
3. [UniMixins - Mixin加载器](#unimixins---mixin加载器)
4. [StructureLib - 结构验证库](#structurelib---结构验证库)
5. [Hodgepodge - 修复集合](#hodgepodge---修复集合)
6. [跨仓库集成](#跨仓库集成)
7. [接口统计](#接口统计)

---

## 仓库概览

| 仓库 | 定位 | Java文件 | 接口数 | Mixin数 | Stars |
|------|------|---------|--------|---------|-------|
| **Angelica** | OptiFine替代/渲染引擎 | 1,158 | 143 | 260 | ⭐⭐⭐⭐ |
| **UniMixins** | Mixin加载器框架 | 87 | 9 | 41 | ⭐⭐⭐ |
| **StructureLib** | 多方块结构验证 | 91 | 26 | 2 | ⭐⭐⭐⭐ |
| **Hodgepodge** | Bug修复/性能优化 | 506 | 20 | 393 | ⭐⭐⭐⭐⭐ |

**总计**: 1,842个Java文件，198个接口，696个Mixin

---

## Angelica - 渲染引擎

**GitHub**: https://github.com/GTNewHorizons/Angelica  
**定位**: OptiFine的开源替代品，专注渲染优化和着色器支持

### 核心特性

#### 1. Celeritas地形渲染系统
```
多线程区块构建 → Iris着色器集成 → 多绘制模式
```

**关键类**:
- `CeleritasWorldRenderer` - 世界渲染管道
- `AngelicaRenderSectionManager` - 区段管理
- `AngelicaChunkRenderer` - 区块渲染器
- `AngelicaChunkBuilderMeshingTask` - 多线程网格构建

**绘制模式**:
- DIRECT - 直接绘制
- INDIRECT - 间接绘制 (GL 4.3+)
- INDIVIDUAL - 独立绘制

#### 2. VBO显示列表仿真系统

**架构流程**:
```
GL命令录制 → 顶点格式分组 → VBO存储 → 变换折叠 → 执行
```

**核心类**:
- `DisplayListManager` - 显示列表管理器
- `CommandRecorder` - GL命令录制器
- `DisplayListVBO` - VBO显示列表对象
- `CompiledDisplayList` - 编译后的显示列表

**优化特性**:
- 变换折叠（Transform Collapsing）
- 格式基础批处理
- 显示列表复用

#### 3. 核心接口（143个）

##### A. 渲染系统接口

| 接口 | 路径 | 功能 |
|------|------|------|
| **IRenderGlobalExt** | `mixins.interfaces` | RenderGlobal扩展 |
| **ISpriteExt** | `mixins.interfaces` | 纹理精灵扩展 |
| **IPatchedTextureAtlasSprite** | `mixins.interfaces` | 纹理图集补丁 |
| **ITexturesCache** | `mixins.interfaces` | 纹理缓存 |
| **IrisShaderProvider** | `rendering.celeritas.api` | Iris着色器提供者 |

##### B. 动态光源接口

| 接口 | 路径 | 功能 |
|------|------|------|
| **IDynamicLightProducer** | `dynamiclights` | 动态光源生产者 |
| **IDynamicLightWorldRenderer** | `dynamiclights` | 动态光源渲染器 |

##### C. Accessor接口（60+）

访问Minecraft私有成员的Mixin接口：
- `EntityRendererAccessor` - 相机/视图参数
- `FontRendererAccessor` - 字体渲染器
- `ChunkTrackerAccessor` - 区块追踪
- `RenderSectionManagerAccessor` - 区段管理器
- ...等60+个访问器

#### 4. Mixin分类（260个）

##### A. 渲染优化 (100+)

**地形渲染** (`mixins.early.celeritas.terrain/`):
- `MixinRenderGlobal` (priority=900) - 地形渲染主类
- `MixinRenderSectionManager` - 区段管理
- `MixinWorldClient` - 世界客户端

**VBO系统** (`mixins.early.angelica.vbo/`):
- `MixinRenderGlobal` - VBO云渲染
- `DisplayListManager` - VBO显示列表仿真

**瓦片实体** (`mixins.early.angelica.optimizations/`):
- `MixinTileEntityRendererDispatcher` - TE渲染调度
- `MixinEffectRenderer` - 粒子效果渲染

##### B. 着色器系统 (40+)

**路径**: `mixins.early.shaders/`

- `startup/MixinInitRenderer` - 渲染器初始化
- `startup/MixinTextureMap` - 纹理映射
- `MixinRendererLivingEntity` - 实体着色器
- `MixinItemRenderer` - 物品着色器
- `MixinRenderDragon` - 龙部分着色器
- `MixinRenderEndPortal` - 末地传送门着色器
- `MixinFramebuffer` - FBO支持

##### C. 性能优化 (30+)

**路径**: `mixins.early.angelica.optimizations/`

- `MixinGLAllocation` - 用fastutil替代HashMap
- `MixinRenderGlobal_ItemRenderDist` - 动态物品渲染距离
- `MixinRendererLivingEntity` - 实体渲染优化
- `MixinItemRenderer` - 物品渲染优化

##### D. HUD缓存 (10+)

**路径**: `mixins.early.angelica.hudcaching/`

- `MixinGuiIngame_HUDCaching` - HUD界面缓存
- `MixinFramebuffer_HUDCaching` - 帧缓冲缓存
- `MixinRenderItem` - 物品渲染缓存

**功能**: 20帧刷新一次HUD，复用像素数据

##### E. MCPatcherForge兼容 (40+)

**路径**: `mixins.early.mcpatcherforge/`

- **CIT** (自定义物品纹理): `cit/client/renderer/MixinRenderGlobal`
- **CTM** (连接纹理): `ctm/MixinRenderBlocks`
- **CC** (彩色方块): `cc/client/renderer/MixinRenderBlocks`
- **天空替换**: `sky/MixinRenderGlobal`

##### F. NotFine功能 (15+)

**路径**: `mixins.early.notfine/`

- `renderer/MixinRenderGlobal` - 云渲染替换
- `clouds/MixinRenderGlobal` - 云效果优化
- `toggle/` - 功能开关
- `fix/` - 渲染修复

##### G. 动态光源 (10+)

**路径**: `mixins.early.angelica.dynamiclights/`

- `MixinEntityRenderer` - 实体光源渲染
- `MixinEntity` - 实体光源计算
- `MixinWorld` - 世界光源管理
- `MixinItemRenderer` - 物品光源
- `MixinEntityCreeper/TNTPrimed` - 爆炸体光源

#### 5. OptiFine替代对照表

| OptiFine功能 | Angelica替代方案 | 实现位置 |
|-------------|-----------------|---------|
| **着色器系统** | Iris Shaders | `shaders/` |
| **动态光源** | DynamicLights | `dynamiclights/` |
| **光照优化** | Celeritas | `celeritas/` |
| **自定义纹理(CIT)** | MCPatcherForge CIT | `mcpatcherforge/cit/` |
| **连接纹理(CTM)** | MCPatcherForge CTM | `mcpatcherforge/ctm/` |
| **彩色方块(CC)** | MCPatcherForge CC | `mcpatcherforge/cc/` |
| **云渲染** | VBO云 + NotFine | `notfine/clouds/` |
| **显示列表** | VBO仿真 | `vbo/DisplayListManager` |
| **HUD优化** | HUD缓存 | `hudcaching/` |

#### 6. 代码示例

##### 使用IrisShaderProvider

```java
public class MyRenderer implements IrisShaderProvider {
    @Override
    public boolean isShadersEnabled() {
        return IrisAPI.isShaderPackInUse();
    }
    
    @Override
    public ShaderOverride getShaderOverride() {
        return ShaderOverride.NONE;
    }
    
    @Override
    public boolean shouldUseFaceCulling() {
        return !isShadersEnabled();
    }
    
    @Override
    public VertexType getVertexType() {
        return isShadersEnabled() 
            ? VertexType.SHADER 
            : VertexType.VANILLA;
    }
}
```

##### 注册动态光源

```java
public class GlowingItem extends Item implements IDynamicLightProducer {
    @Override
    public int getLuminance(ItemStack stack) {
        return 15; // 最大亮度
    }
}
```

---

## UniMixins - Mixin加载器

**GitHub**: https://github.com/GTNewHorizons/UniMixins  
**定位**: 统一的Mixin加载器框架，整合多个Mixin生态

### 核心特性

#### 1. 模块化架构

```
┌─────────────────────────────────────┐
│        module-all (Uber JAR)        │
├─────────────────────────────────────┤
│  module-mixin (UniMix核心)          │
│  module-compat (兼容性修复)          │
│  module-mixinbooterlegacy            │
│  module-gasstation                   │
│  module-gtnhmixins                   │
│  module-mixinextras (高级注入)       │
│  module-mixingasm (ASM兼容)          │
└─────────────────────────────────────┘
```

#### 2. 核心接口（9个）

| 接口 | 模块 | 功能 |
|------|------|------|
| **IEarlyMixinLoader** | mixinbooterlegacy | 加载Vanilla/Forge类Mixin |
| **ILateMixinLoader** | mixinbooterlegacy | 加载模组类Mixin |
| **IEarlyMixinLoader** | gasstation | GasStation早期加载 |
| **ILateMixinLoader** | gasstation | GasStation晚期加载 |
| **IEarlyMixinLoader** | gtnhmixins | GTNH早期（支持loadedCoreMods） |
| **ILateMixinLoader** | gtnhmixins | GTNH晚期（支持loadedMods） |
| **IMixinConfigPlugin** | Mixin库 | Mixin配置插件 |
| **IMixinSafeTransformer** | mixingasm | 标记Mixin安全的ASM转换器 |

#### 3. 接口签名

```java
// IEarlyMixinLoader / ILateMixinLoader (通用)
List<String> getMixinConfigs();
boolean shouldMixinConfigQueue(String mixinConfig);
void onMixinConfigQueued(String mixinConfig);

// IEarlyMixinLoader (GTNH版)
String getMixinConfig();
List<String> getMixins(Set<String> loadedCoreMods);

// ILateMixinLoader (GTNH版)
String getMixinConfig();
List<String> getMixins(Set<String> loadedMods);
```

#### 4. 生命周期

```
1. MixinTweaker初始化 → Launch.blackboard.put("mixin.initialised")
2. IFMLLoadingPlugin.injectData() → AllCore加载所有嵌入插件
3. FML早期: MixinCore, CompatCore, GasStationCore, GTNHMixinsCore初始化
4. EARLY阶段: IEarlyMixinLoader.getMixinConfigs() → 加载Vanilla/Forge Mixin
5. DEFAULT阶段: ASM转换器执行
6. 模组加载: Forge mod discovery → classpath可用
7. LATE阶段: LateMixinOrchestrationMixin → ILateMixinLoader.getMixins()
8. 运行时: IMixinConfigPlugin.preApply/postApply
```

#### 5. MixinExtras扩展注入

**路径**: `module-mixinbooterlegacy/src/main/java/io/github/tox1cozz/mixinextras/`

| 注解 | 用途 |
|-----|------|
| **@ModifyExpressionValue** | 修改表达式值 |
| **@ModifyReturnValue** | 修改方法返回值 |
| **@ModifyReceiver** | 修改方法调用接收器 |
| **@WrapWithCondition** | 条件包装方法调用 |

**示例**:
```java
@ModifyReturnValue(
    method = "getMaxHealth",
    at = @At("RETURN")
)
private float modifyMaxHealth(float original) {
    return original * 2.0f; // 双倍生命值
}
```

#### 6. ASM转换器

| 转换器 | 功能 |
|-------|------|
| **ASMRemapperTransformer** | ASM包名重映射 |
| **EnhanceCrashReportsTransformer** | 崩溃报告增强 |
| **IgnoreDuplicateJarsTransformer** | 重复Jar处理 |
| **HackClasspathModDiscoveryTransformer** | Classpath模组发现 |

#### 7. 配置系统

**配置文件**: `config/unimixins.properties`

```properties
compat.enableRemapper=true
compat.enhanceCrashReports=true
compat.improveInitPhaseDetection=true
gtnhmixins.enableLegacyGTNHMixinExtrasPackage=true
```

#### 8. 使用示例

##### 实现早期Mixin加载器

```java
public class MyEarlyMixins implements IEarlyMixinLoader {
    @Override
    public String getMixinConfig() {
        return "mixins.mymod.early.json";
    }
    
    @Override
    public List<String> getMixins(Set<String> loadedCoreMods) {
        List<String> mixins = new ArrayList<>();
        
        // 仅在特定coremod存在时加载
        if (loadedCoreMods.contains("FMLCorePlugin")) {
            mixins.add("MixinVanillaClass");
        }
        
        return mixins;
    }
}
```

##### 实现晚期Mixin加载器

```java
public class MyLateMixins implements ILateMixinLoader {
    @Override
    public String getMixinConfig() {
        return "mixins.mymod.late.json";
    }
    
    @Override
    public List<String> getMixins(Set<String> loadedMods) {
        List<String> mixins = new ArrayList<>();
        
        // 仅在特定mod存在时加载
        if (loadedMods.contains("gregtech")) {
            mixins.add("MixinGTClass");
        }
        
        return mixins;
    }
}
```

---

## StructureLib - 结构验证库

**GitHub**: https://github.com/GTNewHorizons/StructureLib  
**定位**: 多方块结构定义和验证系统

### 核心架构

```
┌─────────────────────────────────────────┐
│  IStructureDefinition (结构定义)        │ ← Builder模式
├─────────────────────────────────────────┤
│  IStructureElement (结构元素)           │ ← 验证/放置/提示
├─────────────────────────────────────────┤
│  IAlignment/IConstructable (对齐/构建)  │ ← 方向管理
├─────────────────────────────────────────┤
│  StructureUtility (工具类)              │ ← 静态工厂方法
└─────────────────────────────────────────┘
```

### 核心接口（26个）

#### A. 结构定义接口

| 接口 | 路径 | 功能 | 关键方法 |
|------|------|------|---------|
| **IStructureDefinition<T>** | `structure/` | 多方块定义 | `check()`, `build()`, `hints()` |
| **StructureDefinition.Builder<T>** | `structure/` | Builder实现 | `addShape()`, `addElement()` |
| **IStructureElement<T>** | `structure/` | 单元素接口 | `check()`, `placeBlock()` |

#### B. 元素变体接口

| 接口 | 功能 |
|------|------|
| **IStructureElementNoPlacement<T>** | 仅检查，不放置 |
| **IStructureElementCheckOnly<T>** | 仅验证 |
| **IStructureElementDeferred<T>** | 延迟初始化 |
| **IStructureElementChain<T>** | OR链式匹配 |
| **IStructureNavigate<T>** | 内部导航 |

#### C. 对齐与方向接口

| 接口 | 功能 | 关键方法 |
|------|------|---------|
| **IAlignment** | 方向+旋转+翻转 | `getExtendedFacing()`, `setExtendedFacing()` |
| **IAlignmentLimits** | 限制对齐方式 | `isNewExtendedFacingValid()` |
| **AlignmentLimits.Builder** | Builder构建限制 | `allow()`, `deny()` |

#### D. 构建接口

| 接口 | 功能 |
|------|------|
| **IConstructable** | 结构构建 |
| **ISurvivalConstructable** | 生存模式构建 |
| **IConstructableProvider** | 提供构建对象 |
| **IMultiblockInfoContainer<T>** | 多方块信息注册 |

### 三维坐标系统（A、B、C）

```java
// 站在未旋转的控制器前面
A: 左右方向（水平）
B: 上下方向（垂直）
C: 前后方向（深度）

ExtendedFacing = Direction + Rotation + Flip
```

### Builder模式示例

```java
// 1. 创建Builder
StructureDefinition.Builder<MultiblockController> builder = 
    IStructureDefinition.builder();

// 2. 添加形状
builder.addShape("main", new String[][] {
    {"OOO", "OOO", "OOO"},  // Z层 0
    {"OOO", "~H~", "OOO"},  // Z层 1 (~=控制器)
    {"OOO", "OOO", "OOO"}   // Z层 2
});

// 3. 添加元素
builder.addElement('O', StructureUtility.ofBlock(Blocks.stone, 0))
       .addElement('H', hatches);

// 4. 构建
IStructureDefinition<MultiblockController> definition = builder.build();

// 5. 使用
boolean valid = definition.check(controller, "main", world, facing,
    xCoord, yCoord, zCoord, 0, 0, 0, true);
```

### StructureUtility工厂方法

```java
// 简单方块
StructureUtility.ofBlock(Block block, int meta)
StructureUtility.ofBlockAnyMeta(Block block)

// 多方块选择
StructureUtility.ofBlocksFlat(Map<Block, Integer> blocks, ...)
StructureUtility.ofBlocksMap(Map<Block, Collection<Integer>> blocks, ...)

// 方块提示
StructureUtility.ofBlockHint(Block block, int meta)

// 自定义逻辑
StructureUtility.ofBlockAdder(IBlockAdder<T> adder, ...)
StructureUtility.ofTileAdder(ITileAdder<T> adder, ...)

// 等级系统
StructureUtility.ofBlocksTiered(
    ITierConverter<TIER> tierExtractor,
    TIER baseTier,
    BiConsumer<T, TIER> onTierFound,
    ...
)

// 链式（OR逻辑）
StructureUtility.ofChain(IStructureElement<T>... elements)

// 延迟初始化
StructureUtility.defer(Supplier<IStructureElement<T>> supplier)
StructureUtility.lazy(Supplier<IStructureElement<T>> supplier)

// 条件选择
StructureUtility.onlyIf(Predicate<T> condition, IStructureElement<T> element)
StructureUtility.partitionBy(Function<T, K> keyFunction, Map<K, IStructureElement<T>> elements)

// 副作用回调
StructureUtility.onElementPass(Consumer<T> callback, IStructureElement<T> element)
StructureUtility.onElementFail(Consumer<T> callback, IStructureElement<T> element)
```

### 与GT5U集成

```java
public class MyMultiblock extends MTEMultiBlockBase 
    implements IAlignment, IConstructableProvider {
    
    private static final IStructureDefinition<MyMultiblock> STRUCTURE_DEF;
    
    static {
        STRUCTURE_DEF = IStructureDefinition.<MyMultiblock>builder()
            .addShape("main", shapes)
            .addElement('O', StructureUtility.ofBlock(Blocks.stone, 0))
            .addElement('H', ofHatchAdder(MyMultiblock::addEnergyHatch, 50, 1))
            .build();
    }
    
    @Override
    public boolean checkStructure() {
        return STRUCTURE_DEF.check(this, "main", getWorld(), getFacing(),
            getBasePositionX(), getBasePositionY(), getBasePositionZ(),
            0, 0, 0, true);
    }
    
    @Override
    public IConstructable getConstructable() {
        return new IConstructable() {
            @Override
            public void construct(ItemStack trigger, boolean hintsOnly) {
                if (hintsOnly) {
                    STRUCTURE_DEF.hints(MyMultiblock.this, trigger, ...);
                } else {
                    STRUCTURE_DEF.build(MyMultiblock.this, trigger, ...);
                }
            }
        };
    }
}
```

### Mixin分析（2个）

#### MixinWorld - 块变化通知器

**路径**: `mixins.early.blockChangeNotifier.MixinWorld`

```java
@Mixin(World.class)
public class MixinWorld {
    // 捕获原始块和元数据
    @Inject(method = "setBlock(...)", at = @At("HEAD"))
    public void captureOriginal(...) {
        originalBlock = world.getBlock(x, y, z);
        originalMeta = world.getBlockMetadata(x, y, z);
    }
    
    // 触发监听器
    @Inject(method = "setBlock(...)", at = @At("RETURN"))
    public void notifyListeners(...) {
        BlockChangeNotifier.onBlockChange(
            world, chunk, x, y, z,
            originalBlock, newBlock,
            originalMeta, newMeta
        );
    }
}
```

**用途**:
- 实时结构验证
- 块变化追踪
- 多方块完整性监控

---

## Hodgepodge - 修复集合

**GitHub**: https://github.com/GTNewHorizons/Hodgepodge  
**定位**: GTNH的通用bug修复和性能优化集合

### 核心统计

- **100+ Vanilla修复**
- **50+ 性能优化**
- **80+ MOD兼容性补丁**
- **8个ASM转换器**
- **393个Mixin**

### 核心接口（20个）

| 接口 | 功能 |
|------|------|
| **ISimulationDistanceWorld** | 渲染/模拟距离独立控制 |
| **MutableChunkCoordIntPair** | 可变区块坐标（减少分配） |
| **HasID** | 对象ID属性 |
| **INetherSeed** | 下界种子访问 |
| **GameRuleExt** | 游戏规则扩展 |
| **KeyBindingExt** | 按键绑定扩展 |
| **SafeWriteNBT** | 安全NBT写入 |
| **BlockExt_FixXray** | 修复透视漏洞 |
| **IGuiModList/IGuiScrollingList** | MOD列表UI |
| **ITexturesCache** | 纹理缓存 |

### Mixin分类

#### 1. Bug修复（200+）

##### Vanilla核心修复

| 问题 | Mixin | 解决方案 |
|------|-------|---------|
| 过度分配ChunkPos | `MixinChunkCoordIntPair_FixAllocations` | 允许重用对象 |
| Shift递归堆栈溢出 | `MixinContainer_FixShiftRecursion` | 递归改迭代 |
| 槽位ID越界 | `MixinNetHandlerPlayClient_FixHandleSetSlot` | 边界检查 |
| 字体渲染递归溢出 | `MixinFontRenderer_LinewrapRecursion` | 递归改迭代 |
| 栅栏连接错误 | `MixinBlockFence` | 修复类型判定 |
| UV坐标翻转 | `MixinRenderBlocks_FaceYNegUV` | MC-47811修复 |
| 漏斗吞物品 | `MixinTileEntityHopper` | 正确转移逻辑 |
| 火球无法移动 | `MixinEntityFireball` | 恢复火球运动 |

##### 内存泄漏修复

| 泄漏点 | Mixin | 修复 |
|-------|-------|------|
| 服务器引用残留 | `MixinMinecraftServer_ClearServerRef` | 显式清零 |
| 客户端World缓存 | `MixinSkinManager$2` | 解除引用 |
| 红石火把World引用 | `MixinBlockRedstoneTorch` | 移除字段 |
| 卸载Entity残留 | `MixinWorldServerUpdateEntities` | 清理实体 |
| EventHandler未注销 | `MixinEventBus` | 链表清理 |
| 渲染器World缓存 | `MixinRenderGlobal_FixWordLeak` | 引用清理 |

##### 网络修复

| 问题 | Mixin | 解决方案 |
|------|-------|---------|
| 2MiB数据包限制 | `MixinMessageSerializer2` | 扩展到4GiB |
| NBT过大断开 | `MixinPacketBuffer` | 动态调整限制 |
| 自定义消息长度 | `MixinS3FPacketCustomPayload` | 大数据包支持 |
| 数据包编码未验证 | `MixinDataWatcher` | 发送前检查 |

#### 2. 性能优化（50+）

##### ASM级优化

| 优化 | 目标 | 收益 |
|------|------|------|
| **SpeedupLongIntHashMap** | LongIntHashMap | ~50%查询加速 |
| **SpeedupOreDictionary** | OreDictionary | 注册查询加速 |
| **NBTTagCompoundHashMap** | NBT复制 | 避免装箱 |
| **PlayerManager** | PlayerManager | 玩家查询加速 |

##### Mixin级优化

| Mixin | 优化点 | 方式 |
|------|--------|------|
| `MixinChunkProviderClient_RemoveChunkListing` | 客户端区块缓存 | 移除LinkedHashSet |
| `MixinChunkCoordinates_BetterHash` | 哈希冲突 | 更好的散列 |
| `MixinFurnaceRecipes` | 烧炼配方查询 | 缓存最后匹配 |
| `MixinCraftingManager` | 合成配方查询 | 缓存最后匹配 |
| `MixinSpawnerAnimals` | 怪物刷怪 | 视距限制 |
| `MixinEntityPlayer_ThrottlePickup` | 物品拾取事件 | 频率限制 |
| `MixinTcpNoDelay` | 网络延迟 | TCP_NODELAY |
| `FAST_RANDOM` | 随机数 | ThreadLocal |
| `MixinWorld_FastItemPhysics` | 物品物理 | 禁用碰撞 |

#### 3. MOD兼容性修复（80+）

##### Thaumcraft（16个）

```
✓ MixinItem_SortAspectsByName - 按本地化排序魔力
✓ MixinTileWandPedestal - 充能基座Centivis支持
✓ MixinEntityGolemBase - 高维度魔像
✓ MixinThaumcraftApi_SpeedupGetInfusionRecipe - 灌注缓存
✓ MixinBlockMagicalLeaves/Log - 魔法树木修复
✓ MixinGuiResearchRecipe - 研究GUI滚动
```

##### IC2 Classic（9个）

```
✓ MixinIc2WaterKinetic - 水动力保护
✓ MixinItemCropSeed/TileEntityCrop - 库存访问
✓ MixinIc2NanoSuitNightVision - 夜视potion冲突
✓ MixinTileEntityReactorChamber - 反应堆复制
✓ MixinElectricItemManager - 电甲性能
```

##### ExtraUtilities（13个）

```
✓ MixinBlockSpike - 保存NBT
✓ MixinTileEntityEnderQuarry - 修复冻结
✓ MixinBlockDrum - 返回空容器
✓ MixinFluidBufferRetrieval - 流体防void
✓ MixinTileEnderCollector - 末地收集器
```

##### Witchery（6个）

```
✓ MixinEntityReflection - 玩家皮肤反射
✓ MixinRiteClimateChange - 天气仪式
✓ MixinPotionArrayExtender - Potion数组扩展
```

### 配置系统（6个配置类）

```
ASMConfig.java        - ASM转换器开关
FixesConfig.java      - Bug修复配置（100+开关）
SpeedupsConfig.java   - 性能优化配置（20+开关）
TweaksConfig.java     - 功能增强配置
DebugConfig.java      - 调试工具
GeneralConfig.java    - 通用配置
```

### ASM转换器（8个）

| 转换器 | 作用 |
|-------|------|
| **SpeedupProgressBar** | 进度条加速 |
| **SpeedupLongIntHashMap** | HashMap优化 |
| **SpeedupNBTTagCompoundCopy** | NBT复制优化 |
| **SpeedupPlayerManager** | 玩家查询加速 |
| **VarargDissector** | GenLayer优化 |
| **SpeedupOreDictionary** | 矿辞快速查询 |
| **FMLIndexedMessageToMessageCodec** | 网络包修复 |
| **ThermosFurnaceSledgeHammer** | Bukkit烧炉修复 |

---

## 跨仓库集成

### 依赖关系图

```
Hodgepodge
    ├─ depends: GTNHLib 0.6.21+
    ├─ depends: GTNHMixins 2.0.1+
    └─ depends: UniMixins 0.0.20+

Angelica
    └─ uses: UniMixins (Mixin加载)

StructureLib
    └─ uses: GTNHLib (基础工具)

UniMixins
    └─ provides: Mixin加载框架 (所有模组)
```

### 技术栈集成

| 功能 | 提供者 | 使用者 |
|------|-------|--------|
| **Mixin加载** | UniMixins | Angelica, Hodgepodge, StructureLib |
| **渲染优化** | Angelica | GTNH所有模组 |
| **结构验证** | StructureLib | GT5U, TecTech, BartWorks等 |
| **Bug修复** | Hodgepodge | GTNH整体生态 |
| **基础工具** | GTNHLib | 所有GTNH模组 |

### 协同工作示例

#### 1. 多方块渲染优化

```
StructureLib提供结构定义 → 
Angelica优化渲染管道 → 
Hodgepodge修复渲染bug → 
UniMixins加载所有Mixin
```

#### 2. 性能优化链

```
Hodgepodge: 减少对象分配 →
UniMixins: 高效Mixin注入 →
Angelica: VBO批处理 →
StructureLib: 延迟验证
```

---

## 接口统计

### 按仓库统计

| 仓库 | 接口数 | 占比 |
|------|--------|------|
| **Angelica** | 143 | 72.2% |
| **StructureLib** | 26 | 13.1% |
| **Hodgepodge** | 20 | 10.1% |
| **UniMixins** | 9 | 4.5% |
| **总计** | **198** | 100% |

### 按功能统计

| 功能分类 | 接口数 | 主要来源 |
|---------|--------|---------|
| **渲染系统** | 80+ | Angelica |
| **结构验证** | 26 | StructureLib |
| **Mixin加载** | 9 | UniMixins |
| **扩展接口** | 20 | Hodgepodge |
| **访问器接口** | 60+ | Angelica |

### Mixin统计

| 仓库 | Mixin数 | 主要用途 |
|------|---------|---------|
| **Hodgepodge** | 393 | Bug修复/性能优化 |
| **Angelica** | 260 | 渲染优化/着色器 |
| **UniMixins** | 41 | Mixin框架 |
| **StructureLib** | 2 | 块变化通知 |
| **总计** | **696** | - |

---

## 设计模式总结

### 1. Builder模式

**StructureLib**: `IStructureDefinition.Builder<T>`
**Angelica**: `AlignmentLimits.Builder`
**UniMixins**: `MixinBuilder`

### 2. Factory模式

**StructureLib**: `StructureUtility.ofBlock/ofChain/...`
**Angelica**: `ThreadSafeISBRHFactory`
**UniMixins**: `AllCore` 动态模块加载

### 3. Accessor模式

**Angelica**: 60+ Accessor接口
**Hodgepodge**: 扩展接口（ISimulationDistanceWorld等）

### 4. Strategy模式

**StructureLib**: `ITierConverter<TIER>`
**Angelica**: `IrisShaderProvider`

### 5. Observer模式

**StructureLib**: `BlockChangeListener`
**Angelica**: `ChunkTrackerHolder`

### 6. Template Method模式

**StructureLib**: `IStructureElement` 生命周期
**UniMixins**: `IFMLLoadingPlugin` 加载流程

### 7. Adapter模式

**StructureLib**: `IBlockAdder`, `ITileAdder`
**UniMixins**: 多版本Mixin适配

### 8. Lazy Initialization模式

**StructureLib**: `IStructureElementDeferred<T>`
**Angelica**: `Lazy<T>`

---

## 最佳实践

### 1. 使用StructureLib定义多方块

```java
// ✅ 好的做法：使用Builder模式
IStructureDefinition<T> def = IStructureDefinition.<T>builder()
    .addShape("main", shapes)
    .addElement('O', ofBlock(stone, 0))
    .addElement('H', ofChain(hatch1, hatch2))
    .build();

// ❌ 避免：手动遍历验证
for (int x = 0; x < width; x++) {
    for (int y = 0; y < height; y++) {
        for (int z = 0; z < depth; z++) {
            // 手动验证...
        }
    }
}
```

### 2. 使用UniMixins加载Mixin

```java
// ✅ 好的做法：实现ILateMixinLoader
public class MyModMixins implements ILateMixinLoader {
    @Override
    public String getMixinConfig() {
        return "mixins.mymod.late.json";
    }
    
    @Override
    public List<String> getMixins(Set<String> loadedMods) {
        List<String> mixins = new ArrayList<>();
        if (loadedMods.contains("targetmod")) {
            mixins.add("MixinTargetModClass");
        }
        return mixins;
    }
}

// ❌ 避免：硬编码Mixin配置
// 无法动态调整，影响兼容性
```

### 3. 使用Angelica渲染优化

```java
// ✅ 好的做法：实现IDynamicLightProducer
public class GlowingBlock implements IDynamicLightProducer {
    @Override
    public int getLuminance(ItemStack stack) {
        return 15;
    }
}

// ✅ 好的做法：使用IrisShaderProvider
if (IrisAPI.isShaderPackInUse()) {
    // 着色器专用渲染路径
} else {
    // 标准渲染路径
}

// ❌ 避免：硬编码OptiFine检测
// 与Angelica不兼容
```

### 4. 使用Hodgepodge配置

```java
// ✅ 好的做法：检查Hodgepodge配置
if (FixesConfig.fixVanillaBug) {
    // 应用修复逻辑
}

// ✅ 好的做法：使用安全NBT写入
if (tile instanceof SafeWriteNBT) {
    ((SafeWriteNBT) tile).safeWriteToNBT(tag);
}

// ❌ 避免：假设所有修复都启用
// 用户可能禁用特定修复
```

---

## 相关文档

- [GT5U_Readme.md](./GT5U_Readme.md) - GT5-Unofficial接口
- [AE_README.md](./AE_README.md) - AE2架构
- [Useful_Readme.md](./Useful_Readme.md) - 可重用代码
- [GTNH_Repos_Index.md](./GTNH_Repos_Index.md) - 仓库总索引

---

**最后更新**: 2026-02-12  
**维护者**: AI Knowledge Base Team  
**版本**: 1.0  
**覆盖仓库**: 4个核心基础设施仓库
