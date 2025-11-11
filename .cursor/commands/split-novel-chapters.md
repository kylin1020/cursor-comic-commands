# split-novel-chapters

## 📋 Task Checklist

When executing this command, complete tasks in the following order and check off each completed item:

### Stage 1: File Reading and Analysis
- [ ] Receive input file: Confirm txt file path provided by user, read file content
- [ ] Detect file encoding: Automatically detect file encoding (UTF-8, GBK, GB2312, etc.)
- [ ] Preview file structure: Display first 50-100 lines of file to let user understand file structure
- [ ] Identify chapter pattern: Analyze and identify chapter delimiter patterns (第X章, Chapter X, 卷X, special delimiters, etc.)
- [ ] Display recognition results: List first 5-10 recognized chapter titles for user confirmation

### Stage 2: Confirm Splitting Strategy
- [ ] Confirm chapter recognition: Ask user if recognized chapters are correct
- [ ] Adjust recognition rules: If incorrect, let user provide correct chapter examples or custom regular expressions
- [ ] Estimate splitting results: Inform user how many files will be generated and file naming rules
- [ ] Confirm output directory: Confirm output location for chapter files (default is `chapters/` directory)

### Stage 3: Generate and Execute Splitting Script
- [ ] Dynamically generate script: Generate dedicated Python/Bash splitting script based on recognized chapter format
- [ ] Create output directory: Create `chapters/` directory in working directory (if not exist)
- [ ] Execute splitting operation: Run generated script to split txt into independent .md files by chapter
- [ ] Standardize filenames: Ensure filenames are named according to chapter order (e.g., `chapter_001.md`, `chapter_002.md`, etc.)

### Stage 4: Verification and Finishing
- [ ] Verify output results: Check number of generated files and content completeness
- [ ] Display splitting results: List all generated chapter files and their titles
- [ ] Generate index file: Create `chapters/README.md` containing table of contents index for all chapters
- [ ] Clean temporary files: Delete scripts and temporary files generated during process
- [ ] Provide follow-up suggestions: Inform user they can use `/summarize-novel` command to continue processing

---

## Execution Instructions

I need you to help me split a novel txt file by chapters into independent .md files.

**⚠️ Important Note**:
Since each novel txt file's format may be completely different, this command uses an "analyze-confirm-dynamically generate script" approach rather than using a preset fixed script. This ensures splitting accuracy.

### Step 1: Provide File Path and Read Content

Please provide the path to the novel txt file (can be relative or absolute path).

**Examples**:
- `/Users/kylin/projects/novel.txt`
- `./novel.txt`
- `小说名称.txt`

I will first read the first 50-100 lines of the file and show you the file structure.

### Step 2: Analyze and Identify Chapter Structure

I will try to identify the following common chapter delimiter patterns:

1. **Numeric Chapter Formats**:
   - `第一章`, `第二章`, `第三章`... (Chinese numbers)
   - `第1章`, `第2章`, `第3章`... (Arabic numbers)
   - `第001章`, `第002章`... (with zero padding)

2. **English Chapter Formats**:
   - `Chapter 1`, `Chapter 2`...
   - `CHAPTER ONE`, `CHAPTER TWO`...

3. **Volume/Part Formats**:
   - `第一卷`, `第二卷`...
   - `第一部分`, `第二部分`...

4. **Mixed Formats**:
   - `第一章 标题名称`
   - `Chapter 1: 标题名称`
   - `001 标题名称`

5. **Custom Delimiters**:
   - User can specify specific regular expressions or delimiters

### Step 3: Confirm Delimiter Rules and View Preview

After analysis completes, I will display:
- Number of chapters recognized
- Title examples of first 5-10 chapters
- Delimiter rules used (regular expressions)

**If recognition is accurate**:
- Directly confirm and proceed to next step

**If recognition is inaccurate**, you can:
1. Provide several correct chapter title examples
2. Tell me characteristics of chapter titles (e.g., each chapter title starts with "==", or blank line followed by number)
3. If familiar with regular expressions, can directly provide regex pattern
4. Describe delimiter characteristics between chapters

### Step 4: Dynamically Generate and Execute Splitting Script

Based on confirmed chapter format, I will:
1. **Dynamically generate dedicated Python script** (or Bash script), customized for your txt file format
2. Create `chapters/` folder in current directory (if not exist)
3. Execute script to save each chapter as independent `.md` file
4. File naming format: `chapter_001.md`, `chapter_002.md`... (three digits for easy sorting)
5. Each file's top contains chapter title as Markdown level-1 heading

**Script Characteristics**:
- Customized based on actual format, not generic template
- Handle file encoding issues (automatically detect UTF-8/GBK, etc.)
- Intelligently handle blank lines and format issues
- Automatically clean up after execution completes

### Step 5: Verify and Generate Index

After splitting completes, I will:
1. Verify generated file completeness
2. Display all chapter file lists
3. Automatically generate `chapters/README.md` index file, containing:
   - Chapter total count statistics
   - Table of contents list for all chapters (with titles and file links)
   - Word count statistics for each chapter (optional)
4. Clean up temporarily generated script files

---

## 🔧 Dynamic Script Generation Instructions

### Core Philosophy: Customization on Demand, Not Generic Template

This command **does not use preset fixed scripts**, but **dynamically generates dedicated splitting scripts** based on your txt file's actual format.

### Why Dynamic Generation?

Novel txt file formats vary greatly:
- Some use "第一章", some use "Chapter 1"
- Some chapter titles occupy one line alone, some have decorative symbols before and after (like "===第一章===")
- Some have blank line separators, some are compactly arranged
- Some encoding is UTF-8, some is GBK
- Some have table of contents index, some don't

