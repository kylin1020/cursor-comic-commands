# storyboard-chapter

## 📋 Task Flow

### Stage 1: Pre-check Phase (Critical 🔴)
- [ ] Receive and analyze chapter content
- [ ] **Extract all characters and scenes mentioned in chapter**
- [ ] **Check if characters/scenes exist** in `characters/` and `scenes/` directories:
  - [ ] List missing characters (not found in `characters/` directory)
  - [ ] List missing scenes (not found in `scenes/` directory)
- [ ] **If any missing elements found**:
  - [ ] **Load `/add-character-scene` command** for each missing element
  - [ ] **Execute character/scene creation** for all missing elements

### Stage 2: Storyboard Generation Phase
- [ ] Determine shot count & pacing (5s/shot default, 10s for complex)
- [ ] Split by scene/plot/emotion → write to `outputs/storyboard/chapter-<#>/storyboard.md`
- [ ] For each shot (generate one at a time):
  - [ ] Script: shot type, scene, action, dialogue, emotion
  - [ ] **🔴 Check 7 continuity aspects** with previous: Spatial | Temporal | Action | Eyeline | Appearance | Lighting | Environmental
  - [ ] Specify camera angle (front/side/back view)
  - [ ] Generate start/end frame prompts (English, 300-500 words, include continuity)
  - [ ] Generate video prompt (中文, 300-600字, describe transitions)

> ⚠️ **CRITICAL**: Pre-check characters/scenes exist | Maintain continuity between shots | Generate incrementally (20-40 shots/chapter)

---

## 📌 Storyboard Splitting Principles

### When to Cut Shot
- Location changes → New shot
- Time jumps → New shot
- Viewpoint changes significantly → New shot

### 7 Continuity Rules (Critical 🔴)

1. **Spatial**: Location change requires transition | 180° rule | Screen direction consistent
2. **Temporal**: Time jump needs transition | Lighting/shadows match time
3. **Action**: Ending pose → Starting pose connects smoothly | No repeats
4. **Eyeline**: Gaze direction logical | Shot B shows what character sees
5. **Appearance**: Clothing/props/physical state consistent
6. **Lighting**: Source direction/intensity/color consistent in same scene
7. **Environmental**: Weather/background elements unchanged in same period

### Camera & Physical Logic
- **Angles**: Front/Side/Back/Over-shoulder/High/Low angle
- **Action-visual match**: Movement direction must align with camera angle
- **Object placement**: Destination visible in character's path based on camera angle
- **Physics**: No instant teleportation/speed/direction changes

### Pacing Control
- Most scenes: 5 seconds/shot
- Complex/emotional scenes: 10 seconds/shot

### Shot Types & Transitions
- **Shots**: Close-up (emotion) | Close (dialogue) | Medium (action) | Wide (environment) | Panorama (space)
- **Transitions**: Cut (default) | Fade (time passage) | Dissolve (flashback) | Match cut

---

## 📐 Prompt Writing Specifications

### Start/End Frame Image Prompts (English)

**Requirements** (300-500 words, natural language):
- Reference `characters/` and `scenes/` features
- Follow `style.md` definition
- **🔴 Must include all 7 continuity elements**:
  1. **Spatial**: Camera angle | Character position/facing | Spatial relation to previous
  2. **Temporal**: Time of day | Lighting quality | Shadow direction
  3. **Action**: Pose connects to previous | Ongoing movement continuation
  4. **Eyeline**: Where looking | Eye direction
  5. **Appearance**: Clothing/props/physical state (consistent with previous)
  6. **Lighting**: Source direction | Color temperature
  7. **Environmental**: Weather | Background elements

**Example**:
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

### Video Clip Prompts (中文)

**要求** (300-600字，自然语言):
- 描述动态过渡过程、镜头运动、角色动作
- **🔴 必须描述所有连续性要素的动态变化**

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

---

## 🎬 Output Format

Save to: `outputs/storyboard/chapter-<#>/storyboard.md`

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

