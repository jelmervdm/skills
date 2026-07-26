# Post-Workout Analysis & Execution Evaluation

Structured workflow and physiological rules for evaluating completed cycling workouts, quantifying interval compliance, calculating aerobic drift, and diagnosing physical strain.

---

## 1. Post-Workout Analysis Workflow

When evaluating a completed ride, follow a 4-pass structured analysis:

```
Pass 1: Macro Summary (TSS, IF, Duration, NP vs AP, VI)
       │
       ▼
Pass 2: Interval Compliance (Target vs Actual Power, Cadence, Fade)
       │
       ▼
Pass 3: Cardiovascular Response & Decoupling (P:HR Drift, Max HR, HR Recovery)
       │
       ▼
Pass 4: Subjective Alignment (RPE vs Objective Work, Coach Notes)
```

---

## 2. Aerobic Decoupling (Efficiency Factor & P:HR Drift)

Aerobic Decoupling measures cardiovascular stability relative to power output over the course of a ride. As fatigue, dehydration, or heat accumulation occurs, heart rate drifts upward while power remains flat, or power fades while heart rate remains elevated.

### Efficiency Factor (EF)
$$\text{EF} = \frac{\text{Normalized Power (NP)}}{\text{Average Heart Rate (AP_{\text{HR}})}}$$

### Calculating Aerobic Decoupling (P:HR Drift)
1. Divide the ride (or steady-state endurance segment) into two equal halves (Half 1 and Half 2).
2. Calculate $\text{EF}_1 = \frac{\text{NP}_1}{\text{HR}_1}$ and $\text{EF}_2 = \frac{\text{NP}_2}{\text{HR}_2}$.
3. Calculate percentage drift:

$$\text{Decoupling (\%)} = \left(1 - \frac{\text{EF}_2}{\text{EF}_1}\right) \times 100$$

### Decoupling Interpretation Guidelines

| Decoupling Drift | Aerobic Fitness / Status | Actionable Coaching Guidance |
|------------------|--------------------------|------------------------------|
| **$< 3.5\%$** | Excellent Aerobic Base | High endurance capacity. Ready to progress duration or intensity. |
| **$3.5\% - 5.0\%$** | Good / Normal Stability | Target zone achieved. Normal physiological strain. |
| **$5.1\% - 7.5\%$** | Moderate Decoupling | Borderline aerobic strain. Check fueling, hydration, or heat. |
| **$> 7.5\%$** | Severe Decoupling | Excessive strain. Aerobic engine over-taxed. Reduce endurance target or add rest. |

---

## 3. Interval Execution Scoring

Evaluate structured interval work (e.g., 4x8m VO2max or 3x15m Threshold) using the following metrics:

### Target Compliance Ratio
$$\text{Compliance} = \frac{\text{Actual Average Power during Interval}}{\text{Prescribed Target Power}}$$

- **Over-Powering ($> 105\%$)**: Common mistake in early reps. Causes premature anaerobic fatigue and interval fading.
- **On Target ($97\% - 103\%$)**: Ideal execution.
- **Under-Powering ($< 95\%$)**: Sign of improper FTP setting, residual fatigue, or poor pacing.

### Interval Fading Index (IFI)
Compare the average power of the first rep to the last rep:

$$\text{Fade} = \frac{\text{Power}_{\text{First Interval}} - \text{Power}_{\text{Last Interval}}}{\text{Power}_{\text{First Interval}}} \times 100$$

- **$< 3\%$**: Outstanding pacing and energy reserve control.
- **$3\% - 6\%$**: Acceptable fatigue accumulation.
- **$> 6\%$**: Severe pacing error (started too hard) or excessive fatigue accumulated.

---

## 4. Subjective (RPE) vs. Objective Disparity Diagnostics

Rating of Perceived Exertion (RPE on 1–10 scale) provides vital feedback when cross-referenced against objective metrics:

```
                  ┌────────────────────────────────────────┐
                  │ Compare RPE with Objective Power & HR  │
                  └───────────────────┬────────────────────┘
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        ▼                             ▼                             ▼
┌──────────────────┐        ┌──────────────────┐        ┌──────────────────┐
│  RPE High /      │        │  RPE Low /       │        │  RPE High /      │
│  HR High /       │        │  HR Normal /     │        │  HR Low (Suppressed)│
│  Power Low       │        │  Power High      │        │  Power Low       │
└────────┬─────────┘        └────────┬─────────┘        └────────┬─────────┘
         │                           │                           │
         ▼                           ▼                           ▼
  Acute Fatigue,             Peak Adaptation,            Autonomic Fatigue,
  Heat / Dehydration,       High Readiness,             Parasympathetic
  or Early Illness          "In the Zone"               Overreaching
```

### Diagnostic Action Rules
1. **Suppressed Heart Rate + High RPE**: Classic marker of parasympathetic fatigue (over-reaching). Convert next 24-48h to Z1/Rest.
2. **Elevated Heart Rate + Normal Power**: Dehydration, high ambient temperature, caffeine spike, or insufficient recovery between sets.
3. **High Power + Low RPE**: Freshness, high readiness, or FTP improvement. Consider raising FTP benchmark.

---

## 5. Coaching Feedback Template

When delivering post-ride feedback to the athlete, structure comments cleanly:

1. **Headline**: Positive reinforcement & quick rating (e.g., "Solid 9/10 execution on your Sweetspot block").
2. **Key Data Highlights**: Summary of NP, TSS, IF, and interval execution accuracy.
3. **Physiological Insights**: Comment on P:HR drift, cadence stability, and heart rate recovery.
4. **Action Items / Next Steps**: Direct adjustments for the next ride (e.g., "Great work today. Tomorrow is strictly Z1 active recovery—keep power under 150W").
