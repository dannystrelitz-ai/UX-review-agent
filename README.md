# Cognitive UX Audit Skills for Claude Code

A comprehensive UX auditing toolkit for Claude Code that helps identify cognitive friction and usability issues in your frontend code using cognitive psychology principles.

## What's Included

This package provides three powerful skills and one specialized agent for UX analysis:

### Skills
1. **`/ux-review`** - Quick UX review for post-development audits
2. **`/ux-audit`** - Comprehensive cognitive UX audit with detailed persona-based analysis
3. **`/user-expectations`** - Analyzes implicit expectations created by interface elements

### Agent
4. **`ux-audit-agent`** - Autonomous agent that conducts evidence-based UX audits with scoring framework (0-100)

## Documentation

- **[Installation Guide](INSTALL.md)** - Detailed installation instructions for all platforms
- **[Usage Examples](EXAMPLES.md)** - Real-world examples and workflows
- **[README](README.md)** - You are here

## Features

- **Cognitive Gap Detection**: Identifies friction where designs contradict users' prior knowledge and mental models
- **Stroop Effect Analysis**: Catches visual-semantic conflicts (e.g., red "success" buttons, green "delete" actions)
- **Visual Hierarchy Auditing**: Ensures CTAs and information architecture match user goals
- **Persona-Based Evaluation**: Customizes audits based on user profession, digital habitat, and domain semantics
- **Severity Classification**: Prioritizes issues from Critical (Stroop conflicts) to Low (minor optimizations)

## Requirements

- Claude Code 1.0.33 or later
- Basic understanding of UX principles (helpful but not required)

## Quick Start

Install the plugin and start auditing:

```bash
# Add the marketplace
/plugin marketplace add dannystrelitz-ai/UX-review-agent

# Install the plugin
/plugin install ux-audit-agent@ux-audit-tools

# Start using it
claude
# Then ask: "Run a UX review on my app" or use /ux-audit-agent:ux-review
```

For detailed installation instructions, see **[INSTALL.md](INSTALL.md)**.

## Installation

### Plugin Installation (Recommended)

Install the plugin using Claude Code's marketplace system:

```bash
# Add the UX Audit Tools marketplace
/plugin marketplace add dannystrelitz-ai/UX-review-agent

# Install the plugin
/plugin install ux-audit-agent@ux-audit-tools
```

**Verify installation:**
Open Claude Code and type `/ux-audit-agent:` - you should see the available skills in autocomplete.

### Manual Installation (Alternative)

If you prefer to install manually:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/dannystrelitz-ai/UX-review-agent.git
   cd UX-review-agent
   ```

2. **Install as a local plugin**:
   ```bash
   /plugin marketplace add /path/to/UX-review-agent
   /plugin install ux-audit-agent@ux-audit-tools
   ```

3. **Verify installation**:
   ```bash
   /plugin list
   ```

## Usage

Once installed, the plugin provides three skills accessible via the `ux-audit-agent:` namespace:

### Quick UX Review with `ux-review`

Use this after writing frontend code for a quick cognitive UX check:

**Invocation:**
```
/ux-audit-agent:ux-review
```

Or simply ask Claude:
```
"Run a quick UX review on my app"
"Review the UX of this component"
```

This skill is designed to be invoked:
- After completing frontend development work
- When planning new frontend features
- For rapid UX validation

The agent will automatically analyze your UI code for common cognitive friction points.

### Comprehensive Audit with `ux-audit`

For deep, persona-driven UX analysis:

**Invocation:**
```
/ux-audit-agent:ux-audit
```

Or ask Claude:
```
"Conduct a deep UX audit"
"Perform a cognitive UX analysis"
```

This starts an interactive audit process:

1. **Persona Definition**: You'll be asked about:
   - User's profession/domain (e.g., "Software Engineer", "Medical Professional")
   - Digital habitat (e.g., "iOS, macOS, Figma")
   - Domain-specific semantics (e.g., "In finance, red means positive")
   - Focus areas (optional specific screens/components)

2. **Discovery Phase**: The agent will:
   - Scan your codebase for UI files (React, Vue, Svelte, HTML, CSS, etc.)
   - Identify screens and ask you to prioritize them

3. **Analysis Phase**: For each screen:
   - Maps information architecture
   - Classifies CTAs (Primary/Secondary/Tertiary)
   - Identifies visual hierarchy violations
   - Detects cognitive conflicts

4. **Report**: Detailed findings with:
   - Severity levels (1-4)
   - Exact file locations
   - Cognitive conflicts explained
   - Concrete fix recommendations

### Evidence-Based Audit with the UX Audit Agent

For autonomous, scored UX audits (0-100 rating):

**Invocation:**
Simply ask Claude to conduct an audit, and it will automatically use the agent:
```
"Conduct a UX audit of my application"
"Run an evidence-based UX analysis with scoring"
"Audit the checkout flow for cognitive friction"
```

The agent will:
- Perform a defensible, evidence-based analysis
- Apply Nielsen, Shneiderman, and Don Norman heuristics
- Provide a scored report (0-100)
- Prioritize issues by severity and ROI
- Deliver actionable recommendations

### Example Workflow

```bash
# After building a checkout flow, ask Claude:
"Conduct a cognitive UX audit of the checkout flow"

