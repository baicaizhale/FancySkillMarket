---
name: "placeholderapi"
description: "PlaceholderAPI 变量系统的完整使用指南，涵盖内置变量、主流扩展、条件占位符、数学/关系语法"
triggers:
  - "placeholderapi"
  - "papi"
  - "变量"
  - "占位符"
  - "papi ecloud"
  - "placeholder"
  - "记分板变量"
  - "tab变量"
auto_trigger: true
source: "placeholderapi"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "placeholder"
  - "api"
---

# PlaceholderAPI 变量系统完整指南

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 PlaceholderAPI 插件。

检查方法：尝试执行 `/papi version` 命令，如果返回版本信息则说明插件已安装。

如果插件未安装，请告知玩家需要使用变量替换功能时需安装 PlaceholderAPI。

## 基础命令

### 管理命令

| 命令 | 说明 |
|------|------|
| `/papi version` | 查看 PAPI 版本 |
| `/papi list` | 列出所有已安装的变量扩展 |
| `/papi reload` | 重载插件配置 |
| `/papi info <扩展名>` | 查看扩展详细信息（作者、版本、说明） |
| `/papi dump` | 导出调试信息（用于报告问题） |

### eCloud（扩展云下载）

| 命令 | 说明 |
|------|------|
| `/papi ecloud list [all\|installed\|玩家\|作者]` | 列出云端可用的扩展 |
| `/papi ecloud download <扩展名>` | 下载并安装扩展 |
| `/papi ecloud update <扩展名>` | 更新指定扩展 |
| `/papi ecloud refresh` | 刷新云端扩展列表缓存 |
| `/papi ecloud clear` | 清除扩展下载缓存 |
| `/papi ecloud status` | 查看已安装的扩展更新状态 |
| `/papi ecloud info <扩展名>` | 查看扩展详细信息 |
| `/papi ecloud placeholders <扩展名>` | 查看扩展提供的全部变量 |

### 变量测试

| 命令 | 说明 |
|------|------|
| `/papi parse <玩家> <文本>` | 以指定玩家身份解析变量 |
| `/papi parse me <文本>` | 以自己的身份解析变量 |
| `/papi bcparse <玩家> <文本>` | 解析并广播变量（测试用） |

示例：
```
/papi parse baicaizhale %player_name% 等级 %player_level%
/papi parse me %vault_eco_balance%
```

## 内置变量 (Player 扩展)

Player 扩展默认安装，提供玩家基础信息：

| 变量 | 说明 |
|------|------|
| `%player_name%` | 玩家名 |
| `%player_displayname%` | 显示名称 |
| `%player_uuid%` | UUID |
| `%player_health%` | 当前生命值 |
| `%player_max_health%` | 最大生命值 |
| `%player_health_rounded%` | 生命值取整 |
| `%player_level%` | 等级 |
| `%player_exp%` | 当前经验 |
| `%player_exp_to_level%` | 到下一级所需经验 |
| `%player_total_exp%` | 总经验值 |
| `%player_food_level%` | 饥饿值 |
| `%player_saturation%` | 饱食度 |
| `%player_gamemode%` | 游戏模式 |
| `%player_world%` | 当前世界名 |
| `%player_world_type%` | 世界类型 |
| `%player_biome%` | 当前生物群系 |
| `%player_x%` | X 坐标 |
| `%player_y%` | Y 坐标 |
| `%player_z%` | Z 坐标 |
| `%player_direction%` | 朝向 (N/S/E/W) |
| `%player_yaw%` / `%player_pitch%` | 朝向角度 |
| `%player_ping%` | 网络延迟 |
| `%player_ip%` | IP 地址 |
| `%player_armor_%` | 护甲值 |
| `%player_has_permission_<节点>%` | 是否有某权限（返回 yes/no） |
| `%player_is_op%` | 是否为 OP |
| `%player_is_whitelisted%` | 是否在白名单 |
| `%player_is_flying%` | 是否飞行 |
| `%player_is_sleeping%` | 是否在睡觉 |
| `%player_is_sneaking%` | 是否潜行 |
| `%player_is_god%` | 是否无敌 |
| `%player_is_afk%` | 是否暂离 |
| `%player_item_in_hand%` | 手中物品名 |
| `%player_item_in_hand_name%` | 手中物品显示名 |
| `%player_last_damage%` | 上次受伤值 |
| `%player_last_attacker%` | 上次伤害来源 |
| `%player_last_death_cause%` | 最近死亡原因 |
| `%player_seconds_lived%` | 存活秒数 |
| `%player_minutes_lived%` | 存活分钟数 |

