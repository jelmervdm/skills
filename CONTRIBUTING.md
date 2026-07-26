# Contributing to Athletic Performance Agent Skills

Thank you for your interest in contributing! We welcome new sport skills, improved reference domain modules, and fixes to pacing algorithms.

---

## 📋 Guidelines & Standards

All skills in this repository must strictly comply with the **Agent Skills Progressive Disclosure Specification**:

1. **2-Tier Architecture**:
   - **Tier 1 (`SKILL.md`)**: High-level prompt triggers, core workflow (5 steps), coaching philosophy, routing table, and non-negotiable safety guardrails. Must have at least 80 non-blank lines.
   - **Tier 2 (`references/*.md`)**: Deep-domain technical reference files (e.g. `workout-analysis.md`, `readiness-and-recovery.md`, `event-and-race-optimization.md`).

2. **Metadata & Attribution**:
   - Frontmatter must include `name`, `description`, `license: MIT`, `metadata.author: https://github.com/jelmervdm`, and `metadata.related-skills`.
   - Cross-referenced skills in `related-skills` must have reciprocal references in the target skill files.

3. **Validation Check**:
   Before submitting a Pull Request, run the local validation script:
   ```bash
   python3 scripts/validate-skills.py --skills-dir coach
   ```
   Ensure your contribution results in **0 errors** and **0 warnings**.

---

## ⚖️ License & Credit

By contributing to this repository, you agree that your contributions will be licensed under the [MIT License](LICENSE).
