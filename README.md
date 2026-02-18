# GTNewHorizons Complete Knowledge Base

**这是一个为AI和开发者准备的GTNewHorizons生态系统完整知识库**

## 📚 文档索引

### 核心文档（8个文件，9522行）

| 文档 | 行数 | 内容 | 用途 |
|------|------|------|------|
| **[GT5U_Readme.md](./GT5U_Readme.md)** | 2,310 | GT5-Unofficial全接口列表（228个） | 接口查询 |
| **[Useful_Readme.md](./Useful_Readme.md)** | 1,798 | 可重用代码、工具类、设计模式 | 代码参考 |
| **[Wireless_Network_README.md](./Wireless_Network_README.md)** | 2,457 | GT5U玩家无线能量网络完整文档（命令+代码） | 无线能量系统 |
| **[AE_README.md](./AE_README.md)** | 942 | AE2架构与286个接口 | AE2集成 |
| **[PrivateMods_Readme.md](./PrivateMods_Readme.md)** | 660 | 第三方模组201个接口 | 模组扩展 |
| **[Core_Infrastructure_README.md](./Core_Infrastructure_README.md)** | 990 | 核心基础设施198个接口+696个Mixin | 基础设施 |
| **[GTNH_Repos_Index.md](./GTNH_Repos_Index.md)** | 363 | 300+仓库索引与统计 | 导航索引 |
| **README.md** | 2 | 本文档 | 快速入口 |

---

## 🎯 知识库覆盖范围

### 仓库分析覆盖
- ✅ **GT5-Unofficial**: 228个接口
- ✅ **NewHorizonsCoreMod**: 5个接口
- ✅ **GTNHLib**: 81个接口
- ✅ **Applied-Energistics-2-Unofficial**: 286个接口
- ✅ **Angelica**: 143个接口
- ✅ **UniMixins**: 9个接口
- ✅ **StructureLib**: 26个接口
- ✅ **Hodgepodge**: 20个接口
- ✅ **Programmable-Hatches-Mod**: 48个接口
- ✅ **GT-Not-Leisure**: 68个接口
- ✅ **Twist-Space-Technology-Mod**: 17个接口
- ✅ **AE2Things**: 51个接口
- ✅ **NH-Utilities**: 14个接口
- ✅ **123Technology**: 3个接口

**总计**: 14个仓库，999+接口，696个Mixin

### 内容类型
- 📋 接口列表：999+个接口，含包路径、功能描述
- 🔧 工具类库：160+工具类、Helper、Builder
- 🏗️ 设计模式：12+种模式实现与示例
- 🎨 架构图：5个系统架构图解
- 💻 代码示例：60+实战代码示例
- 🔍 Mixin分析：696个Mixin的详细用途
- ⚡ 性能优化：50+优化技巧和实现

---

## 🚀 快速开始

### 场景1: 查找某个接口
```
1. 知道来自GT5U → 查看 GT5U_Readme.md
2. 知道来自AE2 → 查看 AE_README.md
3. 不确定来源 → 查看 GTNH_Repos_Index.md 找到对应文档
```

### 场景2: 学习如何实现某个功能
```
1. 实现GT机器 → Useful_Readme.md #核心系统架构 > MetaTileEntity系统
2. 实现多方块 → Useful_Readme.md #核心系统架构 > Multiblock结构系统
3. 集成AE2存储 → AE_README.md #使用示例 > 创建ME存储设备
4. 使用Mixin → PrivateMods_Readme.md #Mixin使用分析
```

### 场景3: 查找可重用代码
```
1. 工具类 → Useful_Readme.md #工具类体系
2. Builder模式 → Useful_Readme.md #设计模式实现 > 建造者模式
3. 数据结构 → Useful_Readme.md #数据结构与算法
4. 数字格式化 → Useful_Readme.md #GTNHLib > NumberFormatUtil
```

### 场景4: 了解无线能量网络
```
1. 玩家无线网络基础 → Wireless_Network_README.md #玩家无线能量网络
2. 能量扣除机制 → Wireless_Network_README.md #能量扣除机制
3. 命令使用 → Wireless_Network_README.md #命令系统
4. 代码实现 → Wireless_Network_README.md #代码实现细节
```

---

## 📖 文档详细说明

