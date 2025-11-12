# generate-comic-images

## Core Execution Steps

### Step 1: Understand Requirements and Analyze Content
- Determine what to generate (characters/scenes/storyboards), generation scope and types
- **Character Analysis**:
  - Check if the character has multiple age descriptions (e.g., 少年, 青年, 中年), need to generate separate base reference images for **each age group**
  - Check if the character involves multiple scene states (e.g., normal, injured, disguised), need to generate derivative images for **different scenarios**
- **Scene Analysis**:
  - Check if the scene has seasonal variation descriptions (e.g., 春夏秋冬, sunny/rainy), need to generate base reference images for **each season/weather**
  - Medium shots and close-ups of scenes need to be generated according to the corresponding season
- **Storyboard Frame Continuity Analysis** (Critical 🔴):
  - **前帧 and 尾帧 are consecutive frames of the SAME shot** - usually representing a fixed camera or camera movement (pan, tilt, dolly, zoom)
  - **Scene environment should remain HIGHLY CONSISTENT** between 前帧 and 尾帧: same location, same lighting conditions, same weather, same time of day
  - **Main variations between frames** should be: camera position/angle changes (if camera moves), character action progression, focal length adjustments, but NOT scene/location changes
  - **Lighting and atmospheric conditions must stay consistent** - no sudden day-to-night jumps, no weather changes, no unexplained environment transformations
  - When generating 尾帧, emphasize in prompt: "Same shot continuation from 前帧, maintaining identical scene environment, lighting, and atmosphere"
- **Read and Extract Key Information (Multi-level Fusion)**:
  - Read `style.md` to extract **global style keywords** (art style, color tone, lighting, line work, texture, artistic style, etc., about 100 characters)
  - Read current chapter storyboard.md to extract **chapter atmosphere keywords** (emotion, color tone, pacing, environmental tone, period feel, etc., about 60 characters)
  - Read storyboard md to extract **scene descriptions** (this is core content, including scenes, characters, actions, expressions and other visual elements)
  - Read related character/scene md files to get **character/scene details** (appearance features, scene layout, etc.)
- Check for existing reference images in outputs directory to avoid duplicate generation

### Step 2: Optimize Prompts and Prepare Generation Parameters
- **Prompt Construction (Multi-level fusion, total length ≤600 Chinese characters)**:
  - **Base Structure** (Characters/Scenes): `[Specific content description 450-480 chars] + [Age/season annotation 20 chars] + [Global style 100 chars]`
  - **Storyboard Structure** (Single frame generation, consecutive frames related):
    ```
    Start Frame: [Shot type 10 chars] + [Core scene description 280-320 chars] + [Relation to previous shot 50 chars (if any)] + [Chapter atmosphere 60 chars] + [Global style 100 chars]
    End Frame: [Shot type 10 chars] + [Core scene description 280-320 chars] + [SAME SHOT continuation emphasis 50 chars] + [Chapter atmosphere 60 chars] + [Global style 100 chars]
    ```
    - **🔴 End Frame MUST emphasize**: "Same shot continuation, maintaining identical scene, lighting, and atmosphere from start frame. Only [describe specific changes: character movement/camera adjustment/focal shift]."
  - **Scene Description is Core** (Most Important):
    - **Must include** the "scene description" content from storyboard, this is the most core visual element
    - Scene description includes: scene environment, character appearance and actions, expressions, object details, lighting atmosphere, etc.
    - **Start frame and end frame are THE SAME SHOT** (beginning and end moments):
      - Scene location/background: MUST BE IDENTICAL (same room, same outdoor area, same viewing angle)
      - Lighting/weather/time: MUST BE CONSISTENT (no day→night, sunny→rainy jumps)
      - Camera type: MUST MAINTAIN (wide shot stays wide shot, close-up stays close-up, or natural camera movement transition)
      - Only describe progression: character action changes, camera movement (dolly/pan/tilt), or focal adjustments
  - **Expansion and Optimization Tips**:
    - Fully expand core visual elements in scene description, include more details (scene layout, character state, object close-ups, environmental atmosphere, etc.)
    - Global style can describe art style features, color schemes, lighting effects, line texture, artistic style in detail
    - Chapter atmosphere can include emotional tone, color preferences, pacing feel, period sense, etc.
    - Age/season must be clearly marked (e.g., "少年时期", "秋季黄昏")
    - Fully utilize 600 character space, let model get richer information to generate high-quality images
