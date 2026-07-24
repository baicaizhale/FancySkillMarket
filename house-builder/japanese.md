# 日式风格房屋建造指南

## 核心铁律

1. **必须围合**：四面必须有墙，不能透风。墙高至少4格，留门（宽1高2）和窗（宽2高1）。
2. **必须落地**：地基必须连接到地面。如果玩家浮空，用支柱（至少4根）从地板连接到地面。
3. **屋顶必须对称**：左右前后必须一致，不能一边翘一边塌。
4. **先主体后装饰**：没有完整的墙和屋顶，禁止建庭院、走廊、装饰。

---

## 建筑类型识别

玩家说"日式房屋" → 默认建造 **9×11 主屋**（完整版，不是亭子）

结构必须是：
```
        ┌─────────────────┐
        │    大屋顶（挑出墙面2格）   │
        │  ┌─────────────┐  │
        │  │             │  │
        │  │   室内空间   │  │  ← 四面有墙，不能透风
        │  │  (有地板)    │  │
        │  │             │  │
        │  └─────────────┘  │
        │    ↑ 外廊（可选）   │
        └─────────────────┘
              ↓
           地基（落地）
```

---

## 第一步：获取玩家坐标

```
/data get entity <玩家名> Pos
```

拿到 `(px, py, pz)`，所有坐标从这里推导。

### 建筑基准点

| 项目 | 公式 | 说明 |
|------|------|------|
| 建筑中心X | `cx = px` | 与玩家同X |
| 建筑中心Y | `cy = py` | 玩家脚下（地基从这里开始） |
| 建筑中心Z | `cz = pz + 5` | 玩家前方5格 |
| 朝向 | 玩家面朝方向为Z+ | 正面朝玩家前方 |

**主体尺寸**：长9（X方向）× 宽11（Z方向）× 高5（Y方向，从地基到屋顶底部）

---

## 第二步：地基（必须落地）

```
# 地基边框（云杉原木，围一圈，高2格，必须落地）
/fill (cx-4, cy, cz-5) (cx+4, cy+1, cz+5) spruce_log

# 地基内部填充（云杉木板，作为室内地板）
/fill (cx-3, cy+1, cz-4) (cx+3, cy+1, cz+4) spruce_planks
```

**自检**：地基是否从地面开始？是。地板是否在Y+1？是。

---

## 第三步：立柱（四角+中间，必须通到地板）

```
# 四角立柱（从地板通到屋顶底部，高4格）
/fill (cx-4, cy+1, cz-5) (cx-4, cy+4, cz-5) spruce_log
/fill (cx+4, cy+1, cz-5) (cx+4, cy+4, cz-5) spruce_log
/fill (cx-4, cy+1, cz+5) (cx-4, cy+4, cz+5) spruce_log
/fill (cx+4, cy+1, cz+5) (cx+4, cy+4, cz+5) spruce_log

# 正面中间立柱（门两侧）
/fill (cx-1, cy+1, cz+5) (cx-1, cy+4, cz+5) spruce_log
/fill (cx+1, cy+1, cz+5) (cx+1, cy+4, cz+5) spruce_log
```

**自检**：柱子是否从地板开始？是。是否到屋顶高度？是。

---

## 第四步：墙壁（四面围合，这是关键！）

### 4.1 正面墙（朝南，留大门）

```
# 先填整面墙（白色羊毛，模拟土壁）
/fill (cx-3, cy+2, cz+5) (cx+3, cy+4, cz+5) white_wool

# 挖大门（中央，宽1高2）
/fill (cx, cy+2, cz+5) (cx, cy+3, cz+5) air

# 大门两侧窗户（宽2高1）
/fill (cx-3, cy+3, cz+5) (cx-2, cy+3, cz+5) air
/fill (cx+2, cy+3, cz+5) (cx+3, cy+3, cz+5) air
# 装玻璃
/setblock (cx-3, cy+3, cz+5) white_stained_glass_pane
/setblock (cx-2, cy+3, cz+5) white_stained_glass_pane
/setblock (cx+2, cy+3, cz+5) white_stained_glass_pane
/setblock (cx+3, cy+3, cz+5) white_stained_glass_pane
```

### 4.2 背面墙（朝北，实体）

```
/fill (cx-3, cy+2, cz-5) (cx+3, cy+4, cz-5) white_wool
```

### 4.3 左墙（朝西，留窗）

```
/fill (cx-4, cy+2, cz-4) (cx-4, cy+4, cz+4) white_wool
# 挖窗（中间，宽2高1）
/fill (cx-4, cy+3, cz-1) (cx-4, cy+3, cz) air
/setblock (cx-4, cy+3, cz-1) white_stained_glass_pane
/setblock (cx-4, cy+3, cz) white_stained_glass_pane
```