### GT5U_Readme.md - GT5接口完整目录
**内容**:
- 228个接口的完整列表
- 按64个包分类
- 每个接口含：名称、可见性、文件路径、行号、继承关系
- 自动生成的目录导航

**适合**:
- 快速查找特定接口
- 了解包结构
- API参考

---

### Useful_Readme.md - 可重用代码宝典
**内容**:
1. **工具类体系** (160+类)
   - GTUtility, GTModHandler等核心工具
   - Builder模式实现（GTRecipeBuilder等）
   - Factory模式实现
   - Helper类集合

2. **设计模式实现** (12+种)
   - Builder Pattern
   - Factory Pattern
   - Singleton Pattern
   - Lazy Loading Pattern
   - Strategy Pattern
   - 完整代码示例

3. **核心系统架构** (6大系统)
   - Recipe系统 - 配方管理
   - MetaTileEntity系统 - 机器实体
   - Multiblock结构系统 - 多方块验证
   - GUI与ModularUI系统
   - Cover系统 - 覆盖物
   - Network通信系统

4. **数据结构与算法**
   - 自定义集合类
   - 数学/物理计算
   - 图论与网络算法
   - 序列化工具

5. **NHCM和GTNHLib集成**
   - 脚本系统
   - 物品能力系统
   - 坐标系统
   - 对象池等优化

**适合**:
- 学习代码架构
- 查找可复用代码
- 理解设计模式

---

### AE_README.md - AE2深度剖析
**内容**:
1. **核心接口分类** (286个)
   - 网络系统 (IGrid, IGridNode...)
   - 存储系统 (IMEInventory, ICellHandler...)
   - 合成系统 (ICraftingGrid, ICraftingCPU...)
   - Part系统 (IPart, IPartHost...)
   - 安全系统 (ISecurityGrid...)

2. **扩展点与API** (11+扩展点)
   - ICellHandler - 自定义存储单元
   - IExternalStorageHandler - 外部存储
   - IGridCache - 自定义网格模块
   - 完整注册示例

3. **系统架构**
   - Grid系统架构图
   - Storage系统流程
   - Crafting系统流程
   - Part系统组成

4. **使用示例**
   - 创建ME存储设备
   - 实现合成接口
   - 存储集成
   - 能量集成

**适合**:
- AE2模组开发
- ME网络集成
- 存储系统扩展

---

### PrivateMods_Readme.md - 第三方模组解析
**⚠️ 重要**: 包含自定义接口，非官方标准

**内容**:
1. **6个第三方模组分析**
   - Programmable-Hatches (48接口)
   - GT-Not-Leisure (68接口)
   - Twist-Space-Technology (17接口)
   - AE2Things (51接口)
   - NH-Utilities (14接口)
   - 123Technology (3接口)

2. **自定义接口分类**
   - 标注哪些是官方接口
   - 标注哪些是自定义接口
   - 接口功能说明

3. **核心机制**
   - CPU复制系统
   - 无限仓系统
   - 模块化机械
   - 戴森球系统

4. **Mixin使用分析**
   - 性能优化类
   - 功能扩展类
   - 兼容性修复类
   - AE2集成类

5. **跨模组集成模式**
   - AE2+GT混合模式
   - Mixin深度修改
   - 适配器模式

**适合**:
- 高级模组开发
- Mixin技术学习
- 跨模组集成参考

---

### Core_Infrastructure_README.md - 核心基础设施
**内容**:
1. **4个核心基础设施仓库分析**
   - Angelica (143接口, 260 Mixin) - 渲染引擎
   - UniMixins (9接口, 41 Mixin) - Mixin加载器
   - StructureLib (26接口, 2 Mixin) - 结构验证
   - Hodgepodge (20接口, 393 Mixin) - Bug修复集合

2. **Angelica深度分析**
   - Celeritas地形渲染系统
   - VBO显示列表仿真
   - Iris着色器集成
   - 动态光源系统
   - OptiFine替代方案对照

3. **UniMixins框架分析**
   - 模块化Mixin加载
   - MixinExtras高级注入
   - ASM转换器兼容性
   - 生命周期管理

4. **StructureLib使用指南**
   - Builder模式完整示例
   - 结构元素工厂方法
   - 三维坐标系统（A、B、C）
   - 与GT5U集成

5. **Hodgepodge修复清单**
   - 100+ Vanilla修复
   - 50+ 性能优化
   - 80+ MOD兼容性补丁
   - 配置系统详解

