# init-comic

## 📋 Task Checklist

When executing this command, complete tasks in the following order and check off each completed item:

### Stage 1: Information Collection and Analysis
- [ ] Receive preprocessed information: Parse story summary, characters and scenes from user-provided information (recommended to use `/summarize-novel` command first)
- [ ] Verify information completeness: Confirm if character (3-8) and scene (3-10) information is complete and usable
- [ ] Determine anime style: Ask and record user's style choice (Japanese/American/Chinese/Korean, etc.)

### Stage 2: Project Structure Setup
- [ ] Create project base structure: Create all required directories (characters/scenes/chapters/outputs, etc.)
- [ ] Create style.md: Detailed record of style definition, color scheme, line style, lighting treatment, AI generation keywords

### Stage 3: Character Setup and Prompts
- [ ] Create character md files: Create independent document for each main character (including basic info, appearance, clothing, personality)
- [ ] Generate character 正面照 prompts: Create AI prompts for full-body standing image for each character (output to <姓名>-正面照.png)
- [ ] Generate character 三视图 prompts: Create AI prompts for front/side/back reference image for each character (output to <姓名>-三视图.png)
- [ ] Generate character 表情参考图 prompts: Create AI prompts for 6-8 expression collection for each character (output to <姓名>-表情参考图.png)
- [ ] Generate character 动作参考图 prompts: Create AI prompts for 3-5 action pose collection for each character (output to <姓名>-动作参考图.png)

### Stage 4: Scene Setup and Prompts
- [ ] Create scene md files: Create document for each main scene (describe environment, atmosphere, key elements)
- [ ] Generate scene prompts: Create AI prompts for different angles (远景/中景/近景) for each scene (output to <场景名>-<角度>.png)

### Stage 5: Finishing Work
- [ ] Create README.md: Write project documentation, including project structure and usage guide
- [ ] Verify project structure: Ensure all files and directories are correctly created
- [ ] Display project overview: Show user complete project structure and next step suggestions (generate character and scene images)

---

## 📌 Key Prompt Optimization Points

### Prompt Enhancement for Famous Historical Figures
When project involves real historical figures, prompts need to pay special attention to these characters' **historical identity characteristics** and **cultural symbolic significance**. Recommendations:

1. **Clarify Historical Identity**: Clearly indicate character's historical identity and achievements in prompt
   - Example: Not just "an emperor", but "明朝开国皇帝朱元璋, transformation from poor peasant to emperor"
   - Helps AI generate visual images that better match historical figure's temperament

2. **Emphasize Unique Appearance Features**: Famous historical figures often have obvious physiological or iconic features
   - Example: 朱元璋's "驴脸", long head, wide chin are iconic features that need clear description
   - 郑成功's "儒将气质" and "一条腿较重" special physical traits need precise conveyance
   - 海瑞's "补丁满身官袍" symbolizes his incorruptible image

3. **Highlight Power Attributes and Psychological States**: Different power levels of characters have different visual expressions
   - Emperors (朱元璋, 朱棣): Cold, powerful, oppressive presence
   - Incorruptible officials (海瑞): Ascetic, upright, principled
   - Power ministers/eunuchs (魏忠贤): Eerie combination of flattery and cruelty
   - Generals (郑成功, 吴三桂): Combat prowess and internal conflicts

4. **Supplement with Web Search Information** (if needed):
   - If project includes real historical figures, recommend quick search before generating prompts
   - Supplement the figure's: historical status, era background, representative events, evaluations, cultural symbolic significance
   - Integrate this information into prompts to make generated images more accurate and profound

5. **Prompt Template Example** (for historical figures):
   ```
   A [dynasty][identity], [age] years old, [historical identity description].
   His unique characteristics: [iconic appearance], [power temperament], [psychological state].
   Clothing embodiment: [period clothing], [power level clothing], [symbolic meaning].
   Historical background: [main achievements], [representative events], [cultural symbolism].
   Aura expression: [power manifestation], [inner world], [historical mission].
   Background setting: [era background], [environmental atmosphere].
   Art style: [specified style], [quality requirements].
   ```

---

## Execution Instructions

I need you to help me initialize a comic generation project.

### Step 1: Collect Basic Information

**Recommended Workflow**:
1. First use `/summarize-novel` command to analyze novel and generate standardized information output
2. Copy `/summarize-novel` output results
3. When using this command (`/init-comic`), paste the above information

**If user has already provided `/summarize-novel` output**:
- Directly parse user-provided formatted information (containing story summary, characters, scenes)
- Skip analysis and extraction steps

