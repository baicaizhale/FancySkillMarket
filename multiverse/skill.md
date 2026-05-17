---
name: "multiverse"
description: "Multiverse 多世界管理插件的完整使用指南，涵盖 Core、Portals、NetherPortals、Inventories 全部子插件"
triggers:
  - "multiverse"
  - "mv"
  - "世界"
  - "多世界"
  - "传送世界"
  - "传送门"
  - "portal"
  - "世界管理"
  - "mv create"
  - "mv tp"
auto_trigger: true
source: "multiverse"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "world"
  - "admin"
---

# Multiverse 多世界管理完整指南

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 Multiverse-Core 插件。

检查方法：尝试执行 `/mv version` 命令，如果返回版本信息则说明插件已安装。

如果插件未安装，请告知玩家无法使用多世界管理功能。

## 子插件体系

Multiverse 包含四个子插件，按需安装：

| 子插件 | 功能 |
|--------|------|
| **Multiverse-Core** | 核心插件，世界创建/删除/管理（必装） |
| **Multiverse-Portals** | 传送门系统，自定义传送门形状和目的地 |
| **Multiverse-NetherPortals** | 控制下界传送门链接到哪个世界 |
| **Multiverse-Inventories** | 按世界/组隔离玩家背包和属性 |

## Multiverse-Core — 世界管理

### 信息查询

| 命令 | 说明 |
|------|------|
| `/mv version` | 查看 Multiverse 版本 |
| `/mv list` | 列出所有已加载的世界 |
| `/mv info [世界名]` | 查看世界详细信息（环境、种子、玩家数等） |
| `/mv who <世界名>` | 查看指定世界有哪些玩家 |
| `/mv coord` | 查看当前世界和坐标 |

### 创建世界

```
/mv create <世界名> <环境> [选项...]
```

| 环境类型 | 说明 |
|----------|------|
| `normal` | 主世界（Overworld） |
| `nether` | 下界 |
| `the_end` | 末地 |
| `flat` | 超平坦 |

创建选项：

| 选项 | 说明 |
|------|------|
| `-s <种子>` | 指定世界种子 |
| `-g <生成器>` | 指定世界生成器（见下方生成器列表） |
| `-t <类型>` | 世界类型（`flat`、`amplified`、`large_biomes`） |
| `-a <true/false>` | 是否自动加载世界 |
| `--generatortype <生成器>` | 指定自定义生成器 |

示例：
```
/mv create resource normal -s 123456789
/mv create creative_flat flat
/mv create void normal -g VoidGenerator
```

### 世界生成器

| 生成器 | 说明 |
|--------|------|
| 留空 | 使用默认原版生成器 |
| `VoidGenerator` | 虚空世界（需额外安装生成器插件） |
| `CleanroomGenerator` | 可自定义的虚空/分层世界 |
| `SkyBlock` | 空岛生成器（需 aSkyBlock 等插件） |
| `TerrainControl` | 自定义地形生成 |

### 导入世界

| 命令 | 说明 |
|------|------|
| `/mv import <文件夹名> <环境>` | 导入已有世界文件夹（从 `world/` 下级目录） |
| `/mv import <文件夹名> <环境> -g <生成器>` | 导入并指定生成器 |

### 删除与卸载

| 命令 | 说明 |
|------|------|
| `/mv delete <世界名>` | 删除世界（需要 `/mv confirm` 确认） |
| `/mv unload <世界名>` | 卸载世界（保留文件，不从磁盘删除） |
| `/mv load <世界名>` | 加载已卸载的世界 |
| `/mv reload` | 重载 Multiverse 配置 |
| `/mv confirm` | 确认危险操作（删除世界等） |

### 世界传送

| 命令 | 说明 |
|------|------|
| `/mv tp <世界名>` | 传送到指定世界 |
| `/mv tp <世界名> <玩家>` | 将其他玩家传送到指定世界 |
| `/mv tp <世界名> <x> <y> <z>` | 传送到指定世界的指定坐标 |
| `/mvtp <世界名>` | `/mv tp` 的简写 |

### 出生点管理

| 命令 | 说明 |
|------|------|
| `/mv setspawn` | 设置当前世界的出生点（站在目标位置执行） |
| `/mv spawn [世界名]` | 传送到世界的出生点 |
| `/mv respawn <世界名>` | 设置玩家重生世界 |