6. **跨仓库集成**
   - 依赖关系图
   - 技术栈集成
   - 协同工作示例
   - 最佳实践

**适合**:
- 基础设施开发
- 渲染优化学习
- Mixin技术深入
- 多方块结构开发
- 性能调优参考

---

### GTNH_Repos_Index.md - 总索引
**内容**:
- 300+仓库列表
- 优先级分类（Tier 1/2/3）
- 已完成/待完成状态
- 统计数据
- 文档使用指南

**适合**:
- 快速导航
- 了解全局
- 规划学习路径

---

## 🎓 学习路径推荐

### 初学者路线
```
1. 阅读 GT5U_Readme.md 前100个接口
2. 阅读 Useful_Readme.md 的 "工具类体系"
3. 实践：创建一个简单的单方块机器
4. 参考：Useful_Readme.md 的 "完整的配方驱动单方块机器"
```

### 中级开发者路线
```
1. 深入 Useful_Readme.md 的 "核心系统架构"
2. 学习 AE_README.md 的 "存储系统"
3. 实践：创建一个多方块机械
4. 实践：集成AE2存储
5. 参考：Useful_Readme.md 的 "完整的多方块机器"
```

### 高级开发者路线
```
1. 研究 PrivateMods_Readme.md 的 "Mixin使用分析"
2. 分析 PrivateMods_Readme.md 的 "跨模组集成模式"
3. 实践：使用Mixin扩展官方功能
4. 实践：创建复杂的跨模组集成
5. 贡献：添加新仓库文档到知识库
```

---

## 📊 知识库统计

### 内容统计
- **总文档数**: 7个
- **总行数**: 7,065行
- **接口总数**: 994个
- **Mixin总数**: 696个
- **代码示例**: 60+
- **架构图**: 5个

### 覆盖率统计
- **已分析仓库**: 14 / 300+ (4.7%)
- **核心仓库覆盖**: 8/8 (100%)
- **重要第三方覆盖**: 6/20+ (30%)

### 接口来源分布
```
AE2-Unofficial:        286 (28.8%)
GT5-Unofficial:        228 (22.9%)
Angelica:              143 (14.4%)
第三方模组:             201 (20.2%)
GTNHLib:               81  (8.1%)
StructureLib:          26  (2.6%)
Hodgepodge:            20  (2.0%)
UniMixins:             9   (0.9%)
其他:                   5   (0.5%)  # NHCM等
```

---

## 🔧 如何使用此知识库

### 作为开发者参考
```bash
# 查找接口
grep -r "IMetaTileEntity" *.md

# 查找示例
grep -r "代码示例" *.md

# 查找特定功能
grep -r "配方系统" *.md
```

### 作为AI训练数据
- 所有文档使用结构化markdown格式
- 包含完整的代码示例
- 详细的功能描述
- 清晰的分类和索引

### 作为学习资料
- 从README.md开始
- 根据学习路径选择对应文档
- 参考代码示例
- 实践并贡献

---

## 🌟 贡献指南

欢迎贡献新的仓库文档！

### 贡献流程
1. 选择一个未分析的GTNH仓库
2. 克隆并分析接口
3. 按照现有格式编写文档
4. 更新GTNH_Repos_Index.md
5. 提交PR

### 文档标准
- 使用markdown格式
- 包含代码示例
- 标注接口来源（官方/自定义）
- 提供使用场景说明

---

## 🔗 相关链接

- **GTNH官网**: https://www.gtnewhorizons.com/
- **GitHub组织**: https://github.com/GTNewHorizons
- **Wiki**: https://gtnh.miraheze.org/
- **Discord**: https://discord.gg/gtnh

---

## 📝 更新日志

### 2026-02-12 - v1.0 初始版本
- ✅ 创建GT5U_Readme.md（228接口）
- ✅ 创建Useful_Readme.md（核心系统+工具类）
- ✅ 创建AE_README.md（286接口）
- ✅ 创建PrivateMods_Readme.md（201接口）
- ✅ 创建GTNH_Repos_Index.md（总索引）
- ✅ 分析10个仓库
- ✅ 文档化800+接口

---

**维护者**: AI Knowledge Base Team  
**许可**: MIT  
**版本**: 1.0  
**最后更新**: 2026-02-12