**Fixed scripts cannot handle all situations**, only by analyzing actual files and generating targeted scripts can splitting accuracy be guaranteed.

### Script Generation Process

1. **Read and Analyze**: Read first 100 lines of txt file, analyze chapter patterns
2. **Pattern Recognition**: Use regular expressions to match chapter titles
3. **User Confirmation**: Display recognition results to ensure accuracy
4. **Generate Script**: Based on confirmed patterns, generate customized Python or Bash script
5. **Execute Splitting**: Run script to complete splitting
6. **Clean Environment**: Delete temporary script files

### Functions Usually Included in Script

Based on actual needs, generated script may include:

1. **Encoding Detection**: Automatically detect and correctly read file encoding
2. **Chapter Recognition**: Use customized regular expressions to match chapters
3. **Content Extraction**: Extract complete content of each chapter
4. **Format Cleaning**: Remove excess blank lines, standardize format
5. **File Output**: Generate .md files in order
6. **Error Handling**: Handle boundary cases and exceptions

### Tool Selection

- **Python Script**: Suitable for complex formats, needs encoding handling, regex matching, etc.
- **Bash Script**: Suitable for simple fixed formats, uses `csplit`, `awk`, etc.
- **Hybrid Solution**: Combine multiple tools in complex situations

### Example: Processing Methods for Different Formats

**Format 1: Standard Chapter Format**
```
第一章 开端
正文内容...

第二章 发展
正文内容...
```
→ Use simple regex matching `^第.+章`

**Format 2: Decorative Format**
```
============
  第001章
============
正文内容...
```
→ Need to recognize decorative symbols, may need multi-line matching

**Format 3: Mixed Format**
```
Chapter 1: 开端

正文内容...

--- Chapter 2: 发展 ---
正文内容...
```
→ Need flexible regular expressions to handle irregular patterns

---

## 📌 Common Issue Handling

### Issue 1: Chapter Recognition Inaccurate

**Cause**: Novel format is non-standard, chapter markers are inconsistent

**Solutions**:
1. Let user provide several actual chapter title examples
2. Customize regular expression based on examples
3. If chapter markers are completely irregular, recommend user manually annotate before splitting

### Issue 2: File Encoding Error

**Cause**: txt file may use GBK, GB2312, etc. encoding

**Solutions**:
1. Use `chardet` library to automatically detect encoding
2. Prompt user to convert file encoding to UTF-8
3. Script automatically tries multiple encoding methods

### Issue 3: Chapter Content Missing

**Cause**: Some chapters may only have titles without content

**Solutions**:
1. Keep these chapter files during generation, mark as "待补充" (to be supplemented)
2. Specially annotate in index file
3. Remind user to check original file

### Issue 4: Filename Conflict

**Cause**: Target directory already has files with same name

**Solutions**:
1. Ask user whether to overwrite
2. Provide backup option
3. Or add timestamp to avoid conflict

---

## Output Example

### Successful Output Example:

```
✅ Chapter splitting completed!

📊 Statistics:
- Original file: novel.txt (1.2 MB)
- Recognized chapters: 156 chapters
- Output directory: chapters/
- Generated files: 156 .md files
- Index file: chapters/README.md

📁 Output file list (first 10):
  chapter_001.md - 第一章 开端
  chapter_002.md - 第二章 相遇
  chapter_003.md - 第三章 转折
  chapter_004.md - 第四章 冲突
  chapter_005.md - 第五章 发展
  ...
  chapter_156.md - 第一百五十六章 终章

💡 Next step suggestions:
1. View chapters/README.md to browse complete chapter directory
2. Use /summarize-novel command to analyze novel content
3. Use /init-comic command to initialize comic project
```

---

## 💡 Usage Suggestions

### Recommended Workflow

1. **Step 1**: Use this command (`/split-novel-chapters`) to split txt file
2. **Step 2**: Use `/summarize-novel` command to analyze split chapters, extract characters and scenes
3. **Step 3**: Use `/init-comic` command to initialize comic project
4. **Step 4**: Use `/generate-comic-images` command to generate character and scene images

### Notes

1. **Original File Backup**: Recommend backing up original txt file before splitting
2. **Chapter Completeness**: Check if first and last chapters are complete after splitting
3. **Special Character Handling**: Special characters in filenames will be replaced with underscores
4. **Large File Processing**: For very large files (>10MB), splitting may take seconds to tens of seconds

### File Naming Rules

- **Default Format**: `chapter_001.md`, `chapter_002.md`...
- **With Title Format** (optional): `chapter_001_开端.md`, `chapter_002_相遇.md`...
- **Keep Concise**: Avoid overly long filenames, save title information in file content

---

## 🛠️ Technical Details

### Supported File Encodings
- UTF-8 (recommended)
- UTF-8 with BOM
- GBK / GB2312 (Simplified Chinese)
- Big5 (Traditional Chinese)

### Chapter Recognition Regular Expression Examples

```python
# Chinese number chapters
r'^第[一二三四五六七八九十百千零0-9]+章'

# Arabic number chapters
r'^第\s*\d+\s*章'

# English chapters
r'^Chapter\s+\d+'

# Volumes/parts
r'^第[一二三四五六七八九十百千零0-9]+[卷部]'

# Chapters with titles
r'^第\d+章\s+.+'
```

### Output File Format

Format of each chapter file:

```markdown
# 第一章 开端

（章节内容从这里开始...）
```

---

## 🎯 Summary

This command is specifically designed for preprocessing novel txt files and is the first step in the entire comic production workflow. It can:

✅ Intelligently recognize multiple chapter formats
✅ Automatically split and standardize naming
✅ Generate chapter index for easy management
✅ Prepare for subsequent workflow

After completing splitting, you can use other commands to continue processing!

