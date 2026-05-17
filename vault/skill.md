---
name: "vault"
description: "Vault 经济/权限/聊天 API 插件的完整指南，涵盖后端选择、命令、故障排查"
triggers:
  - "vault"
  - "经济"
  - "money"
  - "balance"
  - "支付"
  - "eco"
  - "baltop"
  - "pay"
auto_trigger: true
source: "vault"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "economy"
  - "api"
---

# Vault 经济/权限/聊天 API 插件

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 Vault 插件。

检查方法：尝试执行 `/vault info` 命令，如果返回插件信息则说明已安装。

如果插件未安装，请告知玩家无法使用经济系统功能，需要安装 Vault 及配合的经济插件。

## 说明

Vault 本身是一个**三层抽象 API**，不直接提供任何面向玩家的命令，而是为其他插件提供统一的经济、权限、聊天接口：

- **经济 API**：余额、转账、排行榜等
- **权限 API**：权限检查、组查询等
- **聊天 API**：前缀、后缀、聊天格式等

其他插件通过 Vault 的 API 调用功能，无需关心后端具体是什么插件。

## Vault 自身命令

| 命令 | 说明 |
|------|------|
| `/vault info` | 查看已挂载的经济、权限、聊天后端插件信息 |
| `/vault convert <类型> <源插件> <目标插件>` | 在不同经济/权限插件间迁移数据 |

## 权限节点

| 权限 | 说明 |
|------|------|
| `vault.admin` | 允许使用 Vault 信息和转换命令 |

## 经济 API

### 常用经济后端插件

| 插件 | 特点 |
|------|------|
| **EssentialsX Economy** | 最常见的搭配，稳定可靠 |
| **CMI Economy** | CMI 内置的经济模块 |
| **iConomy** | 老牌经济插件，Vault 原生支持 |
| **BOSEconomy** | 轻量级经济插件 |
| **TheNewEconomy** (TNE) | 功能丰富的现代经济插件 |
| **GemsEconomy** | 基于物品（宝石）的经济 |

### 面向玩家的经济命令

经济命令实际由经济后端插件提供，但命令格式通常兼容：

| 命令 | 说明 |
|------|------|
| `/money` 或 `/balance` | 查看自己的余额 |
| `/money [玩家]` | 查看指定玩家的余额 |
| `/pay <玩家> <金额>` | 转账给其他玩家 |
| `/baltop [页码]` | 查看财富排行榜 |

### 管理员经济命令

| 命令 | 说明 |
|------|------|
| `/eco give <玩家> <金额>` | 给予金钱 |
| `/eco take <玩家> <金额>` | 扣除金钱 |
| `/eco set <玩家> <金额>` | 设置金钱 |
| `/eco reset <玩家>` | 重置为初始金额 |
| `/eco reload` | 重载经济配置 |

### 常见经济权限节点

```
essentials.eco              — 基础经济访问
essentials.eco.loan         — 允许负债（余额可为负）
essentials.pay              — 允许转账
essentials.balancetop       — 查看排行榜
essentials.eco.signs.use    — 使用牌商店交易
```

## 权限 API

Vault 权限 API 为插件提供统一的权限检查接口。

### 常用权限后端插件

| 插件 | 特点 |
|------|------|
| **LuckPerms** | 最推荐的现代权限插件 |
| **PermissionsEx** (PEX) | 老牌权限管理 |
| **GroupManager** | EssentialsX 常用搭配，已停止更新 |
| **bPermissions** | 轻量级权限管理 |
| **PowerfulPerms** | 功能丰富 |

### 权限迁移

```
# 从 GroupManager 迁移到 LuckPerms
/vault convert permissions groupmanager luckperms
```

## 聊天 API

Vault 聊天 API 为聊天插件提供前缀/后缀/组名等信息。

### 常用聊天后端插件

| 插件 | 特点 |
|------|------|
| **EssentialsX Chat** | 基础聊天格式 |
| **CMI Chat** | CMI 内置的聊天模块 |
| **TownyChat** | Towny 配套聊天插件 |
| **Herochat** | 多频道聊天系统 |
| **LunaChat** | 支持代理端的跨服聊天 |

### 聊天 API 提供的功能

- 获取玩家前缀（prefix）、后缀（suffix）
- 获取玩家所在组名
- 获取组前缀/后缀
- 获取玩家昵称/显示名

大多数服务器使用 LuckPerms 的 meta 功能设置 prefix/suffix，然后由聊天插件（如 EssentialsX Chat）通过 Vault 读取并格式化显示。

## 典型搭配推荐

| 场景 | 组合 |
|------|------|
| **最简方案** | Vault + EssentialsX Economy + LuckPerms |
| **全功能方案** | Vault + CMI Economy + LuckPerms |
| **纯经济** | Vault + TheNewEconomy + LuckPerms |
| **RPG 服务器** | Vault + GemsEconomy + LuckPerms |

## 故障排查

### /money 提示"无经济插件"

说明 Vault 没有挂载到经济后端。检查：
1. 是否安装了经济后端插件（如 EssentialsX、CMI）
2. 重启服务器或 `/ess reload`
3. 执行 `/vault info` 确认经济后端是否列出

### 转账失败

常见原因：
- 发送方余额不足
- 接收方被 `/paytoggle` 阻止
- 金额输入格式错误（只支持数字，不支持科学计数法）
- 发送方缺少 `essentials.pay` 权限

### 经济数据丢失

- 经济数据通常存储在插件各自的数据库中（如 EssentialsX 的 `userdata/`）
- Vault 本身不存储数据，数据在后端插件中
- 如果更换经济后端，需用 `/vault convert` 迁移数据

## 注意事项

- Vault **必须**配合其他插件使用，单独安装无任何作用
- 更换经济/权限后端时，务必先用 `/vault convert` 迁移数据，否则玩家数据丢失
- Vault 不支持同时挂载多个同类后端（如两个经济插件），会冲突
- EssentialsX 和 CMI 只能装一个作为经济后端，两者不兼容
- 开发者为插件选择经济接口时，优先使用 Vault API 而非直接依赖某个经济插件