## 内置变量 (Server 扩展)

| 变量 | 说明 |
|------|------|
| `%server_online%` | 在线玩家数 |
| `%server_max_players%` | 最大玩家数 |
| `%server_unique_joins%` | 历史进入总人数 |
| `%server_tps%` | 1分钟平均 TPS |
| `%server_tps_5%` | 5分钟平均 TPS |
| `%server_tps_15%` | 15分钟平均 TPS |
| `%server_uptime%` | 运行时间 |
| `%server_version%` | 服务器版本 |
| `%server_bukkit_version%` | Bukkit 版本 |
| `%server_ram_used%` | 已用内存 (MB) |
| `%server_ram_free%` | 空闲内存 (MB) |
| `%server_ram_total%` | 总内存 (MB) |
| `%server_ram_max%` | 最大内存 (MB) |
| `%server_worlds%` | 加载的世界列表 |

## 常用扩展变量

### Vault 经济

安装 `Vault` 扩展后可用：

| 变量 | 说明 |
|------|------|
| `%vault_eco_balance%` | 玩家余额 |
| `%vault_eco_balance_fixed%` | 余额（格式化，保留两位小数） |
| `%vault_eco_balance_commas%` | 余额（带千位分隔符） |
| `%vault_rank%` | 玩家主权限组 |
| `%vault_prefix%` | 玩家前缀 |
| `%vault_suffix%` | 玩家后缀 |
| `%vault_group%` | 玩家所在组 |

### LuckPerms

安装 `LuckPerms` 扩展后可用：

| 变量 | 说明 |
|------|------|
| `%luckperms_prefix%` | 前缀 |
| `%luckperms_suffix%` | 后缀 |
| `%luckperms_primary_group_name%` | 主组名 |
| `%luckperms_groups%` | 所在组列表 |
| `%luckperms_meta_<键>%` | 获取元数据值 |
| `%luckperms_expiry_time_<权限>%` | 权限到期时间 |
| `%luckperms_has_permission_<节点>%` | 是否有权限 |
| `%luckperms_context_<上下文>%` | 当前上下文值 |

### Essentials / EssentialsX

安装 `Essentials` 扩展后可用：

| 变量 | 说明 |
|------|------|
| `%essentials_balance%` | 余额 |
| `%essentials_nickname%` | 昵称 |
| `%essentials_god%` | 无敌状态 |
| `%essentials_fly%` | 飞行状态 |
| `%essentials_vanished%` | 隐身状态 |
| `%essentials_homes%` | 设家的数量 |
| `%essentials_afk%` | 是否 AFK |
| `%essentials_afk_reason%` | AFK 原因 |
| `%essentials_is_muted%` | 是否被禁言 |
| `%essentials_is_banned%` | 是否被封禁 |
| `%essentials_jailed%` | 是否在监狱中 |
| `%essentials_kit_is_available_<礼包名>%` | 礼包是否可用 |

### mcMMO

安装 `mcMMO` 扩展后可用：

| 变量 | 说明 |
|------|------|
| `%mcmmo_power_level%` | 总等级 |
| `%mcmmo_level_<技能名>%` | 技能等级（如 `mining`、`swords`） |
| `%mcmmo_rank_<技能名>%` | 技能排名 |
| `%mcmmo_party%` | 队伍名 |
| `%mcmmo_party_leader%` | 队长名 |
| `%mcmmo_party_size%` | 队伍人数 |

