# Contributing to Agent Skills

Thank you for your interest in contributing! We welcome agent skills across any domain (e.g., Software Engineering, System Administration & Security, Data & AI, Writing & Communication, Productivity, Sports & Coaching, Health, and Finance).

---

## 📋 Guidelines & Standards

All skills in this repository must strictly comply with the **Agent Skills Progressive Disclosure Specification**:

1. **2-Tier Architecture**:
   - **Tier 1 (`SKILL.md`)**: High-level prompt triggers, core 5-step operational workflow, domain philosophy, routing table, example workflows, constraints, output templates, and non-negotiable safety guardrails. (Minimum 80 non-blank lines).
   - **Tier 2 (`references/*.md`)**: Deep-domain technical reference files loaded on-demand.

2. **Metadata & Attribution**:
   - Frontmatter must include `name`, `description`, `license: MIT`, `metadata.author: https://github.com/jelmervdm`, and `metadata.related-skills`.
   - Cross-referenced skills in `related-skills` must have reciprocal references in target skill files.

3. **Directory Organization**:
   - Place skills inside appropriate category directories (e.g. `coach/`, `sysadmin/`, `developer/`, `writing/`, `productivity/`).

4. **Validation Check**:
   Before submitting a Pull Request, run the local validation scripts against your category:

   ```bash
   # Validate YAML metadata
   python3 scripts/validate-skills.py --skills-dir sysadmin --check yaml

   # Validate reference file links
   python3 scripts/validate-skills.py --skills-dir sysadmin --check references

   # Validate cross-references
   python3 scripts/validate-skills.py --skills-dir sysadmin --check crossrefs

   # Run Markdown Linter
   npx markdownlint-cli *.md sysadmin/*/*.md sysadmin/*/references/*.md
   ```

   Ensure your contribution results in **0 errors** and **0 warnings**.

---

## 🤝 Community & Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

If you discover a security vulnerability, please refer to our [Security Policy](SECURITY.md).

---

## ⚖️ License & Credit

By contributing to this repository, you agree that your contributions will be licensed under the [MIT License](LICENSE).
