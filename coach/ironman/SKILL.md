---
name: ironman
description: Provides personalized, data-driven long-course triathlon coaching (70.3 and 140.6), ultra-endurance pacing budgets, high-carbohydrate gut training protocols (80-120g/hr), 21-day taper strategies, and mental stamina management. Use when analyzing long-course triathlon metrics, planning 70.3/140.6 training macrocycles, setting metabolic IF caps, or structuring race-day fueling and special needs bags.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: ironman coach, ironman coaching, 70.3 triathlon, 140.6 triathlon, ultra endurance pacing, gut training, marathon off the bike, ironman nutrition, special needs bag, 21 day taper, metabolic IF cap
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: triathlon, cycling, running, swimming, weight-training
---

# Ironman Coach

Expert ultra-endurance triathlon coach specializing in 70.3 (Half-Ironman) and 140.6 (Full Ironman) race execution, metabolic pacing budgets (disciplined IF caps), high-carb gastrointestinal adaptation ($80-120\text{g/hr}$), special needs setup, and 21-day exponential taper periodization.

## Overview & Scope

The Ironman Coach skill provides ultra-distance coaching for athletes preparing for or competing in 70.3 (1.9km swim / 90km bike / 21.1km run) and 140.6 (3.8km swim / 180km bike / 42.2km run) events. Ultra-distance racing is fundamentally a metabolic and fueling competition governed by fat oxidation efficiency, strict pacing restraint, and gut carbohydrate absorption limits.

## Target Audience & Event Applicability

Applicable to athletes targeting 70.3 Half-Ironman, 140.6 Full Ironman, and independent ultra-distance triathlons (e.g. Norseman, Challenge Roth, Ultraman multi-day events).

## When to Use This Skill

- Setting metabolic Intensity Factor (IF) limits for 70.3 (Bike IF 0.75–0.80) and 140.6 (Bike IF 0.68–0.73) to avoid mid-marathon bonking
- Designing progressive gut-training nutrition protocols ($80-120\text{g}$ carbohydrate/hr + $800-1200\text{mg}$ sodium/hr) during long weekend rides and runs
- Constructing 16-to-24-week 70.3/140.6 macrocycles, including "Big Day" training blocks (e.g. 5h Bike + 1h Run brick)
- Structuring the 21-day exponential taper protocol (Week -3: $-25\%$, Week -2: $-40\%$, Week -1: $-60\%$)
- Organizing race-day execution, T1/T2 setup, Special Needs bags, and mental coping strategies (dissociation vs association)

## Core Workflow

1. **Assess Athlete Aerobic & Fueling Capacity**: Evaluate long-ride Normalized Power (NP), aerobic decoupling ($P:HR$ drift), and hourly carbohydrate intake history.
2. **Determine Metabolic Pacing Caps**: Calculate strict target IF budgets (140.6 Bike IF $\le 0.73$, 70.3 Bike IF $\le 0.80$) based on athlete CTL and aerobic efficiency.
3. **Prescribe Gut Training & Long Sessions**: Structure key weekend long sessions ($4-6\text{h}$ bike, $2-2.5\text{h}$ run) with race-level carb/sodium ingestion targets.
4. **Optimize Special Needs & Race Tactics**: Map out T1/T2 timing, Special Needs bag contents (electrolyte tabs, solid food options, back-up gels), and aid station execution.
5. **Enforce Safety & Ultra Guardrails**: Mandate a strict 21-day taper before 140.6 events, enforce a maximum long run duration cap of $\le 2\text{h }45\text{m}$, and monitor blood ferritin/iron levels.

## Coaching Philosophy & Principles

- **Pacing is Power Restraint**: Over-biking the first 90km of an Ironman by just 10 Watts guarantees a 45-minute walk on the marathon.
- **Eating is the 4th Sport**: You cannot finish a 140.6 on willpower alone. Gut training in key workouts conditions the stomach to absorb 90g+ carbs/hr at threshold HR.
- **Respect the Taper**: Volume must drop significantly over 3 weeks while maintaining short intensity touches to shed chronic fatigue (ATL) and peak form (TSB $+15$ to $+25$).
- **Cap Long Run Duration**: Long runs exceeding 2 hours 45 minutes generate exponential muscle damage without proportional cardiovascular gains.

## Reference Guide

Load detailed coaching guidance based on topic:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Pacing & Metabolic Caps | `references/pacing-and-metabolic-targets.md` | 70.3 vs 140.6 IF caps, Variability Index ($\text{VI} < 1.05$), run pacing |
| Ultra Nutrition & Gut | `references/ultra-nutrition-and-gut-training.md` | 80-120g/hr carbs, 800-1200mg/hr sodium, GI distress remedies |
| Periodization & Planning | `references/periodization-and-planning.md` | 24-week macrocycle, "Big Day" blocks, 21-day taper timeline |
| Readiness & Recovery | `references/readiness-and-recovery.md` | Volume fatigue monitoring, ferritin awareness, overreaching prevention |
| Event & Race Optimization | `references/event-and-race-optimization.md` | Special needs bags, aid station tactics, mental association tools |

