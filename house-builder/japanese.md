# 日式风格房屋建造指南

日式风格特点：深色木材、直线条、大屋顶挑檐、格子推拉门、庭院景观、自然融合。

## 材料清单

| 部位 | 推荐材料 | 备选材料 |
|------|----------|----------|
| 木构架 | 云杉原木/木板 | 深色橡木、丛林木 |
| 外墙 | 白色羊毛（模拟土壁） | 白色陶瓦、淡灰色混凝土 |
| 屋顶 | 深色橡木楼梯 + 石砖楼梯 | 紫红色陶瓦、海晶石 |
| 地板 | 云杉木板 | 白桦木板、竹板 |
| 推拉门 | 云杉门 + 白色羊毛 | 深色橡木门 |
| 窗纸 | 白色染色玻璃板 | 玻璃板(加活板门遮挡下半) |
| 庭院 | 砾石、草径、砂土 | 沙子、圆石 |
| 装饰 | 灯笼、活板门、竹、樱花(粉色羊毛) | 栅栏、踏石、鲤鱼旗 |

## 推荐尺寸

日式建筑 **横向舒展**，不宜过高：

- 茶室小屋：7 x 7（正方形），高 4
- 主屋：9 x 11（长方形），高 4-5
- 大宅院：13 x 15 + 回廊，高 5

## 核心设计元素

1. **大屋顶挑檐**：屋顶比墙面宽出 2 格以上，屋檐深远
2. **直线条**：没有拱形，全是直线和直角
3. **推拉门（障子）**：外墙大面积用白色和木色组合
4. **架空地板**：房屋高出地面半格到 1 格
5. **内外连通**：推拉门通向庭院/走廊

## 建造步骤（以 9x11 主屋为例）

### 第一步：高台地基

日式房屋通常建在抬高的木台上：

```
# 地基边框（用云杉原木围一圈，高出地面 1 格）
/fill <x> <y+1> <z> <x+8> <y+1> <z+10> spruce_log replace

# 地基内部填充（云杉木板）
/fill <x+1> <y+1> <z+1> <x+7> <y+1> <z+9> spruce_planks replace
```

y 为玩家 y 坐标，地基在地面之上而非之下。

### 第二步：回廊/外廊（縁側）

日式建筑外侧有木质走廊：

```
# 正面外廊（宽 2 格，延伸整个正面）
/fill <x-2> <y+1> <z+10> <x+10> <y+1> <z+11> spruce_planks replace

# 外廊边缘用云杉楼梯做过渡
/fill <x-2> <y+1> <z+12> <x+10> <y+1> <z+12> spruce_stairs replace
```

### 第三步：立柱与横梁

```
# 四角立柱
/fill <x> <y+2> <z> <x> <y+5> <z> spruce_log replace
/fill <x+8> <y+2> <z> <x+8> <y+5> <z> spruce_log replace
/fill <x> <y+2> <z+10> <x> <y+5> <z+10> spruce_log replace
/fill <x+8> <y+2> <z+10> <x+8> <y+5> <z+10> spruce_log replace

# 水平横梁（顶部圈梁）
/fill <x> <y+5> <z> <x+8> <y+5> <z> spruce_log replace
/fill <x> <y+5> <z+10> <x+8> <y+5> <z+10> spruce_log replace
/fill <x> <y+5> <z> <x> <y+5> <z+10> spruce_log replace
/fill <x+8> <y+5> <z> <x+8> <y+5> <z+10> spruce_log replace
```

### 第四步：外墙（土壁 + 障子）

日式外墙下半段为实墙（白色），上半段为格子推拉窗：

```
# 下半段：白色土壁（高 2 格）
/fill <x+1> <y+2> <z+1> <x+7> <y+3> <z+9> white_wool replace

# 上半段：障子推拉门（白色玻璃板 + 木框架）
# 正面（z+10 一侧）用白色玻璃板做推拉门效果
/fill <x+1> <y+4> <z+10> <x+7> <y+5> <z+10> white_stained_glass_pane replace
# 在玻璃之间加云杉原木竖条
/setblock <x+3> <y+2> <z+10> spruce_fence replace
/setblock <x+5> <y+2> <z+10> spruce_fence replace
```

### 第五步：门窗

- **推拉门**：云杉门，宽 2 高 3，成对放置
- 门两侧用 **云杉栅栏** 做门框
- 窗户：**白色染色玻璃板** 配木栅栏框架

### 第六步：屋顶（大挑檐和风 roof）

日式屋顶最核心——**屋檐深远，挑出墙面至少 2 格**。

