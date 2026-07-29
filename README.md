# Agent Skills Repository for AI Assistants

[![Validate Agent Skills](https://github.com/jelmervdm/skills/actions/workflows/validate-skills.yml/badge.svg)](https://github.com/jelmervdm/skills/actions/workflows/validate-skills.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Author: jelmervdm](https://img.shields.io/badge/Author-jelmervdm-blue.svg)](https://github.com/jelmervdm)

A modular, production-grade collection of 2-Tier Progressive Disclosure **AI Agent Skills** designed for LLM assistants (Claude, ChatGPT/OpenAI, and Google Gemini).

---

## 📂 Skill Categories

This repository is organized into domain categories. Each skill contains a Tier 1 `SKILL.md` prompt module and on-demand Tier 2 technical references in `references/`.

### 🏋️ Athletic Performance & Sports Coaching (`coach/`)

| Skill Name | Directory | Primary Focus & Domain | Key Metrics & Methods |
| ------------ | ----------- | ------------------------ | ----------------------- |
| **Cycling Coach** | [`coach/cycling/`](coach/cycling/SKILL.md) | Power-based cycling, workout analysis, race pacing, event optimization | Coggan Z1-Z7, FTP, NP, IF, TSS, TSB, Aerobic Decoupling, Intervals.icu |
| **Running Coach** | [`coach/running/`](coach/running/SKILL.md) | VDOT pacing, marathon periodization, impact stress management | Jack Daniels VDOT, E/M/T/I/R paces, GAP, Cadence (spm), rTSS, Pace Decoupling |
| **Swimming Coach** | [`coach/swimming/`](coach/swimming/SKILL.md) | CSS threshold pacing, SWOLF efficiency, stroke mechanics, shoulder health | Critical Swim Speed (CSS), SWOLF score ($\text{Time} + \text{Strokes}$), DPS, sTSS |
| **Rowing Coach** | [`coach/rowing/`](coach/rowing/SKILL.md) | 2K/5K split pacing, ergometer & water technique, drag factor, spine & rib health | Split /500m, Stroke Rate (spm), Wattage, Drag Factor, Drive:Recovery (1:2), rTSS |
| **Weight Training Coach** | [`coach/weight-training/`](coach/weight-training/SKILL.md) | RIR/RPE autoregulation, mesocycle design, powerlifting, concurrent integration | Reps in Reserve (RIR 0-4), 1RM %, Volume Load, VBT, mTOR/AMPK balancing |
| **Triathlon Coach** | [`coach/triathlon/`](coach/triathlon/SKILL.md) | Multi-sport load balancing, brick workouts, transition mechanics (T1/T2) | Composite Load ($\text{cTSS}$), T2 Brick runs, T1/T2 setup, Sprint/Olympic pacing |
| **Ironman Coach** | [`coach/ironman/`](coach/ironman/SKILL.md) | 70.3 & 140.6 ultra-endurance pacing, high-carb gut training, 21-day taper | Bike IF caps ($\le 0.73$), 80-120g/hr carbs, 800-1200mg/hr sodium, Special Needs |
| **XC Skiing Coach** | [`coach/xc-skiing/`](coach/xc-skiing/SKILL.md) | Skate & Classic subtechniques, roller skiing, cold-air airway safety | V1/V2/V2-Alt shifting, Double Poling core flex, Roller-skiing, Vasaloppet |
| **Sports Nutrition Coach** | [`coach/sports-nutrition/`](coach/sports-nutrition/SKILL.md) | Evidence-based sports nutrition, macro periodization, intra-workout fueling, RED-S | Carbohydrate scaling (3-12g/kg), 30-120g/h carbs, 300-1000mg/h sodium, EA $\ge 45$, AIS supplements |

### 🛡️ System Administration & Security (`sysadmin/`)

| Skill Name | Directory | Primary Focus & Domain | Key Metrics & Methods |
| ------------ | ----------- | ------------------------ | ----------------------- |
| **Firewall Admin** | [`sysadmin/firewall-admin/`](sysadmin/firewall-admin/SKILL.md) | Enterprise firewall rule design, stateful packet filtering, NAT, VPN tunnels, threat inspection | Zone Security (DMZ/LAN/WAN), SNAT/DNAT, IKEv2 IPsec, WireGuard, `nftables`, IPS/DPI |
| **Proxmox Admin** | [`sysadmin/proxmox-admin/`](sysadmin/proxmox-admin/SKILL.md) | Proxmox VE 9.x node/cluster lifecycle, ZFS/Ceph Squid storage, SDN Fabrics, VM/LXC orchestration | Corosync 3, `pvecm`, `qm`/`pct`, ZFS OpenZFS 2.3, Ceph 19.2, PBS, HA Affinity |

*(More categories—such as Software Engineering, Writing & Communications, and Productivity—can be added as dedicated skill subdirectories!)*

---

## 🔌 Live Athletic Data Integration (MCP Server)

To enable your AI coaching skills to directly fetch live workouts, fitness metrics (CTL, ATL, TSB), wellness signals (HRV, RHR, Sleep), and activity stream data from [Intervals.icu](https://intervals.icu), pair these skills with the **[`intervals.icu-mcp`](https://github.com/jelmervdm/intervals.icu-mcp)** server:

- **Repository**: [`https://github.com/jelmervdm/intervals.icu-mcp`](https://github.com/jelmervdm/intervals.icu-mcp)
- **Capability**: Provides live tools and resources for AI agents to query Intervals.icu API endpoints (fitness trends, power/HR stream data, workout creation, and event calendar sync).
- **Supported Environments**: Claude Desktop, Antigravity IDE, Cursor, and VS Code.

---

## 🛠️ Repository Architecture

All skills strictly conform to the **Agent Skills Specification** (2-Tier Progressive Disclosure):

- **Tier 1 (`SKILL.md`)**: Contains YAML frontmatter, core prompt triggers, 5-step operational workflow, coaching/domain philosophy, routing table, and non-negotiable safety guardrails.
- **Tier 2 (`references/*.md`)**: Deep technical reference files loaded on-demand when specific sub-topics are triggered.

---

## 🚀 Installation & Integration Options

> [!TIP]
>
> ### 💡 Zero-Dependency Native Usage (No CLI or Plugins Required)
>
> Every skill in this repository is simply a plain Markdown file (`SKILL.md`). **You do not need Node.js, `npx`, plugins, or marketplace tools to use them.** You can simply copy the contents of any `SKILL.md` into your AI assistant's System Prompt, Project Context, or Custom GPT instructions!

### 1. Manual File Copy / Drop-In (Simplest & Zero Setup)

- **VS Code & Antigravity IDE**: Create a folder named `.agents/skills/` in your project root and copy skill folders into it. The IDE agent automatically reads it.
- **Claude Projects / Desktop**: Open [Claude.ai](https://claude.ai), create a Project, and upload `SKILL.md` and `references/*.md` directly as project context.
- **ChatGPT / Custom GPTs**: Paste `SKILL.md` into Custom GPT System Instructions and upload `references/` into Knowledge Files.
- **Local User Directory**: `cp -r ./coach/* ~/.claude/skills/` or `~/.agents/skills/`.

### 2. Optional CLI & GitHub Install Shortcuts

- **Claude Code CLI**:

  ```bash
  claude plugin install https://github.com/jelmervdm/skills
  ```

- **Agent Skills CLI** (Installs to 40+ AI Agents including Cursor, Windsurf, Claude):

  ```bash
  npx agent-skills-cli@latest add @jelmervdm/skills
  ```

- **skills.sh Ecosystem**:

  ```bash
  npx skills add jelmervdm/skills
  ```

- **Global User Directory (Local Copy)**:

  ```bash
  mkdir -p ~/.claude/skills
  cp -r ./coach/* ~/.claude/skills/
  ```

### 2. VS Code & Antigravity IDE

- **Workspace Skill Discovery**: Copy desired skill folders into `.agents/skills/` within your project root (e.g. `.agents/skills/cycling/` or `.agents/skills/coach/cycling/`). Agentic IDEs automatically detect and auto-load these skills.
- **Direct Workspace Referencing**: Tag skill files directly in agent prompts using `@coach/<sport>/SKILL.md`.
- **Gemini API**: Load `SKILL.md` content directly into `GenerativeModel(system_instruction=...)`.

### 3. Claude Desktop & Projects

- **Claude Projects**: Create a project, upload the desired `SKILL.md` and `references/*.md` files, and set project instructions.
- **Claude Desktop**: Paste `SKILL.md` into system prompt or attach files directly into conversation context.

### 4. OpenAI (ChatGPT / Custom GPTs / API)

- **Custom GPTs**: Paste `SKILL.md` instructions into the GPT Configuration box, and upload `references/*.md` into the GPT **Knowledge Files**.
- **OpenAI API**: Load `SKILL.md` as the `system` message string.

---

## 🤝 Community & Governance

We welcome contributions across all skill domains! To maintain high repository standards and foster a welcoming community:

- 📋 **[Contributing Guidelines](CONTRIBUTING.md)**: Rules for adding skills, progressive disclosure standards, and validation commands.
- 🛡️ **[Code of Conduct](CODE_OF_CONDUCT.md)**: Community standards adapted from the Contributor Covenant v2.1.
- 🔒 **[Security Policy](SECURITY.md)**: Disclosure policy for reporting security issues and prompt injection vectors.
- 💡 **[Propose a New Skill](https://github.com/jelmervdm/skills/issues/new?template=feature_request.md)**: Submit proposals for new specialized skills.
- 🐛 **[Report a Bug](https://github.com/jelmervdm/skills/issues/new?template=bug_report.md)**: Report skill errors, broken links, or validator issues.

---

## ⚖️ License & Credit

This repository is licensed under the **[MIT License](LICENSE)**.  
Created and maintained by **Jelmer** ([@jelmervdm](https://github.com/jelmervdm)).  
Feel free to fork, adapt, and expand into other domains! Please retain copyright credit in forks as required by the MIT License.