- **Prepare Reference Images (max 6, try to fill up)**:
  - **Character Derivative Images**: Use **corresponding age/scene front view** (1 image)
  - **Scene Derivative Images**: Use **corresponding season/weather wide shot** (1 image)
  - **Storyboard Start Frame** (max 6 images):
    1. Front view of characters appearing in the shot (corresponding age, 1-3 images)
    2. Wide shot of the corresponding scene (corresponding season, 1 image)
    3. End frame of previous shot (if there's continuity, 1 image)
    4. Other reference images of related scenes/characters (e.g., special expressions, actions, 1-2 images)
  - **Storyboard End Frame** (max 6 images, start frame is key):
    1. **Start frame of this shot** (required, 1 image)
    2. Front view of characters appearing in the shot (corresponding age, 1-3 images)
    3. Wide shot of the corresponding scene (corresponding season, 1 image)
    4. Related reference images (e.g., special expressions, actions, 0-1 images)

### Step 3: Generate in Batches by Order (Consider Content Variants)
**Round 1**: Generate base reference images - without using reference images
  - For each character's **each age group** → Generate corresponding front view
  - For each scene's **each season/weather variation** → Generate corresponding wide shot
**Round 2**: Generate derivative images - using corresponding base reference images
  - Three-view diagrams, expressions, actions for corresponding age/scene states
  - Medium shots, close-ups for corresponding seasons
**Round 3**: Generate storyboards (frame by frame in sequence)
  - **By storyboard order**, generate start frame first, then end frame
  - Start frame: Use character front view + scene wide shot + previous shot end frame (if any) + other reference images
  - End frame: **Must use start frame** + character front view + scene wide shot + other reference images
  - Can concurrently generate multiple shots' start frames (3-5), but end frames must wait for corresponding start frames to complete
  - No more than 5 concurrent tasks at a time

### Step 4: Quality Check
- After generation completes, automatically read all images for quick inspection
- **Storyboard images must be checked**:
  - Scene description conformity: Check item by item against storyboard scene descriptions
  - Start/end frame correlation: Side-by-side comparison, check scene, character, lighting, action continuity
  - Character age consistency: Compare with character front view
  - Art style consistency: Compare with style.md settings
- Only output concise report when issues are found (list non-conforming items)
- Regenerate problematic images, use successful images as one of reference_images

### Step 5: Final Report
- Concise display: ✅ Success X images / ❌ Failed Y images
- List generated image paths grouped by type

---

## Important Constraints

### Generation Order (Must Follow)
**Character Images**: 正面照 → 三视图 → 表情 → 动作 (each using 正面照 as reference)
**Scene Images**: 远景 → 中景 → 近景 (each using 远景 as reference)
**Storyboard Images**: Generated last, single frame by frame (前帧 → 尾帧, 尾帧 must use 前帧 as reference image)

### Output Path Specifications
**Character Images**: `outputs/characters/[角色名]/[类型].png`
- 正面照: `outputs/characters/[角色名]/正面照.png`
- 三视图: `outputs/characters/[角色名]/三视图.png`
- 表情参考: `outputs/characters/[角色名]/表情参考图.png`
- 动作参考: `outputs/characters/[角色名]/动作参考图.png`

**Scene Images**: `outputs/scenes/[场景名]/[类型].png`
- 远景: `outputs/scenes/[场景名]/远景.png`
- 中景: `outputs/scenes/[场景名]/中景.png`
- 近景: `outputs/scenes/[场景名]/近景.png`

**Storyboard Images**: `outputs/chapters/[章节名]/[分镜号]-[分镜名称]_[帧号].png`
- Example: `outputs/chapters/chapter-001/分镜01-开篇远景_1.png` (前帧)
- Example: `outputs/chapters/chapter-001/分镜01-开篇远景_2.png` (尾帧)

### General Rules
- Base reference images (正面照, 远景) **do not use** reference images, pure text generation
- Derivative images **must** use corresponding base reference images to ensure consistency
- All derivative images of the same character/scene use the same base reference image
- Automatically create directories if they don't exist
- File names strictly follow the above format to ensure clear file organization

### Storyboard Generation Special Rules
- **Single Image Generation Principle**: Generate one image at a time (num_images=1), 前帧 and 尾帧 generated separately
- **End Frame Forced Dependency**: 尾帧 must place corresponding 前帧 in first position of reference images
- **Try to Fill Reference Images**: Try to prepare 6 reference images each time, including:
  - Core references (前帧/正面照/远景)
  - Auxiliary references (expressions, actions, previous shots, related scenes, etc.)
- **Continuity Handling**: If current shot has continuity with previous shot (scene/character/camera related), add previous shot's 尾帧 to 前帧's reference images
- **Retry Strategy**: If regeneration needed, use existing successful related images as reference images

---

## Quality Check Key Points

### Scene Description Conformity (Most Critical 🔴)
- **Generated images must match the scene descriptions in storyboard**
- Check items (compare item by item):
  - Is scene environment correct (e.g., 农家院落, 篱笆, 土房, etc.)
  - Does character appearance match (age, hairstyle, clothing, posture, etc.)
  - Are character actions/postures correct (e.g., 拄竹竿, 眉头紧皱, etc.)
  - Are object details accurate (e.g., close-up items like 牛粪, 虫儿草, etc.)
  - Does lighting atmosphere match (e.g., 阴沉天色, 荒凉氛围, etc.)
- **If scene description doesn't match, must regenerate**

### Start/End Frame Correlation (Storyboard Specific 🔴)
- **前帧 and 尾帧 are consecutive frames of the same shot, must be highly correlated**
- Check items (side-by-side comparison):
  - Is scene environment consistent (same location, same angle)
  - Is character appearance consistent (hairstyle, clothing, age)
  - Are lighting and color tone consistent (can't jump from day to night)
  - Are actions continuous (continuation of 前帧 action, not sudden change)
  - Is camera angle consistent (can't jump from wide shot to close-up)
- Common issues: scene jumps, character costume changes, lighting jumps, camera cuts
- **If correlation is poor, must regenerate 尾帧** (using 前帧 as core reference)

### Character Age Consistency 🔴
- **Same character must have consistent age across different images**, cannot have ±5 years difference
- Check items: wrinkle depth, facial fullness, eye condition, hair graying level, facial bone structure
- During generation use same 正面照 as reference image; during check view 正面照 and derivative images side by side
- If inconsistency found, regenerate immediately

### Character/Animal Count and Identity Consistency 🔴
- **Characters/animals appearing in image must exactly match the count and specified characters in storyboard description**
- Check items:
  - Character count: Cannot have extra or missing characters (if storyboard says "三人" must be three people)
  - Specified characters: Must be characters clearly specified in storyboard (e.g., "李峰" not strangers)
  - Animal count: Animal type and count must match description (e.g., "一只黑猫" cannot become two cats)
  - Character traits: Age, gender, identity must match storyboard settings
- Common issues: extra passersby in background, missing specified characters, wrong animal count, character identity confusion
- **If inconsistency found, must regenerate**, ensure strict correspondence to storyboard description

### Art Style Consistency 🎨
- **Must conform to style.md settings**: line style, color matching, lighting effects, texture quality
- Same series of images (正面照/三视图/表情/动作) must have highly consistent art style
- Multiple angles of same scene should have coordinated art style
- Common issues: sudden color changes, inconsistent line thickness, mismatched styles

### Other Checks
- **Obvious Defects**: Generation distortion, anomalies, character deformities, etc.
- **Detail Completeness**: Are important props/items clearly visible

---

## Storyboard Generation Best Practices

### Core Principles
前帧 and 尾帧 are the beginning and end of the same shot, ensured through **single frame-by-frame generation + multiple reference images**:
- Visual continuity: Character appearance, scene style, lighting consistency
- Action fluidity: 尾帧 uses 前帧 as core reference to ensure smooth transition
- Spatial-temporal consistency: Through global style + chapter atmosphere integrated into prompts
- Generation quality: Single frame generation has higher quality than dual frame generation

### Reference Image Selection Strategy (Try to Fill 6 Images)

**前帧 Reference Images (Prioritized Order)**:
1. Character 正面照 appearing in the shot (corresponding age, 1-3 images)
2. Scene 远景 corresponding to the shot (corresponding season, 1 image)
3. 尾帧 of previous shot (if continuity exists, 1 image)
4. Character expression/action reference images (if special needs, 0-2 images)
5. Scene 中景/近景 (if special composition needs, 0-1 image)

**尾帧 Reference Images (Prioritized Order)**:
1. **前帧 of this shot** (required, first position, 1 image)
2. Character 正面照 appearing in the shot (corresponding age, 1-3 images)
3. Scene 远景 corresponding to the shot (corresponding season, 1 image)
4. Character expression/action reference images (if special needs, 0-2 images)

### Prompt Format (Single Frame Generation)

**Key Points** (English prompts recommended for better model performance):
- Use natural language description, like telling a story
- Scene description is the core content (280-320 words)
- Start frame and end frame must have strong continuity
- Include shot type, chapter atmosphere, and global style
- Total length ≤600 words per prompt

### Critical Considerations for Tool Integration 🎯

**Consistency Constraints (MUST be enforced in prompts)**:
- **Character Consistency Across Frames**:
  - Character age must remain stable (no ±5 years jumps between adjacent frames)
  - Character clothing/appearance state must be logically consistent with previous frame
  - If character has injuries, disabilities, or special states in current shot, must maintain them (don't suddenly heal or change without explanation)
  - Character positioning and perspective must evolve naturally (not teleport or appear without continuity)

- **Scene Environment Consistency**:
  - Scene location must be consistent between 前帧 and 尾帧 (no mysterious scene changes)
  - Lighting/time of day consistency (day/night, sunny/rainy) must match scene description
  - Seasonal context must remain consistent if specified
  - Environmental objects and their positions should be logically consistent
  
- **Temporal Logic** (Most Important 🔴):
  - 前帧 and 尾帧 are consecutive moments of the same shot - describe progression, not reset
  - If previous shot's 尾帧 exists, current 前帧 must logically follow it
  - Don't introduce new characters that weren't foreshadowed in scene description
  - Don't remove characters or objects that existed in 前帧
  
- **Prompt Emphasis for Tool**:
  - Add explicit instruction: *"This frame must logically follow [previous state]. Maintain consistency in character state, location, lighting. Do NOT create unrealistic jumps or contradictions."*
  - For derivative images (expressions, actions): *"Based on [base character front view], generate variation while maintaining age/identity."*

**Example (Based on 分镜001, English natural language)**:

**Start Frame:**
```
This is a wide shot capturing the full panorama of a dilapidated farmhouse courtyard. The scene shows a crude earthen house standing in the center, with collapsed fence walls scattered across the ground in disarray. In the distance, rolling mountains rise and fall against an overcast, gloomy sky that casts a somber mood over everything. On a small path to the right side of the frame, two small figures dressed in tattered, worn clothes are making their way towards the courtyard. The entire yard has a desolate, abandoned feel, with weeds growing wild throughout the space. This is the opening scene of the story, and the atmosphere is oppressive and heavy, setting a melancholic tone. The artwork combines the signature style of Japanese animator Makoto Shinkai with traditional Chinese classical artistic elements, featuring a gloomy color palette that emphasizes the desolate atmosphere. The composition uses strong contrasts between light and dark areas, with intricate attention to detail throughout, resulting in high-quality, exquisite artwork that draws viewers into this somber world.
```

**End Frame:**
```
[SAME SHOT CONTINUATION] This is the exact same wide shot of the farmhouse courtyard from the identical camera position and angle. The scene environment remains completely unchanged: same dilapidated earthen house in center, same collapsed fence walls, same rolling mountains in background, same overcast gloomy sky. Lighting conditions are identical to the start frame - same time of day, same atmospheric mood. The ONLY change is the character positioning: the two figures have now moved closer to the courtyard entrance - 田林 leaning on his bamboo pole is now more visible in the frame, with the elderly man slightly ahead. The fence and house door maintain their exact appearance and positions. Everything about the environment, lighting, weather, and composition remains consistent with the start frame. This is a fixed camera capturing character movement progression within the same continuous moment. The oppressive atmosphere persists unchanged. The artwork maintains the identical fusion of Makoto Shinkai's style with Chinese classical elements, with the same gloomy color palette, same light-dark contrasts, and consistent detail rendering throughout.
```

**Key Points**:
- Use complete sentences and natural flow, not fragmented phrases
- Describe the scene as if explaining it to someone who can't see it
- **🔴 CRITICAL: Start with "[SAME SHOT CONTINUATION]" in end frame prompts** to emphasize this is the same shot
- **Explicitly state "identical camera position/angle"** in end frame description
- **List what remains unchanged** (scene, lighting, weather, environment) before describing what changed
- **Only describe progressive changes**: character movement, camera movement (if any), or natural action progression
- Integrate style elements naturally into the description while maintaining consistency statements

### Generation Strategy
- **Generate by Storyboard Order**: Ensure can use previous shots as reference
- **前帧 in Batches, 尾帧 One by One**:
  - Can concurrently generate 3-5 shots' 前帧
  - After all 前帧 complete, generate corresponding 尾帧 one by one (or small batch concurrency)
- **Dynamic Reference Image Accumulation**: Subsequent shots can use previously generated shot 尾帧 as reference
