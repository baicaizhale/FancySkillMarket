---
name: "residence"
description: "Residence 领地管理插件的完整使用指南，涵盖领地创建、权限标志系统、子区域、租赁、管理员命令"
triggers:
  - "residence"
  - "res"
  - "领地"
  - "圈地"
  - "保护"
  - "领地保护"
  - "res create"
  - "res set"
  - "领地权限"
  - "圈地保护"
auto_trigger: true
source: "residence"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "protection"
  - "land"
---

# Residence 领地保护完整指南

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 Residence 插件。

检查方法：尝试执行 `/res version` 命令，如果返回版本信息则说明插件已安装。

如果插件未安装，请告知玩家的建筑和物品可能不受保护，建议安装领地插件。

## 概念说明

- **领地 (Residence)**：玩家拥有的受保护区域
- **子区域 (Subzone)**：领地内部更精细的子区域，继承父领地设置
- **标志 (Flag)**：控制领地内某种行为的开关（如 `build`、`use`、`pvp`）
- **默认标志**：新领地自动生效的默认权限集合

## 选择工具

| 选择方式 | 说明 |
|----------|------|
| 木锄 (Wooden Hoe) | 默认选择工具（左键=pos1，右键=pos2） |
| 木斧 (Wooden Axe) | 可选选择工具（在 config 中开启） |
| `/res select` | 查看当前选择区域信息 |
| `/res select size` | 查看选区大小和开销 |
| `/res select vert` | 将选区垂直扩展到天空和基岩 |
| `/res select chunk` | 选区对齐到区块边界 |
| `/res select expand <数量>` | 向上扩展选区 |
| `/res select worldedit` | 将 WorldEdit 选区同步为 Residence 选区 |

## 领地管理

### 基础操作

| 命令 | 说明 |
|------|------|
| `/res create <领地名>` | 创建新领地（先用选择工具选好区域） |
| `/res remove <领地名>` | 删除己方领地 |
| `/res confirm` | 确认危险操作 |
| `/res info [领地名]` | 查看领地详细信息（所有者、大小、标志等） |
| `/res list [玩家]` | 列出自己（或他人）的全部领地 |
| `/res listall [页码]` | 列出服务器全部领地 |
| `/res tp <领地名>` | 传送到领地（需要领地允许 `teleport`） |
| `/res current` | 查看当前所在领地 |

### 领地修改

| 命令 | 说明 |
|------|------|
| `/res rename <旧名> <新名>` | 重命名领地 |
| `/res expand <数量>` | 向所朝方向扩展领地 N 格 |
| `/res contract <数量>` | 向所朝方向缩小领地 N 格 |
| `/res give <领地名> <玩家>` | 转让领地所有权 |
| `/res mirror <源领地> <目标领地>` | 镜像复制领地标志设置 |
| `/res auto <方块数>` | 自动扩选区域创建领地（以脚下为中心） |

### 工具与辅助

| 命令 | 说明 |
|------|------|
| `/res compass <领地名>` | 将指南针指向领地 |
| `/res unstuck` | 卡出领地（传送至最近的安全位置） |
| `/res rt [世界] [玩家]` | 随机传送（在领地中随机传送） |
| `/res kick <玩家>` | 将玩家踢出领地 |

### 领地消息

| 命令 | 说明 |
|------|------|
| `/res message enter <消息>` | 设置进入领地时的欢迎消息 |
| `/res message leave <消息>` | 设置离开领地时的告别消息 |
| `/res message remove enter` | 移除进入消息 |
| `/res message remove leave` | 移除离开消息 |

### 领地聊天

| 命令 | 说明 |
|------|------|
| `/res rc [领地名]` | 加入领地聊天频道 |
| `/res rc leave` | 退出领地聊天 |
| `/res rc setcolor <颜色代码>` | 设置聊天颜色 |
| `/res rc setprefix <前缀>` | 设置聊天前缀 |

## 标志系统 (Flags)

领地标志控制各种行为在领地内是否允许。

### 标志设置命令

| 命令 | 说明 |
|------|------|
| `/res set <领地名> <标志> true/false/remove` | 设置领地标志 |
| `/res pset <领地名> <玩家> <标志> true/false/remove` | 为特定玩家设置标志 |
| `/res gset <领地名> <组名> <标志> true/false/remove` | 为权限组设置标志 |
| `/res flags` | 查看所有可用标志列表 |
| `/res flags <领地名>` | 查看领地的标志状态 |
| `/res check <领地名> <标志> [玩家]` | 检查某玩家在某领地的标志值 |
| `/res reset [领地名\|all]` | 重置领地标志为默认值 |
| `/res clearflags` | 清除所有自定义标志 |
| `/res lset <领地名> <blacklist\|ignorelist> <材质>` | 设置方块黑名单/忽略名单 |

