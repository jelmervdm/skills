# Split Pace & Stroke Metrics

Operational guide for determining 500m split pace targets, stroke rate (SPM) zones, drag factor calibration, wattage conversions, and rowing training stress scores (rTSS).

---

## 1. 2K Pace Zones & Split Calculations

Rowing intensity is anchored to an athlete's 2K All-Out Benchmark Time Trial split ($\text{Pace}_{2\text{K}}$ in seconds per 500m).

### Pace & Heart Rate Training Zones

| Zone | Name | Pace Target (/500m) | Stroke Rate (SPM) | % 2K Watts | Adaptations / Purpose |
| ------ | ------ | --------------------- | ------------------- | ------------ | ----------------------- |
| **UT2** | Uncompensated Training 2 | $\text{Pace}_{2\text{K}} + 15\text{ to }22\text{s}$ | 18 – 20 | 50 – 60% | Aerobic base, capillary density, fat oxidation |
| **UT1** | Uncompensated Training 1 | $\text{Pace}_{2\text{K}} + 10\text{ to }14\text{s}$ | 20 – 24 | 60 – 70% | Aerobic threshold, lactate clearance |
| **AT** | Anaerobic Threshold | $\text{Pace}_{2\text{K}} + 5\text{ to }9\text{s}$ | 24 – 28 | 70 – 85% | Lactate threshold, sustained 6K race pace |
| **TR** | Transportation (VO2max) | $\text{Pace}_{2\text{K}} + 0\text{ to }4\text{s}$ | 28 – 32 | 85 – 105% | $\text{VO}_2\max$, stroke power, 2K race pace |
| **AN** | Anaerobic Power | $\text{Pace}_{2\text{K}} - 2\text{ to }6\text{s}$ | 34 – 40+ | 105 – 130%+ | Anaerobic capacity, 250m start/finish sprints |

---

## 2. Wattage & Split Conversion Formulas

Pace on a Concept2 ergometer is non-linear and proportional to the cube root of power:

$$\text{Watts} = \frac{2.80}{\text{Pace}^3}$$

*(where $\text{Pace}$ is split time per meter in seconds, i.e., $\frac{\text{Split}_{500}}{500}$).*

$$\text{Pace (sec/500m)} = 500 \times \sqrt[3]{\frac{2.80}{\text{Watts}}}$$

---

## 3. Drag Factor & Damper Calibration

Damper lever numbers (1–10) vary across ergometers due to dust build-up and altitude. Always calibrate using the **Electronic Drag Factor** on the monitor.

| Category | Recommended Drag Factor | Damper Setting Approx. | Notes |
| ---------- | ------------------------- | ------------------------ | ------- |
| **Heavyweight Men** | 125 – 135 | 4 – 5 | Standard heavyweight 2K testing |
| **Lightweight Men / Heavyweight Women** | 115 – 125 | 3 – 4 | Optimal power-to-sprain balance |
| **Lightweight Women / Juniors** | 105 – 115 | 2 – 3 | Protects young & lighter lumbar spines |
| **Ergometer Marathon / Long UT2** | 110 – 120 | 3 | Reduces lower back fatigue across 90+ min |

---

## 4. Rowing Training Stress Score (rTSS)

Tracking workout stress load for rowing:

$$\text{rTSS} = \frac{T \times \text{Watts}_{\text{actual}} \times \text{IF}}{W_{\text{2K}} \times 3600} \times 100$$

*(where $T$ is duration in seconds, $\text{IF} = \frac{\text{Watts}_{\text{actual}}}{\text{Watts}_{\text{2K}}}$, and $W_{\text{2K}}$ is 2K benchmark wattage).*
