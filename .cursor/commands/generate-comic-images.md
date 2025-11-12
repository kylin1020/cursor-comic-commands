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
- **Spatial Logic Between Shots** (Critical 🔴):
  - **Analyze spatial relationships between consecutive shots** - characters cannot teleport, must move through space logically
  - If shot A shows character in courtyard, shot B cannot suddenly show them inside house without showing the transition (e.g., approaching door, entering)
  - **Track character positions and directions** across shots - if character moves towards an object, subsequent shots should respect that spatial relationship
  - **Camera perspective must respect spatial continuity** - if character is moving towards a location, they might be shot from behind (back view) with destination in background, not always facing camera
- **Physical and Directional Logic** (Critical 🔴):
  - **"Running towards X" does NOT always mean facing camera** - character may be shot from behind/side, with X visible in background/distance
  - **Object/destination placement must match action** - if character runs towards house, house should be in front of character in the frame, not behind
  - **Consider camera angle relative to action direction** - side view, back view, or front view each creates different spatial relationships
  - **Movement must respect physics** - characters cannot instantly change locations, speeds, or directions without logical progression
- **Read and Extract Key Information (Multi-level Fusion)**:
  - Read `style.md` to extract **comprehensive style elements** (≥150-200 characters):
    - Art style fusion description (Japanese Shinkai style specifics + Chinese ancient elements)
    - Color palette: Identify main colors for current story phase (Phase 1/2/3 from style.md)
    - Lighting approach: Single light source principle, contrast intensity, atmospheric effects
    - Line work standards: Stroke width hierarchy (main outline 2-3px, details 0.5-1px, background 0.25-0.5px)
    - Composition philosophy: High contrast, clear focus, layered depth, dramatic shadows
  - Read current chapter storyboard.md to extract **chapter atmosphere keywords** (emotion, color tone, pacing, environmental tone, period feel, etc., about 60 characters)
  - Read storyboard md to extract **scene descriptions** (this is core content, including scenes, characters, actions, expressions and other visual elements)
  - Read related character/scene md files to get **character/scene details** (appearance features, scene layout, etc.)
- Check for existing reference images in outputs directory to avoid duplicate generation

### Step 2: Optimize Prompts and Prepare Generation Parameters
- **Prompt Construction (Multi-level fusion, total length ≤900 Chinese characters)**:
  - **🔴 CRITICAL: Reference Image Purpose Declaration** (Must be included at prompt beginning, ~80-100 words):
    - **Explicitly state the purpose of EACH reference image** to prevent over-fitting
    - Character front views: "Reference images show character's identity, age, facial features, and overall appearance style ONLY. DO NOT copy pose, direction, or specific action from reference. Follow text prompt for actual pose and direction."
    - Scene images: "Reference images show location environment, architecture style, and spatial layout ONLY. DO NOT copy exact composition, camera angle, or lighting from reference. Follow text prompt for camera work and atmosphere."
    - Previous frame (for 尾帧): "Reference start frame for scene continuity and character state ONLY. Character direction, pose, and camera angle should progress according to text description, not stay frozen."
    - Expression/action references: "Reference for [specific purpose, e.g., emotional intensity, gesture style]. Adapt to current context per text prompt."
  - **Base Structure** (Characters/Scenes): `[Reference purpose declaration 80-100 words] + [Specific content description 450-500 words] + [Age/season annotation 20 words] + [Style integration from style.md 150-200 words]`
  - **Storyboard Structure** (Single frame generation, consecutive frames related):
    ```
    Start Frame: [Reference purpose declaration 80-100 words] + [Shot type 10 words] + [Spatial context from previous shot 30 words] + [Core scene description 230-270 words] + [Camera angle and character facing direction 30 words] + [Chapter atmosphere 60 words] + [Style integration from style.md 150-200 words]
    End Frame: [Reference purpose declaration 80-100 words] + [Shot type 10 words] + [Core scene description 250-290 words] + [SAME SHOT continuation emphasis 50 words] + [Chapter atmosphere 60 words] + [Style integration from style.md 150-200 words]
    ```
    - **🔴 End Frame MUST emphasize**: "Same shot continuation, maintaining identical scene, lighting, and atmosphere from start frame. Only [describe specific changes: character movement/camera adjustment/focal shift]."
    - **🔴 Start Frame MUST specify spatial logic**: 
      - Where is character relative to previous shot location (if applicable)
      - What direction is character facing/moving
      - Camera angle relative to character action (front view / side view / back view / over-shoulder / etc.)
      - Where are key objects/destinations in the frame relative to character
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
    - **Style integration from style.md must be COMPREHENSIVE**: Include art style features (Japanese Shinkai + Chinese ancient style fusion), color schemes (select main colors from current story phase), lighting effects (describe specific light sources and shadows), line texture quality, composition principles, visual tone
    - Chapter atmosphere can include emotional tone, color preferences, pacing feel, period sense, etc.
    - Age/season must be clearly marked (e.g., "少年时期", "秋季黄昏")
    - Fully utilize 900 character space, let model get richer information to generate high-quality images