### 建筑与破坏类

| 标志 | 说明 |
|------|------|
| `build` | 放置方块 |
| `destroy` | 破坏方块 |
| `place` | 放置方块（与 build 相同） |
| `break` | 破坏方块（与 destroy 相同） |

### 交互类

| 标志 | 说明 |
|------|------|
| `use` | 使用门、拉杆、按钮、音符盒等 |
| `container` | 打开箱子、熔炉、漏斗、发射器等容器 |
| `craft` | 使用工作台 |
| `enchant` | 使用附魔台 |
| `brew` | 使用酿造台 |
| `anvil` | 使用铁砧 |
| `beacon` | 使用信标 |
| `furnace` | 使用熔炉 |
| `trapdoor` | 使用活板门 |
| `pressure` | 使用压力板 |
| `button` | 使用按钮 |
| `door` | 使用门 |
| `lever` | 使用拉杆 |
| `diode` | 使用红石中继器/比较器 |
| `redstone` | 红石信号传播 |
| `note` | 使用音符盒 |
| `cake` | 吃蛋糕 |
| `itempickup` | 捡起掉落物 |
| `itemdrop` | 丢弃物品 |
| `trade` | 与村民交易 |
| `shear` | 剪羊毛 |
| `hook` | 使用钓鱼竿 |
| `vehicle` | 放置/使用载具（矿车、船） |
| `vehicleDestroy` | 破坏载具 |
| `backup` | 骑乘动物 |
| `egg` | 投掷鸡蛋 |
| `enderpearl` | 使用末影珍珠 |
| `chorusfruit` | 食用紫颂果传送 |

### 战斗与伤害类

| 标志 | 说明 |
|------|------|
| `pvp` | 玩家间战斗 |
| `damage` | 所有类型伤害（包含以下所有） |
| `falldamage` | 摔落伤害 |
| `explosion` | 爆炸伤害（TNT/苦力怕/床/水晶） |
| `tnt` | TNT 爆炸 |
| `creeper` | 苦力怕爆炸 |
| `fireball` | 火球伤害（恶魂、烈焰人） |
| `witherdamage` | 凋零伤害 |
| `lavadestroy` | 岩浆破坏方块 |
| `firedestroy` | 火焰破坏方块 |
| `mobkilling` | 击杀生物 |
| `monsterkilling` | 击杀怪物 |
| `animalkilling` | 击杀动物 |

### 环境与自然类

| 标志 | 说明 |
|------|------|
| `fire` | 火焰蔓延 |
| `firespread` | 火焰传播 |
| `flow` | 液体流动 |
| `waterflow` | 水流 |
| `lavaflow` | 岩浆流 |
| `snowfall` | 积雪 |
| `iceform` | 结冰 |
| `ice` | 冰融化/形成 |
| `growth` | 植物生长 |
| `withering` | 凋零玫瑰造成伤害 |
| `decay` | 树叶腐烂 |
| `spread` | 草/菌丝蔓延 |
| `nodurability` | 物品不掉耐久 |
| `healing` | 自动恢复生命 |
| `keepinv` | 死亡保留物品栏 |
| `keepexp` | 死亡保留经验值 |

### 生物与环境

| 标志 | 说明 |
|------|------|
| `mobspawn` | 生物生成 |
| `animalspawn` | 动物生成 |
| `monsterspawn` | 怪物生成 |
| `animals` | 动物存在/生成 |
| `monsters` | 怪物存在/生成 |
| `nomobs` | 阻止生物进入领地 |
| `animaltrample` | 动物踩踏耕地 |
| `trample` | 踩踏耕地 |
| `villagertrade` | 村民交易 |

### 传送与移动类

| 标志 | 说明 |
|------|------|
| `move` | 移动（设为 false 则无法进入） |
| `teleport` | 传送进入/离开 |
| `command` | 执行命令 |
| `command_<命令名>` | 执行特定命令 |
| `hidden` | 隐藏领地（不在 `/res list` 中显示） |
| `ignite` | 使用打火石点火 |
| `leash` | 使用牵引绳 |
| `piston` | 活塞推动 |
| `nofly` | 禁止飞行 |
| `respawn` | 死后自动在领地内重生 |

