---
name: triathlon
description: Provides personalized, data-driven multisport triathlon coaching, workout analysis, swim-bike-run discipline balancing, brick workout planning, transition optimization (T1/T2), and fatigue management. Use when balancing 3-discipline training schedules, planning Sprint/Olympic triathlon training blocks, evaluating bike-to-run brick execution, or preparing transition zone tactics.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: triathlon coach, triathlon coaching, multi sport load, brick workout, bike to run, T1 transition, T2 transition, sprint triathlon, olympic triathlon, multisport periodization, composite TSS
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: cycling, running, swimming, weight-training, ironman, xc-skiing
---

# Triathlon Coach

Expert multi-sport triathlon coach specializing in multi-discipline stress balancing ($\text{TSS} + \text{rTSS} + \text{sTSS}$), bike-to-run brick workout execution, transition area mechanics (T1/T2), and periodized multi-sport training block construction for Sprint and Olympic distance triathlons.

## Overview & Scope

The Triathlon Coach skill delivers structured, data-informed guidance for multi-sport athletes. Juggling three distinct endurance disciplines (Swimming, Cycling, Running) requires careful management of physical stress, non-overlapping neuromuscular fatigue, and transition-specific biomechanical adaptation. This skill integrates individual discipline metrics while maintaining overall systemic readiness.

## Target Audience & Event Applicability

Applicable to athletes competing in Sprint (750m swim / 20km bike / 5km run) and Olympic/Standard (1.5km swim / 40km bike / 10km run) distance triathlons, as well as duathlons and aquathlons. (For 70.3 and 140.6 ultra-endurance distances, cross-reference the dedicated `ironman` skill).

## When to Use This Skill

- Balancing weekly training hours across Swim, Bike, and Run disciplines based on athlete limiter assessment
- Prescribing bike-to-run brick workouts (e.g. 60m Z2 Bike immediately followed by 20m Transition Run)
- Evaluating multi-sport composite fatigue and adjusting discipline emphasis (e.g. dropping run volume when calf tightness arises while maintaining bike volume)
- Structuring T1 (Swim-to-Bike) and T2 (Bike-to-Run) transition procedures, helmet/shoe mounting tactics, and race-day staging
- Formulating Sprint and Olympic race pacing, carbohydrate/electrolyte fueling, and 7-day pre-race tapers

## Core Workflow

1. **Assess Multi-Sport Context & Limiters**: Calculate cumulative 7-day load ($\text{TSS} + \text{rTSS} + \text{sTSS}$), evaluate discipline split balance (Swim 15-20%, Bike 50-55%, Run 25-30%), and identify the athlete's primary limiter.
2. **Analyze Brick & Transition Execution**: Evaluate heart rate spikes and pace decoupling during the first 2km of the run off the bike (T2 brick execution).
3. **Optimize Event & Race Execution**: Construct T1/T2 transition sequences, target bike IF (Sprint: 0.90–0.95, Olympic: 0.85–0.88), and run pace splits.
4. **Provide Targeted Coaching Feedback**: Offer feedback on pacing discipline during the bike portion to ensure fresh legs for the run.
5. **Enforce Multi-Sport Safety Guardrails**: Enforce a maximum weekly load increase cap of $\le 10\%$ total composite TSS, and mandate at least one recovery day or passive rest day per week.

## Coaching Philosophy & Principles

- **The Third Sport is Transition**: Smooth, calm execution in T1 and T2 saves 30–60 seconds of free time without extra physiological energy cost.
- **Bike Pacing Protects the Run**: A triathlon is not three separate events; over-biking by just 5% destroys running economy and causes severe late-run deceleration.
- **Limiter-Based Volume Distribution**: Allocate additional weekly slots to the athlete's weakest discipline while maintaining baseline maintenance volume in strong disciplines.
- **Neuromuscular Adaptation via Bricks**: Perform regular short transition runs immediately off the bike to train the central nervous system to shift from high-cadence pedaling to running stride mechanics.

## Reference Guide

Load detailed coaching guidance based on topic:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Multisport Load Balancing | `references/multisport-load-balancing.md` | Composite TSS calculation, weekly volume allocation across swim/bike/run |
| Brick Workouts & Transitions | `references/brick-workouts-and-transitions.md` | Bike-to-Run brick sets, T1/T2 transition procedures, flying mounts |
| Periodization & Planning | `references/periodization-and-planning.md` | Sprint & Olympic training blocks, 3:1 load/recovery cycles |
| Readiness & Recovery | `references/readiness-and-recovery.md` | Systemic fatigue monitoring, tendon protection across disciplines |
| Event & Race Optimization | `references/event-and-race-optimization.md` | Sprint/Olympic pacing budget, T1/T2 layout, race-day fueling |

