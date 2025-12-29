---
inclusion: always
---

# Prompt Engineering for Image Generation

## Rule
必须先使用pwd命令获取当前目录，防止输出到意外的目录中

## Reference Image Purpose Declaration (Critical)

**必须在提示词开头包含 (~80-100 词)** 以防止过度拟合:

### For Character Front Views
```
Reference images show character's identity, age, facial features, and overall appearance style ONLY. 
DO NOT copy pose, direction, or specific action from reference. 
Follow text prompt for actual pose and direction.
```

### For Scene Images
```
Reference images show location environment, architecture style, and spatial layout ONLY. 
DO NOT copy exact composition, camera angle, or lighting from reference. 
Follow text prompt for camera work and atmosphere.
```

### For Storyboard End Frames
```
Reference start frame for scene continuity and character state ONLY. 
Character direction, pose, and camera angle should progress according to text description, not stay frozen.
```

## Prompt Structure Templates

### Character Base Image (正面照)
```
[Subject description] + [Ethnic/cultural background] + [Age] + [Facial features] + 
[Hairstyle/color] + [Eye details] + [Body type] + [Clothing] + [Pose: standing neutral] + 
[Background: pure white] + [Art style] + [Quality keywords]
```

### Scene Wide Shot (远景)
```
[Scene type] + [Location description] + [Architectural style] + [Key elements] + 
[Lighting/time of day] + [Weather/atmosphere] + [Color palette] + 
[Art style] + [Quality keywords]
```

### Storyboard Frame
```
[Reference purpose declaration 80-100 words] + 
[Shot type 10 words] + 
[Spatial context from previous shot 30 words] + 
[Core scene description 230-270 words] + 
[Camera angle and character facing direction 30 words] + 
[Chapter atmosphere 60 words] + 
[Style integration 150-200 words]
```

## Style Integration (from style.md)

Must include these elements (150-200 words):
- Art style fusion description
- Color palette (2-3 dominant colors from current story phase)
- Lighting approach (single light source, contrast intensity)
- Line work standards (protagonist 2-3px, details 0.5-1px, background 0.25-0.5px)
- Composition philosophy (high contrast, clear focus, layered depth)

## Historical Figure Prompt Checklist

Before generating prompts for historical figures, verify:
- [ ] Historical identity clearly expressed (dynasty, position, status)
- [ ] Iconic physical features highlighted
- [ ] Power level expressed through temperament/clothing/gaze
- [ ] Representative events hinted at
- [ ] Era-appropriate visual characteristics
- [ ] Psychological complexity reflected
- [ ] Clothing accuracy for era and identity
- [ ] Cultural symbolic significance included
- [ ] Length controlled within limits

## Quality Keywords

### Chinese Prompts
```
高质量精细画面，线条清晰，色彩明亮，光影对比强烈
```

### English Prompts
```
high quality, detailed, sharp lines, vibrant colors, strong lighting contrast, 
masterpiece, best quality, highly detailed
```
