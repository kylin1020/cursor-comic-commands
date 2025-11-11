# add-character-scene

## 📋 Task Checklist

When executing this command, complete tasks in the following order and check off each completed item:

### Stage 1: Information Collection
- [ ] Confirm project status: Check if project structure is complete (style.md, characters/, scenes/ directories exist)
- [ ] Read style definition: Read defined style from style.md to ensure new content maintains consistency
- [ ] Ask for addition type: Let user choose to add character, scene, or both
- [ ] Collect detailed information: Obtain detailed descriptions and related chapter information for new character/scene

### Stage 2: Character Addition (If Needed)
- [ ] Create character md file: Create new character's md document in `characters/` directory
- [ ] Fill in character basic info: Include name, age, identity, personality, etc.
- [ ] Describe character appearance: Detailed description of hairstyle, hair color, eyes, face shape, build, clothing features
- [ ] Generate character 正面照 prompt: Create AI prompt for full-body standing image
- [ ] Generate character 三视图 prompt: Create AI prompt for front/side/back reference image
- [ ] Generate character 表情参考图 prompt: Create AI prompt for 6-8 expression collection
- [ ] Generate character 动作参考图 prompt: Create AI prompt for 3-5 action pose collection
- [ ] Create character output directory: Create new character's output directory under `outputs/characters/`

### Stage 3: Scene Addition (If Needed)
- [ ] Create scene md file: Create new scene's md document in `scenes/` directory
- [ ] Fill in scene basic info: Describe scene name, type, atmosphere, function
- [ ] Describe scene environment: Detailed description of location, architecture, decoration, lighting, weather elements
- [ ] Generate scene 远景 prompt: Create AI prompt for panoramic perspective
- [ ] Generate scene 中景 prompt: Create AI prompt for medium shot perspective
- [ ] Generate scene 近景 prompt: Create AI prompt for close-up details
- [ ] Create scene output directory: Create new scene's output directory under `outputs/scenes/`

### Stage 4: Record Updates
- [ ] Update changelog: Create or update `updates_log.md` in project root directory, record content and time of this addition
- [ ] Optional: Update story_analysis: If new content relates to specific chapter, can update story analysis document

### Stage 5: Display Results
- [ ] Display new content: List all newly created character and scene information
- [ ] Display AI prompt preview: Show generated prompt examples
- [ ] Provide next step suggestions: Prompt to use `/generate-comic-images` command to generate reference images for new character/scene

---

## Execution Instructions

This command is used to **add new characters or scenes** to an initialized comic project. Suitable for new characters or locations appearing during story progression.

### Prerequisite Checks

Before starting, need to confirm:
1. Project has been initialized through `/init-comic` command
2. `style.md` file exists (to maintain style consistency)
3. `characters/` and `scenes/` directories exist

If project is not initialized, should prompt user to run `/init-comic` command first.

### Step 1: Ask for Addition Type

Ask user what content to add this time:
1. **Add character only** - For new appearing characters
2. **Add scene only** - For new appearing locations
3. **Add both character and scene** - For new elements appearing together

### Step 2: Collect Information

#### If adding character, ask for:
- **Character name**
- **Basic info**: Age, gender, identity, occupation
- **Appearance features**: Hairstyle, hair color, eye color, face shape, build, height
- **Clothing design**: Daily clothing, special clothing, accessories
- **Personality traits**: Personality description, speaking style, behavioral habits
- **Character relationships**: Relationships with existing characters
- **Appearance chapters**: First appearance and main active chapters

#### If adding scene, ask for:
- **Scene name**
- **Scene type**: Indoor/outdoor, urban/rural, public/private, etc.
- **Environment description**: Architectural style, decoration features, spatial layout
- **Atmosphere characteristics**: Lighting, color tone, weather, time period
- **Key elements**: Iconic items, special decorations
- **Function description**: Role of this scene in the story
- **Appearance chapters**: First appearance and main usage chapters

### Step 3: Create Character File (If Needed)

