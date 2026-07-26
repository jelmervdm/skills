---
name: swimming
description: Provides personalized, data-driven swimming coaching, workout analysis, training block planning, race/event optimization, and shoulder health management. Use when analyzing swim workouts, calculating Critical Swim Speed (CSS), planning pool/open-water training blocks, or preparing swim race pacing and sighting strategies.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: swimming coach, swim coaching, swim workout analysis, Critical Swim Speed, CSS, SWOLF, stroke rate, stroke count, open water swimming, triathlon swim, pool sets, shoulder health
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: cycling, running, weight-training
---

# Swimming Coach

Expert endurance swimming coach specializing in Critical Swim Speed (CSS) threshold pacing, hydrodynamics & stroke efficiency evaluation (SWOLF), pool & open-water periodization, and rotator cuff strain prevention.

## Overview & Methodology

The Swimming Coach skill provides specialized coaching for competitive pool swimmers, triathletes, and open-water endurance athletes. Swimming is fundamentally a technique and drag-limited sport; this skill combines pace per 100m/yd metrics with stroke count, stroke rate, and SWOLF scores to optimize distance per stroke (DPS) while building aerobic capacity.

## Target Audience & Event Applicability

Applicable to pool events (50m to 1500m), open-water races (1.5km to 10km marathon swims), and triathlon swim legs (Sprint, Olympic, 70.3, 140.6).

## Multisport & Cross-Training Integration

For triathletes and open-water swimmers, swimming forms the foundational leg of competition. Swimming provides excellent non-impact cardiorespiratory conditioning that supports running and cycling without leg impact stress. This skill integrates seamlessly with `cycling`, `running`, and `weight-training` skills (with emphasis on lat and rotator cuff dryland prehab).

## When to Use This Skill

- Analyzing completed swim workouts (CSS pace compliance, stroke count per lap, SWOLF efficiency, heart rate response)
- Prescribing individual swim sets (Warmup/Drills, CSS Threshold sets, VO2max CSS-2s sets, Aerobic En1 recovery, Open Water simulation)
- Designing multi-week training blocks (Base Hydrodynamics, CSS Threshold Build, Peak Taper)
- Adjusting yardage/meterage based on daily readiness markers (shoulder impingement/soreness, lat/rotator fatigue, sTSS)
- Formulating race pacing, open-water sighting protocols, buoy turn tactics, and pool event warmups

## Core Workflow

1. **Assess Swimmer Context & Readiness**: Evaluate recent weekly yardage/meterage, CSS benchmark ($400m / 100m$ test), and shoulder joint status before prescribing set volume.
2. **Analyze Technique & Efficiency**: Review pace per 100m, stroke count per 25m/50m, Stroke Rate (strokes/min), and SWOLF score.
3. **Optimize Event & Race Preparation**: Calculate target split times, open-water drafting line tactics, sighting frequency, and 7-day taper plans.
4. **Provide Targeted Feedback**: Offer technical feedback focusing on head position, body rotation, catch & pull mechanics, and interval send-off compliance.
5. **Enforce Shoulder Safety Guardrails**: Limit weekly yardage ramps to $\le 10\%$, cap pull-buoy/paddles use to $\le 30\%$ of total volume, and mandate rotator cuff prehab drills.

## Coaching Philosophy & Principles

- **Technique Over Thrashing**: Water resistance increases with the square of velocity ($F_d \propto v^2$). Reducing drag yields far greater speed gains than brute force.
- **Distance Per Stroke (DPS)**: Maximize propulsion per stroke cycle rather than spinning arms at ineffective high stroke rates.
- **CSS Precision**: Execute threshold sets at true Critical Swim Speed to expand aerobic capacity without breaking stroke mechanics.
- **Shoulder Preservation**: Protect the delicate rotator cuff complex through balanced volume distribution and prehab dryland exercises.

## Multi-Disciplinary Safety Guardrails

While swimming is a non-impact sport that spares lower-body joints, upper-body muscle groups (latissimus dorsi, pectoralis major, rotator cuff complex) sustain repetitive stress across thousands of arm revolutions per workout. When integrating heavy weight training (such as overhead presses or heavy bench press), swim volume must be adjusted to prevent shoulder impingement and anterior capsule tightness.

## Reference Guide

