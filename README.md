# Athletic Performance Coaching Agent Skills

[![Validate Agent Skills](https://github.com/jelmervdm/skills/actions/workflows/validate-skills.yml/badge.svg)](https://github.com/jelmervdm/skills/actions/workflows/validate-skills.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Author: jelmervdm](https://img.shields.io/badge/Author-jelmervdm-blue.svg)](https://github.com/jelmervdm)

Production-grade, 2-Tier Progressive Disclosure AI agent skills for endurance sports, resistance training, and multi-sport competition. Engineered for LLMs (Claude, GPT-4o, Gemini) to deliver data-backed workouts, periodization, race pacing, and fatigue management.

---

> [!CAUTION]
> ### ⚠️ Medical & Athletic Safety Disclaimer
> The training guidance, metrics, pacing formulas, and physiological recommendations contained in these skills are intended for informational, educational, and athletic coaching support only. **They do not constitute medical advice.** High-intensity endurance training, heavy resistance lifting, and extreme cold/heat exposure carry inherent physiological risks. Always consult a qualified physician or sports medicine specialist before undertaking new training regimens, especially if you have pre-existing cardiovascular, respiratory, or musculoskeletal conditions.

---

## 🏆 Available Coaching Skills

| Skill Name | Directory | Primary Focus & Domain | Key Metrics & Methods |
|------------|-----------|------------------------|-----------------------|
| **Cycling Coach** | [`coach/cycling/`](coach/cycling/SKILL.md) | Power-based cycling, workout analysis, race pacing, event optimization | Coggan Z1-Z7, FTP, NP, IF, TSS, TSB, Aerobic Decoupling, Intervals.icu |
| **Running Coach** | [`coach/running/`](coach/running/SKILL.md) | VDOT pacing, marathon periodization, impact stress management | Jack Daniels VDOT, E/M/T/I/R paces, GAP, Cadence (spm), rTSS, Pace Decoupling |
| **Swimming Coach** | [`coach/swimming/`](coach/swimming/SKILL.md) | CSS threshold pacing, SWOLF efficiency, stroke mechanics, shoulder health | Critical Swim Speed (CSS), SWOLF score ($\text{Time} + \text{Strokes}$), DPS, sTSS |
| **Weight Training Coach** | [`coach/weight-training/`](coach/weight-training/SKILL.md) | RIR/RPE autoregulation, mesocycle design, powerlifting, concurrent integration | Reps in Reserve (RIR 0-4), 1RM %, Volume Load, VBT, mTOR/AMPK balancing |
| **Triathlon Coach** | [`coach/triathlon/`](coach/triathlon/SKILL.md) | Multi-sport load balancing, brick workouts, transition mechanics (T1/T2) | Composite Load ($\text{cTSS}$), T2 Brick runs, T1/T2 setup, Sprint/Olympic pacing |
| **Ironman Coach** | [`coach/ironman/`](coach/ironman/SKILL.md) | 70.3 & 140.6 ultra-endurance pacing, high-carb gut training, 21-day taper | Bike IF caps ($\le 0.73$), 80-120g/hr carbs, 800-1200mg/hr sodium, Special Needs |
| **XC Skiing Coach** | [`coach/xc-skiing/`](coach/xc-skiing/SKILL.md) | Skate & Classic subtechniques, roller skiing, cold-air airway safety | V1/V2/V2-Alt shifting, Double Poling core flex, Roller-skiing, Vasaloppet |

---

## 🛠️ Repository Architecture

All skills strictly conform to the **Agent Skills Specification** (2-Tier Progressive Disclosure):

- **Tier 1 (`SKILL.md`)**: Contains YAML frontmatter, core prompt triggers, 5-step operational workflow, coaching philosophy, routing table, and non-negotiable safety guardrails. (Token efficient).
- **Tier 2 (`references/*.md`)**: Deep technical reference files loaded on-demand when specific sub-topics are triggered (e.g. `race-and-pacing.md`, `readiness-and-recovery.md`).

---

## 🚀 Application Integration Guide

### 1. Claude Desktop & Claude Projects

To add these skills to **Claude Desktop** or **Claude.ai Projects**:

#### Method A: Custom Project Context (Recommended)
1. Open [Claude.ai](https://claude.ai) or Claude Desktop and create a new **Project** (e.g. *"My Endurance Coach"*).
2. Click **Add Content** -> **Upload Files**.
3. Select the desired Tier 1 `SKILL.md` (e.g. `coach/cycling/SKILL.md`) and relevant Tier 2 reference files from `references/`.
4. In the **Project Instructions**, paste the following prompt:
   ```text
   You are an expert endurance athletic coach. Follow the workflows, physiological boundaries, and reference guides defined in the attached SKILL.md and reference files. Always prioritize athlete safety and data-backed pacing.
   ```

#### Method B: Local System Prompt
Copy the contents of Tier 1 `SKILL.md` directly into the system prompt input box in Claude.

---

### 2. OpenAI (ChatGPT / Custom GPTs / API)

To deploy a skill as an **OpenAI Custom GPT**:

1. Go to [ChatGPT -> Explore GPTs -> Create a GPT](https://chatgpt.com/gpts/editor).
2. Under **Configure**:
   - **Name**: `Cycling & Endurance Coach` (or sport of choice).
   - **Description**: `Data-driven athletic performance coach by @jelmervdm`.
   - **Instructions**: Open the desired `SKILL.md` file, copy lines 16 through end, and paste into the **Instructions** text box.
   - **Knowledge**: Click **Upload files** and select all `.md` files inside the `references/` directory for that skill.
3. Enable Code Interpreter / Data Analysis if analyzing `.csv` workout exports (e.g., Intervals.icu or Strava data).

#### OpenAI API Integration (Python)
```python
from openai import OpenAI

client = OpenAI()

# Load Tier 1 SKILL.md
with open("coach/cycling/SKILL.md", "r") as f:
    skill_prompt = f.read()

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": skill_prompt},
        {"role": "user", "content": "My TSB is -32 and my HRV dropped 20% today. I have 4x8m VO2max intervals scheduled. What should I do?"}
    ]
)
print(response.choices[0].message.content)
```

---

### 3. Gemini & Antigravity IDE

To use these skills with **Google Gemini** or within **Antigravity IDE**:

#### In Antigravity IDE / Gemini Workspace
1. Ensure the `skills/` directory is in your active workspace (e.g. `/home/jelmer/skills/coach/`).
2. When starting a coaching prompt, tag the skill file or reference path:
   ```text
   @coach/cycling/SKILL.md Analyze my last ride where NP was 240W and HR drifted from 140 to 160 bpm over 2 hours.
   ```

#### Gemini API System Instruction
```python
import google.generativeai as genai

genai.configure(api_key="YOUR_API_KEY")

with open("coach/cycling/SKILL.md", "r") as f:
    cycling_skill = f.read()

model = genai.GenerativeModel(
    model_name="gemini-1.5-pro",
    system_instruction=cycling_skill
)

response = model.generate_content("Calculate my aerobic decoupling if 1st half EF was 1.40 and 2nd half EF was 1.32.")
print(response.text)
```

---

## 📜 License & Attribution

This repository is licensed under the **MIT License**.

Created and maintained by **Jelmer** ([@jelmervdm](https://github.com/jelmervdm)).  
Contributions, bug reports, and PRs are welcome!