# Or use the skill directly:
/ux-audit-agent:ux-audit

# Agent asks:
"What is the primary user's role?"
> E-commerce shopper, mobile-first, familiar with Amazon/Shopify

"Any specific screens to prioritize?"
> Checkout page and cart

# Agent analyzes and reports:
### Severity 1: Destructive Action Styled as Primary CTA
**Location:** checkout.tsx:45
**Problem:** "Remove All Items" button has same prominence as "Place Order"
**Fix:** Change to text link with confirmation modal
```

## What Gets Analyzed

### Visual Hierarchy
- Information weight vs. goal relevance
- CTA classification (Primary/Secondary/Tertiary)
- Common violations: CTA overload, buried primary actions, competing twins

### Cognitive Friction Points

#### 1. Prior Knowledge Alignment
- Terminology matches user's profession
- Layout follows domain conventions
- Power users see expected advanced features

#### 2. Stroop Interference
- **Color conflicts**: Red success messages, green destructive actions
- **Spatial conflicts**: Button positions contradicting platform norms
- **Iconic conflicts**: Icons with non-standard meanings

#### 3. Memory & Closure Load
- Recognition over recall violations
- Missing context indicators
- Unclear completion states

## Severity Levels

- **Level 1 (Critical)**: Stroop conflicts causing potential destructive actions
- **Level 2 (High)**: Domain terminology/layout mismatches
- **Level 3 (Medium)**: Platform convention deviations
- **Level 4 (Low)**: Minor optimizations

## Supported UI Technologies

The skills can analyze:
- React, Vue, Svelte, Angular components
- HTML templates
- CSS/SCSS/Tailwind files
- Design tokens and theme files
- UI configuration files

## Tips for Best Results

1. **Be Specific with Personas**: The more details about your user's background, the better the audit
2. **Prioritize Screens**: Start with high-traffic or critical user journeys
3. **Run After Major Changes**: Best used after implementing new features or redesigns
4. **Combine Both Skills**: Use `/ux-review` for quick checks, `/ux-audit` for deep analysis

## Example Reports

### Visual Hierarchy Issue
```
### CTA Overload on Dashboard

**Severity:** Level 2 — High
**Location:** dashboard.tsx:120-135

**Problem:** 4 buttons competing as primary CTAs
**User Impact:** Decision paralysis, unclear next action

**Recommended Fix:**
- Keep "Create New Project" as primary (solid blue)
- Demote "Import", "Templates", "Settings" to secondary (outline)
```

### Stroop Conflict
```
### Color-Action Mismatch in Delete Flow

**Severity:** Level 1 — Critical
**Location:** settings.tsx:89

**Cognitive Conflict:**
- Automatic brain sees: Green = Safe/Confirm
- Required action: Delete account (destructive)

**Recommended Fix:**
Change "Delete Account" button from green to red outline style
Add two-step confirmation to prevent accidental deletion
```

## Contributing

Issues and pull requests welcome! This is an evolving toolkit based on cognitive psychology and UX research.

## License

MIT

## Credits

Based on cognitive psychology principles including:
- Nielsen Norman Group Heuristics
- Shneiderman's Eight Golden Rules
- Stroop Effect research
- Visual hierarchy theory