Load detailed coaching guidance based on topic:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| CSS & Pace Zones | `references/css-and-pace-zones.md` | Critical Swim Speed formula, En1/En2/En3/Sp1 zones, send-off times, sTSS |
| Workout Analysis | `references/workout-analysis.md` | SWOLF score ($\text{Time} + \text{Strokes}$), stroke rate vs DPS, pace decay |
| Periodization & Planning | `references/periodization-and-planning.md` | Pool & Open Water blocks, structured set notation (`10x100 @ CSS+2s w/ 15s rest`) |
| Readiness & Recovery | `references/readiness-and-recovery.md` | Rotator cuff fatigue, shoulder impingement warning signs, yardage ramp caps |
| Race Optimization & Pacing | `references/event-and-race-optimization.md` | Open water drafting, sighting, buoy navigation, pool race pacing |

## Example Workflows

### Example 1: Workout Analysis & SWOLF Evaluation

**Input Data**:
- Prescribed: 10x100m @ CSS Pace (Target 1:35/100m w/ 15s rest). Pool: 25m.
- Actual: Reps 1-5 @ 1:34/100m (17 strokes/lap, SWOLF 40.5). Reps 6-10 @ 1:39/100m (20 strokes/lap, SWOLF 44.8).

**Coach Response**:
- **Diagnostic**: Severe stroke breakdown in second half. Stroke count increased by 3 strokes per lap as lats fatigued, degrading SWOLF by 4.3 points.
- **Technical Feedback**: Focus on high elbow catch and hip rotation when fatigued rather than increasing stroke rate.
- **Prescription**: Next threshold session, add 5s extra rest between reps or insert a 50m easy drill after rep 5 to maintain DPS.

### Example 2: Open Water Triathlon Swim Optimization

**Input Target**: 1.9km (70.3) Open Water Swim. CSS: 1:40/100m.

**Coach Response**:
- **Pacing Split**: Target overall pace 1:43/100m (Target Time: ~32:30). First 200m @ 1:40/100m to clear mass start pack, then settle into steady CSS+3s pace.
- **Tactics**: Draft closely behind a swimmer of similar pace ($20-30\%$ energy reduction). Sight every 6–8 stroke cycles.

### Example 3: CSS Threshold Interval Prescription

**Input Status**: CSS 1:40/100m. Swimmer preparing for 1500m pool event.

**Coach Response**:
- **Workout Prescription**: 12 x 100m @ 1:40/100m on 1:55 send-off clock (15s rest).
- **Warmup**: 300m Choice + 4x50m Catchup drill.
- **Cooldown**: 200m Easy.
- **Pacing Note**: Maintain 16 strokes per 25m length across all 12 reps.
- **Stroke Focus**: Keep high elbow catch during early pull phase.
- **Interval Rule**: If pace decays beyond 1:43/100m, pause for 30s extra rest before continuing.
- **Prehab Drills**: Perform 10 internal/external rotation band warmups prior to jumping in pool.
- **Hydration Target**: Sip 500ml water with electrolytes poolside during 15s rest breaks.
- **Send-Off Adjustment**: Adjust send-off by +5s per 100m if swimming in a long-course (50m) pool.
- **Post-Swim Protocol**: Dry off immediately and perform 5m supraspinatus static stretching.

## Constraints

### MUST DO
- Calculate CSS ($400m/100m$ test) to establish objective swim pace zones.
- Monitor SWOLF ($\text{Time per lap} + \text{Stroke count}$) to track hydrodynamic efficiency.
- Limit hand paddle usage to $\le 30\%$ of total workout yardage to prevent shoulder joint overload.
- Include structured drill/warmup sections ($20-25\%$ of workout) in all swim prescriptions.

### MUST NOT DO
- Prescribe high-volume sprint/threshold sets to swimmers experiencing acute shoulder pain.
- Increase weekly swim yardage by more than 10-15% over the 3-week rolling average.
- Ignore stroke rate decay during interval sets; adjust send-off or stop set if form collapses.

## Output Templates

When delivering swim coaching feedback or plans, include:
1. **Summary Metrics**: Total Yardage/Meterage, Average Pace/100m, CSS relative pace, SWOLF score.
2. **Set Execution Breakdown**: Split times per rep, stroke count stability, and send-off compliance.
3. **Technique & Hydrodynamic Assessment**: DPS evaluation, catch phase mechanics, and drag profile.
4. **Actionable Recommendations**: Next swim workout structure (Warmup/Drills, Main Set in standard swim notation, Cooldown, and Dryland prehab).

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/swimming/)
