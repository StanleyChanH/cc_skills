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

2. Navigate to the desired skill directory:
   ```bash
   cd Crewai/crewai
   ```

3. Load the skill in Claude:
   - Use the `/skill` command with the skill name
   - Reference the documentation files as needed

### Using Skills
Each skill contains:
- **SKILL.md**: Main skill file with usage instructions
- **references/**: Complete documentation extracted from official sources
- **assets/**: Templates, boilerplate code, and examples
- **scripts/**: Automation helpers

### For Beginners
1. Start with the `getting_started.md` reference file
2. Use the quick reference patterns in SKILL.md
3. Explore examples in the assets/ directory

### For Advanced Users
1. Dive into `advanced.md` and `api.md` for detailed information
2. Check `enterprise.md` for deployment patterns
3. Use scripts/ for automation tasks

## 📊 Skill Information

| Skill | Version | Generated | Size | Status |
|-------|---------|-----------|------|--------|
| CrewAI | 1.0.0 | 2025-10-30 | ~10MB | ✅ Active |

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

### v1.0.0 (2025-10-30)
- Initial release
- CrewAI skill included
- Complete documentation set
- Repository structure established

---

**Last Updated:** October 30, 2025
**Repository Size:** ~10MB
**Skills Count:** 1