- **Prepare Reference Images (max 6, try to fill up)**:
  - **🔴 CRITICAL**: When using reference images, **MUST declare their purpose in prompt** to prevent over-fitting (see Reference Purpose Declaration section)
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
**Character Images**: `outputs/characters/[角色名]/[类型].png` (类型: 正面照/三视图/表情参考/动作参考)
**Scene Images**: `outputs/scenes/[场景名]/[类型].png` (类型: 远景/中景/近景)
**Storyboard Images**: `outputs/chapters/[章节名]/[分镜号]-[分镜名称]_[帧号].png` (帧号: 1=前帧, 2=尾帧)

### General Rules
- Base reference images (正面照, 远景) **do not use** reference images, pure text generation
- Derivative images **must** use corresponding base reference images to ensure consistency
- **🔴 CRITICAL**: All prompts using reference images **MUST include Reference Purpose Declaration** at the beginning (~80-100 words) to prevent over-fitting and ensure model follows text instructions for pose/direction/angle
- All derivative images of the same character/scene use the same base reference image
- Automatically create directories if they don't exist
- File names strictly follow the above format to ensure clear file organization

### Storyboard Generation Special Rules
- **Sequential Frame Generation Principle**: Generate frames one by one, 前帧 first, then 尾帧
- **Frame Dependency**: 尾帧 generation MUST depend on the generated 前帧 image - 前帧 is passed as reference_images to ensure visual continuity
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
- **Detailed style.md compliance check**:
  - Line work: Verify protagonist has 2-3px sharp outlines, details 0.5-1px fine, background 0.25-0.5px soft
  - Color palette: Confirm 2-3 dominant colors match current story phase (Phase 1: gold/emerald/dark purple; Phase 2: grey/cyan/blood red; Phase 3: moonwhite/spirit blue/gold)
  - Lighting: Check for single light source principle, high contrast shadows, atmospheric depth
  - Art fusion: Identify Japanese Shinkai elements (delicate light effects, dreamy atmosphere) AND Chinese ancient elements (architecture, clothing, cultural aesthetics)
  - Composition: Verify high contrast framing, clear focal points, layered depth with dramatic shadows
- Same series of images (正面照/三视图/表情/动作) must have highly consistent art style
- Multiple angles of same scene should have coordinated art style
- Common issues: sudden color changes, inconsistent line thickness, mismatched styles, style fusion elements missing

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
- **🔴 MUST START with Reference Image Purpose Declaration** (~80-100 words) - this prevents model from over-fitting reference images
- Use natural language description, like telling a story
- Scene description is the core content (230-290 words, adjusted for reference purpose declaration)
- Start frame and end frame must have strong continuity
- Include shot type, chapter atmosphere, and comprehensive global style integration
- **Total length: 800-900 words per prompt** (increased from 600 to ensure style compliance)
- **CRITICAL**: Extract and integrate style.md elements:
  - Art style fusion: Japanese Shinkai + Chinese ancient elements
  - Color palette: Select 2-3 main colors from current story phase in style.md
  - Lighting: Describe specific light source, shadow depth, and atmosphere
  - Line work: Specify detail level (protagonist: 2-3px clear lines, details: 0.5-1px fine lines, background: 0.25-0.5px soft)
  - Composition: Mention high contrast, clear focal point, layered depth

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
  - **🔴 MUST BEGIN with Reference Purpose Declaration** (~80-100 words) specifying what each reference image provides and what it does NOT dictate
  - Add explicit instruction: *"This frame must logically follow [previous state]. Maintain consistency in character state, location, lighting. Do NOT create unrealistic jumps or contradictions."*
  - For derivative images (expressions, actions): *"REFERENCE PURPOSE: The character front view shows identity, age, and appearance style ONLY - do not copy pose or direction. Generate the described [expression/action] freely per text prompt."*
  - For storyboard frames: *"REFERENCE PURPOSES: [List each reference and its specific purpose]. Follow text description for actual pose, direction, camera angle, and composition."*

