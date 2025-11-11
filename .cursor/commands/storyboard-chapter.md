# storyboard-chapter

## 📋 Task Flow

- [ ] Receive and analyze chapter content, determine storyboard quantity and pacing
- [ ] Split shots by scene, plot, emotion
- [ ] For each storyboard (one at a time):
  - [ ] Write script (shot type, scene, action, dialogue, emotion)
  - [ ] Generate start/end frame image prompts
  - [ ] Generate video clip prompts
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

**Key Points** (English prompts recommended for better model performance):
- Use natural language to describe the dynamic transition process
- Clearly specify camera movement and character actions
- Describe emotional and environmental changes
- 200-400 words (English)

**Example (English, natural language)**:
```
This is a medium shot with a fixed camera position. The scene begins with 李小明 standing calmly in the cafe. As the moment unfolds, his body begins to lean slightly forward, and his right hand slowly rises from his side, eventually pointing forward. His facial expression undergoes a gradual transformation - starting from a calm, neutral look, his eyes begin to widen in surprise, and his mouth opens slightly in reaction to something he sees. Throughout this 4-second sequence, the background cafe lighting remains stable and consistent, maintaining the warm atmosphere. The pacing of his movements is moderate and natural, neither rushed nor too slow. The animation follows a Japanese anime style with smooth, fluid character movements that feel organic and believable.
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

#### Video Prompt (English, natural language)

```
This is a 5-second sequence captured in a wide shot from a fixed overhead camera position. The scene begins with a gentle fade-in effect. We see 李小明 push open the glass door and step into the cafe. He walks steadily from the right edge of the frame towards the center-right area, making his way towards the seating area on the left side. As he moves through the space, the other customers in the background show subtle, natural movements - small gestures and slight shifts that bring life to the scene. The warm lighting throughout the cafe remains stable and consistent, maintaining the cozy, welcoming atmosphere. The pacing of the entire sequence is relaxed and unhurried, allowing viewers to take in the environment. The animation follows a Japanese anime style with smooth, fluid character movements that feel natural and believable.
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