**If user has not used `/summarize-novel`**:
- Ask user to provide the following information:
  1. **Story Summary**: Story overview (300-500 chars), including theme, main plot, ending direction
  2. **Main Characters** (3-8): Name, age, appearance features, personality, clothing and other detailed information
  3. **Main Scenes** (3-10): Scene name, environment description, atmosphere, etc.
- Recommend user to use `/summarize-novel` command to automatically generate this information

### Step 2: Verify Information Completeness

Check if provided information meets requirements:
- Is story summary clear and complete
- Does each character have sufficient appearance, personality, clothing descriptions
- Does each scene have environment and atmosphere descriptions
- If missing, ask user to supplement

### Step 3: Determine Style
Ask user what anime style they want to use, provide options:
- Japanese anime style (Miyazaki, Shinkai, Kyoto Animation, etc.)
- American comic style (Marvel, DC, etc.)
- Chinese style anime
- Korean webtoon style
- Or let user customize

Ask in detail about style's colors, lines, lighting characteristics.

**⚠️ If project involves historical figures**:
- Confirm whether to emphasize historical accuracy (clothing, architecture, artifacts, etc.)
- Ask about attitude towards character appearance: Fully according to historical records vs idealized transformation
- Confirm if need to reinforce "historical figure" identity markers in prompts
- For figures with special appearance features (like 朱元璋's "驴脸"), confirm whether to preserve or refine
- Consider era background's impact on visual expression

### Step 4: Create Project Structure
Create complete project structure in current working directory:
- `style.md` - Detailed record of style definition, including color scheme, line style, lighting treatment, character and scene drawing requirements, and general keywords for AI image generation
- `characters/` directory - Create independent md file for each main character (e.g., `李小明.md`, `王雪儿.md`), containing character's basic info, appearance features, clothing design, personality traits
- `scenes/` directory - Create md file for each main scene (e.g., `咖啡厅.md`, `校园操场.md`), describing scene's environment, atmosphere, key elements
- `chapters/` directory - Reserved chapter directory (to create storyboard scripts through separate command later)
- `outputs/` directory - Pre-create output directory structure, including:
  - `outputs/characters/李小明/`, `outputs/characters/王雪儿/`, etc. - Output directory for each character
  - `outputs/scenes/咖啡厅/`, `outputs/scenes/校园操场/`, etc. - Output directory for each scene
  - `outputs/chapters/` - Chapter output directory
- `README.md` - Project documentation, including project structure, workflow and usage guide

**Key Point**: In each character's md file, need to generate detailed AI image generation prompts for the following content:

1. **正面照** - Full-body standing image, neutral expression, white background, output to `outputs/characters/李小明/front_view.png` (example)

2. **三视图** - Character design reference image of front/side/back views, maintain consistency, output to `outputs/characters/李小明/three_views.png` (example)

3. **表情参考图** - Merge multiple expressions (happy, sad, angry, surprised, scared, embarrassed, etc., 6-8) into one image for generation, like emoticon design, each expression occupies one grid, output to `outputs/characters/李小明/expressions.png` (example). This can reduce generation frequency and cost.

4. **动作参考图** - Merge 3-5 key actions (like combat stance, running, walking, sitting, etc.) into one image for generation, each action occupies one grid, output to `outputs/characters/李小明/actions.png` (example). Can also save generation cost.

All prompts must use **natural language description format**:
- Follow style requirements defined in style.md
- Use complete sentences to describe what to generate, naturally fluent like storytelling
- Describe character's appearance features in detail but concisely (hairstyle, hair color, eyes, face shape, build, clothing, accessories, etc.)
- For 表情参考图, should state "This is a character expression reference image containing multiple expressions"
- For 动作参考图, should state "This is a character action reference image containing multiple action poses"

#### **🔍 Prompt Optimization Strategy for Historical Figures**:

| Character Type | Prompt Emphasis | Specific Optimization Direction |
|---------|-----------|----------|
| **Emperors** | Power characteristics, sense of authority, cold temperament | Emphasize emperor identity, ruler's oppressive presence, historical status; highlight iconic features (like 朱元璋's "驴脸") |
| **Incorruptible Officials** | Integrity image, principled nature, ascetic sense | Emphasize incorruptible quality, patched clothing, unwavering gaze, upright unyielding temperament |
| **Power Ministers/Eunuchs** | Power desire, contradiction between flattery and cruelty | Highlight illusory nature of power, transformation from humble to powerful, eerie dual personality |
| **Generals** | Combat prowess, internal conflicts, historical mission | Emphasize military talent, inner struggles, dilemma of loyalty or betrayal, representative events |
| **Female Characters** | Era background, identity status, personality complexity | Consider era's constraints on women, their choices and power, depth of inner world |

#### **Three-Tier Prompt Writing Method** (especially applicable to historical figures):

