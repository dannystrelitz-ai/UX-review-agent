# Installation Guide

Complete guide for installing the Cognitive UX Audit skills for Claude Code.

## Prerequisites

- Claude Code CLI installed ([installation instructions](https://docs.anthropic.com/claude-code))
- Git (optional, for cloning)

## Installation Methods

### Method 1: Global Installation (Recommended)

Install the skills globally so they're available in all your projects.

```bash
# Clone the repository
git clone https://github.com/your-username/ux-agent.git

# Navigate to the directory
cd ux-agent

# Create global skills directory (if it doesn't exist)
mkdir -p ~/.claude/skills

# Copy skills to global directory
cp .claude/skills/* ~/.claude/skills/

# Verify installation
ls ~/.claude/skills/
# Should show: ux-audit.md  ux-review.md
```

**Verify it works**:
```bash
# Start Claude Code in any project
claude

# Type /ux and press Tab
# You should see /ux-audit and /ux-review in autocomplete
```

---

### Method 2: Per-Project Installation

Install skills only for a specific project.

```bash
# Navigate to your project
cd /path/to/your/project

# Clone this repo (or download)
git clone https://github.com/your-username/ux-agent.git /tmp/ux-agent

# Create project skills directory
mkdir -p .claude/skills

# Copy skills to project
cp /tmp/ux-agent/.claude/skills/* .claude/skills/

# Clean up
rm -rf /tmp/ux-agent

# Verify
ls .claude/skills/
# Should show: ux-audit.md  ux-review.md
```

**When to use**:
- Testing the skills before global installation
- Using different versions per project
- Customizing skills for specific projects

---

### Method 3: Direct Download (No Git)

If you don't have Git or prefer manual download:

1. **Download the skills**:
   - Go to: https://github.com/your-username/ux-agent
   - Click: "Code" → "Download ZIP"
   - Extract the ZIP file

2. **Copy to Claude Code**:
   ```bash
   # For global installation
   mkdir -p ~/.claude/skills
   cp /path/to/extracted/ux-agent/.claude/skills/* ~/.claude/skills/

   # OR for per-project
   cd /path/to/your/project
   mkdir -p .claude/skills
   cp /path/to/extracted/ux-agent/.claude/skills/* .claude/skills/
   ```

---

## Verification

After installation, verify the skills are working:

1. **Start Claude Code**:
   ```bash
   claude
   ```

2. **Test autocomplete**:
   - Type: `/ux`
   - Press: `Tab`
   - Expected: See `/ux-audit` and `/ux-review` suggestions

3. **Test quick review**:
   ```bash
   /ux-review
   ```
   Should start the UX review process

4. **Test comprehensive audit**:
   ```bash
   /ux-audit
   ```
   Should ask: "What is the primary user's role?"

---

## Troubleshooting

### Skills don't appear in autocomplete

**Problem**: You type `/ux` but nothing shows up.

**Solutions**:

1. **Check installation path**:
   ```bash
   # Global
   ls ~/.claude/skills/

   # Per-project
   ls .claude/skills/
   ```

2. **Verify file names**:
   Skills must be `.md` files:
   - ✓ `ux-audit.md`
   - ✓ `ux-review.md`
   - ✗ `ux-audit.txt`

3. **Check permissions**:
   ```bash
   chmod 644 ~/.claude/skills/*.md
   ```

4. **Restart Claude Code**:
   - Exit: `Ctrl+C` or type `exit`
   - Restart: `claude`

### "Command not found" error

**Problem**: `/ux-review` says "command not found"

**Cause**: File names don't match command names.

**Solution**:
```bash
# Skill filename determines command name
# ux-review.md → /ux-review
# ux-audit.md → /ux-audit

# Check your files match:
ls ~/.claude/skills/
```

### Skills work but give errors

**Problem**: Skill starts but crashes or gives unexpected errors.

**Solutions**:

1. **Update to latest version**:
   ```bash
   cd /path/to/ux-agent
   git pull origin main
   cp .claude/skills/* ~/.claude/skills/
   ```

2. **Check frontmatter**:
   First lines of skill should be:
   ```markdown
   ---
   name: ux-review
   description: ...
   ---
   ```

3. **Check Claude Code version**:
   ```bash
   claude --version
   ```
   These skills require Claude Code v1.0.0+

---

## Updating

### Update Global Installation

```bash
# Navigate to repo
cd /path/to/ux-agent

# Pull latest changes
git pull origin main

# Re-copy to global
cp .claude/skills/* ~/.claude/skills/

# Restart Claude Code
```

### Update Per-Project Installation

```bash
# Navigate to project
cd /path/to/your/project

# Re-download/copy latest skills
git clone https://github.com/your-username/ux-agent.git /tmp/ux-agent
cp /tmp/ux-agent/.claude/skills/* .claude/skills/
rm -rf /tmp/ux-agent
```

---

## Uninstallation

### Remove Global Installation

```bash
# Remove skills
rm ~/.claude/skills/ux-audit.md
rm ~/.claude/skills/ux-review.md

# Or remove entire skills directory (if no other skills)
rm -rf ~/.claude/skills/
```

### Remove Per-Project Installation

```bash
# Navigate to project
cd /path/to/your/project

# Remove skills
rm .claude/skills/ux-audit.md
rm .claude/skills/ux-review.md

# Or remove entire .claude directory (if no other config)
rm -rf .claude/
```

---

## Advanced Configuration

### Customizing Skills

You can edit the skills to customize behavior:

```bash
# Edit global skill
code ~/.claude/skills/ux-audit.md

# Edit project-specific skill
code .claude/skills/ux-audit.md
```

**Common customizations**:

1. **Change default persona assumptions**:
   Edit the "Additional Context" section

2. **Adjust severity thresholds**:
   Edit the "Severity Levels" section

3. **Add industry-specific patterns**:
   Add to the "Visual Hierarchy Patterns" section

### Using Different Versions

Use different skill versions for different projects:

```bash
# Project A: Use stable version
cd project-a
cp ~/.claude/skills-stable/* .claude/skills/

# Project B: Use experimental version
cd project-b
cp ~/.claude/skills-experimental/* .claude/skills/
```

---

## Platform-Specific Notes

### macOS / Linux

Standard installation works as documented above.

**Tip**: Add alias for quick updates:
```bash
# In ~/.bashrc or ~/.zshrc
alias ux-update='cd ~/ux-agent && git pull && cp .claude/skills/* ~/.claude/skills/'
```

### Windows

Use PowerShell or Git Bash:

```powershell
# Create skills directory
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills"

# Copy skills
Copy-Item .\ux-agent\.claude\skills\* "$env:USERPROFILE\.claude\skills\"
```

**Path differences**:
- Global: `C:\Users\YourName\.claude\skills\`
- Per-project: `C:\path\to\project\.claude\skills\`

---

## Getting Help

If you encounter issues:

1. **Check documentation**: [README.md](README.md), [EXAMPLES.md](EXAMPLES.md)
2. **Search issues**: https://github.com/your-username/ux-agent/issues
3. **Create new issue**: Provide:
   - Claude Code version (`claude --version`)
   - Installation method used
   - Error messages
   - Steps to reproduce

---

## Next Steps

After installation:

1. Read [EXAMPLES.md](EXAMPLES.md) for usage examples
2. Try `/ux-review` on an existing project
3. Run `/ux-audit` on your main user flow
4. Customize skills for your domain (optional)
