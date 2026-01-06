# Installation Guide

Two quick ways to install the UX audit tools: use the Claude plugin marketplace or clone this repo and let an agent install it for you.

## Option 1: Claude Marketplace (Recommended)

1. Open Claude Code and run:
   ```shell
   /plugin marketplace add dannystrelitz-ai/UX-review-agent
   /plugin install ux-audit-agent@ux-audit-tools
   ```
2. Verify you can run:
   - `/ux-review`
   - `/ux-audit`

Reference: https://code.claude.com/docs/en/plugin-marketplaces

## Option 2: Clone + Agent Install

1. Clone the repo:
   ```bash
   git clone https://github.com/dannystrelitz-ai/UX-review-agent.git
   cd UX-review-agent
   ```
2. Open Claude Code point to the cloned folder and ask an agent:
   - “Add the local marketplace and install the UX audit plugin.”

If you want the exact commands, the agent can run:
```shell
/plugin marketplace add .
/plugin install ux-audit-agent@ux-audit-tools
```