**Tier 1: Historical Identity Positioning**
- Clearly indicate dynasty, position, historical status
- Example: `明朝开国皇帝朱元璋`, `南明忠臣郑成功`, `清廉刚直的海瑞`
- **Purpose**: Let AI model understand this is not a fictional character, but a figure with deep historical background

**Tier 2: Unique Feature Description**
- Highlight iconic features that distinguish this figure from others
- Include: Physical traits, power symbols, psychological qualities, representative clothing
- Example: `长脑袋和宽下巴的独特容貌`, `满身补丁的官袍象征廉洁`, `精光四射的权欲眼神`
- **Purpose**: Ensure generated image has recognizability and historical accuracy

**Tier 3: Power and Psychology Fusion**
- Combine historical period and figure's psychological state
- Describe how power changed or shaped this figure
- Example: `从贫农到帝王，眼神中混合了智慧和残忍`, `孤臣坚守的悲壮感`, `权力顶峰时的疯狂与崩溃后的恐惧对比`
- **Purpose**: Endow character with richer expressiveness and historical significance

- **Prompt Format Requirements**:
  - Control within 500 chars (Chinese) or 800 words (English)
  - Use complete sentences in natural language, don't pile up keywords
  - Can use Chinese or English description, but maintain language consistency
  - Don't use special symbols, line breaks, all content in one paragraph
  - Organize description in order: "subject-historical identity-appearance-clothing-power characteristics-psychological state-background-style-quality"
  - **Chinese Example (Fictional Character)**: `画一个20岁的年轻男性角色正面全身像。他有着短黑色头发，棕色眼睛，瓜子脸，身材修长。穿着白色衬衫和深色长裤。他自然站立，表情平静中性。纯白色背景。采用日系动漫风格，线条清晰，色彩明亮，高质量精细画面。`
  - **Chinese Example (Historical Figure)**: `画明朝开国皇帝朱元璋的正面全身像，40多岁，面容特征独特强势。他有长脑袋、宽大下巴，典型的"驴脸"，皮肤黝黑粗糙，眼神深邃冷酷透着智慧和残忍。穿着明黄龙袍，绣着金龙纹样，平天冠装束，散发不可侵犯的帝王气场。纯白背景。日系动漫风格，线条清晰精细，光影对比强烈，高质量精细画面。`

Scene md files should also contain generation prompts, supporting different angles (远景, 中景, 近景).

#### **📋 Historical Figure Prompt Checklist** (Check before generating prompts):

Before generating prompts for historical figures, ensure the following information is complete:

- [ ] **Historical Identity**: Is the figure's dynasty, official position, historical status clearly expressed in the prompt?
- [ ] **Physical Features**: Are the figure's iconic facial features highlighted? (e.g., "驴脸", "无须", "一腿较重", etc.)
- [ ] **Power Level**: Is the figure's power level fully expressed through temperament, clothing, gaze, etc.?
- [ ] **Representative Events**: Are the figure's representative events or historical status hinted at or explicitly mentioned?
- [ ] **Era Background**: Are visual characteristics of the era the figure lived in considered?
- [ ] **Psychological Complexity**: For figures with complex psychology (like 吴三桂's contradictions, 魏忠贤's transformation), is it fully expressed?
- [ ] **Clothing Accuracy**: Does clothing description match the figure's era and identity?
- [ ] **Cultural Symbolism**: Is the figure's cultural symbolic significance reflected? (e.g., 海瑞's integrity, 郑成功's loyalty)
- [ ] **Contrast**: For figures with multiple periods, are differences between periods reflected?
- [ ] **Length Control**: Is prompt controlled within required character count?

**Supplementary Guidance When Check Fails**:
- If historical background information is missing, recommend web search supplementation
- If iconic features are not obvious, can review historical evaluations and literature
- If power temperament is insufficient, consider adding power-related visual vocabulary
- If cultural symbolic significance is unclear, can consult biographies and critical biographies of historical figures

### After Completing Initialization

After completing all file creation, show me:
1. **Project Structure Overview** - Clear directory tree display
2. **Created Character List** - Contains each character's basic information and AI prompt preview
3. **Created Scene List** - Contains each scene's description and AI prompt preview
4. **Next Step Suggestions**:
   - Use `/generate-comic-images` command to batch generate character reference images (正面照, 三视图, 表情图, 动作图)
   - Use `/generate-comic-images` command to batch generate scene reference images (远景, 中景, 近景)
   - After generating character and scene images, can use separate command to create storyboard scripts for specific chapters
   - **For subsequent chapters requiring new characters/scenes**, use `/add-character-scene` command to supplement new character or scene settings