| `feed` | 自动恢复饱食度 |
| `hotfloor` | 岩浆块伤害 |

### 经济类

| 标志 | 说明 |
|------|------|
| `bank` | 领地银行存款 |
| `buy` | 允许购买该领地 |
| `sell` | 领地出售状态 |

## 子区域 (Subzone)

在领地内部创建更精细的子区域，每个子区域可独立设置标志。

| 命令 | 说明 |
|------|------|
| `/res subzone create <领地名> <子区域名>` | 在主领地内创建子区域 |
| `/res subzone remove <领地名> <子区域名>` | 删除子区域 |
| `/res subzone list <领地>` | 列出领地内所有子区域 |
| `/res subzone info <领地名> <子区域名>` | 查看子区域信息 |

子区域的标志设置与主领地相同：`/res pset <领地名>.<子区域名> <玩家> <标志> true`

## 租赁与市场

| 命令 | 说明 |
|------|------|
| `/res market` | 查看领地市场列表 |
| `/res market info` | 查看市场详细状态 |
| `/res market sell <价格>` | 将当前领地挂牌出售 |
| `/res market unsell` | 取消出售 |
| `/res rent <领地名> <天数>` | 租赁领地 |
| `/res rent release` | 释放租赁的领地 |
| `/res rent info` | 查看租赁状态 |
| `/res bank deposit <金额>` | 向领地银行存钱 |
| `/res bank withdraw <金额>` | 从领地银行取钱 |

## 默认组标志

管理员可在 `groups.yml` 或通过命令设置不同玩家组的默认领地标志（新手/VIP/MVP 等自动获得不同权限）。

## 管理员命令

| 命令 | 说明 |
|------|------|
| `/resadmin` | 查看管理命令列表 |
| `/resadmin remove <领地名>` | 强制删除任意领地 |
| `/resadmin setowner <领地名> <玩家>` | 强制变更领地所有者 |
| `/resadmin reload` | 重载 Residence 配置 |
| `/resadmin lease set <天数>` | 设置领地最大租期 |
| `/resadmin lease renewcost <金额>` | 设置续费价格 |
| `/resadmin clearworld` | 清除世界所有领地（危险操作） |
| `/resadmin check` | 检查领地数据完整性 |
| `/resadmin server <领地名>` | 将领地设为服务器所有（不受玩家权限影响） |
| `/resadmin resclass <类型> add <领地名>` | 将领地加入特殊分类 |
| `/resadmin flags <玩家>` | 查看玩家的标志权限 |
| `/resadmin listhidden` | 列出所有隐藏领地 |
| `/resadmin reset` | 重置所有领地标志为默认 |

## 实用示例

### 创建安全领地
```
# 用木锄选好区域后
/res create my_home
/res set my_home build false      # 关闭建筑（仅所有者可）
/res set my_home container false  # 关闭容器（仅所有者可）
/res set my_home use true         # 允许使用门/按钮
/res set my_home move true        # 允许进入
/res pset my_home friend_name build true  # 给朋友建筑权限
```

### 创建 PVP 竞技场
```
/res create pvp_arena
/res set pvp_arena pvp true
/res set pvp_arena build false
/res set pvp_arena monsterspawn false
# 进入和离开的消息
/res message pvp_arena enter &c你进入了PVP区域！
/res message pvp_arena leave &a你离开了PVP区域
```

### 租赁商店
```
/res market sell 1000
# 其他玩家可购买
```

## 注意事项

- 领地从 Y=-64 到 Y=320 覆盖整个垂直空间，想创建地下领地需要用子区域
- `false` 表示只对**领地所有者**有效，其他玩家默认不允许；`true` 表示所有人（包括非成员）都可以
- 标志权限优先级：玩家标志 (`/res pset`) > 组标志 (`/res gset`) > 领地标志 (`/res set`) > 默认组标志
- 删除领地时，领地内所有子区域也会被删除
- 选择工具不消耗耐久，即使是木锄也不会损坏
- 领地名不区分大小写，推荐用小写英文
- 领地创建消耗金钱（如经济系统启用），费用在 `config.yml` 中配置（默认按方块数计费）
- 领地有最大数量限制和最大面积限制（可在配置和权限节点中调整）
- 如果想全面禁用爆炸保护（如允许苦力怕炸领地），需同时设置 `creeper`、`tnt`、`explosion` 为合适的值
