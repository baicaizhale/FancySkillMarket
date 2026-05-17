---
name: "mcmmo"
description: "mcMMO 技能系统的完整使用指南，涵盖全技能机制、队伍系统、管理命令"
triggers:
  - "mcmmo"
  - "技能"
  - "等级"
  - "经验"
  - "mcmmo技能"
  - "挖矿技能"
  - "剑术"
  - "弓箭"
  - "钓鱼技能"
  - "修理"
  - "炼金"
  - "party"
  - "组队"
  - "mctop"
  - "mcstats"
auto_trigger: true
source: "mcmmo"
author: "FancyHelper Team"
version: "1.1.0"
categories:
  - "plugin"
  - "skill"
  - "rpg"
---

# mcMMO 技能系统完整指南

## 插件检查

在使用以下命令前，请先检查服务器是否已安装 mcMMO 插件。

检查方法：尝试执行 `/mcmmo version` 命令，如果返回版本信息则说明插件已安装。

如果插件未安装，请告知玩家无法使用技能系统和等级功能。

## 玩家命令

### 信息查询

| 命令 | 说明 |
|------|------|
| `/mcstats` | 查看自己的全部技能统计和等级 |
| `/mcstats <技能名>` | 查看指定技能的详细数据 |
| `/mctop [技能名]` | 查看技能排行榜（支持分页） |
| `/mctop <技能名> <页码>` | 查看指定技能的排行榜第 N 页 |
| `/inspect <玩家>` | 查看其他玩家的 mcMMO 统计 |
| `/mcrank` | 查看自己的总等级排名 |
| `/mmopower` 或 `/powerlevel` | 查看总等级 (Power Level) |
| `/mcability` | 切换右键触发主动技能的开关 |
| `/mcscoreboard [keep\|clear]` | 管理 mcMMO 计分板 |

### 队伍系统

mcMMO 的 Party 系统支持组队共享经验、队伍聊天和队伍传送。

| 命令 | 说明 |
|------|------|
| `/party` | 查看队伍信息和帮助 |
| `/party create <队伍名>` | 创建队伍 |
| `/party join <玩家>` | 加入指定玩家的队伍 |
| `/party invite <玩家>` | 邀请玩家加入队伍 |
| `/party accept <玩家>` | 接受组队邀请 |
| `/party leave` | 离开当前队伍 |
| `/party kick <玩家>` | 踢出队员（队长专用） |
| `/party disband` | 解散队伍（队长专用） |
| `/party chat` | 切换到队伍聊天模式 |
| `/party password <密码>` | 设置队伍加入密码 |
| `/party lock` | 锁定队伍，禁止自由加入 |
| `/party unlock` | 解锁队伍 |
| `/party owner <玩家>` | 转移队长（队长专用） |
| `/party mode` | 切换经验分配模式（均分/按贡献） |
| `/ptp <玩家>` | 传送到队友身边（需要队伍传送权限） |

队伍经验分享：队员之间距离较近时，经验会共享给附近队友。队伍等级越高，分享范围和比例越大。

## 管理员命令

| 命令 | 说明 |
|------|------|
| `/mmoedit <玩家> <技能> <等级>` | 设置玩家技能等级 |
| `/addxp <玩家> <技能> <数值>` | 给玩家增加技能经验 |
| `/skillreset <玩家> <技能>` | 重置玩家指定技能等级 |
| `/mcrefresh <玩家>` | 刷新玩家的 mcMMO 数据 |
| `/hardcore` | 切换硬核模式惩罚开关 |
| `/vampirism` | 切换吸血模式开关 |
| `/mcnotify` | 切换技能升级通知 |
| `/mmoupdate` | 手动更新 mcMMO 数据 |

## 主动技能（Super Abilities）

每个技能满级后右键/左键触发主动技能，有冷却时间。右键物品触发：

