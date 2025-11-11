# storyboard-chapter

## 📋 Task Flow

- [ ] Receive and analyze chapter content, determine storyboard quantity and pacing
- [ ] Split shots by scene, plot, emotion
- [ ] For each storyboard (one at a time):
  - [ ] Write script (shot type, scene, action, dialogue, emotion)
  - [ ] Generate start/end frame image prompts (English, natural language)
  - [ ] Generate video clip prompts (**中文，自然语言描述**)
  - [ ] **Immediately output this storyboard to md file** (incremental write)
- [ ] Continue until all storyboards are generated and written to `outputs/storyboard/chapter-<章节号>/storyboard.md`

> ⚠️ **IMPORTANT**: Since a chapter may require 20-40 storyboards, **please generate and write each storyboard incrementally** instead of generating all at once. This approach:
> - Avoids issues with overly long responses
> - Provides real-time progress feedback
> - Reduces memory pressure

---

## 📌 Storyboard Splitting Principles

### When to Cut Shot
- Location changes → New shot
- Time jumps → New shot
- Viewpoint changes significantly → New shot

### Pacing Control
- Fast-paced action: 3-5 seconds/shot
- Dialogue scenes: 5-10 seconds/shot
- Emotional scenes: 10-15 seconds/shot

### Shot Types
- **Close-up**: Emphasize expressions, details, emotions
- **Close shot**: Above shoulders, dialogue
- **Medium shot**: Above waist, action interaction
- **Wide shot**: Full body, environmental relationships
- **Panorama**: Large scenes, sense of space

### Transition Methods
- Direct cut (Cut): Fast and natural
- Fade in/out (Fade): Time passage
- Dissolve: Space-time transition, flashback
- Match cut: Visual transition

---

## 📐 Prompt Writing Specifications

### Start/End Frame Image Prompts

**Key Points** (English prompts recommended for better model performance):
- Use natural language description, like telling a story
- Reference character features from `characters/`
- Reference scene features from `scenes/`
- Follow `style.md` style definition
- 300-500 words (English)

**Example (English, natural language)**:
```
This is a medium shot showing a 20-year-old young man named 李小明 standing inside a cozy cafe. He has short black hair and brown eyes, wearing a simple white shirt and dark pants. His hands rest naturally at his sides, and his expression is calm as he looks forward. The cafe around him has a warm, inviting atmosphere with wooden tables and chairs, and soft warm-toned lighting creates a comfortable ambiance. The camera captures him from the front, with his figure positioned slightly left of center in the frame. The artwork follows a Japanese anime style similar to Makoto Shinkai's work, featuring clear, precise line work, bright and pleasant colors, and high-quality detailed rendering.
```

### Video Clip Prompts

**Key Points** (**必须使用中文，自然语言描述**):
- 使用自然语言描述动态过渡过程
- 明确指定镜头运动和角色动作
- 描述情绪和环境变化
- 200-400 字（中文）

**Example (中文，自然语言)**:
```
这是一个固定机位的中景镜头。场景开始时，李小明平静地站在咖啡厅里。随着时间推移，他的身体开始微微前倾，右手从身侧缓缓抬起，最终指向前方。他的面部表情逐渐变化——从平静、中性的表情开始，眼睛因看到什么而逐渐睁大，嘴巴也因反应而微微张开。在这4秒的序列中，背景咖啡厅的灯光保持稳定一致，维持着温馨的氛围。他的动作节奏适中自然，既不匆忙也不过于缓慢。动画遵循日本动漫风格，角色动作流畅自然，感觉真实可信。
```

---

## 🎬 Storyboard Script Output Format

Output file: `outputs/storyboard/chapter-<章节号>/storyboard.md`

```markdown
# 第X章分镜脚本

**章节标题**: <标题>
**章节概要**: <简要描述>
**总分镜数**: <数量>
**预估时长**: <分钟>

---

## 分镜概览

| 分镜号 | 镜头类型 | 场景 | 角色 | 时长 | 描述 |
|-------|---------|------|------|------|------|
| 001 | 远景 | 咖啡厅 | 李小明 | 5秒 | 建立环境 |
| 002 | 中景 | 咖啡厅 | 李小明 | 4秒 | 走向座位 |
| ... | ... | ... | ... | ... | ... |

---

## 详细分镜

### 【分镜 001】

**镜头类型**: 远景
**场景**: 咖啡厅（参考：`scenes/咖啡厅.md`）
**角色**: 李小明（参考：`characters/李小明.md`）
**时长**: 5秒
**转场**: 淡入

**画面描述**:
咖啡厅全景，李小明从门口走进，暖色调灯光营造温馨氛围。

**对白/旁白**:
（背景音乐：轻柔爵士乐）

**情绪**: 平静、温馨

---

#### Start Frame Prompt (English, natural language)

```
This is a wide shot showing a cozy cafe interior from an overhead angle. The scene captures a warm, inviting space with wooden tables and chairs arranged throughout, a bar counter visible in the background, and a few customers seated here and there. The lighting is warm and welcoming. On the right side of the frame, a glass door has just opened, and a 20-year-old young man named 李小明 is entering through the doorway. He has short black hair and is wearing a white shirt. The camera position is fixed, giving us a bird's-eye view of the entire scene. The artwork is rendered in a Japanese anime style with a warm color palette and high-quality detailed rendering.
```

---

#### End Frame Prompt (English, natural language)

```
This is a wide shot of the same cafe interior, maintaining the overhead angle and fixed camera position. The environment remains unchanged from before - the same cozy atmosphere, wooden furniture, and warm lighting. 李小明 has now walked further into the space and appears in the center-right area of the frame. We see him from behind as he heads towards the seating area on the left side of the cafe. The glass door through which he entered is now closed. Everything else in the scene remains consistent with the previous moment. The artwork continues in the same Japanese anime style with warm color tones and detailed, high-quality rendering.
```

---

#### Video Prompt (中文，自然语言)

```
这是一个5秒的序列，采用固定俯视机位的远景镜头。场景以柔和的淡入效果开始。我们看到李小明推开玻璃门，走进咖啡厅。他稳步从画面右侧边缘走向中心右侧区域，朝着左侧的座位区走去。当他穿过空间时，背景中的其他顾客展现出细微、自然的动作——小幅度的手势和轻微的移动，为场景带来生机。整个咖啡厅的温暖灯光保持稳定一致，维持着温馨、欢迎的氛围。整个序列的节奏轻松不匆忙，让观众能够充分感受环境。动画遵循日本动漫风格，角色动作流畅自然，感觉真实可信。
```

---

### 【分镜 002】
... (and so on)
```

---

## 💡 Usage Guide

### Provide Chapter Information

Need to provide:
1. **Chapter number**: e.g., 1, 2, 3
2. **Chapter title**: Title name
3. **Chapter content**: Complete text

### Storyboard Quantity Reference

- Short chapter (500-1000 chars): 10-15 storyboards
- Medium chapter (1000-2000 chars): 15-25 storyboards
- Long chapter (2000+ chars): 25-40 storyboards

### Special Requirements (Optional)

- Emotional scenes that need emphasis
- Slow motion or special effect shots
- Camera language preferences
- Transition method preferences

---

## ⚠️ Notes

- Adjacent storyboards visually coherent
- Character appearance, clothing, lighting maintain consistency
- Follow 180-degree axis rule
- Prompts sufficiently detailed, reference character and scene settings
- Single shot no longer than 15 seconds
- Consider AI video generation technology limitations (3-10 seconds)

---

**Ready? Provide chapter information and start creating storyboard script!**
