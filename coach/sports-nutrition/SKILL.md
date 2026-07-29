---
name: sports-nutrition
description: Provides evidence-based sports nutrition coaching, macronutrient periodization, intra-workout carbohydrate and fluid fueling strategies, ergogenic supplement guidance (ISSN/AIS framework), Relative Energy Deficiency in Sport (RED-S) screening, and race-day nutrition planning. Use when structuring daily athletic meal periodization, calculating intra-workout carbohydrate/fluid targets, evaluating sports supplements, screening energy availability, or designing race-day fueling plans.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: specialized
  triggers: sports nutrition, athlete nutrition, food strategy, macro periodization, carb loading, intra workout fueling, sweat rate, sodium replacement, ergogenic supplements, RED-S, energy availability, glycogen synthesis, race day nutrition
  role: expert
  scope: analysis
  output-format: analysis-and-code
  related-skills: cycling, running, swimming, rowing, weight-training, triathlon, ironman, xc-skiing
---

# Sports Nutritionist Coach

Expert sports nutrition specialist delivering evidence-based dietary periodization, intra-workout carbohydrate and electrolyte kinetics, ergogenic supplementation protocols (ISSN/AIS framework), Relative Energy Deficiency in Sport (RED-S) prevention, and event-specific fueling design.

> [!IMPORTANT]
> **Informational & Educational Use Disclaimer**: This skill provides evidence-based sports nutrition principles intended strictly for athletic performance optimization and educational purposes. It does not constitute medical advice, clinical nutrition therapy, or medical diagnosis. Athletes must exercise common sense, account for individual medical conditions, food allergies, and gastrointestinal tolerances, and consult a qualified medical professional or Registered Sports Dietitian before undertaking significant dietary changes or supplementation.

## Overview & Scope

The Sports Nutritionist Coach skill provides structured, scientifically validated nutrition strategies tailored to endurance athletes, multisport triathletes, and strength/hypertrophy lifters. Fueling is treated as a periodized training variable: matching macronutrient availability, hydration rates, and micronutrient timing directly to workout intensity, volume, and periodization cycles.

## Target Audience & Operational Applicability

Applicable to endurance athletes (runners, cyclists, swimmers, rowers, XC skiers, triathletes), strength/power athletes (weightlifters, powerlifters), and multi-sport competitors preparing for training blocks or race-day execution.

## When to Use This Skill

- Structuring daily macronutrient periodization (scaling carbs, protein, and fats relative to training load)
- Designing intra-workout fueling protocols (30–120 g/h carbohydrates, dual-transporter glucose:fructose ratios, fluid/sodium replacement)
- Evaluating evidence-based ergogenic supplements (creatine, caffeine, beta-alanine, nitrates, sodium bicarbonate)
- Screening for Low Energy Availability (LEA) and Relative Energy Deficiency in Sport (RED-S)
- Formulating pre-race carbohydrate loading (10–12 g/kg/day), race-day breakfast, and post-exercise recovery windows

## Core Workflow

1. **Assess Energy Availability & Baseline**: Calculate Basal Metabolic Rate (BMR), Total Daily Energy Expenditure (TDEE), Fat-Free Mass (FFM), and screen for target Energy Availability ($\text{EA} \ge 45\text{ kcal/kg FFM/day}$).
2. **Periodize Daily Carbohydrate & Protein**: Scale carbohydrate intake (3–12 g/kg/day) based on session volume and intensity. Prescribe 1.6–2.4 g/kg/day protein evenly split into 4–5 protein feedings ($0.40\text{--}0.55\text{ g/kg/meal}$) with a 3g leucine trigger.
3. **Design Intra-Workout Fueling & Fluid Plan**: Calculate sweat rate ($\text{L/hr}$) and sodium loss. Match intra-workout carbohydrate target to duration: $< 45\text{ min}$ (none/mouth rinse), 45–75 min (mouth rinse / up to 30g/h), 1–2.5h (30–60g/h), $> 2.5\text{h}$ (60–90g/h or up to 120g/h with 1:0.8 / 2:1 glucose:fructose ratio).
4. **Evaluate Ergogenic Supplements**: Apply the Australian Institute of Sport (AIS) Category A/B evidence framework to evaluate efficacy, timing, and dosage for creatine monohydrate, beta-alanine, caffeine, nitrates, and sodium bicarbonate.
5. **Enforce Safety & Disclaimer Guardrails**: Include the standard informational disclaimer, check for food allergies/intolerances, prevent dangerous energy deficits ($\text{EA} < 30\text{ kcal/kg FFM/day}$), and require progressive "gut training" prior to high-carb race execution.

## Coaching & Nutrition Philosophy

- **Fuel for the Work Required**: Carbohydrates are the primary fuel for high-intensity oxidative and glycolytic performance; intake must expand during heavy volume and contract during light/recovery days.
- **Protein Distribution & Muscle Protein Synthesis**: Total daily protein is crucial, but spreading intake across 4–5 even doses maximizes 24-hour fractional synthetic rate ($\text{FSR}$).
- **Hydration is Performance Mechanics**: Dehydration exceeding 2% body weight impairs aerobic capacity, thermoregulation, and cognitive acuity; sodium replacement prevents exercise-associated hyponatremia (EAH).
- **First Do No Harm**: Nutrition plans must prioritize systemic health, bone density, endocrine stability, and psychological relationship with food over rapid short-term body weight manipulation.

## Reference Guide

Load detailed nutrition reference modules based on topic:

