# Contributing to Agent Skills

Thank you for your interest in contributing! We welcome agent skills across any domain (e.g., Software Engineering, Writing & Communication, Productivity, Data & AI, Sports & Coaching, Health, and Finance).

---

## 📋 Guidelines & Standards

All skills in this repository must strictly comply with the **Agent Skills Progressive Disclosure Specification**:

1. **2-Tier Architecture**:
   - **Tier 1 (`SKILL.md`)**: High-level prompt triggers, core 5-step operational workflow, domain philosophy, routing table, and non-negotiable safety guardrails. (Minimum 80 non-blank lines).
   - **Tier 2 (`references/*.md`)**: Deep-domain technical reference files loaded on-demand.

2. **Metadata & Attribution**:
   - Frontmatter must include `name`, `description`, `license: MIT`, `metadata.author: https://github.com/jelmervdm`, and `metadata.related-skills`.
   - Cross-referenced skills in `related-skills` must have reciprocal references in the target skill files.

3. **Directory Organization**:
   - Place skills inside appropriate category directories (e.g. `coach/`, `developer/`, `writing/`, `productivity/`).

4. **Validation Check**:
   Before submitting a Pull Request, run the local validation scripts:

   ```bash
   python3 scripts/validate-skills.py --skills-dir coach --check yaml
   python3 scripts/validate-skills.py --skills-dir coach --check references
   python3 scripts/validate-skills.py --skills-dir coach --check crossrefs
   ```

   Ensure your contribution results in **0 errors** and **0 warnings**.

---

## ⚖️ License & Credit

By contributing to this repository, you agree that your contributions will be licensed under the [MIT License](LICENSE).