### 世界属性修改

```
/mv modify set <属性> <值> [世界名]
```

| 属性 | 值 | 说明 |
|------|-----|------|
| `gamemode` | `survival`/`creative`/`adventure`/`spectator` | 游戏模式 |
| `difficulty` | `peaceful`/`easy`/`normal`/`hard` | 难度 |
| `pvp` | `true`/`false` | PVP 开关 |
| `animals` | `true`/`false` | 动物生成 |
| `monsters` | `true`/`false` | 怪物生成 |
| `animalsSpawn` | `true`/`false` | 动物自然生成 |
| `monsterSpawn` | `true`/`false` | 怪物自然生成 |
| `hunger` | `true`/`false` | 饥饿值 |
| `healOnRest` | `true`/`false` | 睡觉回血 |
| `keepSpawnInMemory` | `true`/`false` | 始终保持世界加载 |
| `autoLoad` | `true`/`false` | 服务器启动时自动加载 |
| `environment` | `normal`/`nether`/`the_end` | 世界环境 |
| `alias` | `<颜色代码><名称>` | 设置彩色别名 |
| `price` | `<金额>` | 传送费用 |
| `generator` | `<生成器名>` | 切换世界生成器 |
| `scaling` | `<数值>` | 世界边界缩放比例（1.0=默认，8.0=下界比例） |
| `respawnWorld` | `<世界名>` | 死亡重生世界 |
| `weather` | `true`/`false` | 天气变化 |
| `allowFlight` | `true`/`false` | 允许飞行 |
| `allowEndPortalsEnter` | `true`/`false` | 允许使用末地传送门 |
| `allowNetherPortalsEnter` | `true`/`false` | 允许使用下界传送门 |

示例：
```
/mv modify set gamemode creative
/mv modify set difficulty peaceful resource
/mv modify set alias &b[资源世界] resource
```

### 世界克隆与修复

| 命令 | 说明 |
|------|------|
| `/mv clone <源世界> <新世界名>` | 克隆世界（完整复制） |
| `/mv regen <世界名>` | 重新生成世界（删除所有玩家建筑！） |
| `/mv debug <世界名>` | 调试模式查看世界加载信息 |
| `/mv purge [世界名\|all] <all\|animals\|monsters\|<生物名>>` | 清除世界中指定实体 |

### 环境与辅助

| 命令 | 说明 |
|------|------|
| `/mv env` | 显示所有可用的环境类型 |
| `/mv who [世界名\|-a]` | 查看各世界的玩家列表 |
| `/mv list --raw` | 列出原始世界名 |

### 权限节点

```
multiverse.access.<世界名>     — 允许进入某世界
multiverse.exempt.<世界名>     — 免传送费用
multiverse.teleport.self       — 允许自己跨世界传送
multiverse.teleport.other      — 允许传送其他玩家
multiverse.core.list           — 允许查看世界列表
multiverse.core.coord          — 允许查看坐标
```

## Multiverse-Portals — 传送门

### 创建传送门

**步骤：**

1. 用 `/mvp wand` 获取传送门选区工具（木斧）
2. 左键/右键选择传送门区域
3. 执行创建命令

| 命令 | 说明 |
|------|------|
| `/mvp create <传送门名>` | 创建传送门（基于木斧选区） |
| `/mvp remove <传送门名>` | 删除传送门 |
| `/mvp select <传送门名>` | 选中传送门区域 |
| `/mvp info` | 查看当前所在传送门信息 |
| `/mvp list` | 列出所有传送门 |
| `/mvp modify desc <描述>` | 设置传送门描述 |
| `/mvp show` | 显示传送门粒子边框 |
| `/mvp hide` | 隐藏传送门粒子边框 |

### 设置传送门目的地

| 命令 | 说明 |
|------|------|
| `/mvp modify dest <目标>` | 设置传送门目的地 |
| `/mvp modify dest p:<传送门名>` | 传送到另一个传送门 |
| `/mvp modify dest w:<世界名>` | 传送到世界出生点 |
| `/mvp modify dest w:<世界名>:<x>,<y>,<z>` | 传送到指定世界坐标 |
| `/mvp modify dest e:<世界名>:<x>,<y>,<z>:<俯仰>:<偏航>` | 传送到指定世界坐标 |

