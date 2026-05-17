---
name: "luckperms"
description: "LuckPerms 权限管理插件的完整使用指南，涵盖用户/组管理、上下文、元数据、网页编辑器"
triggers:
  - "luckperms"
  - "lp"
  - "权限"
  - "permission"
  - "权限组"
  - "权限管理"
  - "lp editor"
  - "前缀"
  - "后缀"
auto_trigger: true
source: "luckperms"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "permission"
  - "admin"
---

# LuckPerms 权限管理完整指南

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 LuckPerms 插件。

检查方法：尝试执行 `/lp version` 命令，如果返回版本信息则说明插件已安装。

如果插件未安装，请告知玩家使用 Minecraft 原版命令（如 `/op`、`/deop`、`/ban`）来管理权限。

## 核心概念

LuckPerms 的权限模型：
- **用户 (User)**：每个玩家对应一个 User 对象
- **组 (Group)**：预设的权限集合，用户通过继承组获得权限
- **权限 (Permission)**：具体的一条权限节点，值为 `true`（允许）或 `false`（拒绝）
- **继承 (Inheritance)**：组可以继承其他组，用户也可以继承组
- **上下文 (Context)**：在不同世界/服务器/条件下拥有不同权限
- **元数据 (Meta)**：前缀、后缀、权重等附加属性

## 用户管理

### 基础操作

| 命令 | 说明 |
|------|------|
| `/lp user <玩家> info` | 查看玩家全部权限、组、元数据 |
| `/lp user <玩家> permission set <节点> true` | 授予权限 |
| `/lp user <玩家> permission set <节点> false` | 拒绝权限（覆盖组的允许） |
| `/lp user <玩家> permission unset <节点>` | 移除权限设置 |
| `/lp user <玩家> permission clear` | 清除玩家所有权限 |
| `/lp user <玩家> permission check <节点>` | 检查玩家是否拥有某权限 |
| `/lp user <玩家> permission info` | 列出玩家全部直接设置的权限 |

### 组操作

| 命令 | 说明 |
|------|------|
| `/lp user <玩家> parent add <组名>` | 将玩家加入权限组 |
| `/lp user <玩家> parent remove <组名>` | 将玩家移出权限组 |
| `/lp user <玩家> parent set <组名>` | 设置玩家唯一主组（替换所有现有组） |
| `/lp user <玩家> parent settrack <路线> <组名>` | 沿晋升路线设置玩家组 |
| `/lp user <玩家> parent info` | 查看玩家继承的组 |
| `/lp user <玩家> parent cleartrack <路线>` | 清除晋升路线 |

### 临时权限

| 命令 | 说明 |
|------|------|
| `/lp user <玩家> permission settemp <节点> true <时长>` | 临时授予权限 |
| `/lp user <玩家> parent addtemp <组名> <时长>` | 临时加入权限组 |

时长格式示例：`7d`（7天）、`30m`（30分钟）、`2h30m`（2小时30分钟）、`1w2d`（1周2天）。

## 权限组管理

### 基础操作

| 命令 | 说明 |
|------|------|
| `/lp creategroup <组名>` | 创建新权限组 |
| `/lp deletegroup <组名>` | 删除权限组 |
| `/lp listgroups` | 列出所有权限组 |
| `/lp group <组名> info` | 查看组详情（权限、继承、元数据） |
| `/lp group <组名> rename <新名称>` | 重命名权限组 |

### 组权限

| 命令 | 说明 |
|------|------|
| `/lp group <组名> permission set <节点> true` | 为组设置权限 |
| `/lp group <组名> permission unset <节点>` | 移除组权限 |
| `/lp group <组名> permission clear` | 清除组全部权限 |
| `/lp group <组名> permission info` | 列出组的直接权限 |

### 组继承

| 命令 | 说明 |
|------|------|
| `/lp group <组名> parent add <父组>` | 设置继承关系（子组继承父组权限） |
| `/lp group <组名> parent remove <父组>` | 移除继承 |
| `/lp group <组名> parent set <父组>` | 设置唯一父组 |
| `/lp group <组名> parent info` | 查看继承关系 |

典型继承链：`default` → `vip` → `mvp` → `admin`（高层级继承低层级的所有权限）

### 权重与显示

| 命令 | 说明 |
|------|------|
| `/lp group <组名> setweight <数值>` | 设置组权重（数字越大优先级越高） |

权重用于决定多组冲突时的优先级，以及 tab 列表中组的显示顺序。

## 元数据 (Meta)

元数据是附加在用户/组上的键值对，常用于前缀、后缀、昵称等。

| 命令 | 说明 |
|------|------|
| `/lp user <玩家> meta set <键> <值>` | 为用户设置元数据 |
| `/lp user <玩家> meta unset <键>` | 移除用户元数据 |
| `/lp user <玩家> meta clear` | 清除用户所有元数据 |
| `/lp user <玩家> meta info` | 查看用户元数据 |
| `/lp group <组名> meta set <键> <值>` | 为组设置元数据 |
| `/lp group <组名> meta unset <键>` | 移除组元数据 |

常用元数据键（配合聊天插件使用）：
- `prefix` — 前缀（如 `&b[VIP] `）
- `suffix` — 后缀（如 ` &7[新人]`）
- `username` — 自定义显示名称
- `name-color` — 名称颜色
- `chat-color` — 聊天文字颜色

## 上下文 (Context)