Create `characters/<角色名>.md` file for each new character, with the following structure:

```markdown
# 角色名

## 基本信息
- 姓名：
- 年龄：
- 性别：
- 身份/职业：
- 首次登场：第X章

## 外貌特征
- 发型/发色：
- 瞳色：
- 脸型：
- 身材/身高：
- 特殊标记：

## 服装设定
- 日常服装：
- 特殊服装：
- 配饰：

## 性格特点
- 性格描述：
- 说话风格：
- 行为习惯：

## 角色关系
- （与其他角色的关系）

## AI图像生成提示词

### 正面照 (front_view.png)
（提示词内容）

### 三视图 (three_views.png)
（提示词内容）

### 表情参考图 (expressions.png)
（提示词内容）

### 动作参考图 (actions.png)
（提示词内容）
```

**Prompt Generation Requirements**:
- Strictly follow the style defined in `style.md`
- Use natural language description, within 500 chars (Chinese) or 800 chars (English)
- Include complete appearance, clothing, action, expression, background, style descriptions
- Maintain style consistency with existing characters

### Step 4: Create Scene File (If Needed)

Create `scenes/<场景名>.md` file for each new scene, with the following structure:

```markdown
# 场景名

## 基本信息
- 场景名称：
- 场景类型：
- 首次出场：第X章
- 功能说明：

## 环境描述
- 地点特征：
- 建筑风格：
- 空间布局：
- 装饰特点：

## 氛围特点
- 光线：
- 色调：
- 天气/时间：
- 整体氛围：

## 关键元素
- 标志性物品：
- 特殊装饰：
- 重要细节：

## AI图像生成提示词

### 远景 (wide_shot.png)
（提示词内容）

### 中景 (medium_shot.png)
（提示词内容）

### 近景 (close_up.png)
（提示词内容）
```

### Step 5: Create Output Directories

Create corresponding output directories for new characters and scenes:
- Characters: `outputs/characters/<角色名>/`
- Scenes: `outputs/scenes/<场景名>/`

### Step 6: Record Update Log

Create or update `updates_log.md` in project root directory, with the following format:

```markdown
# 项目更新日志

## YYYY-MM-DD - 新增角色/场景

### 新增角色
- **角色名1** - 简短描述，首次登场章节
- **角色名2** - 简短描述，首次登场章节

### 新增场景
- **场景名1** - 简短描述，首次出场章节
- **场景名2** - 简短描述，首次出场章节

---
```

### After Completing Addition

Display to user:
1. **New Content List** - List all newly created characters and scenes
2. **File Creation Confirmation** - Show created file paths
3. **AI Prompt Preview** - Display some generated prompt examples
4. **Output Directory Confirmation** - List created output directories
5. **Next Step Suggestions**:
   - Use `/generate-comic-images` command to generate reference images for new characters (正面照, 三视图, 表情图, 动作图)
   - Use `/generate-comic-images` command to generate reference images for new scenes (远景, 中景, 近景)
   - If need to use these new elements in specific chapters, can create or update corresponding chapter storyboard scripts

## Notes

1. **Maintain Style Consistency**: All new content must strictly follow the style defined in `style.md`
2. **Check for Duplicates**: Check if characters or scenes with same name already exist before creating
3. **Relationship Documentation**: Record relationships between new characters/scenes and existing elements
4. **Chapter Tracking**: Clearly record first appearance and main active chapters
5. **Prompt Quality**: Ensure prompts are detailed and follow AI image generation best practices

## Example Usage

**User**: "我需要添加一个新角色，名叫张伟，是个30岁的警察，会在第8章登场。"

**Execution Process**:
1. Confirm project structure is complete
2. Read style.md to understand style
3. Collect detailed information about 张伟 (appearance, clothing, personality, etc.)
4. Create `characters/张伟.md`
5. Generate 4 AI prompts (正面照, 三视图, 表情, 动作)
6. Create `outputs/characters/张伟/` directory
7. Update `updates_log.md`
8. Display results and provide next step suggestions
