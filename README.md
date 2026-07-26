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
| **Weight Training Coach** | [`coach/weight-training/`](coach/weight-training/SKILL.md) | RIR/RPE autoregulation, mesocycle design, powerlifting, concurrent integration | Reps in Reserve (RIR 0-4), 1RM %, Volume Load, VBT, mTOR/AMPK balancing |
| **Triathlon Coach** | [`coach/triathlon/`](coach/triathlon/SKILL.md) | Multi-sport load balancing, brick workouts, transition mechanics (T1/T2) | Composite Load ($\text{cTSS}$), T2 Brick runs, T1/T2 setup, Sprint/Olympic pacing |
| **Ironman Coach** | [`coach/ironman/`](coach/ironman/SKILL.md) | 70.3 & 140.6 ultra-endurance pacing, high-carb gut training, 21-day taper | Bike IF caps ($\le 0.73$), 80-120g/hr carbs, 800-1200mg/hr sodium, Special Needs |
| **XC Skiing Coach** | [`coach/xc-skiing/`](coach/xc-skiing/SKILL.md) | Skate & Classic subtechniques, roller skiing, cold-air airway safety | V1/V2/V2-Alt shifting, Double Poling core flex, Roller-skiing, Vasaloppet |

*(More categories—such as Software Engineering, Writing & Communications, and Productivity—can be added as dedicated skill subdirectories!)*

---

## 🛠️ Repository Architecture

All skills strictly conform to the **Agent Skills Specification** (2-Tier Progressive Disclosure):

- **Tier 1 (`SKILL.md`)**: Contains YAML frontmatter, core prompt triggers, 5-step operational workflow, coaching/domain philosophy, routing table, and non-negotiable safety guardrails.
- **Tier 2 (`references/*.md`)**: Deep technical reference files loaded on-demand when specific sub-topics are triggered.

---

## 🚀 Integration & Usage Guide

### 1. Claude Desktop & Projects

- **Claude Projects**: Create a project, upload the desired `SKILL.md` and `references/*.md` files, and set project instructions.
- **Claude Desktop**: Paste `SKILL.md` into system prompt or attach files directly into conversation context.

### 2. OpenAI (ChatGPT / Custom GPTs / API)

- **Custom GPTs**: Paste `SKILL.md` instructions into the GPT Configuration box, and upload `references/*.md` into the GPT **Knowledge Files**.
- **OpenAI API**: Load `SKILL.md` as the `system` message string.

### 3. VS Code & Antigravity IDE

- **Workspace Skill Discovery**: Copy desired skill folders into `.agents/skills/` within your project root (e.g. `.agents/skills/cycling/` or `.agents/skills/coach/cycling/`). Agentic IDEs automatically detect and auto-load these skills.
- **Direct Workspace Referencing**: Tag skill files directly in agent prompts using `@coach/<sport>/SKILL.md`.
- **Gemini API**: Load `SKILL.md` content directly into `GenerativeModel(system_instruction=...)`.

---

## ⚖️ License & Credit

This repository is licensed under the **MIT License**.  
Created and maintained by **Jelmer** ([@jelmervdm](https://github.com/jelmervdm)).  
Feel free to fork, adapt, and expand into other domains! Please retain copyright credit in forks as required by the MIT License.
