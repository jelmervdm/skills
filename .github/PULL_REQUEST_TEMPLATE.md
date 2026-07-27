## Description

*Provide a clear and concise summary of the changes proposed in this Pull Request (e.g., new skill addition, bug fix in existing reference, validator enhancement).*

---

## Type of Change

- [ ] 🆕 New Agent Skill (2-Tier Progressive Disclosure)
- [ ] 📖 Documentation / Technical Reference Update
- [ ] 🛠️ Validator / CI Script Enhancement
- [ ] 🐛 Bug Fix / Warning Fix

---

## Skill Metadata Compliance Checklist

*If submitting or updating an Agent Skill, ensure the following standards are met:*

- [ ] Skill files follow the 2-Tier Progressive Disclosure structure (`<category>/<skill-name>/SKILL.md` and `<category>/<skill-name>/references/*.md`).
- [ ] Frontmatter includes required keys (`name`, `description`, `license: MIT`, `metadata.author`, `metadata.related-skills`).
- [ ] `SKILL.md` contains between **80 and 100 non-blank lines** (excluding YAML frontmatter).
- [ ] `SKILL.md` includes exactly 5 numbered steps in `## Core Workflow`.
- [ ] All cross-referenced skills in `related-skills` have reciprocal references in target skill files.

---

## Local Verification Commands Executed

- [ ] Validated YAML metadata:

  ```bash
  python3 scripts/validate-skills.py --skills-dir <category> --check yaml
  ```

- [ ] Validated reference file links:

  ```bash
  python3 scripts/validate-skills.py --skills-dir <category> --check references
  ```

- [ ] Validated cross-references:

  ```bash
  python3 scripts/validate-skills.py --skills-dir <category> --check crossrefs
  ```

- [ ] Ran markdown linter:

  ```bash
  npx markdownlint-cli *.md <category>/*/*.md <category>/*/references/*.md
  ```

- [ ] Resulted in **0 errors** and **0 warnings**.