| 技能 | 主动技能 | 效果 |
|------|---------|------|
| 采矿 (Mining) | 超级破坏者 (Super Breaker) | 短时间内极速挖矿，三倍掉落 |
| 挖掘 (Excavation) | 千兆钻孔机 (Giga Drill Breaker) | 短时间内极速挖掘，三倍掉落 |
| 伐木 (Woodcutting) | 树木终结者 (Tree Feller) | 一斧砍倒整棵树 |
| 剑术 (Swords) | 锯齿打击 (Serrated Strikes) | 对目标造成流血伤害 |
| 徒手 (Unarmed) | 狂暴打击 (Berserker) | 徒手攻击力大幅提升，可击碎方块 |
| 斧技 (Axes) | 头颅粉碎者 (Skull Splitter) | 斧头范围伤害 |
| 驯兽 (Taming) | 万兽之王 (Call of the Wild) | 召唤附近动物为你战斗 |
| 草药学 (Herbalism) | 绿拇指 (Green Thumb) | 范围内作物瞬间成熟 |
| 钓鱼 (Fishing) | 渔夫的盛宴 (Fisherman's Feast) | 大幅提升钓鱼速度和稀有度 |
| 修理 (Repair) | 奥秘锻造 (Arcane Forging) | 修理时概率保留附魔 |

## 技能专用命令

在游戏中输入 `/技能名` 可查看该技能的详细数据和描述：

| 命令 | 技能 |
|------|------|
| `/mining` | 采矿 |
| `/excavation` | 挖掘 |
| `/woodcutting` | 伐木 |
| `/swords` | 剑术 |
| `/unarmed` | 徒手 |
| `/archery` | 弓箭 |
| `/axes` | 斧技 |
| `/taming` | 驯兽 |
| `/fishing` | 钓鱼 |
| `/repair` | 修理 |
| `/acrobatics` | 杂技 |
| `/alchemy` | 炼金 |
| `/smelting` | 冶炼 |
| `/herbalism` | 草药学 |
| `/crossbows` | 弩技 |
| `/tridents` | 三叉戟 |
| `/salvage` | 回收分解 |

## 技能详解

### 采矿 (Mining)
挖石头和矿物提升等级。
- **主动技能**：Super Breaker（右键镐子触发）
- **被动效果**：随等级提升，挖矿有概率双倍掉落（Double Drops）
- **爆炸采矿 (Blast Mining)**：用 TNT 炸矿也能获得经验，且矿物不会被炸毁

### 挖掘 (Excavation)
挖泥土、沙子、沙砾、黏土等软质方块提升等级。
- **主动技能**：Giga Drill Breaker
- **被动效果**：挖掘有概率掉落宝藏（钻石、火药、萤石粉等）

### 伐木 (Woodcutting)
砍伐原木提升等级。
- **主动技能**：Tree Feller（右键斧头触发，一斧砍倒整棵树）
- **被动效果**：随等级提升，砍树有概率双倍掉落原木
- **注意**：Tree Feller 会对斧头造成额外耐久消耗

### 剑术 (Swords)
用剑攻击实体提升等级。
- **主动技能**：Serrated Strikes（右键剑触发，造成流血 DoT）
- **被动效果**：
  - **流血 (Bleed)**：攻击有概率造成额外持续伤害
  - **反击 (Counter Attack)**：被攻击时有概率反弹伤害

### 徒手 (Unarmed)
空手攻击实体提升等级。
- **主动技能**：Berserker
- **被动效果**：
  - **铁拳 (Iron Arm)**：随等级提升徒手攻击力
  - **缴械 (Disarm)**：攻击有概率打掉对手手中物品
  - **箭矢偏折 (Arrow Deflect)**：有概率弹开飞来的箭矢

### 弓箭 (Archery)
用弓箭射中实体提升等级。
- **主动技能**：无
- **被动效果**：
  - **眩晕 (Daze)**：射中对手有概率造成迷惑效果
  - **箭矢回收 (Arrow Retrieval)**：有概率回收射出的箭矢
  - **追踪箭 (Tracking Arrow)**：在 PvP 中射出的箭会自动微调轨迹

### 斧技 (Axes)
用斧头攻击实体提升等级。与剑术不同，斧技侧重范围伤害。
- **主动技能**：Skull Splitter
- **被动效果**：
  - **致命一击 (Critical Strikes)**：攻击有概率造成暴击
  - **斧头精通 (Axe Mastery)**：随等级提升斧头伤害
  - **破甲 (Armor Impact)**：攻击有概率造成额外护甲耐久损耗

### 驯兽 (Taming)
驯服狼、猫、马、鹦鹉等动物提升等级。
- **主动技能**：Call of the Wild
- **被动效果**：
  - **野兽学识 (Beast Lore)**：右键动物查看其属性
  - **环境感知 (Environmentally Aware)**：驯服的狼/猫受伤时自动传送到你身边
  - **猎手的敏锐 (Hunter's Insight)**：驯服的动物攻击力随等级提升

### 钓鱼 (Fishing)
钓鱼提升等级。
- **主动技能**：Fisherman's Feast
- **被动效果**：
  - **宝藏猎人 (Treasure Hunter)**：钓鱼有概率钓到稀有物品（附魔书、鞍、命名牌等）
  - **摇晃 (Shake)**：钓鱼时晃动鱼竿吸引鱼群

### 修理 (Repair)
用铁块或钻石块在铁砧上修理物品提升等级。
- **主动技能**：Arcane Forging
- **被动效果**：
  - **奥秘锻造 (Arcane Forging)**：修理时概率保留附魔
  - **回收 (Salvage)**：可拆解物品回收部分材料
  - **修理精通 (Repair Mastery)**：随等级提升修理效率

### 杂技 (Acrobatics)
从高处跳下或翻滚落地提升等级。
- **主动技能**：无
- **被动效果**：
  - **翻滚 (Roll)**：落地时潜行可以翻滚减伤
  - **优雅落地 (Graceful Roll)**：随等级提升摔落伤害减免
  - **闪避 (Dodge)**：战斗中有概率闪避攻击

### 炼金 (Alchemy)
酿造药水提升等级。
- **主动技能**：无
- **被动效果**：
  - **催化 (Catalysis)**：酿造速度随等级提升
  - **混合 (Concoctions)**：药水效果持续时间自动延长

### 冶炼 (Smelting)
熔炼物品提升等级。
- **主动技能**：无
- **被动效果**：
  - **燃料效率 (Fuel Efficiency)**：熔炼时燃料消耗降低
  - **二次熔炼 (Second Smelt)**：有概率同时产出两份成品

### 草药学 (Herbalism)
收获作物和植物提升等级。
- **主动技能**：Green Thumb
- **被动效果**：
  - **农夫的自豪 (Farmer's Diet)**：吃食物回复更多饥饿值
  - **海拉的丰收 (Hylian Luck)**：挖掘特定方块有概率掉落稀有种子
  - **双倍作物 (Double Drops)**：收获作物有概率双倍掉落

### 弩技 (Crossbows)
用弩射击提升等级（1.14+ 新增技能）。
- **主动技能**：无
- **被动效果**：
  - **戏法射击 (Trick Shot)**：弩射击有概率穿透多个目标
  - **近距射击 (Point Blank)**：近距离射击额外伤害

## 经验与等级

- 每个技能最高等级默认 10,000 级（Standard 模式满级 1,000，之后为"终局"阶段）
- 等级超过 1,000 后可解锁终局子技能（如 Mining 的 Mother Lode 三倍掉落、Woodcutting 的 Clean Cuts、Herbalism 的 Verdant Bounty）
- 升级获得"总等级"（Power Level），用于 `/mctop` 排名
- 技能等级越高，被动效果触发概率越高
- 硬核模式下，死亡会清空技能数据（具体看配置）

## 注意事项

- 主动技能默认右键对应工具触发，可通过 `/mcability` 切换开关
- 部分技能在 PvP 中表现不同，如 Serrated Strikes 对玩家伤害降低
- 队伍经验分享需要队员在 75 格范围内
- 方块破坏的经验获取受 WorldGuard/Residence 等领地插件影响，无权限时无法获得经验
- mcMMO 支持 MySQL 数据库存储，大服建议开启以提升性能
- `/mmoedit` 修改等级后，玩家可能需要重新登录才能看到变化
- 爆炸采矿 (Blast Mining) 需要挖掘等级 ≥ 125 且在 TNT 附近潜行右键