### 传送门填充

| 命令 | 说明 |
|------|------|
| `/mvp modify fill <方块>` | 设置传送门填充方块（如 `water`、`portal`、`air`） |
| `/mvp modify price <金额>` | 设置传送费用 |
| `/mvp modify owner <玩家>` | 设置传送门所有者 |

## Multiverse-NetherPortals — 下界传送门

控制原版下界传送门的目的地映射。

| 命令 | 说明 |
|------|------|
| `/mvnp link <模式> <来源世界> <目标世界>` | 设置下界传送门链接 |
| `/mvnp unlink <来源世界>` | 移除下界传送门链接 |

链接模式：
- `nether` — 双向链接，主世界→下界
- `end` — 双向链接，主世界→末地
- `custom` — 自定义单向链接
- `reverse` — 反向下界→主世界的链接

## Multiverse-Inventories — 世界背包隔离

按世界/组隔离背包、末影箱、生命值、饥饿值、经验、药水效果等。

### 世界分组

在 `config.yml` 或通过命令创建"世界组"：

```
worlds:
  survival:
    worlds: world,world_nether,world_the_end
  creative:
    worlds: creative_flat
```

效果：survival 组的三个世界共享背包，进入 creative_flat 时背包独立。

### 隔离内容

可配置是否隔离以下内容：
- 背包 (inventory)
- 末影箱 (ender_chest)
- 生命值和饥饿值 (health/hunger)
- 经验值 (experience)
- 药水效果 (potion_effects)
- 经济余额 (economy)
- 游戏模式 (game_mode)
- 床出生点 (bed_spawn)

### 管理命令

| 命令 | 说明 |
|------|------|
| `/mvinv group` | 引导式创建/编辑/删除世界组 |
| `/mvinv create-group <组名> <世界名列表> <共享类型>` | 创建世界组 |
| `/mvinv delete-group <组名>` | 删除世界组 |
| `/mvinv info <组名>` | 查看组配置详情 |
| `/mvinv add-worlds <组名> <世界名>` | 向组中添加世界 |
| `/mvinv add-share <组名> <共享类型>` | 添加共享类型 |
| `/mvinv remove-share <组名> <共享类型>` | 移除共享类型 |
| `/mvinv toggle last_location` | 开关"上次位置"功能 |
| `/mvinv config <属性> <值>` | 修改配置 |
| `/mvinv reload` | 重载配置 |
| `/mvinv migrate <插件名>` | 从其他背包隔离插件迁移数据 |
| `/mvinv playerdata import <世界名>` | 导入原版玩家数据 |

共享类型：`all`（全部）、`inventory`（背包）、`enderchest`（末影箱）、`health`（生命值）、`experience`（经验）、`hunger`（饥饿值）、`potion-effects`（药水效果）、`economy`（经济）、`bed_spawn`（床出生点）

## 常用场景示例

### 创建资源世界
```
/mv create resource normal
/mv modify set alias &a[资源世界] resource
/mv modify set difficulty peaceful resource
```

### 创建空岛世界
```
/mv create skyblock normal -g SkyBlock
/mv modify set alias &b[空岛] skyblock
```

### 设置跨世界传送门
```
/mvp wand → 选区 → /mvp create shop_portal
/mvp modify dest w:shop
/mvp modify fill portal
```

### 禁止某世界 PVP
```
/mv modify set pvp false resource
```

## 注意事项

- 删除世界用 `/mv delete` 会**物理删除**世界文件夹，不可恢复，务必先备份
- 卸载（`/mv unload`）不会删除文件夹，只是从内存中移除
- 世界名区分大小写，建议全部小写并用下划线（如 `resource_world`）
- 导入世界时文件夹必须已存在于服务器根目录（如 `worlds/old_world/`）
- Multiverse-Portals 的传送门区域需要 WorldEdit 配合选区
- 下界传送门映射要在 `bukkit.yml` 中禁用原版下界传送后，再用 `/mvnp link` 接管
- 如果安装了 EssentialsX Spawn，`/spawn` 命令可能被覆盖，注意权限冲突
- 大量世界（10+）会增加服务器内存和 CPU 开销，合理规划