上下文允许在不同条件（世界、服务器、游戏模式）下拥有不同权限。

| 命令 | 说明 |
|------|------|
| `/lp user <玩家> permission set <节点> true context=world:<世界名>` | 仅在指定世界生效的权限 |
| `/lp user <玩家> permission set <节点> true context=server:<服务器名>` | 仅在指定服务器生效的权限 |
| `/lp user <玩家> parent add <组名> context=world:<世界名>` | 仅在指定世界的组 |

常见上下文类型：
- `world=<世界名>` — 特定世界（如 `world=nether`）
- `server=<服务器名>` — 多服务器网络下特定服务端
- `world-type=<nether\|the_end\|overworld>` — 世界类型
- `gamemode=<survival\|creative\|adventure\|spectator>` — 游戏模式

支持组合上下文：`context=world:nether+server:lobby`

## 晋升路线 (Tracks)

晋升路线定义了组之间的线性升级路径。

| 命令 | 说明 |
|------|------|
| `/lp createtrack <路线名>` | 创建晋升路线 |
| `/lp track <路线名> append <组名>` | 在路线末尾添加组 |
| `/lp track <路线名> info` | 查看路线详情 |
| `/lp listtracks` | 列出所有路线 |
| `/lp user <玩家> promote <路线名>` | 沿路线晋升玩家（下一级组） |
| `/lp user <玩家> demote <路线名>` | 沿路线降级玩家（上一级组） |

常见路线示例：`default → vip → mvp → elite → champion`

## 网页编辑器

网页编辑器是管理权限最推荐的方式，提供可视化界面。

| 命令 | 说明 |
|------|------|
| `/lp editor` | 生成一个临时的网页编辑器链接 |

执行后在浏览器打开链接，编辑完成后点击保存按钮，更改会自动同步到服务器。链接为一次性使用，有效时间通常为 10 分钟。

**注意**：网页编辑器生成的是临时链接，不要分享给不可信的人。编辑完成后务必点击"Apply"保存。

## 调试与查询

| 命令 | 说明 |
|------|------|
| `/lp verbose on` | 开启权限详细日志（所有权限检查都会输出） |
| `/lp verbose off` | 关闭详细日志 |
| `/lp verbose record` | 记录详细日志到文件 |
| `/lp verbose upload` | 上传日志到网站供分析 |
| `/lp search <权限节点>` | 搜索谁拥有某权限 |
| `/lp user <玩家> permission check <节点>` | 检查玩家是否拥有某权限 |
| `/lp tree <范围>` | 以树状图查看权限结构 |
| `/lp log recent` | 查看最近的权限变更日志 |
| `/lp log search <关键词>` | 搜索权限日志 |

## 高级管理

### 数据操作

| 命令 | 说明 |
|------|------|
| `/lp export <文件名>` | 导出全部权限数据为 JSON |
| `/lp import <文件名>` | 从 JSON 导入权限数据 |
| `/lp apply <文件名>` | 批量应用权限设置（不清除现有） |
| `/lp bulkupdate` | 批量更新操作（如给所有 VIP 组添加某权限） |

### 同步

| 命令 | 说明 |
|------|------|
| `/lp sync` | 强制从存储后端同步数据 |
| `/lp networksync` | 在多服务端网络中同步权限变更 |

### 通用管理

| 命令 | 说明 |
|------|------|
| `/lp reloadconfig` | 重新加载插件配置文件（不影响权限数据） |
| `/lp info` | 查看插件版本和存储后端信息 |
| `/lp debug` | 导出调试信息 |
| `/lp creategroup <组名>` | 创建新组 |
| `/lp deletegroup <组名>` | 删除组 |
| `/lp clonegroup <源组> <新组>` | 克隆组 |

## 批量操作示例

```
# 批量更新：为所有包含 "vip" 的组添加 fly 权限
/lp bulkupdate group permission set essentials.fly true group.meta."group-name" ~~ "vip"

# 批量删除：移除 default 组的 build 权限
/lp bulkupdate group permission unset essentials.build group.meta."group-name" ~~ "default"
```

## 存储后端

LuckPerms 支持多种存储方式，配置在 `config.yml` 中：

| 后端 | 适用场景 |
|------|----------|
| **H2**（默认） | 小服、单机服，无需额外配置 |
| **MySQL** | 中等规模、需要远程访问数据 |
| **MariaDB** | MySQL 的替代，兼容 MySQL 语法 |
| **PostgreSQL** | 大型网络、高并发 |
| **MongoDB** | 非关系型数据需求 |
| **YAML/JSON** | 极简场景，不推荐生产使用 |

大服和多服务端网络建议使用 MySQL/MariaDB，所有服务器共用同一数据库即可实现权限同步。

## 注意事项

- **权限优先级**：直接设置的权限 > 继承组的权限；`false` > `true`；较高权重组 > 较低权重组
- 使用 `/lp editor` 是最推荐的管理方式，避免命令输错
- 修改权限后通常立即生效，无需 `/lp reloadconfig` 或 `/lp sync`
- `/lp reloadconfig` 仅重载配置文件（如存储设置），不重载权限数据本身，数据同步用 `/lp sync`
- 临时权限到期后自动清除，不需要手动操作
- 批量操作前建议先用 `/lp export` 备份数据
- 权限节点区分大小写，请严格按照插件文档中的节点名称
- 常见权限通配符：`essentials.*`（所有 Essentials 权限）、`*`（所有权限，通常仅给管理员）