技能名：`mining`、`excavation`、`woodcutting`、`swords`、`unarmed`、`archery`、`axes`、`taming`、`fishing`、`repair`、`acrobatics`、`alchemy`、`smelting`、`herbalism`、`crossbows`

### WorldGuard

安装 `WorldGuard` 扩展后可用：

| 变量 | 说明 |
|------|------|
| `%worldguard_region_name%` | 当前所在区域名 |
| `%worldguard_regions%` | 区域内玩家列表 |
| `%worldguard_region_owner%` | 区域所有者 |
| `%worldguard_region_members%` | 区域成员列表 |
| `%worldguard_region_type%` | 区域类型 |

### 其他重要扩展

| 扩展名 | 用途 | 关键变量 |
|--------|------|----------|
| `Player` | 内置，玩家信息 | `%player_name%`、`%player_health%` |
| `Server` | 内置，服务器信息 | `%server_online%`、`%server_tps%` |
| `Vault` | 经济/权限 | `%vault_eco_balance%`、`%vault_prefix%` |
| `LuckPerms` | 高级权限 | `%luckperms_prefix%`、`%luckperms_meta_<key>%` |
| `Essentials` | EssentialsX 状态 | `%essentials_nickname%`、`%essentials_afk%` |
| `CMI` | CMI 状态 | `%cmi_user_balance%`、`%cmi_user_nickname%` |
| `PlaceholderAPI-Expansion` | 数学计算 | `%math_<表达式>%` |
| `CheckItem` | 物品检查 | `%checkitem_<条件>%` |
| `Javascript` | 自定义 JS 逻辑 | `%javascript_<脚本>%` |
| `Statistic` | 玩家统计 | `%statistic_<类型>%` |
| `Tab` | TAB 插件 | `%tab_tabprefix%`、`%tab_tabsuffix%` |

## 条件占位符

格式：`%condition_<判断>_<true时输出>_<false时输出>%`

或使用关系占位符比较两个变量：

```
%relational_<变量1> <运算符> <变量2> <true输出> <false输出>%
```

### 数学占位符

```
%math_<表达式>%
```

示例：
- `%math_0_1+2%` → `3`
- `%math_0_{vault_eco_balance}*2%` → 余额的两倍
- `%math_0_{player_level}/2%` → 等级的一半

`%math_<精度>_<表达式>%`，精度为小数位数。

## 应用场景

### Tab 列表自定义

```
# TAB 插件配置示例
tabprefix: "%luckperms_prefix%%player_name%"
tabsuffix: " &7[%player_level%级]"
```

### 计分板 (Scoreboard)

```
# 常见计分板变量组合
%player_name%
%vault_eco_balance%
%mcmmo_power_level%
%server_online% / %server_max_players%
%server_tps%
```

### 聊天格式

```
# EssentialsX Chat 配置示例
format: "%luckperms_prefix%%player_displayname%%luckperms_suffix%&f: %message%"
```

### 物品 Lore

```
# 物品描述中嵌入动态变量
&7持有者: %player_name%
&7等级要求: %player_level% / 30
```

## 注意事项

- 变量区分大小写：`%player_name%` 正确，`%Player_Name%` 错误
- 有些变量在控制台解析时返回空值（如 `%player_*%` 类），需在玩家上下文中使用
- eCloud 下载扩展后需 `/papi reload` 生效
- 部分扩展需要安装对应插件才能正常工作（如 Vault 扩展需要先装 Vault）
- 变量嵌套支持：`%vault_eco_balance%` 可嵌入其他变量中
- TPS 变量在服务器启动初期可能不准（需要收集数据）
- `/papi parse` 是调试利器，遇到变量不显示时优先用它测试
- 部分扩展在 `/papi ecloud` 中的名称可能与插件名不同，使用 `/papi ecloud list` 搜索
