# GT5U翻译系统说明

## 概述

本文档说明如何将Translation-of-GTNH中的中文翻译映射到GT5U物品/方块/流体。

**重要**: 所有翻译必须来自真实的Translation-of-GTNH仓库，不能编造！

## Translation-of-GTNH 仓库

- **仓库**: https://github.com/Kiwi233/Translation-of-GTNH
- **本地克隆**: `/tmp/gtnh_repos/Translation-of-GTNH`

## 翻译文件位置

```
Translation-of-GTNH/resources/
├── GregTech[gregtech]/lang/zh_CN.lang       (3,590条翻译)
├── GregTech[miscutils]/lang/zh_CN.lang      (3,807条翻译 - GT++)
├── GregTech[tectech]/lang/zh_CN.lang        (1,854条翻译)
├── GregTech[kubatech]/lang/zh_CN.lang       (211条翻译)
├── GregTech[ggfab]/lang/zh_CN.lang          (30条翻译)
├── GregTech[bartworks]/lang/zh_CN.lang      (255条翻译)
└── GregTech[goodgenerator]/lang/zh_CN.lang  (520条翻译)
```

## Lang文件格式

### 1. 直接物品翻译
```properties
item.itemName.name=中文名称
```

示例（BartWorks）:
```properties
item.GT_Rockcutter_Item_LV.name=岩石切割机LV
item.GT_Teslastaff_Item.name=特斯拉权杖
```

### 2. 方块翻译
```properties
tile.blockName.name=中文名称
tile.blockName.0.name=中文名称（meta 0）
tile.blockName.1.name=中文名称（meta 1）
```

示例（GoodGenerator）:
```properties
MAR_Casing.name=力场约束机械方块
radiationProtectionSteelFrame.name=防辐射钢框架
```

### 3. 组件模板翻译
```properties
gt.component.dust=%s粉
gt.component.ingot=%s锭
gt.component.plate=%s板
```

这些是模板，`%s`会被材料名替换。

### 4. GT特殊格式
```properties
gt.blockmachines.名称.name=中文名
gt.blockcasings.名称.name=中文名
```

## ItemList枚举到翻译的映射问题

### 问题描述

GT5U的`ItemList`枚举使用的是代码中的枚举名（如`Hull_LV`），但在lang文件中，物品的key是基于实际注册的ID（unlocalized name）。

这两者**不一定相同**！

### 示例

```java
// 枚举名称
ItemList.Hull_LV

// 可能的unlocalized name
"gt.blockmachines.hull.lv"
```

在lang文件中的key可能是：
```properties
gt.blockmachines.hull.lv.name=LV机械外壳
```

### 解决方案

要准确映射，需要：

1. **从GT5U源码中找到每个ItemList枚举的set()调用**
   ```java
   ItemList.Hull_LV.set(
       new MTEBasicHull(10, "hull.tier.01", "LV Machine Hull", 1)
       .getStackForm(1)
   );
   ```
   
2. **从set()调用中提取unlocalized name**（上例中是`"hull.tier.01"`）

3. **在lang文件中查找对应的翻译**
   ```properties
   gt.blockmachines.hull.tier.01.name=LV机械外壳
   ```

## 当前状态

### 已验证的翻译资源

| 模块 | Lang文件 | 翻译数量 | 状态 |
|------|---------|---------|------|
| GregTech | ✓ | 3,590 | 可用 |
| GT++ | ✓ | 3,807 | 可用 |
| TecTech | ✓ | 1,854 | 可用 |
| Kubatech | ✓ | 211 | 可用 |
| GGFab | ✓ | 30 | 可用 |
| BartWorks | ✓ | 255 | 可用 |
| GoodGenerator | ✓ | 520 | 可用 |

### 映射状态

- ❌ **ItemList枚举 → Unlocalized Name**: 需要分析GT5U源码
- ✓ **Unlocalized Name → 中文名**: 已有Translation-of-GTNH数据
- ❌ **ItemList枚举 → 中文名**: 无法自动映射（缺少第一步）

## 添加翻译的方法

### 方法1: 手动映射（最准确）

1. 在GT5U源码中找到物品的set()调用
2. 提取unlocalized name
3. 在对应模块的zh_CN.lang中搜索
4. 添加到MD文档

### 方法2: 模式匹配（部分可行）

对于命名规范的物品，可以尝试模式匹配：

```python
# 枚举名: Hull_LV
# 可能的key模式:
- gt.blockmachines.hull.lv.name
- gt.blockmachines.hull_lv.name
- item.hull_lv.name
```

**警告**: 这种方法可能产生错误映射！

### 方法3: 源码分析（最完整）

克隆GT5U仓库，编写脚本分析所有ItemList.set()调用：

```bash
cd /tmp/gtnh_repos/GT5-Unofficial
grep -r "ItemList\.[A-Za-z0-9_]*\.set" src/
```

提取每个枚举的unlocalized name，然后映射到翻译。

## 示例：已验证的翻译

### BartWorks（直接匹配）

| 物品ID | Lang Key | 中文名 |
|--------|----------|--------|
| GT_Rockcutter_Item_LV | item.GT_Rockcutter_Item_LV.name | 岩石切割机LV |
| GT_Teslastaff_Item | item.GT_Teslastaff_Item.name | 特斯拉权杖 |

### GoodGenerator（直接匹配）

| 方块ID | Lang Key | 中文名 |
|--------|----------|--------|
| MAR_Casing | MAR_Casing.name | 力场约束机械方块 |
| radiationProtectionSteelFrame | radiationProtectionSteelFrame.name | 防辐射钢框架 |

### TecTech（直接匹配）

| 方块ID | Lang Key | 中文名 |
|--------|----------|--------|
| quantumStuff | tile.quantumStuff.name | 量子物质 |
| quantumGlass | tile.quantumGlass.name | 量子玻璃 |

## 翻译脚本

位置: `/tmp/add_chinese_names_v2.py`

功能:
- 加载所有模块的zh_CN.lang文件
- 显示翻译数量和示例
- 分析翻译可用性

运行:
```bash
python3 /tmp/add_chinese_names_v2.py
```

## 下一步行动

1. **克隆GT5U源码** （如果尚未克隆）
2. **分析ItemList.set()调用** 提取unlocalized names
3. **创建映射表** 枚举名 → unlocalized name → 中文名
4. **更新MD文档** 添加中文名列

## 重要原则

⚠️ **绝对不能编造翻译！**

- ✅ 只使用Translation-of-GTNH中真实存在的翻译
- ✅ 无法找到翻译的标记为"未翻译"
- ❌ 不能根据英文名猜测中文翻译
- ❌ 不能使用机器翻译
- ❌ 不能编造任何翻译

## 验证方法

所有添加的翻译必须可以通过以下命令验证：

```bash
# 在Translation-of-GTNH中搜索翻译
grep "翻译的中文名" /tmp/gtnh_repos/Translation-of-GTNH/resources/*/lang/zh_CN.lang
```

如果grep找不到，说明翻译是编造的，必须删除！

## 总结

- Translation-of-GTNH提供了完整的翻译数据
- 所有模块的lang文件都已加载并验证
- 主要挑战是ItemList枚举名到unlocalized name的映射
- 需要分析GT5U源码才能准确映射
- 所有翻译必须真实，不能编造

---

**文档更新**: 2026-02-19
**翻译数据版本**: Translation-of-GTNH (latest)
**GT5U版本**: 对应Translation-of-GTNH支持的版本
