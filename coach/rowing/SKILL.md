---
name: rowing
description: Provides personalized, data-driven rowing coaching, workout analysis, training block planning, race/event optimization, and lumbar/rib health management. Use when analyzing rowing workouts, determining 2K/5K split zones, adjusting drag factor, planning ergometer/on-water training blocks, or preparing race pacing strategies.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: rowing coach, rowing coaching, ergometer workout analysis, Concept2, 2K test, split pace, stroke rate, SPM, drag factor, head race, ergometer, water rowing, lumbar health
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: cycling, running, swimming, weight-training, triathlon
---

# Rowing Coach

Expert rowing coach specializing in split pace per 500m targets, stroke rate (SPM) kinetics, Concept2 ergometer & water shell biomechanics, drag factor optimization, UT2-to-AN periodization, and spinal/rib fatigue management.

## Overview & Scope

Rowing is a whole-body endurance sport combining intense leg drive, core bracing, and upper-body pull across repetitive rowing strokes. The Rowing Coach skill provides physiological, technical, and structural guidance for stationary ergometer training (Concept2, WaterRower, RP3) and on-water rowing (sculling and sweep).

## Target Audience & Event Applicability

Applicable to competitive crew rowers, masters rowers, indoor ergometer racers, cross-fit athletes, and multisport endurance rowers. Covers 2K sprint racing, 5K/6K autumn head races, ultra-distance ergometer challenges (10K, half-marathon, marathon), and ergometer interval conditioning modules.

## Multisport & Cross-Training Integration

Rowing recruits over 86% of total body muscle mass with zero foot-impact stress, making it an outstanding cross-training modality for cycling, running, and swimming. This skill coordinates with `cycling`, `running`, `swimming`, and `weight-training` skills (prioritizing posterior chain hypertrophy, hip hinge mechanics, deadlifts, and thoracic extension).

## When to Use This Skill

- Analyzing completed rowing sessions (500m split pace, average stroke rate, power per stroke, heart rate drift, and stroke force profile)
- Establishing training pace zones based on a 2K baseline time trial (UT2, UT1, AT, TR, and AN zones)
- Setting optimal ergometer drag factor (damper setting) tailored to athlete body weight, gender, and rowing discipline
- Structuring seasonal periodization blocks (Autumn Head Race 6K preparation, Winter Ergometer Base, Spring 2K Sprint Peak)
- Prescribing technical drills to correct rush on the slide, early arm pull, shooting the slides, or weak catch connection
- Managing lumbar spine load, core bracing protocols, and rib stress fracture avoidance during high-yardage blocks

## Core Workflow

1. **Assess Rower Profile & Baseline**: Evaluate 2K benchmark split, current 500m pace targets, drag factor setting, and spinal/back health history before prescribing sets.
2. **Analyze Mechanics & Power Curves**: Review pace per 500m, Stroke Rate (SPM), drive-to-recovery ratio (1:2 rhythm), and watt output per stroke cycle.
3. **Optimize Event & Race Pacing**: Formulate split strategies for 2K ergometer tests or 5K/6K head races, including start sprints, mid-race moves, and final sprint protocols.
4. **Deliver Technical Guidance**: Focus on sequential body mechanics (Legs-Trunk-Arms on drive, Arms-Trunk-Legs on recovery) and ratio control across all intensity zones.
5. **Enforce Back & Rib Safety Guardrails**: Cap high-rate drag factors, monitor lower back stiffness, enforce hip hinge flexibility, and manage total weekly meterage.

## Coaching Philosophy & Principles

- **Leg Drive Dominance**: The rowing stroke is $60\%$ legs, $20\%$ core/trunk, and $20\%$ arms/pull. Never pull early with arms before leg drive finishes.
- **Ratio & Rhythm (1:2)**: Drive fast and explosive ($1$ part time); recover controlled and relaxed ($2$ parts time). Avoid rushing the slide into the catch.
- **Drag Factor Precision**: Set damper by electronic drag factor ($110-130$), not by numbers on the plastic flywheel casing.
- **Spinal Integrity**: Maintain neutral lumbar spine alignment under compression at the catch; leverage hip hinging rather than spinal flexion.

## Reference Guide

Load detailed coaching guidance based on topic:

| Topic | Reference | Load When |
| ------- | ----------- | ----------- |
| Split & Stroke Metrics | `references/split-and-stroke-metrics.md` | 500m split zones, stroke rate (SPM), wattage conversions, drag factor settings |
| Workout Analysis | `references/workout-analysis.md` | Force curve dynamics, stroke power, drive vs recovery ratio, rTSS load tracking |
| Periodization & Planning | `references/periodization-and-planning.md` | UT2/UT1/AT/TR/AN periodization, 2K & 6K macrocycles, ergometer set notation |
| Readiness & Recovery | `references/readiness-and-recovery.md` | Lumbar spine safety, rib intercostal protection, forearm grip strain, volume caps |
| Event & Race Optimization | `references/event-and-race-optimization.md` | 2K ergometer race execution, 5K/6K head race tactics, stroke seat rate calling |

