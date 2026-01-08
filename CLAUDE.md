# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code plugin that provides UX auditing capabilities based on cognitive psychology principles. The plugin includes three skills and one autonomous agent for analyzing user interfaces.

## Plugin Architecture

### Structure
```
.claude/
├── agents/
│   └── ux-audit-agent.md       # Autonomous agent with scoring framework
└── skills/
    ├── ux-audit/               # Deep persona-driven audit
    ├── ux-review/              # Quick post-development review
    └── user-expectations/      # Expectation gap analysis
```

### Plugin Definition
- **Plugin manifest**: `.claude-plugin/plugin.json`
- **Marketplace config**: `.claude-plugin/marketplace.json`
- The plugin is distributed via Claude Code's marketplace system

## Skills vs Agent

**Skills** (invoked with `/skill-name`):
- Interactive, step-by-step workflows
- Ask clarifying questions during execution
- Guide users through the audit process

**Agent** (`ux-audit-agent`):
- Autonomous execution
- Produces scored reports (0-100)
- Automatically invoked by Claude when appropriate

## Core UX Framework

All components use a consistent cognitive psychology framework:

1. **Prior Knowledge Alignment** - Terminology and layout match user's profession/domain
2. **Stroop Interference Detection** - Visual-semantic conflicts (color, position, icon mismatches)
3. **Memory & Closure Load** - Recognition over recall, clear completion states
4. **Visual Hierarchy** - Information weight matches goal relevance, CTA classification

### Severity Levels
- **Level 1 (Critical)**: Stroop conflicts causing destructive actions
- **Level 2 (High)**: Domain terminology/layout mismatches
- **Level 3 (Medium)**: Platform convention deviations
- **Level 4 (Low)**: Minor optimizations

### Audit Scoring (Agent Only)
The autonomous agent uses weighted sections:
- System Feedback & State Awareness (15%)
- User Control & Reversibility (15%)
- Cognitive Load & Clarity (15%)
- Error Prevention & Recovery (15%)
- Consistency & Standards (10%)
- Mental Model Alignment (10%)
- Flexibility & Efficiency (10%)
- Closure & Flow Completeness (5%)
- Help & Self-Explanation (5%)
- Affordance & Signifier Integrity (5%)

## Development Workflows

### Testing Skills
To test a skill after modifications:
1. Navigate to a project with UI code
2. Invoke the skill: `/ux-audit-agent:skill-name`
3. Verify it follows the documented workflow in the SKILL.md file

### Testing the Agent
1. Ask Claude to "conduct a UX audit" in a project with UI code
2. Verify it produces a scored report with all sections
3. Check that it applies heuristics without restating them

### Plugin Installation Testing
```bash
# Add local marketplace
/plugin marketplace add .

# Install from local marketplace
/plugin install ux-audit-agent@ux-audit-tools

# Verify installation
/plugin list
```

## File Organization

### Documentation
- `README.md` - User-facing overview and quick start
- `INSTALL.md` - Installation instructions for end users
- `EXAMPLES.md` - Real-world usage examples
- `STRUCTURE.md` - Repository structure reference

### Legacy Structure
The `agents/` and `skills/` folders at root level are legacy - they contain older versions kept for reference. The active components are in `.claude/`.

## Key Principles

When modifying this plugin:

1. **Maintain Framework Consistency** - All components share the same cognitive psychology foundation
2. **Evidence-Based Analysis** - Claims must be tied to specific heuristics (Nielsen Norman, Shneiderman, Don Norman)
3. **Actionable Output** - Every issue identified must include concrete fixes with file locations
4. **Progressive Disclosure** - Skills guide users step-by-step; agent works autonomously
5. **Persona-Driven Context** - All audits must account for user profession, digital habitat, and domain semantics

## Cognitive Psychology References

The framework is based on:
- Nielsen Norman Group Usability Heuristics (10 principles)
- Shneiderman's Eight Golden Rules of Interface Design
- Don Norman's Cognitive Design Principles
- Stroop Effect research (visual-semantic conflicts)
- Visual hierarchy theory (information weight vs. goal relevance)

## Common Modification Patterns

### Adding a New Skill
1. Create `.claude/skills/new-skill-name/SKILL.md`
2. Add frontmatter with `name`, `description`, and `model: inherit`
3. Follow existing skill structure: phases, instructions, output format
4. Update plugin.json if needed for marketplace

### Modifying Agent Behavior
- Edit `.claude/agents/ux-audit-agent.md`
- Maintain the scoring framework and weighted sections
- Keep output format consistent (Executive Summary → Score Breakdown → Critical Failures → High-ROI Fixes → Non-Issues)

### Updating Documentation
- User-facing changes go in README.md and EXAMPLES.md
- Technical changes update STRUCTURE.md
- Keep CLAUDE.md (this file) focused on development guidance