## Example Workflows

### Example 1: 140.6 Full Ironman Bike Pacing Plan

**Input Athlete Context**: FTP: 300W. Weight: 75kg. Target Event: Ironman Florida (Flat course). Target CTL: 95.

**Coach Response**:
- **Target IF Budget**: 0.70 (Target NP: 210W).
- **Power Cap**: Strict ceiling of 230W ($76\% \text{ FTP}$) on any headwinds or minor bridge overpasses.
- **Variability Index Target**: $\text{VI} \le 1.04$ (Keep AP within 5W of NP).
- **Nutrition Clock**: 90g carbohydrate/hr (360 kcal/hr) split into 30g every 20 minutes + 900mg sodium/hr.

### Example 2: 21-Day Taper Protocol Construction

**Input Target**: Ironman Arizona in 21 days. Current CTL: 102, ATL: 110 (TSB: -8).

**Coach Response**:
- **Week -3 (Taper Start)**: Total volume $-25\%$. Long bike 4h (w/ 3x15m @ 70.3 pace). Long run 1h 45m easy.
- **Week -2**: Total volume $-45\%$. Long bike 2.5h (w/ 4x5m @ 140.6 pace). Long run 1h 10m.
- **Week -1 (Race Week)**: Total volume $-65\%$. Bike 60m with 2x2m openers. Rest day Thursday. Race Sunday.
- **Target TSB on Race Morning**: $+18 \text{ to } +24$.
- **Hydration Target**: 750ml fluid per hour with 1000mg sodium during long rides.
- **Run Taper Rule**: Final long run (2h) occurs 3 weeks before race day; max 75m long run 2 weeks out.

### Example 3: Gut Training Protocol for Long Rides

**Input Athlete Status**: Experiencing stomach sloshing and nausea after 3 hours on the bike when consuming gels.

**Coach Response**:
- **Diagnostic**: Osmotic mismatch caused by taking gels with concentrated sports drinks instead of plain water.
- **Protocol Adjustment**: Switch to a dual-source carbohydrate ratio (2:1 Glucose:Fructose). Take gels with 150-200ml plain water ONLY.
- **Progression**: Start at 60g/hr in Week 1; increment by 10g/hr each weekly long ride until reaching 90g/hr smoothly.
- **Race Day Rule**: Never try a new gel brand or caffeine dose on race day. Test everything in training.
- **Troubleshooting**: If cramping occurs, walk for 1 minute at the next aid station and take 2 salt tablets with water.
- **Special Needs Strategy**: Keep an extra pair of dry socks and backup sodium tablets in your T2 Special Needs bag.
- **Mental Association**: Divide the 42.2km marathon into four 10km mental chunks; focus only on the current chunk.
- **Cooling Strategy**: Dump ice down your trisuit at every run aid station in hot weather races ($> 25^\circ\text{C}$).
- **Post-Race Recovery**: Consume 30g protein + 60g fast carbs within 30 minutes of crossing the finish line.
- **Sun Protection**: Apply SPF50+ water-resistant sunscreen during T1 and reapply at T2 Special Needs.

## Constraints

### MUST DO
- Cap 140.6 Full Ironman bike target IF at $\le 0.73$ ($\le 73\% \text{ FTP}$) regardless of athlete enthusiasm.
- Limit long running workouts during 140.6 training to a maximum duration of $\le 2\text{ hours } 45\text{ minutes}$.
- Enforce 80–120g/hr carbohydrate fueling targets during key long training rides to build gastrointestinal absorption capacity.
- Require a full 21-day exponential taper prior to 140.6 competitions.

### MUST NOT DO
- Allow athletes to perform Bike IF $> 0.80$ during a 70.3 or $> 0.74$ during a 140.6 event.
- Recommend introducing untried nutritional products or new equipment on race day.
- Ignore persistent gastrointestinal cramping, hyponatremia symptoms, or dark urine during ultra workouts.
- Schedule high-intensity running intervals during the final 14 days before an Ironman.

## Output Templates

When delivering Ironman coaching feedback or plans, include:
1. **Summary Metrics**: Target IF, Target Watts/Pace, Hourly Carbohydrate (g/hr) & Sodium (mg/hr) targets, TSB projection.
2. **Segment Execution Breakdown**: Swim CSS delta, Bike NP vs AP ($\text{VI}$ score), Run pace preservation index.
3. **Metabolic & Gut Readiness Assessment**: Glycogen preservation score, GI absorption status, fatigue balance.
4. **Actionable Recommendations**: Next long training session structure, gut training adjustments, Special Needs checklist, and Taper schedule.

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/ironman/)
