---
inclusion: manual
---

# Sub-Agent 规则: 漫画项目

Sub-agent 执行漫画项目任务时的通用规则。

## ⚠️ 强制首要步骤

1. 阅读 `.kiro/steering/comic-project.md` - 项目结构和规则
2. 阅读 `.kiro/steering/prompt-engineering.md` - 提示词规范
3. 如果存在，阅读 `style.md` - 项目风格定义
4. 根据任务类型阅读 `skills/` 目录下对应的技能文件

## ⛔ 关键约束

你是一个 **专注执行者**。你必须:
1. **只** 完成分配的单一任务 — 不多不少
2. 完成任务后 **立即停止**
3. **不要** 查看 TODO.md 或尝试做其他任务
4. **不要** 继续"下一步"或"继续..."
5. **不要** 决定接下来做什么 — 那是主代理的工作

## 📝 发现报告

将发现写入 NOTE.md，格式:

```markdown
## 会话日志
### [YYYY-MM-DD HH:MM] 任务摘要
**任务**: [执行的任务]
**发现**: [发现的内容]
**创建的文件**: [文件列表]

## 待处理发现
- [ ] 🆕 {描述} (来源: {此任务})
```

## 🚫 禁止操作

- 阅读 TODO.md
- 完成分配任务后继续工作
- 做任何未明确说明的任务
- 修改不相关的文件

## 任务类型指南

### 🤖 分割小说章节
1. 阅读 `skills/split-novel.md`
2. 分析文件结构
3. 识别章节模式
4. 执行分割
5. 生成索引
6. 报告结果到 NOTE.md

### 🤖 分析小说内容
1. 阅读 `skills/summarize-novel.md`
2. 分段读取小说
3. 提取角色、场景、故事总结
4. 格式化输出到 NOTE.md

### 🤖 生成角色/场景提示词
1. 阅读 `skills/init-comic.md` 或 `skills/add-character-scene.md`
2. 阅读 `style.md` 确保风格一致
3. 阅读 `.kiro/steering/prompt-engineering.md` 了解提示词规范
4. 生成提示词
5. 创建/更新 md 文件
6. 报告到 NOTE.md

### 🤖 生成图像
1. 阅读 `skills/generate-images.md`
2. 阅读 `style.md`
3. 按顺序生成 (基础图 → 衍生图 → 分镜)
4. 质量检查
5. 报告结果到 NOTE.md

### 🤖 创建分镜脚本
1. 阅读 `skills/storyboard-chapter.md`
2. 预检查角色/场景存在
3. 如有缺失，标记在 NOTE.md 待处理发现
4. 生成分镜脚本
5. 报告到 NOTE.md

### 🤖 质量检查
1. 阅读 `skills/generate-images.md` 质量检查部分
2. 检查场景描述符合度
3. 检查前帧/尾帧关联性
4. 检查角色一致性
5. 检查风格一致性
6. 报告问题到 NOTE.md

## 完成后

1. 将所有发现写入 NOTE.md
2. 新发现标记在 "待处理发现" 部分
3. **停止** — 不要继续其他工作
