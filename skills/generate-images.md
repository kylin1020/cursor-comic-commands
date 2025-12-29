---
inclusion: manual
---

# 技能: 生成漫画图像

批量生成角色参考图、场景参考图和分镜图像。

## 触发条件
- 项目已初始化，角色/场景文件已创建
- 需要生成 AI 图像

## 生成顺序 (必须遵循)

### 第一轮: 基础参考图 (不使用参考图)
- 角色正面照 (front_view.png)
- 场景远景 (wide_shot.png)

### 第二轮: 衍生图像 (使用基础参考图)
- 角色三视图 (three_views.png)
- 角色表情参考图 (expressions.png)
- 角色动作参考图 (actions.png)
- 场景中景 (medium_shot.png)
- 场景近景 (close_up.png)

### 第三轮: 分镜图像 (按分镜顺序)
- 前帧 (start frame) 先生成
- 尾帧 (end frame) 必须使用前帧作为参考

## 输出路径规范

```
outputs/
├── characters/[角色名]/
│   ├── front_view.png      # 正面照
│   ├── three_views.png     # 三视图
│   ├── expressions.png     # 表情参考图
│   └── actions.png         # 动作参考图
├── scenes/[场景名]/
│   ├── wide_shot.png       # 远景
│   ├── medium_shot.png     # 中景
│   └── close_up.png        # 近景
└── chapters/[章节名]/
    └── [分镜号]-[分镜名称]_[帧号].png
```

## 提示词构建

### 基础结构 (角色/场景)
```
[参考图用途声明 80-100词] + 
[具体内容描述 450-500词] + 
[年龄/季节标注 20词] + 
[style.md风格整合 150-200词]
```

### 分镜结构
```
前帧: [参考图用途声明] + [镜头类型] + [空间上下文] + 
      [核心场景描述] + [镜头角度] + [章节氛围] + [风格整合]

尾帧: [参考图用途声明] + [同一镜头延续] + [不变元素] + 
      [变化描述] + [章节氛围] + [风格整合]
```

## 参考图用途声明 (关键!)

### 角色正面照参考
```
Reference images show character's identity, age, facial features, 
and overall appearance style ONLY. DO NOT copy pose, direction, 
or specific action from reference. Follow text prompt for actual 
pose and direction.
```

### 场景参考
```
Reference images show location environment, architecture style, 
and spatial layout ONLY. DO NOT copy exact composition, camera 
angle, or lighting from reference. Follow text prompt for camera 
work and atmosphere.
```

### 分镜尾帧参考
```
Reference start frame for scene continuity and character state ONLY. 
Character direction, pose, and camera angle should progress according 
to text description, not stay frozen.
```

## 参考图选择策略

### 前帧参考图 (最多6张，优先级排序)
1. 出镜角色的正面照 (对应年龄，1-3张)
2. 对应场景的远景 (对应季节，1张)
3. 上一镜头的尾帧 (如有连续性，1张)
4. 角色表情/动作参考图 (如有特殊需求，0-2张)

### 尾帧参考图 (最多6张，优先级排序)
1. **本镜头的前帧** (必需，第一位，1张)
2. 出镜角色的正面照 (对应年龄，1-3张)
3. 对应场景的远景 (对应季节，1张)
4. 相关参考图 (0-1张)

## 质量检查要点

### 场景描述符合度 (最关键 🔴)
- 场景环境是否正确
- 角色外貌是否匹配
- 角色动作/姿势是否正确
- 物品细节是否准确
- 光线氛围是否匹配

### 前帧/尾帧关联性 (分镜专用 🔴)
- 场景环境是否一致 (同一地点、同一角度)
- 角色外貌是否一致 (发型、服装、年龄)
- 光线色调是否一致 (不能从白天跳到黑夜)
- 动作是否连续 (前帧动作的延续，不是突然变化)
- 镜头角度是否一致 (不能从远景跳到特写)

### 角色年龄一致性 🔴
- 同一角色在不同图像中年龄一致
- 检查: 皱纹深度、面部丰满度、眼睛状态、头发灰白程度

### 角色/动物数量一致性 🔴
- 图像中出现的角色/动物必须与分镜描述完全匹配
- 不能多人、少人、错人

### 艺术风格一致性 🎨
- 必须符合 style.md 设定
- 线条风格、色彩搭配、光影效果、质感品质

## 生成策略

- **按分镜顺序生成**: 确保可以使用前面镜头作为参考
- **前帧批量，尾帧逐个**: 可并发生成3-5个镜头的前帧，尾帧需等待对应前帧完成
- **动态参考图积累**: 后续镜头可使用之前生成的镜头尾帧作为参考

## 重试策略

如需重新生成:
- 使用已成功的相关图像作为参考图
- 调整提示词中的问题描述
- 确保参考图用途声明正确