**Prompt Format Examples (with comprehensive style.md integration)**:
- **前帧**: `[Reference purpose declaration 80-100 words] + [Shot type] + [Scene/character/action details 230-270 words] + [Previous shot relation if any 50 words] + [Chapter atmosphere 60 words] + [Comprehensive style integration 180-220 words]`
- **尾帧**: `[Reference purpose declaration 80-100 words] + [SAME SHOT CONTINUATION] + [State unchanged elements] + [ONLY changed: character/camera progression] + [Chapter atmosphere 60 words] + [Comprehensive style integration 180-220 words]`

**Reference Purpose Declaration Examples**:
- For **前帧** with character + scene + previous frame:
  ```
  REFERENCE IMAGE PURPOSES: The provided character front view is for identity, age, and facial features reference ONLY - do not copy their pose or facing direction. The scene wide shot shows environment layout and architecture style ONLY - do not copy camera angle or exact composition. The previous frame shows continuity context ONLY - current shot should follow logically but with distinct camera positioning as described below. Follow the text description for all pose, direction, and camera work.
  ```
- For **尾帧** with start frame + character + scene:
  ```
  REFERENCE IMAGE PURPOSES: The start frame (first reference) shows scene environment, lighting, and character state to maintain continuity - character should progress naturally in pose and position as described, NOT stay frozen. Character front views are for identity consistency ONLY - adapt pose and direction per text. Scene image is for environment style ONLY. All composition and camera work must follow text description below.
  ```
- For **character derivative images** (expressions/actions) with front view:
  ```
  REFERENCE IMAGE PURPOSES: The character front view shows identity, age, facial structure, and appearance style for consistency ONLY. Generate the described [expression/action/pose] freely based on text prompt - do not rigidly copy the reference pose or angle.
  ```

**Style Integration Template** (Must extract from current story phase in style.md):
```
Art Style: [Japanese Shinkai distinctive features] + [Chinese ancient architectural/clothing elements]
Color Palette: [2-3 dominant colors from current phase] with supporting accent colors
Lighting: [Specific light source description], [shadow treatment], [atmospheric effects], [contrast intensity]
Line Work: Protagonist outlines 2-3px sharp and flowing, details 0.5-1px fine and precise, background 0.25-0.5px soft
Composition: [High contrast framing], [Clear focal point with emphasis], [Layered depth], [Dramatic shadow placement]
Visual Tone: [Emotional resonance], [Temporal/seasonal quality], [Cinematic atmosphere]
```

**Key Points**:
- **🔴 CRITICAL: Every prompt MUST start with Reference Purpose Declaration** (~80-100 words) to prevent over-fitting
- **🔴 尾帧必须以 "[SAME SHOT CONTINUATION]" 开头**（在 Reference Purpose Declaration 之后），强调是同一镜头
- **尾帧先说明不变的**（场景/光照/天气），再描述变化（角色移动/镜头调整）
- **Reference purpose must be specific**: State what each reference image provides (identity/environment/continuity) and what it does NOT dictate (pose/angle/direction)
- **Style integration must fill 180-220 words** - DO NOT use generic style phrases, extract SPECIFIC details from style.md
- Use natural language, complete sentences, not fragmented keywords
- **Ensure color palette is tied to story phase** (check style.md Phase 1/2/3 colors)

### Generation Strategy
- **Generate by Storyboard Order**: Ensure can use previous shots as reference
- **前帧 in Batches, 尾帧 One by One**:
  - Can concurrently generate 3-5 shots' 前帧
  - After all 前帧 complete, generate corresponding 尾帧 one by one (or small batch concurrency)
- **Dynamic Reference Image Accumulation**: Subsequent shots can use previously generated shot 尾帧 as reference
