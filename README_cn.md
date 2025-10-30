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

2. 导航到所需的技能目录：
   ```bash
   cd Crewai/crewai
   ```

3. 在 Claude 中加载技能：
   - 使用 `/skill` 命令加上技能名称
   - 根据需要参考文档文件

### 使用技能
每个技能包含：
- **SKILL.md**：包含使用说明的主要技能文件
- **references/**：从官方来源提取的完整文档
- **assets/**：模板、样板代码和示例
- **scripts/**：自动化辅助工具

### 初学者指南
1. 从 `getting_started.md` 参考文件开始
2. 使用 SKILL.md 中的快速参考模式
3. 探索 assets/ 目录中的示例

### 高级用户指南
1. 深入研究 `advanced.md` 和 `api.md` 获取详细信息
2. 查看 `enterprise.md` 了解部署模式
3. 使用 scripts/ 中的自动化任务

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