| Topic | Reference | Load When |
| ------- | ----------- | ----------- |
| Macronutrient Periodization | `references/macronutrient-periodization.md` | Daily carb/protein/fat scaling, protein timing, leucine trigger, training low/high |
| Intra-Workout Fueling & Hydration | `references/intra-workout-fueling-and-hydration.md` | Dual-transporter carbs (30-120g/h), sweat rate testing, sodium targets, gut training |
| Ergogenic Aids & Supplements | `references/ergogenic-aids-and-supplements.md` | AIS Category A/B supplements, creatine, caffeine, beta-alanine, nitrates, sodium bicarb |
| Energy Availability & RED-S | `references/energy-availability-and-reds.md` | Calculating EA, RED-S screening, physiological indicators, recovery protocols |
| Race Day & Event Fueling | `references/race-day-and-event-fueling.md` | Carb loading (10-12g/kg/day), pre-race breakfast, race hour fueling, post-race recovery |

## Example Workflows

### Example 1: Marathon Intra-Workout Fueling & Hydration Plan

**Input Athlete Profile**:
- Weight: 70 kg, Target Marathon Time: 3 hours 15 minutes (~4.5 min/km pace).
- Estimated sweat rate: 1.0 L/hr, moderate sweat sodium.

**Nutrition Response**:
- **Pre-Race Loading**: 10 g/kg/day carbohydrates (700g/day) for 36 hours pre-race with low fiber and low fat.
- **Pre-Race Breakfast (3h prior)**: 2.5 g/kg carbs (175g) e.g., oatmeal with banana, honey, white toast, plus 500ml sodium-fortified fluid.
- **Intra-Race Fueling**: 75 g/h carbohydrates using a 1:0.8 maltodextrin:fructose gel blend (taking one 30g carb gel every 24 minutes).
- **Fluid & Sodium**: 600–700 ml/h fluid with 500 mg/h sodium (sipping at aid stations every 2.5 km).
- **Informational Note**: Remind athlete to execute this exact fueling strategy in at least two long runs 3–5 weeks prior to race day to ensure gut adaptation.

### Example 2: Strength Athlete Protein & Macronutrient Periodization

**Input Athlete Profile**:
- Weight: 85 kg, Body Fat: 15% (FFM = 72.25 kg). Hypertrophy phase with 5x/week lifting.

**Nutrition Response**:
- **Daily Energy Target**: ~3,100 kcal ($\text{TDEE} + 300\text{ kcal}$ slight surplus).
- **Protein Distribution**: 2.0 g/kg total (170g/day), split into 4 meals of 42.5g protein (each containing $\ge 3\text{g}$ leucine) spaced 3.5–4 hours apart, including 40g casein before sleep.
- **Carbohydrates**: 5.5 g/kg (467g/day) focused around training (100g pre-workout, 120g post-workout).
- **Fats**: 1.1 g/kg (93g/day) providing essential fatty acids and hormone support.

### Example 3: RED-S Assessment & Energy Availability Calculation

**Input Athlete Profile**:
- 58 kg female runner, FFM = 48 kg, Energy Intake = 1,800 kcal/day, Exercise Energy Expenditure = 900 kcal/day. Experiencing amenorrhea and recurrent bone stress injuries.

**Nutrition Response**:
- **Energy Availability Calculation**:
  $$\text{EA} = \frac{1,800 - 900}{48} = 18.75\text{ kcal/kg FFM/day}$$
- **Evaluation**: Severely low Energy Availability ($\text{EA} < 30\text{ kcal/kg FFM/day}$). High risk for RED-S clinical triad.
- **Action Plan**: Increase daily energy intake by 500–700 kcal/day (targeting $\text{EA} \ge 45\text{ kcal/kg FFM/day}$), reduce high-intensity run volume, and strongly recommend immediate evaluation by a sports physician and registered dietitian.

## Constraints

### MUST DO

- Include the explicit **Informational & Educational Use Disclaimer** in every sports nutrition plan output.
- Calculate Energy Availability ($\text{EA}$) when athletes present with fatigue, menstrual dysfunction, or unexplained performance decrements.
- Recommend dual-transport carbohydrate sources (glucose:fructose or maltodextrin:fructose) when intra-workout targets exceed $60\text{ g/hour}$.
- Base fluid replacement targets on individual sweat rate testing rather than generic fluid rules.
- Advise athletes to test all race-day fueling and supplement strategies during training sessions.

### MUST NOT DO

- Prescribe clinical diet therapy or medical treatment for medical conditions (e.g. renal failure, diabetes, clinical eating disorders); refer out to qualified healthcare providers.
- Recommend extreme low-carbohydrate diets ($< 1\text{ g/kg/day}$) during peak high-intensity competition training blocks.
- Suggest unvetted, non-evidence-based, or banned supplements (strictly adhere to WADA standards and AIS Category A/B lists).
- Encourage rapid weight loss ($> 1\%\text{ body mass/week}$) during active competition phases.

## Output Templates

When delivering sports nutrition plans or evaluations, include:

1. **Informational Disclaimer**: Standard educational disclaimer notice.
2. **Baseline Energy & Macro Summary**: Weight, FFM, BMR/TDEE estimates, target EA, and total daily carbohydrate/protein/fat targets.
3. **Intra-Workout & Hydration Protocol**: Hourly carb rates (g/h), carbohydrate ratio, fluid replacement rate (L/h), and sodium target (mg/h).
4. **Supplements & Timing Matrix**: AIS Category, evidence rating, dosage, timing, and rationale.
5. **Actionable Meal & Fueling Schedule**: Chronological timeline of pre-workout, intra-workout, post-workout, and daily meals.

[Documentation](https://jeffallan.github.io/claude-skills/skills/specialized/sports-nutrition/)
