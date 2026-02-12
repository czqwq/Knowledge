# GTNewHorizons 仓库索引与知识库

**组织地址**: https://github.com/GTNewHorizons  
**总仓库数**: 300+ 个仓库  
**项目类型**: GregTech: New Horizons 整合包及其生态系统

---

## 📊 已分析的仓库

### 核心仓库（已完成文档）

| 仓库 | 文档 | 接口数 | 状态 |
|------|------|--------|------|
| **GT5-Unofficial** | [GT5U_Readme.md](./GT5U_Readme.md) | 228 | ✅ 已完成 |
| **NewHorizonsCoreMod** | [Useful_Readme.md](./Useful_Readme.md#newhorizonscoremod-可重用代码) | 5 | ✅ 已完成 |
| **GTNHLib** | [Useful_Readme.md](./Useful_Readme.md#gtnhlib-可重用代码库) | 81 | ✅ 已完成 |
| **Applied-Energistics-2-Unofficial** | [AE_README.md](./AE_README.md) | 286 | ✅ 已完成 |

**总计**: 600+ 核心接口已文档化

### 第三方模组（已完成文档）

| 仓库 | 文档 | 接口数 | 状态 |
|------|------|--------|------|
| **Programmable-Hatches-Mod** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#1-programmable-hatches-mod) | 48 | ✅ 已完成 |
| **GT-Not-Leisure** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#2-gt-not-leisure) | 68 | ✅ 已完成 |
| **Twist-Space-Technology-Mod** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#3-twist-space-technology-mod) | 17 | ✅ 已完成 |
| **AE2Things** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#4-ae2things) | 51 | ✅ 已完成 |
| **NH-Utilities** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#5-nh-utilities) | 14 | ✅ 已完成 |
| **123Technology** | [PrivateMods_Readme.md](./PrivateMods_Readme.md#6-123technology) | 3 | ✅ 已完成 |

**总计**: 201个第三方接口已文档化

---

## 🔧 重要的GTNH仓库（推荐优先分析）

### Tier 1 - 核心基础设施

| 仓库名 | 描述 | 优先级 | 预计接口数 |
|--------|------|--------|-----------|
| GT-New-Horizons-Modpack | 主整合包配置 | 🔴 高 | ~10 |
| Angelica | OptiFine替代（渲染优化） | 🔴 高 | ~50 |
| ModularUI2 | GUI库 | 🔴 高 | ~40 |
| StructureLib | 结构验证库 | 🔴 高 | ~30 |

### Tier 2 - 主要模组

| 仓库名 | 描述 | 优先级 | 预计接口数 |
|--------|------|--------|-----------|
| Botania | 植物魔法 | 🟡 中 | ~60 |
| Thaumcraft | 神秘时代4 | 🟡 中 | ~100 |
| StorageDrawers | 储物抽屉 | 🟡 中 | ~20 |
| NotEnoughItems | NEI | 🟡 中 | ~40 |
| Railcraft | 铁路 | 🟡 中 | ~50 |
| EnderIO | 末影接口 | 🟡 中 | ~70 |
| IndustrialCraft2 | 工业2 | 🟡 中 | ~80 |
| Forestry | 林业 | 🟡 中 | ~60 |

### Tier 3 - 辅助模组

| 仓库名 | 描述 | 优先级 | 预计接口数 |
|--------|------|--------|-----------|
| WitchingGadgets | 神秘插件 | 🟢 低 | ~30 |
| ThaumicEnergistics | 神秘能源学 | 🟢 低 | ~25 |
| GalaxySpace | 星系空间 | 🟢 低 | ~40 |
| BartWorks | 巴特工坊 | 🟢 低 | ~35 |
| TecTech | 科技技术 | 🟡 中 | ~50 |
| KubaTech | 库巴科技 | 🟢 低 | ~20 |
| GoodGenerator | 好的发电机 | 🟢 低 | ~25 |

---

## 📚 知识库文档索引

### 主要文档

1. **GT5U_Readme.md** - GT5-Unofficial 完整接口列表
   - 228个接口
   - 按包分类
   - 包含功能描述

2. **Useful_Readme.md** - 可重用代码文档  
   - GT5U核心系统架构
   - NHCM和GTNHLib工具类
   - 设计模式实现
   - 实战代码示例

3. **AE_README.md** - AE2架构详解
   - 286个接口
   - 网络/存储/合成系统
   - 扩展点与API
   - 集成示例

4. **PrivateMods_Readme.md** - 第三方模组分析
   - 201个自定义接口
   - Mixin使用分析
   - 跨模组集成模式

### 接口分类统计

| 分类 | 接口数量 | 文档位置 |
|------|---------|---------|
| **机器实体系统** | 80+ | GT5U_Readme.md, Useful_Readme.md |
| **配方系统** | 50+ | Useful_Readme.md |
| **存储系统** | 120+ | AE_README.md |
| **网络系统** | 60+ | AE_README.md |
| **合成系统** | 40+ | AE_README.md |
| **GUI系统** | 45+ | GT5U_Readme.md, AE_README.md |
| **工具接口** | 100+ | GT5U_Readme.md, Useful_Readme.md |
| **第三方自定义** | 201 | PrivateMods_Readme.md |

**总计**: 800+ 接口已文档化

---

## 🎯 Mixin使用分析

### 已识别的Mixin用途

#### 1. 性能优化类Mixin

**来源**: Angelica, GTNHLib

```java
// 渲染优化
@Mixin(RenderGlobal.class)
public class MixinRenderGlobal {
    @Inject(method = "renderEntities")
    private void onRenderEntities(CallbackInfo ci) {
        // 批量渲染优化
    }
}
```

**用途**: 
- 渲染管线优化
- 内存分配优化
- 区块加载优化

#### 2. 功能扩展类Mixin

**来源**: GT-Not-Leisure, Programmable-Hatches

```java
// 扩展官方类功能
@Mixin(MTEHatchInput.class)
public class MixinHatchInput {
    @Inject(method = "onPostTick", at = @At("HEAD"))
    private void onPostTick(CallbackInfo ci) {
        if (this instanceof IInfinitySlot) {
            ((IInfinitySlot) this).updateInfinityStorage();
        }
    }
}
```

**用途**:
- 无限仓扩展
- ME仓集成
- 自定义逻辑注入

#### 3. 兼容性修复类Mixin

**来源**: NewHorizonsCoreMod

```java
// 修复Mod间冲突
@Mixin(SomeModClass.class)
public class MixinCompatFix {
    @Redirect(method = "crashingMethod")
    private void fixCrash(...) {
        // 安全处理
    }
}
```

**用途**:
- Mod冲突修复
- API版本兼容
- 崩溃防护

#### 4. AE2集成类Mixin

**来源**: Programmable-Hatches, AE2Things

```java
// 深度集成AE2
@Mixin(CraftingCPUCluster.class)
public class MixinCPUCluster {
    @Inject(method = "markDirty")
    private void onMarkDirty(CallbackInfo ci) {
        if (externalManager != null) {
            externalManager.postUpdate();
        }
    }
}
```

**用途**:
- CPU复制系统
- 模式优化
- 存储扩展

---

## 🔍 待探索的关键仓库

### 高价值仓库（接口丰富）

1. **StructureLib** - 结构验证框架
   - 多方块结构API
   - 自动生成系统
   - 验证工具

2. **ModularUI2** - 现代GUI框架
   - Widget系统
   - 数据绑定
   - 动画支持

3. **Angelica** - 渲染引擎
   - VAO/VBO接口
   - 着色器系统
   - 性能优化

4. **TecTech** - 高科技扩展
   - 高级多块
   - 能源系统
   - 参数系统

5. **BartWorks** - 化学处理
   - 生物化学接口
   - 材料系统
   - 反应器接口

### 特殊用途仓库

- **CookingForBlockheads** - 厨房系统
- **Chisel** - 装饰方块
- **HoloInventory** - 全息显示
- **WirelessCraftingTerminal** - 无线终端
- **OpenComputers** - 计算机系统

---

## 📝 文档使用指南

### 查找接口

1. **按功能查找**:
   - 机器相关 → GT5U_Readme.md
   - 存储相关 → AE_README.md
   - 工具类 → Useful_Readme.md
   - 自定义 → PrivateMods_Readme.md

2. **按模组查找**:
   - GT5U → GT5U_Readme.md
   - AE2 → AE_README.md
   - NHCM/GTNHLib → Useful_Readme.md
   - 第三方 → PrivateMods_Readme.md

3. **按实现模式查找**:
   - Builder模式 → Useful_Readme.md
   - Factory模式 → Useful_Readme.md, AE_README.md
   - Mixin → PrivateMods_Readme.md

### 学习路径

#### 初学者
1. 阅读 GT5U_Readme.md 了解基础接口
2. 阅读 Useful_Readme.md 学习工具类
3. 实践简单的机器实现

#### 中级开发者
1. 深入 AE_README.md 学习网络系统
2. 研究 Useful_Readme.md 的设计模式
3. 尝试多方块机械

#### 高级开发者
1. 分析 PrivateMods_Readme.md 的Mixin技术
2. 研究跨模组集成
3. 贡献新的扩展

---

## 🌟 贡献指南

### 添加新仓库文档

1. 克隆仓库并分析
2. 提取接口列表
3. 识别Mixin用途
4. 编写使用示例
5. 更新此索引文档

### 文档格式

```markdown
## 仓库名称

**地址**: https://github.com/GTNewHorizons/xxx
**接口数**: XX个

### 核心接口

| 接口 | 包 | 功能 |
|------|----|----|
| ... | ... | ... |

### Mixin分析

...

### 使用示例

...
```

---

## 📊 统计数据

### 当前覆盖率

- **已分析仓库**: 10 / 300+ (3.3%)
- **已文档化接口**: 800+
- **文档总行数**: 5000+
- **代码示例**: 50+

### 接口来源分布

```
GT5-Unofficial:        228 (28%)
AE2-Unofficial:        286 (36%)
GTNHLib:               81  (10%)
第三方模组:             201 (25%)
其他:                   4   (1%)
```

### 文档类型分布

```
接口列表:     40%
使用示例:     30%
架构说明:     20%
Mixin分析:    10%
```

---

## 🔗 相关链接

- **官方网站**: https://www.gtnewhorizons.com/
- **GitHub组织**: https://github.com/GTNewHorizons
- **Wiki**: https://gtnh.miraheze.org/
- **Discord**: https://discord.gg/gtnh

---

**最后更新**: 2026-02-12  
**维护者**: AI Knowledge Base  
**版本**: 1.0
