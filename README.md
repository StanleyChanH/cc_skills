# CC Skills Repository

A curated collection of Claude Skills generated from official documentation, ready for immediate use.

## 📋 Overview

This repository contains automatically generated Claude Skills that provide comprehensive assistance with various frameworks and libraries. Each skill is created from official documentation and includes:

- Complete reference documentation
- Code examples with syntax highlighting
- Quick reference patterns
- Organized structure for easy navigation

## 🚀 Available Skills

### [CrewAI](./Crewai/crewai/SKILL.md)
**Version:** 1.0.0
**Generated:** October 30, 2025
**Size:** ~10MB documentation

Use this skill when working with CrewAI - a framework for building multi-agent AI systems. Helpful for creating AI agents, defining tasks, managing workflows, and orchestrating multi-agent collaborations.

**Features:**
- Multi-agent system development
- Task management and workflow orchestration
- Comprehensive API documentation
- Advanced guides and examples
- Enterprise deployment patterns

**Documentation Structure:**
- `getting_started.md` - Introduction and basic concepts
- `api.md` - Complete API reference
- `guides.md` - Step-by-step tutorials
- `advanced.md` - Advanced patterns and techniques
- `enterprise.md` - Enterprise deployment and scaling
- `tools.md` - Available tools and integrations

### [LangChain v1.0 (Alpha)](./LangChain/langchain/SKILL.md)
**Version:** 1.0.0 Alpha
**Generated:** October 31, 2025
**Size:** ~25KB documentation

Use this skill when working with LangChain v1.0 (Alpha) - the revolutionary framework representing a fundamental architectural shift from Chain-based orchestration to unified Agent architecture with LangGraph engine.

**Features:**
- Unified Agent architecture with `create_agent` entry point
- Revolutionary shift from Chain-based orchestration to Agent-based development
- LangGraph engine for powerful stateful, interruptible workflows
- Enhanced streaming capabilities with `astream_events`
- Production-ready design addressing previous "easy for prototype, hard for production" limitations
- Comprehensive API documentation for v1.0 architecture

**Documentation Structure:**
- `core_components.md` - Core components and architectural changes
- `getting_started.md` - Introduction to v1.0 concepts
- `other.md` - Additional documentation and migration guides

## 📁 Repository Structure

```
cc_skills/
├── Crewai/
│   └── crewai/
│       ├── SKILL.md              # Main skill file
│       ├── references/           # Comprehensive documentation
│       │   ├── advanced.md
│       │   ├── api.md
│       │   ├── concepts.md
│       │   ├── enterprise.md
│       │   ├── getting_started.md
│       │   ├── guides.md
│       │   ├── tools.md
│       │   └── ...
│       ├── assets/              # Templates and examples
│       └── scripts/             # Helper scripts
├── LangChain/
│   └── langchain/
│       ├── SKILL.md              # Main skill file
│       ├── references/           # v1.0 documentation
│       │   ├── core_components.md
│       │   ├── getting_started.md
│       │   └── other.md
│       ├── assets/              # Templates and examples
│       └── scripts/             # Helper scripts
├── README.md                    # This file
└── README_cn.md                 # Chinese version
```

## 🔧 How to Use

### Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/StanleyChanH/cc_skills.git
   cd cc_skills
   ```

## 📦 Installation Methods

There are **two methods** to use these skills with Claude:

### Method 1: Upload ZIP File to Claude (Recommended)

**Best for:** Quick testing, one-time use, or when you don't want to modify files locally

**Steps:**
1. **Download the ZIP file** for your desired skill:
   - CrewAI: Download `Crewai/crewai.zip` from the repository
   - LangChain v1.0: Download `LangChain/langchain.zip` from the repository
   - You can download it directly from GitHub or use:
     ```bash
     # If you have the repo cloned
     cp Crewai/crewai.zip ~/Downloads/crewai.zip
     cp LangChain/langchain.zip ~/Downloads/langchain.zip
     ```

2. **Upload to Claude:**
   - Open Claude Code or Claude.ai
   - Drag and drop the `.zip` file into the chat
   - Or use the upload button/attach file option

3. **Use the skill:**
   - Claude will automatically extract and load the skill
   - Start using it immediately with your questions
   - Example: "Help me create a CrewAI agent for data analysis"

**Advantages:**
- ✅ No local file setup required
- ✅ Works immediately after upload
- ✅ Perfect for testing and exploration
- ✅ No risk of breaking local files

### Method 2: Copy to Claude Skills Directory

**Best for:** Permanent installation, frequent use, custom modifications

**Steps:**
1. **Locate your Claude skills directory:**
   ```bash
   # The skills directory is typically at:
   ~/.claude/skills/
   ```

2. **Copy the skill folder:**
   ```bash
   # Create the skills directory if it doesn't exist
   mkdir -p ~/.claude/skills/

   # Copy the CrewAI skill
   cp -r Crewai/crewai ~/.claude/skills/

   # Copy the LangChain v1.0 skill
   cp -r LangChain/langchain ~/.claude/skills/
   ```

3. **Verify installation:**
   ```bash
   # Check if the skills are properly installed
   ls ~/.claude/skills/crewai/
   # Should show: SKILL.md, references/, assets/, scripts/

   ls ~/.claude/skills/langchain/
   # Should show: SKILL.md, references/, assets/, scripts/
   ```

4. **Use the skill:**
   - Open Claude Code
   - Use the skill name directly: `/skill crewai` or `/skill langchain`
   - Or simply start asking questions about CrewAI or LangChain v1.0

**Advantages:**
- ✅ Permanent installation
- ✅ Available in all Claude sessions
- ✅ Can modify and customize files
- ✅ Faster loading after first use
- ✅ Works offline once installed

## 🚀 Using the Skills

### With CrewAI Skill

**Basic Usage Examples:**
```bash
# After installation, you can ask:
"Help me create a multi-agent system for data analysis"
"How do I define tasks in CrewAI?"
"Show me examples of agent role definitions"
"What are the best practices for workflow orchestration?"
```

**Accessing Documentation:**
- The skill includes comprehensive documentation in `references/`
- Ask Claude to "show me the getting started guide" or "reference the API documentation"
- All examples and guides are available through natural language queries

### With LangChain v1.0 Skill

**Basic Usage Examples:**
```bash
# After installation, you can ask:
"How do I use create_agent in LangChain v1.0?"
"What's the difference between Chain and Agent architecture in v1.0?"
"Show me examples of using LangGraph for stateful workflows"
"How do I migrate from Chain-based to Agent-based development?"
"What are the streaming capabilities with astream_events?"
```

**Accessing Documentation:**
- The skill includes v1.0 specific documentation in `references/`
- Ask Claude to "explain the unified Agent architecture" or "show me v1.0 migration guide"
- All architectural changes and new features are covered through natural language queries

### Skill Structure Overview
Each skill contains:
- **SKILL.md**: Main skill file with usage instructions and metadata
- **references/**: Complete documentation extracted from official sources
  - **CrewAI**: `getting_started.md`, `api.md`, `guides.md`, `advanced.md`, `enterprise.md`, `tools.md`
  - **LangChain v1.0**: `core_components.md`, `getting_started.md`, `other.md`
- **assets/**: Templates, boilerplate code, and examples
- **scripts/**: Automation helpers

### For Beginners
1. **Start with Method 1** (ZIP upload) for testing
2. Use the `getting_started.md` reference file for foundational concepts
3. Ask simple questions like "What is CrewAI?" or "How do agents work?"
4. Explore examples in the assets/ directory

### For Advanced Users
1. **Use Method 2** (local installation) for permanent access
2. Dive into `advanced.md` and `api.md` for detailed information
3. Check `enterprise.md` for deployment patterns
4. Use scripts/ for automation tasks
5. Modify and customize the skill files as needed

## 🔧 Troubleshooting

### ZIP Upload Issues
- **Problem:** Claude doesn't recognize the skill after upload
- **Solution:** Ensure the ZIP file contains the proper structure with SKILL.md at the root
- **Alternative:** Try extracting the ZIP and uploading the folder directly

### Local Installation Issues
- **Problem:** Skill not found in ~/.claude/skills/
- **Solution:**
  1. Verify the directory path: `ls ~/.claude/skills/`
  2. Check permissions: `ls -la ~/.claude/skills/crewai/`
  3. Ensure SKILL.md exists: `test -f ~/.claude/skills/crewai/SKILL.md`

### Performance Issues
- **Problem:** Skill loads slowly
- **Solution:** Large documentation files (like this 10MB CrewAI skill) may take time to index
- **Tip:** Allow Claude a few moments to process the documentation after first load

## 📊 Skill Information

| Skill | Version | Generated | Size | Status |
|-------|---------|-----------|------|--------|
| CrewAI | 1.0.0 | 2025-10-30 | ~10MB | ✅ Active |
| LangChain v1.0 | 1.0.0 Alpha | 2025-10-31 | ~25KB | ✅ Active |

## 🔄 Updating Skills

To update skills with the latest documentation:

1. Check the skill version in its SKILL.md file
2. Re-run the documentation scraper with the same configuration
3. The skill will be rebuilt with the latest information
4. Update the version number and generation date

## 🤝 Contributing

Contributions are welcome! You can help by:

- Adding new skills for other frameworks
- Improving existing documentation
- Adding more examples and templates
- Reporting issues or suggesting improvements

### Adding a New Skill

1. Create a new directory under the project root
2. Follow the same structure as existing skills
3. Include a comprehensive SKILL.md file
4. Add organized documentation in references/
5. Update this README with your skill information

## 📝 License

This repository contains skills generated from official documentation. Each skill may have its own licensing terms. Please check the individual skill documentation for specific licensing information.

## 🔗 Links

- **GitHub Repository:** https://github.com/StanleyChanH/cc_skills
- **Claude Code Documentation:** https://docs.claude.com
- **Issues and Suggestions:** https://github.com/StanleyChanH/cc_skills/issues

## 📈 Version History

### v1.1.0 (2025-10-31)
- Added LangChain v1.0 (Alpha) skill
- Updated repository structure
- Enhanced documentation with architectural changes
- Added unified Agent architecture support

### v1.0.0 (2025-10-30)
- Initial release
- CrewAI skill included
- Complete documentation set
- Repository structure established

---

**Last Updated:** October 31, 2025
**Repository Size:** ~10MB
**Skills Count:** 2