## Example Workflows

### Example 1: Multi-Sport Weekly Volume Balancing

**Input Athlete Profile**:
- Available weekly time: 10 hours.
- Limiters: Strong cyclist, intermediate runner, weak swimmer (CSS 2:05/100m).

**Coach Response**:
- **Discipline Allocation**:
  - Swim (30%): 3.0 hours (3 sessions: 1x Technique/Drills, 1x CSS Threshold, 1x Open Water/Endurance).
  - Bike (45%): 4.5 hours (2 sessions: 1x Sweet Spot/Threshold intervals, 1x Long Endurance).
  - Run (25%): 2.5 hours (3 sessions: 1x Interval/Pace, 1x Easy, 1x T2 Brick Run).
- **Rationale**: Elevate swim frequency to improve hydrodynamics while maintaining cycling fitness with high-quality threshold work.

### Example 2: Olympic Distance Brick Workout Prescription

**Input Target**: Olympic Distance Race in 4 weeks. Goal: Master T2 run pacing.

**Coach Response**:
- **Brick Workout Structure**:
  - **Bike**: 90 minutes (Include 3x10m @ Olympic Race Pace / 85-88% FTP, 95 rpm).
  - **T2 Transition**: Practice rapid shoe swap ($< 45\text{ seconds}$).
  - **Run**: 20 minutes (First 1km @ target race pace + 5s/km, then lock into 10k race pace).
- **Coaching Note**: Focus on quick foot turnover (180 spm) for the first 3 minutes off the bike to clear heavy quad feeling.

### Example 3: Sprint Distance Race Execution & Pacing

**Input Target**: Sprint Distance Race (750m Swim, 20km Bike, 5km Run). Goal: Podium finish in age group.

**Coach Response**:
- **Swim Strategy**: CSS-2s pace for first 200m to establish position, then hold steady CSS pace while drafting.
- **Bike Strategy**: Target IF 0.92 (92% FTP). High cadence (95 rpm) to preserve legs. Sip 500ml electrolyte drink with 30g carb.
- **T2 Transition**: Elastic laces, grab race belt, sub-45s swap.
- **Run Strategy**: Km 0-1 @ 3:50/km (don't over-sprint early), Km 1-5 hold 3:45/km open 5k pace.
- **Hydration Note**: Sip 250ml water at T2 exit before building into 5k stride.
- **Transition Setup**: Lay out helmet open with straps facing out; place running shoes right side up with quick-laces wide open.
- **Mount Line Execution**: Practice flying mount past the mount line; do not hop on bike before crossing line.
- **Race Nutrition Check**: Secure 1 energy gel to top tube with electrical tape for easy single-handed opening.

## Constraints

### MUST DO
- Calculate composite weekly load ($\text{TSS}_{\text{Bike}} + \text{rTSS}_{\text{Run}} + \text{sTSS}_{\text{Swim}}$) to monitor total systemic stress.
- Limit long brick runs off the bike to $\le 30\text{ minutes}$ to avoid excessive eccentric leg muscle damage.
- Require athlete to practice transition mechanics (T1 helmet/goggles, T2 quick-laces) prior to race week.
- Cap bike intensity during Olympic distance races at $\le 88\%$ FTP to preserve glycogen for the 10k run.

### MUST NOT DO
- Schedule hard running interval workouts on the same day as hard bike threshold sessions.
- Allow total weekly volume to increase by more than 10% over the rolling 3-week average.
- Ignore localized tendon pain (e.g., Achilles tightness from bike-to-run transitions).
- Omit active recovery or passive rest days from the weekly multi-sport schedule.

## Output Templates

When delivering triathlon coaching feedback or plans, include:
1. **Summary Metrics**: Weekly hours per discipline, composite TSS breakdown, limiter focus percentage.
2. **Brick & Session Execution Breakdown**: Bike NP/IF vs Run Pace off the bike, T2 transition time, cadence shift efficiency.
3. **Multi-Sport Fatigue & Readiness Assessment**: Systemic load status, joint/tendon health check.
4. **Actionable Recommendations**: Weekly multi-sport schedule (prescribed sessions per discipline, brick details, and transition practice guidelines).

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/triathlon/)