```
# 屋顶主体（从 y+6 到 y+8，用深色橡木楼梯逐层搭建）
# 第一层屋檐（挑出墙面 2 格，用楼梯）
/fill <x-2> <y+6> <z-2> <x+10> <y+6> <z+12> dark_oak_planks replace

# 屋顶斜面（用楼梯从外向内逐级升高）
# 左侧屋檐：从 x-2 到 x+3，每高一格向内缩 1 格
/fill <x-2> <y+6> <z-2> <x-2> <y+6> <z+12> dark_oak_stairs[facing=east] replace
/fill <x-1> <y+7> <z-1> <x-1> <y+7> <z+11> dark_oak_stairs[facing=east] replace
/fill <x+0> <y+8> <z-1> <x+0> <y+8> <z+11> dark_oak_stairs[facing=east] replace

# 右侧屋檐类推
/fill <x+10> <y+6> <z-2> <x+10> <y+6> <z+12> dark_oak_stairs[facing=west] replace
...

# 屋脊线（最顶部用石砖楼梯压顶）
/fill <x+4> <y+9> <z-1> <x+4> <y+9> <z+11> stone_brick_stairs replace
```

**屋檐角**：四个角微微上翘（日式建筑标志性特征）：
```
# 左前屋檐角微微挑高
/setblock <x-2> <y+7> <z-2> dark_oak_stairs[facing=east] replace
```

### 第七步：走廊与连接

日式建筑中 **回廊** 连接各个房间：

```
# 连接主屋和茶室的走廊
/fill <x+9> <y+1> <z+3> <x+12> <y+1> <z+6> spruce_planks replace
# 走廊顶
/fill <x+9> <y+3> <z+3> <x+12> <y+3> <z+6> dark_oak_planks replace
# 走廊柱子
/setblock <x+9> <y+2> <z+3> spruce_fence replace
```

### 第八步：日式庭院（枯山水）

```
# 枯山水核心区域（在房屋前方）
/fill <x-5> <y> <z+5> <x-1> <y> <z+14> gravel replace
/fill <x-5> <y> <z+5> <x-1> <y> <z+14> sand replace

# 踏石（用石砖台阶嵌入砾石中，蜿蜒路径）
/setblock <x-3> <y+1> <z+7> stone_brick_slab replace
/setblock <x-2> <y+1> <z+9> stone_brick_slab replace
/setblock <x-3> <y+1> <z+11> stone_brick_slab replace
/setblock <x-2> <y+1> <z+13> stone_brick_slab replace

# 石灯笼（用栅栏+台阶+活板门组合）
/setblock <x-4> <y+1> <z+8> stone_brick_wall replace
/setblock <x-4> <y+2> <z+8> stone_brick_slab replace
/setblock <x-4> <y+2> <z+8> lantern hanging=true replace

# 矮松（用云杉树或大型杜鹃花丛）
/setblock <x-4> <y+1> <z+10> azalea replace
```

### 第九步：入口

- **石阶**：从地面到外廊，用 **石砖台阶** 宽 3 格
- **门廊**：入口处屋檐挑出更大（3 格），用立柱支撑
- **暖帘**：入口用 **红色羊毛** + **云杉栅栏** 做半截门帘

### 第十步：围墙与植被

```
# 竹围墙（用云杉栅栏+活板门模拟竹栅栏）
/fill <x-6> <y+1> <z+2> <x-6> <y+2> <z+14> spruce_fence replace

# 竹林（在围墙边）
/setblock <x-7> <y> <z+3> bamboo replace
/setblock <x-7> <y> <z+7> bamboo replace
/setblock <x-7> <y> <z+11> bamboo replace

# 樱花树（用橡树+粉色羊毛/粉色花瓣）
/setblock <x-3> <y+1> <z+2> oak_sapling replace
# 树冠用粉色羊毛
/fill <x-5> <y+4> <z+0> <x-1> <y+6> <z+4> pink_wool replace
```

## 日式风成品参考

```
尺寸: 9 x 11，屋檐挑出 2-3 格，整体占地更大
外观: 深色木构架 + 白墙 + 深色大屋顶 + 纸窗
屋顶: 大挑檐，四角微翘，深色瓦片
庭院: 枯山水、石灯笼、踏石、竹林
氛围: 宁静、禅意、与自然融为一体
```

## 变体

### 茶室
- 极小尺寸（5 x 5）
- 矮门（需俯身进入，用活板门做门）
- 内部设 **壁龛**（展示架+画）
- 窗外正对庭院最佳景观

### 日式城堡天守阁
- 多层结构（5-7 层）
- 每层比下层缩小，呈金字塔形
- 最下层：石砌基座（深板岩）
- 以上各层：白墙+深色木框
- 屋顶：各层独立，翘角显著
- 顶层：金鯱装饰（用金块+海晶灯）

### 温泉旅馆
- 长条形建筑（15 x 7）
- 半个墙高落地窗
- 室外温泉池：**水** 周围用 **石砖** 围边，冒 **气泡柱**（用灵魂沙）
- 周围种 **樱花树** 和 **竹子**
- 入口悬挂 **暖帘**（红色/蓝色羊毛）
