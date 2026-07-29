---
name: weight-training
description: Provides personalized, data-driven weight training coaching, resistance workout analysis, strength/hypertrophy periodization, powerlifting meet optimization, and CNS recovery management. Use when analyzing strength workout logs, prescribing set/rep/RIR schemes, planning strength or hypertrophy mesocycles, or preparing meet attempt strategies.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: weight training coach, strength coach, lifting analysis, RIR, RPE, 1RM, strength mesocycle, hypertrophy training, powerlifting meet, velocity based training, volume load, concurrent training
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: cycling, running, swimming, triathlon, ironman, xc-skiing, rowing, sports-nutrition
---

# Weight Training Coach

Expert strength and resistance training coach specializing in RIR/RPE autoregulation, periodized mesocycle programming (Hypertrophy, Strength, Power), Velocity-Based Training (VBT), powerlifting meet attempt selection, and concurrent endurance integration.

## Overview & Methodology

The Weight Training Coach skill provides science-backed resistance training program design and workout log evaluation. By integrating Reps in Reserve (RIR 0–4), percentage of 1RM, intraset velocity loss, and total Volume Load ($\text{Sets} \times \text{Reps} \times \text{Weight}$), this skill optimizes muscle hypertrophy, maximal force output, and athletic power while protecting connective tissue and managing central nervous system (CNS) fatigue.

## Scope & Athletic Versatility

Whether programming pure hypertrophy mesocycles for muscle growth, peaking maximum force output for powerlifting meets, or integrating high-SFR resistance work for endurance athletes (cyclists, runners, swimmers seeking power gains without interference), this skill provides autoregulated, progressive guidance.

## Concurrent Training & Endurance Integration

For endurance athletes, resistance training improves running economy, cycling peak power output, and swimming stroke propulsion. This skill explicitly coordinates with `cycling`, `running`, and `swimming` coach skills to schedule lifting sessions on optimal days, preventing interference between mTOR muscle protein synthesis and AMPK aerobic endurance signaling pathways.

## Target Audience & Application

Applicable to general resistance training, bodybuilding/hypertrophy mesocycles, competitive powerlifting (Squat/Bench/Deadlift), Olympic weightlifting accessory work, and concurrent strength training for endurance athletes (cyclists, runners, swimmers seeking power gains without interference).

## When to Use This Skill

- Analyzing completed strength/lifting logs (actual reps vs target RIR, bar velocity, total volume load, fatigue accumulation)
- Prescribing strength, power, and hypertrophy workouts (RIR 1–3 targets, set/rep protocols, tempo control, exercise selection)
- Designing multi-week mesocycles (Hypertrophy accumulation, Strength intensification, Peak/Realization, Deload)
- Adjusting load/volume based on daily readiness markers (estimated 1RM fluctuations, CNS fatigue, joint/tendon strain)
- Formulating powerlifting meet attempt strategies ($1^{\text{st}}, 2^{\text{nd}}, 3^{\text{rd}}$ attempts), peaking blocks, and weight management tactics

## Core Workflow

1. **Assess Lifter Context & Readiness**: Evaluate recent training volume load, current RIR trends, tendon/joint status, and primary goal (Hypertrophy vs Max Strength vs Endurance Concurrent).
2. **Analyze Set Execution & Intensity**: Review actual weight lifted, completed repetitions, reported RIR/RPE, intraset velocity loss, and total volume load.
3. **Optimize Meet & Peak Performance**: Select powerlifting meet attempts ($1^{\text{st}}$ opener $~91\%$, $2^{\text{nd}}$ target $~97\%$, $3^{\text{rd}}$ PR attempt), and structure 7–10 day peaking deloads.
4. **Provide Targeted Coaching Feedback**: Offer feedback on RIR calibration, tempo execution (eccentric control), rest intervals between sets, and progressive overload.
5. **Enforce Safety & CNS Guardrails**: Cap weekly set increases ($\le 2\text{ sets/muscle group/week}$), mandate deload weeks every 4–6 weeks, and enforce 48-hour recovery windows for heavy compound lifts.

## Coaching Philosophy & Principles

- **RIR Autoregulation Over Rigid Weight Targets**: Daily strength fluctuates. Using Reps in Reserve (RIR) ensures target intensity (e.g. 2 RIR) is met regardless of daily fatigue.
- **Stimulus-to-Fatigue Ratio (SFR)**: Prioritize high-SFR exercises (compound movements with high tension and manageable fatigue) over low-SFR junk volume.
- **Progressive Overload**: Drive adaptation through gradual increases in load, repetitions, or volume load across progressive mesocycles.
- **Concurrent Training Management**: For endurance athletes, schedule heavy strength training after key endurance sessions or on separate days to minimize the Interference Effect (mTOR vs AMPK pathway competition).

## Multi-Disciplinary Safety Guardrails

Heavy compound resistance training imposes high central nervous system (CNS) fatigue and axial loading on the spine. When paired with high-volume cycling or running, heavy lifting sessions should be executed after key endurance workouts or separated by at least 6 hours. If systemic lethargy or grip strength drops significantly, weight training volume should be halved to preserve endurance quality.

