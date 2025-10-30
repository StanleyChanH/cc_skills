# CC Skills 技能仓库

从官方文档自动生成的 Claude Skills 精选集合，可立即使用。

## 📋 项目概述

本仓库包含自动生成的 Claude Skills，为各种框架和库提供全面的帮助。每个技能都基于官方文档创建，包括：

- 完整的参考文档
- 带语法高亮的代码示例
- 快速参考模式
- 易于导航的组织结构

## 🚀 可用技能

### [CrewAI](./Crewai/crewai/SKILL.md)
**版本：** 1.0.0
**生成时间：** 2025年10月30日
**文档大小：** ~10MB

在使用 CrewAI 时使用此技能 - 一个用于构建多代理 AI 系统的框架。有助于创建 AI 代理、定义任务、管理工作流和协调多代理协作。

**功能特性：**
- 多代理系统开发
- 任务管理和工作流编排
- 全面的 API 文档
- 高级指南和示例
- 企业部署模式

**文档结构：**
- `getting_started.md` - 介绍和基本概念
- `api.md` - 完整的 API 参考
- `guides.md` - 分步教程
- `advanced.md` - 高级模式和技巧
- `enterprise.md` - 企业部署和扩展
- `tools.md` - 可用工具和集成

## 📁 仓库结构

```
cc_skills/
├── Crewai/
│   └── crewai/
│       ├── SKILL.md              # 主要技能文件
│       ├── references/           # 全面的文档
│       │   ├── advanced.md
│       │   ├── api.md
│       │   ├── concepts.md
│       │   ├── enterprise.md
│       │   ├── getting_started.md
│       │   ├── guides.md
│       │   ├── tools.md
│       │   └── ...
│       ├── assets/              # 模板和示例
│       └── scripts/             # 辅助脚本
├── README.md                    # 英文说明
└── README_cn.md                 # 中文说明（本文件）
```

## 🔧 使用方法

### 安装步骤
1. 克隆此仓库：
   ```bash
   git clone https://github.com/StanleyChanH/cc_skills.git
   cd cc_skills
   ```

## 📦 安装方法

有**两种方法**可以在 Claude 中使用这些技能：

### 方法一：上传 ZIP 文件到 Claude（推荐）

**适用场景：** 快速测试、一次性使用、或不想在本地修改文件时

**步骤：**
1. **下载所需技能的 ZIP 文件**：
   - CrewAI：从仓库下载 `Crewai/crewai.zip`
   - 可以直接从 GitHub 下载，或使用：
     ```bash
     # 如果已克隆仓库
     cp Crewai/crewai.zip ~/Downloads/crewai.zip
     ```

2. **上传到 Claude**：
   - 打开 Claude Code 或 Claude.ai
   - 将 `.zip` 文件拖拽到聊天窗口中
   - 或使用上传按钮/附加文件选项

3. **使用技能**：
   - Claude 会自动解压并加载技能
   - 立即开始提问使用
   - 示例："帮我创建一个用于数据分析的 CrewAI 代理"

**优势：**
- ✅ 无需本地文件设置
- ✅ 上传后立即可用
- ✅ 非常适合测试和探索
- ✅ 无破坏本地文件的风险

### 方法二：复制到 Claude 技能目录

**适用场景：** 永久安装、频繁使用、自定义修改

**步骤：**
1. **定位 Claude 技能目录**：
   ```bash
   # 技能目录通常位于：
   ~/.claude/skills/
   ```

2. **复制技能文件夹**：
   ```bash
   # 如果技能目录不存在，创建它
   mkdir -p ~/.claude/skills/

   # 复制 CrewAI 技能
   cp -r Crewai/crewai ~/.claude/skills/
   ```

3. **验证安装**：
   ```bash
   # 检查技能是否正确安装
   ls ~/.claude/skills/crewai/
   # 应该显示：SKILL.md, references/, assets/, scripts/
   ```

4. **使用技能**：
   - 打开 Claude Code
   - 直接使用技能名称：`/skill crewai`
   - 或直接开始询问有关 CrewAI 的问题

**优势：**
- ✅ 永久安装
- ✅ 在所有 Claude 会话中可用
- ✅ 可以修改和自定义文件
- ✅ 首次使用后加载更快
- ✅ 安装后可离线工作

