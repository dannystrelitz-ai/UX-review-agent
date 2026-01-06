# Repository Structure

```
ux-agent/
├── .claude/
│   ├── settings.local.json          # Local Claude Code settings
│   └── skills/
│       ├── ux-audit/
│       │   └── SKILL.md             # Comprehensive cognitive UX audit skill
│       ├── ux-audit-agent/
│       │   └── SKILL.md             # Evidence-based UX audit with scoring
│       ├── ux-review/
│       │   └── SKILL.md             # Quick UX review skill
│       └── user-expectations/
│           └── SKILL.md             # Expectations analysis skill
├── .git/                            # Git repository data
├── .gitignore                       # Git ignore rules
├── EXAMPLES.md                      # Detailed usage examples and workflows
├── INSTALL.md                       # Complete installation guide
├── LICENSE                          # MIT License
├── README.md                        # Main documentation
├── STRUCTURE.md                     # This file - repository structure
└── package.json                     # NPM package configuration

```

## File Descriptions

### Core Skills

**`.claude/skills/ux-audit/SKILL.md`**
- Comprehensive, interactive UX audit workflow
- Persona-driven analysis (profession, digital habitat, domain semantics)
- Multi-step process: context gathering → screen discovery → visual hierarchy → cognitive audit
- Generates detailed reports with severity levels
- Use: `/ux-audit`

**`.claude/skills/ux-audit-agent/SKILL.md`**
- Evidence-based UX audit using Nielsen Norman, Shneiderman, and Don Norman principles
- Produces scored reports (0-100) with weighted sections
- Identifies critical failures and high-ROI fixes
- Professional-grade output for stakeholder discussions
- Use: `/ux-audit-agent`

**`.claude/skills/ux-review/SKILL.md`**
- Quick UX review for post-development checks
- Lightweight cognitive audit
- Best for rapid validation after feature development
- Use: `/ux-review`

**`.claude/skills/user-expectations/SKILL.md`**
- Analyzes implicit user expectations created by interface elements
- Compares what is promised vs. what is delivered
- Tracks expectation carryover across screens
- Uncovers deep UX insights beyond standard heuristics
- Use: `/user-expectations`

### Documentation

**`README.md`**
- Overview of the project
- Quick start guide
- Feature highlights
- Basic installation instructions
- Links to detailed guides

**`INSTALL.md`**
- Comprehensive installation guide
- Multiple installation methods (global, per-project, manual)
- Platform-specific instructions (macOS, Linux, Windows)
- Troubleshooting section
- Update and uninstallation guides

**`EXAMPLES.md`**
- Real-world usage examples
- Different scenarios (e-commerce, enterprise, components)
- Sample audit reports
- Interpretation guides
- Integration with development workflows

**`STRUCTURE.md`**
- This file
- Repository organization
- File purposes and relationships

### Configuration

**`package.json`**
- NPM package metadata
- Dependencies and scripts
- Claude Code skill registration
- Keywords for discoverability

**`.gitignore`**
- Files to exclude from version control
- Node modules, logs, IDE files, etc.

**`.claude/settings.local.json`**
- Local Claude Code configuration
- User-specific settings (not committed to git in typical usage)

### Legal

**`LICENSE`**
- MIT License
- Open source usage terms

## Usage Flow

```
User types: /ux-audit
     ↓
Claude Code reads: .claude/skills/ux-audit.md
     ↓
Skill executes: Interactive persona gathering
     ↓
Skill analyzes: Codebase UI files
     ↓
Skill reports: Cognitive friction points with fixes
```

## Installation Locations

### Global Installation
```
~/.claude/skills/
├── ux-audit/
│   └── SKILL.md
├── ux-audit-agent/
│   └── SKILL.md
├── ux-review/
│   └── SKILL.md
└── user-expectations/
    └── SKILL.md
```

### Per-Project Installation
```
your-project/
└── .claude/skills/
    ├── ux-audit/
    │   └── SKILL.md
    ├── ux-audit-agent/
    │   └── SKILL.md
    ├── ux-review/
    │   └── SKILL.md
    └── user-expectations/
        └── SKILL.md
```

## Key Relationships

```
README.md
  ├──→ INSTALL.md (detailed installation)
  ├──→ EXAMPLES.md (usage examples)
  └──→ .claude/skills/* (the actual skills)

INSTALL.md
  └──→ .claude/skills/* (installation targets)

EXAMPLES.md
  └──→ .claude/skills/* (demonstrates skill usage)

package.json
  └──→ .claude/skills/* (declares skills for npm)
```

## For Contributors

When adding new features:

1. **New skill**: Create folder in `.claude/skills/` with `SKILL.md` file
2. **Metadata**: Add frontmatter with `name`, `description`, and `model: inherit`
3. **Update**: `package.json` → `claudeCode.skills` array
4. **Document**: Add usage examples to `EXAMPLES.md`
5. **Announce**: Update `README.md` and `STRUCTURE.md` with new capability

## For Users

To understand this package:

1. **Start**: Read `README.md`
2. **Install**: Follow `INSTALL.md`
3. **Learn**: Study `EXAMPLES.md`
4. **Use**: Type `/ux-audit`, `/ux-review`, `/ux-audit-agent`, or `/user-expectations` in Claude Code