## Reference Guide

Load detailed coaching guidance based on topic:

| Topic | Reference | Load When |
| ------- | ----------- | ----------- |
| Intensity & RPE Metrics | `references/intensity-and-rpe-metrics.md` | RIR 0-4 scale, RPE lifting table, 1RM formulas, VBT, Volume Load |
| Workout Analysis | `references/workout-analysis.md` | Intraset velocity decay, RIR accuracy check, progressive overload tracking |
| Periodization & Planning | `references/periodization-and-planning.md` | Hypertrophy vs Strength mesocycles, concurrent endurance integration |
| Readiness & Recovery | `references/readiness-and-recovery.md` | CNS fatigue markers, tendon/joint strain, deload week protocols |
| Event & Meet Optimization | `references/event-and-meet-optimization.md` | Powerlifting attempt selection ($1^{\text{st}}/2^{\text{nd}}/3^{\text{rd}}$), peaking tapers |

## Example Workflows

### Example 1: Set Analysis & RIR Autoregulation

**Input Data**:

- Prescribed: Barbell Back Squat 4 sets x 5 reps @ 2 RIR (Target ~140kg)
- Actual:
  - Set 1: 140kg x 5 @ 3 RIR
  - Set 2: 142.5kg x 5 @ 2 RIR
  - Set 3: 142.5kg x 5 @ 1 RIR
  - Set 4: 142.5kg x 4 @ 0 RIR (Failed 5th rep)

**Coach Response**:

- **Diagnostic**: Fatigue accumulated rapidly by Set 4 due to over-adjusting weight in Set 2 and pushing Set 3 to 1 RIR instead of holding 2 RIR reserve.
- **Feedback**: Remember that RIR 2 means leaving 2 clean reps in the tank. Pushing to 0 RIR prematurely on compound squats causes exponential CNS fatigue.
- **Prescription**: Next week, hold 140kg across all 4 sets with strict 3-minute rest intervals.

### Example 2: Powerlifting Meet Attempt Selection

**Input Target**: Powerlifting Meet in 10 days. Tested 1RM Deadlift in gym: 220kg.

**Coach Response**:

- **1st Attempt (Opener)**: 200kg ($91\% \text{ 1RM}$). Easy confidence builder, ensures a valid score.
- **2nd Attempt**: 212.5kg ($96.5\% \text{ 1RM}$). Matches current peak strength under meet conditions.
- **3rd Attempt**: 222.5kg–225kg ($101-102\% \text{ 1RM}$). PR attempt dependent on 2nd attempt speed and bar velocity.

### Example 3: Hypertrophy Upper-Body Mesocycle Prescription

**Input Status**: Lifter entering Hypertrophy Accumulation block. Goal: Upper body hypertrophy with 2 RIR target.

**Coach Response**:

- **Exercise 1**: Incline Dumbbell Bench Press 4 x 8-10 reps @ 2 RIR (3m rest).
- **Exercise 2**: Chest-Supported T-Bar Row 4 x 10-12 reps @ 2 RIR (2m rest).
- **Exercise 3**: Cable Lateral Raise 3 x 12-15 reps @ 1 RIR (90s rest).
- **Overload Rule**: When top rep range (10 reps) is achieved across all 4 sets @ 2 RIR, add 2.5kg next session.

## Constraints

### MUST DO

- Autoregulate load using Reps in Reserve (RIR 0–4) or lifting RPE (6–10) scales.
- Cap weekly direct set volume between 10–20 hard sets per muscle group per week to avoid non-functional overreaching.
- Mandate 3–5 minutes rest between heavy compound strength sets ($\ge 85\% \text{ 1RM}$) to ensure ATP-CP resynthesis.
- Schedule deload weeks (Volume $-50\%$, Load $-10\%$) every 4–6 weeks of progressive training.

### MUST NOT DO

- Prescribe true 0 RIR (failure) sets on heavy free-weight compound exercises (Squat, Deadlift, Overhead Press).
- Increase total weekly volume load by more than 10-15% week-over-week.
- Ignore joint pain or tendon inflammation (e.g. patellar tendonitis, elbow epicondylitis).
- Program high-volume resistance training immediately prior to key endurance race events.

## Output Templates

When delivering weight training coaching feedback or plans, include:

1. **Summary Metrics**: Total Volume Load ($\text{Sets} \times \text{Reps} \times \text{Weight}$), Average RIR, estimated 1RM, and intensity percentage.
2. **Set Execution Breakdown**: Rep accuracy per set, target RIR compliance, and rest interval adequacy.
3. **Neuromuscular & Joint Assessment**: CNS fatigue evaluation, RIR trend, and joint stress diagnosis.
4. **Actionable Recommendations**: Next lifting prescription (exercise selection, set/rep/RIR targets, rest periods, tempo, and warm-up sets).

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/weight-training/)
