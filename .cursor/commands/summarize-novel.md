# summarize-novel

## 📋 Task Checklist

When executing this command, complete tasks in the following order and check off each completed item:

### Stage 1: Reading and Analysis
- [ ] Confirm novel file path: Ask user to provide novel txt file path
- [ ] Read novel content: Use segmented reading to avoid exceeding context limits (if file is too large)
- [ ] Initial scan: Understand novel's overall structure, length and chapter count

### Stage 2: Content Extraction
- [ ] Extract story summary: Analyze entire story's theme, main plot, conflict, climax and ending direction (300-500 chars)
- [ ] Extract main characters: Identify 3-8 main characters, record each character's appearance, personality, clothing, age, relationships, etc.
- [ ] Extract main scenes: Identify repeatedly appearing or important scenes and locations in story, record environmental features and atmosphere

### Stage 3: Formatted Output
- [ ] Generate structured output: Organize all extracted information according to standard format
- [ ] Verify completeness: Ensure all key information is included and clearly described
- [ ] Display output results: Show formatted content to user for easy copying

---

## 执行说明

这个命令用于分析小说内容，提取关键信息并输出格式化的总结，供后续 `init-comic` 命令使用。

### 第一步：获取小说文件

询问用户提供小说txt文件的完整路径。

**注意**：
- 如果文件非常大（超过100章或500KB），建议分段读取
- 可以先读取开头部分了解角色和场景，再读取中间和结尾了解故事发展和结局
- 不要一次性读取整个超大文件

### 第二步：分析提取信息

从小说中提取以下内容：

#### 1. 故事总结（300-500字）
包含：
- **故事主题**：这个故事讲述的核心思想或情感
- **主要情节**：故事的起承转合，主要冲突和矛盾
- **结局方向**：故事的结局走向（如果小说未完结，则总结当前进展）
- **故事基调**：悲剧、喜剧、温馨、热血、悬疑等

#### 2. 主要角色（3-8个）
每个角色需要提取：
- **姓名**：角色的名字（如果有昵称也记录）
- **年龄/性别**：大致年龄段和性别
- **外貌特征**：
  - 发型和发色
  - 眼睛颜色和形状
  - 脸型和身材
  - 身高体型
  - 特殊标记（疤痕、痣、纹身等）
- **服装风格**：
  - 日常穿着风格
  - 标志性服装
  - 配饰（眼镜、帽子、首饰等）
- **性格特点**：3-5个关键性格标签，如开朗、冷静、暴躁、温柔等
- **角色关系**：与其他主要角色的关系
- **角色定位**：主角、配角、反派等

**提取技巧**：
- 关注小说中对角色外貌的直接描写
- 从对话和行为中推断性格特点
- 注意角色的服装描述和穿着习惯
- 如果小说中没有明确描述某些外貌特征（如眼睛颜色），可以根据角色设定和故事背景合理推断，但要标注"推断"

#### 3. 主要场景（3-10个）
每个场景需要提取：
- **场景名称**：简短的场景名字（如"主角的家"、"学校教室"、"城市街道"等）
- **场景描述**：
  - 场景的整体环境（室内/室外、时代背景、地理位置）
  - 关键元素和特征（家具、建筑、植物、道具等）
  - 光线和氛围（明亮/昏暗、温馨/冷清等）
  - 色调和风格（现代/古代、都市/乡村等）
- **重要程度**：这个场景在故事中出现的频率和重要性

**提取技巧**：
- 优先提取反复出现的场景
- 关注重要剧情发生的场景
- 注意场景的细节描写
- 如果某个场景描述不够详细，可以根据场景类型添加常见元素，但要标注"标准化描述"

### 第三步：生成标准化输出

将提取的信息按照以下格式整理并输出：

```
=================================
漫画项目初始化信息
=================================

【故事总结】
[300-500字的故事总结，包含主题、主线、冲突、结局方向]

【主要角色】

1. 角色名：[姓名]
   - 年龄/性别：[年龄] / [性别]
   - 外貌特征：
     * 发型发色：[描述]
     * 眼睛：[描述]
     * 脸型身材：[描述]
     * 身高体型：[描述]
     * 特殊标记：[描述或"无"]
   - 服装风格：
     * 日常穿着：[描述]
     * 标志性服装：[描述]
     * 配饰：[描述或"无"]
   - 性格特点：[3-5个关键词]
   - 角色关系：[与其他角色的关系]
   - 角色定位：[主角/配角/反派等]

2. 角色名：[姓名]
   [同上格式]

[重复3-8个角色]

【主要场景】

1. 场景名：[场景名称]
   - 场景描述：[详细描述环境、元素、氛围]
   - 光线氛围：[明暗、色调、情绪]
   - 重要程度：[高/中/低]

2. 场景名：[场景名称]
   [同上格式]

[重复3-10个场景]

=================================
以上信息可直接复制给 init-comic 命令使用
=================================
```

1. **信息提取原则**：
   - 优先使用小说中的直接描写
   - 对于缺失的信息，可以合理推断，但要标注
   - 如果某些角色或场景描述不够详细，可以根据常见设定补充，但要标注"标准化描述"或"推断"

2. **角色和场景数量**：
   - 角色不少于3个，不超过8个（超过8个会导致后续工作量过大）
   - 场景不少于3个，不超过10个
   - 如果小说角色/场景过多，优先选择最重要和出现频率最高的

3. **输出格式**：
   - 严格按照模板格式输出
   - 使用清晰的分隔符便于复制
   - 所有信息都要填写完整，不要留空

4. **验证完整性**：
   - 每个角色至少有3个可视化特征（发型、眼睛、服装等）
   - 每个场景至少有环境描述和氛围描述
   - 故事总结要能让读者理解故事的核心内容