## 🚀 使用技能

### 使用 CrewAI 技能

**基本使用示例：**
```bash
# 安装后，您可以询问：
"帮我创建一个用于数据分析的多代理系统"
"如何在 CrewAI 中定义任务？"
"展示代理角色定义的示例"
"工作流编排的最佳实践是什么？"
```

**访问文档：**
- 技能包含 `references/` 中的全面文档
- 询问 Claude"显示入门指南"或"参考 API 文档"
- 所有示例和指南都可通过自然语言查询访问

### 技能结构概览
每个技能包含：
- **SKILL.md**：包含使用说明和元数据的主要技能文件
- **references/**：从官方来源提取的完整文档
  - `getting_started.md` - 介绍和基本概念
  - `api.md` - 完整的 API 参考
  - `guides.md` - 分步教程
  - `advanced.md` - 高级模式和技巧
  - `enterprise.md` - 企业部署和扩展
  - `tools.md` - 可用工具和集成
- **assets/**：模板、样板代码和示例
- **scripts/**：自动化辅助工具

### 初学者指南
1. **从方法一开始**（ZIP 上传）进行测试
2. 使用 `getting_started.md` 参考文件了解基础概念
3. 询问简单问题，如"什么是 CrewAI？"或"代理如何工作？"
4. 探索 assets/ 目录中的示例

### 高级用户指南
1. **使用方法二**（本地安装）获得永久访问
2. 深入研究 `advanced.md` 和 `api.md` 获取详细信息
3. 查看 `enterprise.md` 了解部署模式
4. 使用 scripts/ 进行自动化任务
5. 根据需要修改和自定义技能文件

## 🔧 故障排除

### ZIP 上传问题
- **问题：** Claude 上传后无法识别技能
- **解决方案：** 确保 ZIP 文件包含正确的结构，SKILL.md 在根目录
- **替代方案：** 尝试解压 ZIP 并直接上传文件夹

### 本地安装问题
- **问题：** 在 ~/.claude/skills/ 中找不到技能
- **解决方案：**
  1. 验证目录路径：`ls ~/.claude/skills/`
  2. 检查权限：`ls -la ~/.claude/skills/crewai/`
  3. 确保 SKILL.md 存在：`test -f ~/.claude/skills/crewai/SKILL.md`

### 性能问题
- **问题：** 技能加载缓慢
- **解决方案：** 大型文档文件（如这个 10MB 的 CrewAI 技能）可能需要时间来索引
- **提示：** 在首次加载后给 Claude 几分钟时间处理文档

## 📊 技能信息

| 技能 | 版本 | 生成时间 | 大小 | 状态 |
|------|------|----------|------|------|
| CrewAI | 1.0.0 | 2025-10-30 | ~10MB | ✅ 活跃 |

## 🔄 更新技能

要使用最新文档更新技能：

1. 检查其 SKILL.md 文件中的技能版本
2. 使用相同配置重新运行文档抓取器
3. 技能将使用最新信息重建
4. 更新版本号和生成日期

## 🤝 贡献指南

欢迎贡献！您可以通过以下方式帮助：

- 为其他框架添加新技能
- 改进现有文档
- 添加更多示例和模板
- 报告问题或提出改进建议

### 添加新技能

1. 在项目根目录下创建新目录
2. 遵循与现有技能相同的结构
3. 包含全面的 SKILL.md 文件
4. 在 references/ 中添加有组织的文档
5. 在此 README 中更新您的技能信息

## 📝 许可证

本仓库包含从官方文档生成的技能。每个技能可能有自己的许可条款。请查看各个技能文档以了解具体的许可信息。

## 🔗 相关链接

- **GitHub 仓库：** https://github.com/StanleyChanH/cc_skills
- **Claude Code 文档：** https://docs.claude.com
- **问题和建议：** https://github.com/StanleyChanH/cc_skills/issues

## 📈 版本历史

### v1.0.0 (2025-10-30)
- 首次发布
- 包含 CrewAI 技能
- 完整的文档集
- 建立仓库结构

---

**最后更新：** 2025年10月30日
**仓库大小：** ~10MB
**技能数量：** 1