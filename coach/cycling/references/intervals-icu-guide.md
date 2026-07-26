# Intervals.icu MCP Tool Integration Guide

Operational workflows for using `intervals.icu-mcp` server tools to retrieve athlete metrics, analyze activity streams, evaluate wellness data, and schedule structured workouts.

---

## 1. Tool Integration Overview

The `cycling-coach` skill acts as an intelligent decision layer on top of `intervals.icu-mcp`. The interaction flow follows:

```
┌─────────────────┐       Query Tools       ┌─────────────────────┐
│                 ├────────────────────────►│                     │
│  Cycling Coach  │                         │  intervals.icu-mcp  │
│      Skill      │◄────────────────────────┤                     │
└────────┬────────┘      Parsed Data        └─────────────────────┘
         │
         ▼
 ┌───────────────┐
 │ Coaching Logic│  (Decoupling, TSB Check, Readiness Analysis)
 └───────┬───────┘
         │
         ▼
 ┌───────────────┐       Update Tools       ┌─────────────────────┐
 │ Action / Plan ├────────────────────────►│  intervals.icu-mcp  │
 │ Prescription  │                          │  (Schedule/Workout) │
 └───────────────┘                          └─────────────────────┘
```

---

## 2. Common Coaching Workflows & Tool Queries

### Workflow A: Morning Readiness Assessment
Before evaluating or modifying today's workout, query wellness and fitness status:

1. **Fetch Athlete Profile & Benchmarks**: Get current FTP, LTHR, weight, and max HR.
2. **Fetch Fitness & Form Metrics**: Retrieve CTL, ATL, and TSB values for the last 7–14 days.
3. **Fetch Daily Wellness**: Inspect sleep score, resting heart rate, HRV (rMSSD), and fatigue rating.

### Workflow B: Post-Workout Analysis
When analyzing a completed ride:

1. **Fetch Activity Details**: Retrieve normalized power (NP), average power (AP), total TSS, Intensity Factor (IF), average HR, and max HR.
2. **Fetch Activity Streams / Intervals**: Inspect lap power, lap cadence, and 30-second power stream to calculate Aerobic Decoupling (P:HR drift) and interval execution accuracy.
3. **Generate Feedback**: Synthesize execution score and provide actionable coaching commentary to the athlete.

### Workflow C: Training Plan & Workout Prescriptions
When building or adjusting an upcoming week:

1. **Fetch Calendar Schedule**: Inspect scheduled workouts for the upcoming 7–14 days.
2. **Update / Prescribe Workout**: Push structured workout steps (warmup, main set, cooldown) to Intervals.icu using standard workout markup.

---

## 3. Intervals.icu Workout Syntax Format

When creating or updating workouts in Intervals.icu, format the description using text markup:

```text
- Warmup
  - 10m 55% FTP

- Main Set 4x
  - 8m 102% FTP 90rpm
  - 4m 50% FTP 85rpm

- Cooldown
  - 10m 50% FTP
```

---

## 4. Troubleshooting & Data Safety

- **Missing Heart Rate / Power Data**: If an activity lacks heart rate or power streams, calculate load based on RPE or Heart Rate Stress Score (hrSS).
- **FTP Discrepancies**: If actual NP significantly exceeds target IF (e.g. IF > 1.15 on a 60m ride), flag to the athlete that their FTP setting in Intervals.icu may be outdated and recommend a benchmark test.
- **Overwriting Workflows**: Always inspect existing calendar events before calling update tools to avoid accidental deletion of planned races or notes.
