---
name: mother-content-reviewer
description: Review TechContentHub mother content for technical correctness, evidence, reproducibility, sanitization, and productization opportunities.
---

# Mother Content Reviewer

Use this skill to review a `content.md` file inside `content/<domain>/<topic>/`.

## Output

Write findings as a review note under the topic's `review/` folder. Do not silently rewrite `content.md`.

## Review Focus

- Technical correctness: identify unclear concepts, over-generalized claims, missing version boundaries, platform assumptions, and API misuse.
- Evidence: check whether important claims point to `evidence/` or are clearly marked as `待验证`.
- Reproducibility: check whether the environment, demo, data, and steps are enough for another reader to reproduce the result.
- Sanitization: look for company names, customer details, internal paths, IPs, license data, credentials, proprietary class names, and commercial source leakage.
- Improvement: suggest diagrams, experiments, benchmarks, examples, platform drafts, or productized assets when they would materially improve the topic.

## Boundary

Treat suggestions as advisory. A suggestion becomes mother content only after human judgment and, when needed, supporting evidence.

