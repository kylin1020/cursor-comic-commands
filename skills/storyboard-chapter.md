---
inclusion: manual
---

# 技能: 创建章节分镜脚本

为指定章节创建详细的分镜脚本。

## 触发条件
- 项目已初始化
- 角色和场景参考图已生成
- 需要为特定章节创建分镜

## 执行流程

### 阶段 1: 预检查 (关键 🔴)

1. 接收并分析章节内容
2. **提取章节中提到的所有角色和场景**
3. **检查角色/场景是否存在**:
   - 检查 `characters/` 目录
   - 检查 `scenes/` 目录
4. **如果发现缺失元素**:
   - 列出缺失的角色
   - 列出缺失的场景
   - 调用 `add-character-scene` 技能创建缺失元素

### 阶段 2: 分镜生成

1. 确定镜头数量和节奏 (默认5秒/镜头，复杂场景10秒)
2. 按场景/情节/情绪分割
3. 为每个镜头生成:
   - 脚本: 镜头类型、场景、动作、对白、情绪
   - **检查7个连续性方面**
   - 指定镜头角度
   - 生成前帧/尾帧提示词 (英文，300-500词)
   - 生成视频提示词 (中文，300-600字)

## 分镜分割原则

### 何时切换镜头
- 地点变化 → 新镜头
- 时间跳跃 → 新镜头
- 视角显著变化 → 新镜头

### 7个连续性规则 (关键 🔴)

1. **空间**: 位置变化需要过渡 | 180°规则 | 画面方向一致
2. **时间**: 时间跳跃需要过渡 | 光线/阴影匹配时间
3. **动作**: 结束姿势 → 开始姿势平滑连接 | 无重复
4. **视线**: 注视方向合理 | 镜头B展示角色所看内容
5. **外观**: 服装/道具/身体状态一致
6. **光照**: 同一场景中光源方向/强度/颜色一致
7. **环境**: 同一时期天气/背景元素不变

### 镜头与物理逻辑
- **角度**: 正面/侧面/背面/过肩/俯视/仰视
- **动作-视觉匹配**: 移动方向必须与镜头角度对齐
- **物体放置**: 目的地在角色路径中基于镜头角度可见
- **物理**: 无瞬间传送/速度/方向变化

### 节奏控制
- 大多数场景: 5秒/镜头
- 复杂/情感场景: 10秒/镜头

### 镜头类型与转场
- **镜头**: 特写(情感) | 近景(对话) | 中景(动作) | 远景(环境) | 全景(空间)
- **转场**: 切(默认) | 淡入淡出(时间流逝) | 溶解(闪回) | 匹配剪辑

## 提示词规范

### 前帧/尾帧图像提示词 (英文)

**要求** (300-500词，自然语言):
- 参考 `characters/` 和 `scenes/` 特征
- 遵循 `style.md` 定义
- **必须包含所有7个连续性元素**

**示例**:
```
[CONTINUITY: Continues from previous - 李小明 approaching cafe entrance]
Medium shot, 李小明 (20s man) just inside cafe after entering glass door.
SPATIAL: Front view eye-level, right of center facing camera, glass door background right.
TEMPORAL: Mid-afternoon, soft daylight through windows.
ACTION: Right foot completing step, body weight forward (continuing walk).
EYELINE: Looking left towards seating area.
APPEARANCE: Short black hair, brown eyes, clean white shirt, dark pants, brown bag on left shoulder.
LIGHTING: Warm afternoon sun from left, gentle shadows right, warm tone.
ENVIRONMENT: Wooden tables/chairs, clear sunny weather through windows.
Japanese anime style, clear lines, bright colors, high quality.
```

### 视频片段提示词 (中文)

**要求** (300-600字，自然语言):
- 描述动态过渡过程、镜头运动、角色动作
- **必须描述所有连续性要素的动态变化**

**示例**:
```
【连续性：紧接上镜，李小明刚推开咖啡厅门】
4秒序列，固定正面中景。
空间：正面平视略偏右，从门口迈步入内，背景右侧玻璃门。
时间光线：下午，柔和光从左侧窗户照入，右侧温柔阴影，暖色调晴天。
动作：右脚落地完成一步（延续上镜），身体前倾重心前移，随后左脚迈出，左肩棕色包随晃动。
视线：目光略偏左看座位区，眼神好奇。
外观：白衬衫深裤左肩棕包，衣服平整。
环境：木桌椅温暖装饰不变。
动作流畅自然节奏适中，日系动漫风格连贯真实。
```

## 输出格式

保存到: `outputs/chapters/chapter-<#>/storyboard.md`

```markdown
# 第X章分镜脚本
**章节标题**: <标题> | **概要**: <描述> | **总镜数**: <#> | **时长**: <分钟>

## 分镜概览
| # | 镜头 | 场景 | 角色 | 时长 | 描述 |
|---|-----|-----|-----|-----|-----|
| 001 | 远景 | 咖啡厅 | 李小明 | 5s | 建立环境 |

## 详细分镜

### 【分镜 001】
**镜头**: 远景 | **场景**: 咖啡厅 (`scenes/咖啡厅.md`) | **角色**: 李小明 (`characters/李小明.md`)
**时长**: 5秒 | **转场**: 淡入 | **情绪**: 平静温馨

**画面**: 咖啡厅全景，李小明从门口走进，暖色调灯光。
**对白**: （背景音乐：轻柔爵士乐）

#### Start Frame Prompt
```
[English, 300-500 words with all 7 continuity elements]
```

#### End Frame Prompt
```
[English, 300-500 words with all 7 continuity elements]
```

#### Video Prompt
```
【中文，300-600字，描述所有连续性要素的动态变化】
```

### 【分镜 002】
...
```

## 关键提醒

> ⚠️ **关键**: 预检查角色/场景存在 | 保持镜头间连续性 | 增量生成 (每章20-40个镜头)