### 4.4 右墙（朝东，留窗）

```
/fill (cx+4, cy+2, cz-4) (cx+4, cy+4, cz+4) white_wool
# 挖窗（中间，宽2高1）
/fill (cx+4, cy+3, cz-1) (cx+4, cy+3, cz) air
/setblock (cx+4, cy+3, cz-1) white_stained_glass_pane
/setblock (cx+4, cy+3, cz) white_stained_glass_pane
```

**自检**：四面墙是否围合？是。是否有洞？只有门和窗。室内是否封闭？是。

---

## 第五步：屋顶（必须对称，这是灵魂）

日式屋顶核心：**大挑檐，四面一致，中间高四周低**。

```
# 屋顶第一层（最宽，挑出墙面2格，用深色橡木木板）
/fill (cx-6, cy+5, cz-7) (cx+6, cy+5, cz+7) dark_oak_planks

# 屋顶第二层（缩进1格）
/fill (cx-5, cy+6, cz-6) (cx+5, cy+6, cz+6) dark_oak_planks

# 屋顶第三层（再缩进1格）
/fill (cx-4, cy+7, cz-5) (cx+4, cy+7, cz+5) dark_oak_planks

# 屋顶第四层（再缩进1格）
/fill (cx-3, cy+8, cz-4) (cx+3, cy+8, cz+4) dark_oak_planks

# 屋脊（最顶部，1格宽）
/fill (cx-2, cy+9, cz-3) (cx+2, cy+9, cz+3) dark_oak_planks
```

**四角微翘**（标志性特征）：
```
/setblock (cx-6, cy+6, cz-7) dark_oak_stairs[facing=east]
/setblock (cx+6, cy+6, cz-7) dark_oak_stairs[facing=west]
/setblock (cx-6, cy+6, cz+7) dark_oak_stairs[facing=east]
/setblock (cx+6, cy+6, cz+7) dark_oak_stairs[facing=west]
```

**自检**：
- [ ] 屋顶是否四面挑出一致？
- [ ] 是否从外向内逐层升高？
- [ ] 四角是否对称微翘？
- [ ] 屋脊是否在正中央？

---

## 第六步：门和内部

```
# 大门（云杉木门，分上下，朝外开）
/setblock (cx, cy+2, cz+5) spruce_door[facing=south,half=lower]
/setblock (cx, cy+3, cz+5) spruce_door[facing=south,half=upper]

# 室内地板（与地基地板同层，已经铺好）
# 室内家具
/setblock (cx-2, cy+2, cz+2) bed[facing=north,part=foot]
/setblock (cx-2, cy+2, cz+3) bed[facing=north,part=head]

/setblock (cx+2, cy+2, cz+2) crafting_table
/setblock (cx+2, cy+2, cz+3) furnace[facing=south]

/setblock (cx, cy+2, cz+0) chest[facing=south]
```

---

## 第七步：外廊（可选，但主体完成后才能做）

```
# 正面外廊（宽2格，云杉木板）
/fill (cx-4, cy+1, cz+6) (cx+4, cy+1, cz+7) spruce_planks

# 外廊柱子（支撑屋顶挑出部分）
/fill (cx-4, cy+1, cz+7) (cx-4, cy+4, cz+7) spruce_fence
/fill (cx+4, cy+1, cz+7) (cx+4, cy+4, cz+7) spruce_fence
```

---

## 第八步：落地支柱（如果浮空）

如果建筑不在地面上，**必须**加支柱：

```
# 四角支柱，从地基通到地面（或最近实体方块）
/fill (cx-4, cy, cz-5) (cx-4, <地面Y>, cz-5) spruce_log
/fill (cx+4, cy, cz-5) (cx+4, <地面Y>, cz-5) spruce_log
/fill (cx-4, cy, cz+5) (cx-4, <地面Y>, cz+5) spruce_log
/fill (cx+4, cy, cz+5) (cx+4, <地面Y>, cz+5) spruce_log
```

---

## 终极自检清单（输出命令前必须全部打勾）

```
□ 四面墙是否围合？（不能透风）
□ 墙高是否≥4格？
□ 门是否在正面中央？宽1高2？
□ 窗户是否在墙上？不是悬空？
□ 屋顶是否四面挑出一致？
□ 屋顶是否从外向内逐层升高？
□ 屋脊是否在正中央？
□ 地基是否落地？（或支柱是否通到地面）
□ 室内是否有地板？（不能站在空气上）
□ 家具是否在室内？（不能放在屋顶上或墙外）
```

**如果任何一项未通过，停止建造，重新计算坐标。**


---

你把这套给AI试试，如果还造出亭子，我直播吃键盘。
