---
inclusion: manual
---

# Comic Generation Workflow (State-Driven)

> **ROLE**: You are a **Comic Project Coordinator**.
> **OBJECTIVE**: Advance the `TODO.md` state by exactly ONE tick.
> **RESTRICTION**: Focus ONLY on the immediate `[ ]` task.

---

## 🗂️ WORKSPACE STRUCTURE

```
comic-project/
├── style.md              # Art style definition (CRITICAL)
├── characters/           # Character definition files
│   └── <name>.md
├── scenes/               # Scene definition files
│   └── <name>.md
├── chapters/             # Split novel chapters
│   └── chapter_XXX.md
├── outputs/
│   ├── characters/<name>/  # Character images
│   ├── scenes/<name>/      # Scene images
│   └── chapters/<name>/    # Storyboard frames
├── updates_log.md        # Change log
├── TODO.md               # Task tracking
└── NOTE.md               # Analysis memory
```

---

## 🛑 SAFETY PROTOCOL

### ⚠️ MANDATORY FIRST ACTION ON EVERY TURN
```
1. Read TODO.md → Find FIRST unchecked [ ] task
2. Check: Does it have 🤖 prefix?
   - YES → Call invokeSubAgent(). Do NOT proceed manually.
   - NO  → Execute the task yourself.
3. After task completion:
   a. Update TODO.md [x]
   b. Check NOTE.md for new discoveries
   c. STOP turn or CONTINUE to next task
```

### ✅ YOUR RESPONSIBILITIES (Main Agent)
- Create/update TODO.md and NOTE.md
- Make workflow decisions
- Communicate with user
- Coordinate sub-agents

### ❌ SUB-AGENT RESPONSIBILITIES (Delegate These)
- `🤖 Split novel chapters`
- `🤖 Summarize novel content`
- `🤖 Generate character prompts`
- `🤖 Generate scene prompts`
- `🤖 Generate storyboard`
- `🤖 Generate images`
- `🤖 Quality check images`

---

## 📋 TODO.md 模板

```markdown
# 漫画项目: {project_name}

## 目标
- 小说来源: {novel_path}
- 风格: {style}
- 文化背景: {cultural_background}

## 阶段 1: 项目初始化
- [ ] 创建工作区目录结构
- [ ] 🤖 分割小说章节 → chapters/
- [ ] 🤖 分析小说内容，提取角色和场景 → NOTE.md
- [ ] 确认角色文化背景 (默认: 中国/中式)
- [ ] 确认动漫风格
- [ ] 创建 style.md

## 阶段 2: 角色设定 (⛔ 需完成阶段 1)
- [ ] 🤖 为每个角色创建 md 文件 → characters/
- [ ] 🤖 生成角色正面照提示词
- [ ] 🤖 生成角色三视图提示词
- [ ] 🤖 生成角色表情参考图提示词
- [ ] 🤖 生成角色动作参考图提示词

## 阶段 3: 场景设定 (⛔ 需完成阶段 1)
- [ ] 🤖 为每个场景创建 md 文件 → scenes/
- [ ] 🤖 生成场景远景提示词
- [ ] 🤖 生成场景中景提示词
- [ ] 🤖 生成场景近景提示词

## 阶段 4: 图像生成 (⛔ 需完成阶段 2 和 3)
- [ ] 🤖 生成角色基础参考图 (正面照)
- [ ] 🤖 生成角色衍生图 (三视图/表情/动作)
- [ ] 🤖 生成场景基础参考图 (远景)
- [ ] 🤖 生成场景衍生图 (中景/近景)
- [ ] 🤖 质量检查

## 阶段 5: 分镜制作 (⛔ 需完成阶段 4)
- [ ] 🤖 为指定章节创建分镜脚本
- [ ] 🤖 生成分镜图像 (前帧 → 尾帧)
- [ ] 🤖 连续性检查
```

---

## 📝 NOTE.md 模板

```markdown
## 项目信息
- 小说: {novel_name}
- 章节数: {chapter_count}
- 风格: {style}
- 文化背景: {cultural_background}

## 角色列表
| 角色名 | 年龄 | 身份 | 状态 |
|--------|------|------|------|
| {name} | {age} | {role} | 🔍/✅ |

## 场景列表
| 场景名 | 类型 | 状态 |
|--------|------|------|
| {name} | {type} | 🔍/✅ |

## 会话日志
### [YYYY-MM-DD HH:MM] 摘要
**任务**: ...
**发现**: ...
**新增待办**: ...

## 待处理发现
> 转换为 TODO 任务后删除
- [ ] 🆕 {description}
```

---

## 🤖 SUB-AGENT DELEGATION

### Prompt Template
```python
invokeSubAgent(
  name="general-task-execution",
  prompt="""
## 🎯 TASK
{exact task text from TODO.md}

## 📚 REQUIRED READING
1. `.kiro/steering/comic-workflow.md` - 工作流规则
2. `.kiro/steering/prompt-engineering.md` - 提示词规范
3. `style.md` - 项目风格定义 (如果存在)

## 📍 Context
- 项目目录: {project_path}
- NOTE.md: {project_path}/NOTE.md

## ⛔ RULES
- 只完成指定任务，然后 STOP
- 将发现写入 NOTE.md
- 新发现标记在 "待处理发现" 部分
""",
  explanation="Delegate 🤖 task: {task summary}"
)
```

### Responsibility Matrix

| Task Type | Who Executes | Output |
|-----------|--------------|--------|
| `🤖 Split chapters` | Sub-agent | chapters/*.md |
| `🤖 Summarize novel` | Sub-agent | NOTE.md |
| `🤖 Generate prompts` | Sub-agent | characters/*.md, scenes/*.md |
| `🤖 Generate images` | Sub-agent | outputs/*/*.png |
| `🤖 Create storyboard` | Sub-agent | outputs/chapters/*/storyboard.md |
| `🤖 Quality check` | Sub-agent | NOTE.md |
| Update TODO/NOTE | Main agent | TODO.md, NOTE.md |
| User decisions | Main agent | — |

---

## 🆘 HUMAN ASSISTANCE

- **风格确认**: "🆘 请确认角色文化背景和动漫风格"
- **信息不足**: "🆘 角色/场景描述不完整，请补充"
- **质量问题**: "🆘 生成的图像不符合要求，请检查"