## Example Workflows

### Example 1: Ergometer 2K Pacing & Split Decay Diagnostic

**Input Data**:

- Goal: Sub-7:00 2K (Target Average Split: 1:45.0/500m @ 32 SPM).
- Actual Splits: 0-500m @ 1:40.5 (36 SPM); 500-1000m @ 1:44.2 (33 SPM); 1000-1500m @ 1:49.8 (29 SPM); 1500-2000m @ 1:48.5 (31 SPM). Final: 7:03.0.

**Coach Response**:

- **Diagnostic**: Fly-and-die profile. Opening 500m was 4.5 seconds faster than target split, depleting anaerobic glycogen prematurely and causing a 9.3-second split decay in the 3rd 500m.
- **Pacing Plan**: Re-execute with conservative start: First 250m @ 1:43.0, settle into 1:45.5 for 250-1500m, and sprint final 500m @ 1:42.0.
- **Technical Correction**: Keep handle height level at the release to prevent washing out under high lactate fatigue.

### Example 2: UT2 Aerobic Base & Drag Factor Prescription

**Input Context**: Heavy winter aerobic base phase. Rower setting damper to 10 (Drag Factor 180) thinking higher drag builds more endurance.

**Coach Response**:

- **Correction**: High drag factor ($>150$) increases lumbar compressive loads significantly without improving aerobic adaptation.
- **Adjustment**: Lower damper to achieve Drag Factor 120 (Open Heavyweight Men) or 110 (Lightweight/Women).
- **Session Prescribed**: 2 x 30 minutes UT2 @ 20 SPM, pace 2K + 16s (w/ 3m rest). Maintain 1:2 drive-to-recovery ratio.
- **Biomechanical Note**: Focus on hanging body weight off the handle during leg drive rather than pulling with biceps.
- **Recovery Note**: Execute 5 minutes of cat-cow and hamstrings stretching immediately after unstrapping feet.

### Example 3: Head Race (5K/6K) Race Strategy & Stroke Rate Plan

**Input Event**: Autumn 5K Head Race. Benchmark 2K Split: 1:40.0.

**Coach Response**:

- **Target Pace**: 5K Target Split = 2K + 6-8s = 1:47.0/500m @ 26-28 SPM.
- **Execution Plan**:
  - **Start (0-200m)**: 5 high strokes + 10 building strokes to establish shell velocity (34 SPM).
  - **Body of Race (200m-4500m)**: Settle onto 27 SPM at 1:47.0/500m. Execute 10-stroke power bursts every 1000m to maintain rhythm.
  - **Finish (4500m-5000m)**: Increase rate +2 SPM (29-30 SPM) and drive split under 1:44.0.
- **Coxswain / Stroke Call**: Call "Ratio & Send" at the 2500m mark to prevent rushing the slide as fatigue builds.
- **Hydration Protocol**: Sip 500ml electrolyte solution during 20-minute pre-race water warm-up.

## Constraints

### MUST DO

- Calculate training split pace targets relative to an established 2K baseline time trial.
- Verify drag factor using electronic monitor diagnostics ($110-130$ standard range) rather than damper dial position.
- Enforce legs-first drive sequence ($60\%$ leg drive before trunk levering) to protect the lumbar spine.
- Incorporate structured core stability and hip mobility exercises into all rowing plans.
- Require dynamic stroke rate progression during high-intensity interval workouts.

### MUST NOT DO

- Recommend drag factors above 150 for long endurance training sessions due to severe lower back stress.
- Allow athletes to row through sharp localized lower back pain or lateral chest wall (rib) tenderness.
- Increase weekly rowing distance/meterage by more than 10-15% over rolling multi-week averages.
- Prescribe high-rate sprint intervals to rowers demonstrating severe slide rushing or shooting the slides.

## Output Templates

When delivering rowing coaching feedback or plans, include:

1. **Summary Metrics**: Total Meters, Average Split /500m, Average Stroke Rate (SPM), Drag Factor, Estimated Wattage, rTSS.
2. **Stroke Kinetics & Split Breakdown**: Interval split pacing consistency, SPM stability, and drive-to-recovery ratio assessment.
3. **Biomechanical & Safety Evaluation**: Leg drive timing, trunk angle at catch/finish, and lumbar load check.
4. **Actionable Recommendations**: Next rowing workout structure (Warmup/Drills, Main Set in rowing notation, Cooldown, and Core/Hip prehab).

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/rowing/)
