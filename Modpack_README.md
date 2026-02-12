# GTNH整合包配置与管理文档

**仓库地址**: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack  
**整合包版本**: GTNH 2.9.x (版本号: 2110)  
**目的**: 为AI提供GTNH整合包的完整配置知识库

---

## 目录

1. [整合包概览](#整合包概览)
2. [目录结构](#目录结构)
3. [配置系统](#配置系统)
4. [自定义内容](#自定义内容)
5. [任务系统](#任务系统)
6. [服务器管理](#服务器管理)
7. [发布流程](#发布流程)
8. [资源包系统](#资源包系统)

---

## 整合包概览

### 基本信息

| 项目 | 内容 |
|------|------|
| **名称** | GregTech: New Horizons (GTNH) |
| **Minecraft版本** | 1.7.10 |
| **当前版本** | 2.9.x (内部版本号: 2110) |
| **最新更新** | 2025-11-30 |
| **模组数量** | 100+ |
| **难度定位** | 极难 (Tier 0 → Tier 11 UIV) |

### 核心特性

- ✅ **完整GT进度树**: 从石器时代到超级终极压（UIV）
- ✅ **精细配方调整**: 所有配方经过平衡性调整
- ✅ **任务引导系统**: 11个Tier + 专项任务线
- ✅ **自定义内容**: 燃料、掉落、工具提示
- ✅ **性能优化**: 多项优化补丁和配置
- ✅ **社区驱动**: 活跃的GitHub开发

### 统计数据

```
配置文件总数: 580+
├── .cfg文件: 400+
├── .xml文件: 30+
├── .json文件: 100+
├── 资源包: 7个
└── 工作流脚本: 6个
```

---

## 目录结构

### 主要目录

```
GT-New-Horizons-Modpack/
├── config/              # 配置文件（580+）
│   ├── GTNewHorizons/   # GTNH专有配置
│   ├── gregtech/        # GregTech配置
│   ├── GTPlusPlus/      # GT++配置
│   ├── NEI/             # NEI配置
│   ├── betterquesting/  # 任务系统
│   ├── AppliedEnergistics2/
│   ├── forestry/
│   ├── thaumcraft/
│   └── [100+ 其他模组配置]
├── mods/                # 模组JAR文件（不在仓库）
├── scripts/             # CraftTweaker脚本（未使用）
├── resourcepacks/       # 资源包（7个）
├── journeymap/          # 地图配置
├── serverutilities/     # 服务器工具
│   ├── server/          # 服务器端配置
│   └── client/          # 客户端配置
├── release/             # 发布文件夹
├── .github/             # GitHub工作流
│   ├── workflows/       # 自动化流程
│   └── scripts/         # Python脚本
├── changelog.py         # 变更日志生成
├── servers.json         # 推荐服务器列表
└── README.md            # 整合包说明
```

### 配置目录详解

```
config/
├── GTNewHorizons/          # GTNH核心配置
│   ├── CustomFuels.xml     # 自定义燃料值
│   ├── CustomDrops.xml     # 怪物掉落
│   ├── CustomToolTips.xml  # 工具提示
│   ├── HazardousItems.xml  # 危险物品
│   ├── dreamcraft.cfg      # DreamCraft配置
│   └── blocklimiter.cfg    # 方块限制
├── gregtech/               # GregTech主配置
│   ├── GregTech.cfg        # 主配置文件
│   ├── Client.cfg          # 客户端设置
│   ├── MachineStats.cfg    # 机器统计
│   ├── Pollution.cfg       # 污染系统
│   ├── OverpoweredStuff.cfg# 平衡性调整
│   └── WorldGeneration.cfg # 世界生成
├── betterquesting/         # 任务系统
│   ├── DefaultQuests.json  # 默认任务
│   ├── [各种任务线JSON]
│   └── questbook/          # 任务书本地化
├── NEI/                    # Not Enough Items
│   ├── client.cfg
│   ├── hiddenitems.cfg     # 隐藏物品列表
│   ├── hiddenhandlers.cfg  # 隐藏处理器
│   └── collapsibleitems.cfg# 可折叠物品
└── [100+ 其他模组配置目录]
```

---

## 配置系统

### A. GTNewHorizons 核心配置

#### 1. CustomFuels.xml - 自定义燃料系统

**路径**: `config/GTNewHorizons/CustomFuels.xml`

**功能**: 精细化燃料值设定，支持9档压缩

**配置结构**:
```xml
<customfuels>
  <fuel>
    <item>minecraft:diamond</item>
    <burntime>32000</burntime>  <!-- 燃烧时间 tick -->
  </fuel>
  <fuel>
    <item>gregtech:gt.metaitem.01:32519</item> <!-- 压缩煤炭 -->
    <burntime>16000</burntime>
  </fuel>
  <fuel>
    <item>appliedenergistics2:tile.BlockSingularity</item>
    <burntime>2147483647</burntime> <!-- 奇异性: 无限燃烧 -->
  </fuel>
</customfuels>
```

**特色燃料**:
- 钻石: 32000 tick
- 压缩煤炭（9个档次）: 16000 - 1296000000 tick
- 奇异性: 永久燃烧 (2^31-1 tick)
- 超立方体: 超长燃烧时间

#### 2. CustomDrops.xml - 怪物掉落调整

**路径**: `config/GTNewHorizons/CustomDrops.xml`

**功能**: 自定义怪物掉落物品和概率

**配置结构**:
```xml
<drops>
  <mob name="Zombie">
    <item>gregtech:gt.metaitem.01:2300</item> <!-- 铜粉 -->
    <chance>0.05</chance>  <!-- 5%概率 -->
    <amount>1-3</amount>
  </mob>
  <mob name="Skeleton">
    <item>gregtech:gt.metaitem.01:2301</item> <!-- 锡粉 -->
    <chance>0.03</chance>
  </mob>
</drops>
```

#### 3. CustomToolTips.xml - 工具提示定制

**路径**: `config/GTNewHorizons/CustomToolTips.xml`

**功能**: 为物品添加自定义工具提示

**配置结构**:
```xml
<tooltips>
  <item>
    <name>gregtech:gt.blockmachines:9231</name>
    <tooltip>
      <line>Large Turbine Controller</line>
      <line>Tier: EV</line>
      <line>Efficiency: 100%</line>
    </tooltip>
  </item>
</tooltips>
```

#### 4. HazardousItems.xml - 危险物品管理

**路径**: `config/GTNewHorizons/HazardousItems.xml`

**功能**: 标记危险物品，触发特殊效果

**危险类型**:
- 🔥 **Fire**: 岩浆桶、火焰弹
- ☠️ **Poison**: 剧毒药水、蜘蛛眼
- ⚡ **Radiation**: 放射性物质、核废料
- ❄️ **Cryogenic**: 液氮、超冷流体

**配置示例**:
```xml
<hazardous>
  <item type="radiation">
    <name>gregtech:gt.metaitem.01:30087</name> <!-- 铀燃料棒 -->
    <level>3</level>  <!-- 辐射等级 -->
    <effect>poison,3,600</effect> <!-- 中毒III, 30秒 -->
  </item>
</hazardous>
```

#### 5. blocklimiter.cfg - 方块限制器

**路径**: `config/GTNewHorizons/blocklimiter.cfg`

**功能**: 限制某些方块的放置数量（服务器性能保护）

**配置示例**:
```properties
# 最大刷怪笼数量
spawner.max=10

# 最大漏斗数量
hopper.max=500

# 最大区块加载器数量
chunkloader.max=20
```

### B. GregTech 配置

#### GregTech.cfg - 主配置

**路径**: `config/gregtech/GregTech.cfg`

**关键配置项**:

```properties
general {
    # 调试模式
    B:debug_mode=false
    
    # 启用污染系统
    B:pollution_enabled=true
    
    # GT硬模式
    B:hardmode=true
    
    # 允许GT机器在雨中爆炸
    B:machine_rain_explosion=true
    
    # IC2能源网兼容
    B:ic2_energy_net=true
}

worldgen {
    # 禁用原版矿石生成
    B:disable_vanilla_ores=true
    
    # GT矿脉生成
    B:enable_gt_ore_veins=true
}

machines {
    # 机器维护系统
    B:enable_maintenance=true
    
    # 完美超频
    B:perfect_overclock=false
}
```

#### Pollution.cfg - 污染系统

**路径**: `config/gregtech/Pollution.cfg`

**污染源**:
```properties
pollution {
    # 熔炉污染
    furnace_pollution=10
    
    # 爆炸污染
    explosion_pollution=50
    
    # Galacticraft火箭
    rocket_pollution=1000
    
    # Railcraft机车
    locomotive_pollution=5
}

effects {
    # 污染导致草变色
    grass_color_change=true
    
    # 污染导致花枯萎
    flower_death=true
    
    # 污染导致水变色
    water_color_change=true
}
```

### C. NEI 配置

#### hiddenitems.cfg - 隐藏物品列表

**路径**: `config/NEI/hiddenitems.cfg`

**功能**: 隐藏NEI中的无用/调试物品

**配置格式**:
```
minecraft:command_block@0
minecraft:barrier@0
gregtech:gt.blockmachines:9999  # 调试机器
```

### D. BetterQuesting 任务配置

**路径**: `config/betterquesting/`

**主要文件**:
- `DefaultQuests.json` - 默认任务数据
- `QuestDatabase.json` - 任务数据库
- `QuestLines.json` - 任务线定义
- `questbook/` - 任务本地化文件

**任务结构** (在下一节详述)

---

## 自定义内容

### 自定义燃料系统

#### 燃料分级表

| 燃料 | 燃烧时间 | 压缩等级 |
|------|---------|---------|
| 煤炭 | 1600 tick | 0 |
| 压缩煤炭×1 | 16000 tick | 1 |
| 压缩煤炭×2 | 144000 tick | 2 |
| 压缩煤炭×3 | 1296000 tick | 3 |
| 压缩煤炭×4 | 11664000 tick | 4 |
| 压缩煤炭×5 | 104976000 tick | 5 |
| 压缩煤炭×6 | 944784000 tick | 6 |
| 压缩煤炭×7 | 1296000000 tick | 7 |
| 压缩煤炭×8 | 1296000000 tick | 8 |
| 压缩煤炭×9 | 1296000000 tick | 9 |

**特殊燃料**:
- **钻石**: 32000 tick (20倍煤炭)
- **烈焰粉**: 2400 tick
- **奇异性**: 2147483647 tick (永久)

#### 配置自定义燃料

```xml
<!-- 添加新燃料 -->
<fuel>
  <item>modid:custom_fuel</item>
  <burntime>100000</burntime>
</fuel>

<!-- 修改现有燃料 -->
<fuel>
  <item>minecraft:coal</item>
  <burntime>3200</burntime>  <!-- 原版1600 → 3200 -->
</fuel>
```

### 自定义怪物掉落

#### 掉落配置示例

```xml
<drops>
  <!-- 僵尸掉落铜粉 -->
  <mob name="Zombie">
    <item>gregtech:gt.metaitem.01:2300</item>
    <chance>0.05</chance>
    <amount>1-3</amount>
  </mob>
  
  <!-- 末影人掉落末影珍珠+ -->
  <mob name="Enderman">
    <item>gregtech:gt.metaitem.01:17533</item>
    <chance>0.1</chance>
  </mob>
  
  <!-- Boss掉落 -->
  <mob name="WitherBoss">
    <item>gregtech:gt.metaitem.01:32501</item>
    <chance>1.0</chance>
    <amount>64</amount>
  </mob>
</drops>
```

### 工具提示系统

#### 多语言工具提示

```xml
<tooltips>
  <item>
    <name>gregtech:gt.blockmachines:1</name>
    <tooltip lang="en_US">
      <line>Electric Blast Furnace</line>
      <line>Voltage: HV+</line>
      <line>Can process: Steel, Aluminium, etc.</line>
    </tooltip>
    <tooltip lang="zh_CN">
      <line>电力高炉</line>
      <line>电压: HV+</line>
      <line>可处理: 钢、铝等</line>
    </tooltip>
  </item>
</tooltips>
```

---

## 任务系统

### 任务Tier体系

```
Tier 0: Stone Age (石器时代)
  └─ 木工、石器工具、基础生存

Tier 1: LV (低压 - 32EU/t)
  └─ 蒸汽时代、青铜机器、基础电力

Tier 2: MV (中压 - 128EU/t)
  └─ 钢铁时代、电力机器、自动化

Tier 3: HV (高压 - 512EU/t)
  └─ 不锈钢、高级电路、AE2

Tier 4: EV (极高压 - 2048EU/t)
  └─ 钛、等离子体、核反应堆

Tier 5: IV (绝缘压 - 8192EU/t)
  └─ 钨钢、聚变反应堆

Tier 6: LuV (低超压 - 32768EU/t)
  └─ 铑钯、量子计算机

Tier 7: ZPM (零点模 - 131072EU/t)
  └─ 锇、纳米技术

Tier 8: UV (终极压 - 524288EU/t)
  └─ 中子素、暗物质

Tier 9: UHV (超终极压 - 2097152EU/t)
  └─ 奇异物质、时空操控

Tier 10: UEV (超绝缘压 - 8388608EU/t)
  └─ 维度科技、无限能源

Tier 11: UIV (超超绝缘压 - 33554432EU/t)
  └─ 神级科技、最终目标
```

### 专项任务线

```
Space Race (太空竞赛)
  ├─ Moon Landing (登月)
  ├─ Mars Colony (火星殖民)
  ├─ Asteroid Mining (小行星采矿)
  └─ Dyson Sphere (戴森球)

Bee Breeding (蜜蜂育种)
  ├─ Basic Bees (基础蜜蜂)
  ├─ Industrial Bees (工业蜜蜂)
  ├─ Magical Bees (魔法蜜蜂)
  └─ Space Bees (太空蜜蜂)

Thaumcraft Research (神秘研究)
  ├─ Basic Aspects (基础要素)
  ├─ Forbidden Magic (禁忌魔法)
  ├─ Alchemy (炼金术)
  └─ Golemancy (魔像学)

End Game Goals (终局目标)
  ├─ Creative Mode Items (创造模式物品)
  ├─ Infinity Ingot (无限锭)
  ├─ Stargate (星门)
  └─ Ultimate Achievement (终极成就)
```

### 任务配置结构

**路径**: `config/betterquesting/`

```json
{
  "questID": 1000,
  "name": "Electric Blast Furnace",
  "description": "Build your first EBF",
  "questLogic": "AND",
  "tasks": [
    {
      "taskID": "retrieval",
      "items": [
        {
          "item": "gregtech:gt.blockmachines:1001",
          "amount": 1
        }
      ]
    }
  ],
  "rewards": [
    {
      "rewardID": "item",
      "item": "gregtech:gt.metaitem.01:32501",
      "amount": 64
    }
  ],
  "preRequisites": [999]  // 前置任务ID
}
```

---

## 服务器管理

### ServerUtilities 配置

**路径**: `serverutilities/`

#### 权限系统

**ranks.txt** - 权限等级定义:
```
[default]
permissions=["modifyworld.chat"]
max_homes=1
max_claims=10

[vip]
parent=default
permissions=["modifyworld.teleport", "serverutilities.homes.2"]
max_homes=3
max_claims=50

[admin]
parent=vip
permissions=["*"]
max_homes=10
max_claims=1000
op_level=4
```

**players.txt** - 玩家权限:
```
{
  "uuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "name": "PlayerName",
  "rank": "vip",
  "power": 100
}
```

#### 区块声明系统

**serverutilities.cfg**:
```properties
claims {
    # 最大可声明区块数
    I:max_claimed_chunks=500
    
    # 最大可加载区块数
    I:max_force_loaded_chunks=50
    
    # 区块声明成本
    D:claim_cost=10.0
}

teams {
    # 启用团队系统
    B:enable_teams=true
    
    # 最大团队成员数
    I:max_team_members=20
}
```

---

## 发布流程

### 自动化发布系统

**GitHub Actions工作流**: `.github/workflows/release-tags.yml`

```yaml
name: Release Tags

on:
  push:
    tags:
      - 'v*'  # 匹配 v2.9.0 等标签

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Generate Changelog
        run: python changelog.py
      
      - name: Create Release
        uses: actions/create-release@v1
        with:
          tag_name: ${{ github.ref }}
          release_name: GTNH ${{ github.ref }}
          body_path: CHANGELOG.md
```

### changelog.py - 变更日志生成器

**路径**: `changelog.py`

**功能**:
- 自动提取Git提交信息
- 关联GitHub Issue/PR
- 分类变更（新增、修复、调整）
- 生成Markdown格式

**使用方法**:
```bash
# 生成2.9.0到2.9.1之间的变更日志
python changelog.py --from v2.9.0 --to v2.9.1

# 输出到文件
python changelog.py > CHANGELOG.md
```

**输出示例**:
```markdown
## GTNH 2.9.1 - 2025-11-30

### Added
- [#1234] Add new fusion reactor tier
- [#1235] Add cosmic neutronium processing

### Fixed
- [#1236] Fix crash with Large Turbine
- [#1237] Fix recipe conflict

### Changed
- [#1238] Adjust EBF power consumption
- [#1239] Rebalance UHV recipes
```

### 版本管理

**版本号结构**:
```
GTNH 2.9.1
  │  │ │
  │  │ └─ Patch版本 (bug修复)
  │  └─── Minor版本 (新内容)
  └────── Major版本 (重大更新)

内部版本号: 2110
  ├─ 21: 年份 (2021)
  └─ 10: 序号
```

---

## 资源包系统

### 内置资源包

**路径**: `resourcepacks/`

| 资源包 | 大小 | 功能 |
|--------|------|------|
| **Fast Leaves Fix.zip** | 小 | 优化叶子渲染，提升FPS |
| **Realistic Sky GT New Horizons.zip** | 中 | 真实天空纹理 |
| **Glow Lines Only Galacticraft Thermal Padding GT V1.0.0.zip** | 小 | 发光线条效果 |
| **Round Large Turbine Overlay.zip** | 小 | 圆形大型涡轮UI |
| **IronChest Old Textures.zip** | 小 | 铁箱子遗留纹理 |
| **Ore GT New Horizons.zip** | 中 | 矿石纹理统一 |
| **Tinkers Construct Old Textures.zip** | 小 | 匠魂遗留纹理 |

### 推荐资源包加载顺序

```
1. Ore GT New Horizons.zip (底层)
2. Fast Leaves Fix.zip
3. Realistic Sky GT New Horizons.zip
4. Round Large Turbine Overlay.zip
5. Glow Lines Only... (顶层)
```

### JourneyMap 配置

**路径**: `journeymap/config/`

```properties
waypoint {
    # 允许死亡点
    B:death_waypoint=true
    
    # 最大路径点数量
    I:max_waypoints=1000
}

map {
    # 启用洞穴地图
    B:cave_mapping=true
    
    # 地图更新频率
    I:update_frequency=2
}
```

---

## 配置最佳实践

### 客户端性能优化

```properties
# config/gregtech/Client.cfg
performance {
    # 禁用不必要的粒子效果
    B:disable_particles=true
    
    # 简化机器渲染
    B:simple_machine_render=true
    
    # 降低污染视觉效果
    B:reduce_pollution_effects=true
}
```

### 服务器性能优化

```properties
# serverutilities.cfg
optimization {
    # 限制漏斗检查频率
    I:hopper_check_interval=8
    
    # 限制区块加载器
    I:max_chunkloaders=100
    
    # 自动清理掉落物
    I:item_despawn_time=6000
}

# config/gregtech/GregTech.cfg
server {
    # 禁用客户端同步
    B:disable_client_sync=true
    
    # 减少网络包大小
    B:compress_network_packets=true
}
```

### 难度调整建议

```properties
# config/GTNewHorizons/dreamcraft.cfg
difficulty {
    # 配方难度（1-10）
    I:recipe_difficulty=8
    
    # 是否启用GT硬模式
    B:hard_mode=true
    
    # 是否需要维护
    B:require_maintenance=true
}
```

---

## 常见配置任务

### 1. 添加自定义燃料

```xml
<!-- config/GTNewHorizons/CustomFuels.xml -->
<fuel>
  <item>mymod:custom_coal</item>
  <burntime>20000</burntime>
</fuel>
```

### 2. 调整怪物掉落

```xml
<!-- config/GTNewHorizons/CustomDrops.xml -->
<mob name="Creeper">
  <item>gregtech:gt.metaitem.01:2089</item> <!-- 硫粉 -->
  <chance>0.2</chance>
  <amount>2-5</amount>
</mob>
```

### 3. 隐藏NEI物品

```
# config/NEI/hiddenitems.cfg
modid:unwanted_item@*
gregtech:gt.metaitem.01:32000  # 隐藏特定meta
```

### 4. 添加工具提示

```xml
<!-- config/GTNewHorizons/CustomToolTips.xml -->
<item>
  <name>gregtech:gt.blockmachines:5132</name>
  <tooltip>
    <line>§6Large Plasma Turbine</line>
    <line>§7Tier: LuV</line>
    <line>§aEfficiency: 105%</line>
  </tooltip>
</item>
```

### 5. 配置服务器权限

```
# serverutilities/server/ranks.txt
[moderator]
parent=vip
permissions=[
  "modifyworld.kick",
  "serverutilities.claims.modify_others"
]
max_claims=200
```

---

## 脚本系统（未来）

**当前状态**: 整合包未使用CraftTweaker脚本

**原因**: 配方调整通过模组配置文件管理，更易维护

**未来规划**: 可能引入.zs脚本用于复杂配方逻辑

**如果需要脚本**:
```groovy
// scripts/custom_recipes.zs
import mods.gregtech.RecipeBuilder;

// 添加自定义配方
RecipeBuilder.create("custom_steel")
  .inputs(<ore:ingotIron> * 1, <ore:dustCarbon> * 1)
  .fluidInputs(<liquid:oxygen> * 1000)
  .outputs(<ore:ingotSteel> * 1)
  .duration(200)
  .EUt(120)
  .buildAndRegister();
```

---

## 相关文档

- [Core_Infrastructure_README.md](./Core_Infrastructure_README.md) - 核心基础设施
- [ModularUI_README.md](./ModularUI_README.md) - GUI框架
- [GT5U_Readme.md](./GT5U_Readme.md) - GT5U接口
- [GTNH_Repos_Index.md](./GTNH_Repos_Index.md) - 仓库总索引

---

## 社区资源

### 官方资源
- **官网**: https://www.gtnewhorizons.com/
- **GitHub**: https://github.com/GTNewHorizons
- **Discord**: https://discord.gg/gtnh
- **Wiki**: https://gtnh.miraheze.org/

### 文档资源
- **任务书**: 游戏内BetterQuesting
- **配方查询**: NEI/JEI
- **进度树**: GTNH Wiki

### 下载地址
- **CurseForge**: https://www.curseforge.com/minecraft/modpacks/gt-new-horizons
- **Technic**: https://www.technicpack.net/modpack/greg-tech-new-horizons

---

**最后更新**: 2026-02-12  
**整合包版本**: GTNH 2.9.x (2110)  
**维护者**: AI Knowledge Base Team  
**版本**: 1.0
