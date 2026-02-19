# GoodGenerator Fabricator 物品列表

**模块**: GGFab
**总计**: 18 个物品
**文件**: `src/main/java/ggfab/GGItemList.java`
**枚举类**: `GGItemList`
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/ggfab/GGItemList.java

---

## 📋 说明

本文档列出GoodGenerator Fabricator模块的所有ItemList枚举项。

### 使用示例

```java
import ggfab.GGItemList;

// 获取1个物品
ItemStack item = GGItemList.LinkedInputBus.get(1);

// 获取64个物品
ItemStack items = GGItemList.AdvAssLine.get(64);

// 检查物品是否已注册
if (GGItemList.LinkedInputBus.hasBeenSet()) {
    // 使用物品
}
```

---

## 📜 完整列表

| 枚举键值 | 获取代码 |
|---------|---------|
| `AdvAssLine` | `GGItemList.AdvAssLine.get(1)` |
| `LinkedInputBus` | `GGItemList.LinkedInputBus.get(1)` |
| `SingleUseCrowbar` | `GGItemList.SingleUseCrowbar.get(1)` |
| `SingleUseCrowbarMold` | `GGItemList.SingleUseCrowbarMold.get(1)` |
| `SingleUseFile` | `GGItemList.SingleUseFile.get(1)` |
| `SingleUseFileMold` | `GGItemList.SingleUseFileMold.get(1)` |
| `SingleUseHardHammer` | `GGItemList.SingleUseHardHammer.get(1)` |
| `SingleUseHardHammerMold` | `GGItemList.SingleUseHardHammerMold.get(1)` |
| `SingleUseSaw` | `GGItemList.SingleUseSaw.get(1)` |
| `SingleUseSawMold` | `GGItemList.SingleUseSawMold.get(1)` |
| `SingleUseScrewdriver` | `GGItemList.SingleUseScrewdriver.get(1)` |
| `SingleUseScrewdriverMold` | `GGItemList.SingleUseScrewdriverMold.get(1)` |
| `SingleUseSoftMallet` | `GGItemList.SingleUseSoftMallet.get(1)` |
| `SingleUseSoftMalletMold` | `GGItemList.SingleUseSoftMalletMold.get(1)` |
| `SingleUseWireCutter` | `GGItemList.SingleUseWireCutter.get(1)` |
| `SingleUseWireCutterMold` | `GGItemList.SingleUseWireCutterMold.get(1)` |
| `SingleUseWrench` | `GGItemList.SingleUseWrench.get(1)` |
| `SingleUseWrenchMold` | `GGItemList.SingleUseWrenchMold.get(1)` |

---

## 相关文档

- [Registry_Multi_Module_README.md](Registry_Multi_Module_README.md) - 多模块注册系统总览
- [GregTech_Item.md](GregTech_Item.md) - GregTech主模块物品列表

**数据提取时间**: 2026-02-19  
**数据来源**: GT5-Unofficial实际源代码