# TechContentHub Directory Guide

This document defines what each folder is for, what belongs there, what should stay out, and how content moves through the repository.

## Global Rules

### One source of truth

Each concrete technical topic should have exactly one mother content file:

```text
content/<domain>/<topic>/content.md
```

Use this file for the most complete technical understanding. Platform drafts and product notes should be derived from it.

### Organize by technical problem

Use this shape:

```text
content/<technical-domain>/<specific-topic>/
```

Do not organize the main library by platform:

```text
bilibili/
zhihu/
wechat/
xiaohongshu/
```

Those belong under a topic's `publish/` folder.

### Keep Git lightweight

This repository should mainly contain text, small reproducible examples, small diagrams, small datasets, templates, scripts, and reviewable technical assets.

Do not store large raw media, large datasets, SDKs, installers, compiled outputs, third-party binary packages, or customer/private source material here.

When large files are needed, put them in an external asset store and record the path or link in Markdown.

Recommended external shape:

```text
TechContentHub-Assets/
└─ content/
   └─ <domain>/
      └─ <topic>/
         ├─ raw-video/
         ├─ large-model/
         ├─ source-data/
         └─ source-material/
```

### Use logical media links

Use `media://assets/...` to reference large external files from Markdown.

Example:

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

Resolve `media://assets/` through:

```text
config/media-roots.local.yaml
```

This config file is committed intentionally. After cloning the repository on another computer, edit its `path` value to match that computer's Baidu Netdisk sync folder.

### Separate fact from suggestion

AI-generated suggestions should not become technical facts automatically.

Use this flow:

```text
AI suggestion -> review/ -> human judgment -> evidence or experiment -> content.md
```

If a claim is useful but not verified, mark it clearly in `content.md` as `待验证`.

## Root Files

### `README.md`

Purpose:

- Explain what `TechContentHub` is.
- Show the core workflow.
- Link to the most important documents.

Put here:

- Repository positioning.
- High-level rules.
- Links to `INDEX.md`, `CONTEXT.md`, and `docs/`.

Do not put here:

- Long technical notes.
- Full platform drafts.
- One-off temporary ideas.

### `INDEX.md`

Purpose:

- Act as the top-level navigation page for mature topics.

Put here:

- Stable topics after they move into `content/`.
- Short manually curated links or topic names grouped by domain.

Do not put here:

- Every temporary idea in `inbox/`.
- Unverified claims.
- Long summaries that duplicate `content.md`.

Maintenance rule:

- Update it when a topic becomes stable enough to be worth rediscovering.

### `CONTEXT.md`

Purpose:

- Define repository vocabulary.

Put here:

- Terms such as Mother Content, Topic, Domain, Evidence, Review, Derived Content, Productized Asset, External Asset Store.

Do not put here:

- Implementation steps.
- Folder-by-folder operating instructions.
- Technical research notes.

Use `docs/directory-guide.md` for operating rules.

### `config/media-roots.local.yaml`

Purpose:

- Map logical `media://` roots to local disk paths.

Put here:

- The local path for `media://assets/`.
- The storage type, such as `baidu-netdisk-sync`.
- A short description of what the root stores.

Do not put here:

- Passwords.
- Access tokens.
- Private share links.
- Per-topic asset lists.

Constraint:

- This file is tracked by Git for simplicity.
- When using a new computer, edit `path` to the local Baidu Netdisk sync directory.
- Keep the URI prefix stable so existing Markdown links do not need to change.

Example:

```yaml
version: 1

roots:
  assets:
    uri_prefix: "media://assets/"
    storage: "baidu-netdisk-sync"
    path: "D:/BaiduSyncdisk/TechContentHub-Assets"
```

### `.gitignore`

Purpose:

- Keep large, generated, private, and noisy files out of Git.

Put here:

- Build output patterns.
- Binary and archive patterns.
- Large model/data/media patterns.
- Cache and temporary file patterns.

Constraint:

- If you intentionally need to version a normally ignored small file, document why near the topic that uses it.

## `docs/`

Purpose:

- Store repository-level documentation.

Put here:

- `design.md`: high-level design.
- `directory-guide.md`: folder responsibilities and constraints.
- Future workflow notes, ADRs, or maintenance documents.

Do not put here:

- Topic-specific research. Put that under `content/<domain>/<topic>/`.
- Platform drafts. Put those under a topic's `publish/`.
- Temporary capture notes. Put those under `inbox/`.

Suggested future files:

```text
docs/
├─ design.md
├─ directory-guide.md
├─ media-links.md
├─ workflow.md
└─ adr/
```

## `inbox/`

Purpose:

- Capture raw ideas and unresolved material quickly.

Put here:

- Work problems worth investigating.
- Rough article or video ideas.
- AI conversation excerpts.
- Links to docs, issues, Stack Overflow answers, or papers.
- Small screenshots.
- Small CSV or JSON snippets.
- Temporary benchmark notes.

Do not put here:

- Large videos.
- Large datasets.
- SDKs or installers.
- Complete commercial projects.
- Customer/private raw data.
- Build outputs.
- Anything you already know belongs in a stable topic.

Constraint:

- `inbox/` may be messy in content state, but it should stay lightweight in file size.
- For large raw material, create a small Markdown note that points to the external asset location.

Example:

```markdown
# OSG rendering issue

Status: raw capture

Large assets:

- TechContentHub-Assets/inbox/osg-rendering-issue/raw-video/
- TechContentHub-Assets/inbox/osg-rendering-issue/source-model/
```

Promotion rule:

```text
inbox/<rough-note>.md
  -> content/<domain>/<topic>/content.md
```

Move material out of `inbox/` when it has:

- A clear technical problem.
- A likely domain.
- Enough value to maintain over time.

### `inbox/tmp/`

Purpose:

- Hold short-lived scratch notes.

Constraint:

- Anything still useful after a short period should move to `inbox/` or `content/`.
- Do not rely on this folder for long-term storage.

## `content/`

Purpose:

- The main mother content asset library.

Put here:

- Verified or actively maintained technical topics.
- One folder per domain.
- One folder per concrete topic.

Do not put here:

- Random capture notes.
- Platform-only drafts without mother content.
- Large binary assets.
- Full commercial source projects.
- Private/customer material that has not been sanitized.

Domain examples:

```text
content/
├─ cpp/
├─ osg/
├─ opengl/
├─ qt/
├─ cmake/
├─ linux/
├─ rendering/
├─ cae/
└─ ai-coding/
```

Topic naming:

- Use lowercase English slugs.
- Prefer `kebab-case`.
- Make the topic specific enough to be useful.

Good:

```text
osg-opengl-version/
linux-rpath-packaging/
cmake-find-package-debugging/
```

Weak:

```text
notes/
misc/
final/
article/
```

## Standard Topic Folder

Every mature topic should follow this shape:

```text
content/<domain>/<topic>/
├─ content.md
├─ external-assets.md
├─ evidence/
├─ assets/
├─ demo/
├─ data/
├─ review/
└─ publish/
```

### `content.md`

Purpose:

- The mother content and only source of truth for the topic.

Put here:

- Problem background.
- Technical principles.
- Your understanding.
- Verified conclusions.
- Version and platform constraints.
- Reproduction steps.
- Demo explanation.
- Common mistakes.
- Performance notes.
- Scope and limitations.
- Open questions.

Do not put here:

- Platform-specific phrasing as the primary structure.
- Unchecked AI suggestions as facts.
- Private customer details.
- Internal company paths, hostnames, IPs, credentials, license data, or proprietary class names.

Constraint:

- If a claim depends on version, platform, driver, compiler, operating system, or hardware, state that boundary.
- If evidence is missing, mark the claim as `待验证`.

### `external-assets.md`

Purpose:

- Index large external files used by the topic.

Put here:

- `media://assets/...` URIs for raw videos, large models, heavy datasets, source footage, large archives, installers, and other files kept outside Git.
- File names, storage location, type, purpose, and relationship to evidence or publishing work.

Do not put here:

- The large files themselves.
- Private credentials or share passwords.
- Small assets that should live directly under `assets/` or `data/`.

Suggested entry:

```markdown
## Original Recording

- Name: 10 million instance performance test recording
- Type: video
- URI: media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
- Storage: Baidu Netdisk sync
- Purpose: Bilibili source material and performance evidence
```

Constraint:

- Prefer one `external-assets.md` per topic.
- Keep external asset paths aligned with the topic path when possible.
- If an external file supports a technical claim, mention the related evidence file.

### `evidence/`

Purpose:

- Store support material behind technical claims.

Put here:

- Official documentation notes.
- Standards references.
- Release note links.
- GitHub issue links.
- Experiment notes.
- Benchmark methodology and results.
- Environment details.
- Reproduction records.

Do not put here:

- Random ideas.
- AI suggestions without validation.
- Large raw datasets.
- Full copies of copyrighted manuals when a citation or short note is enough.

Suggested files:

```text
evidence/
├─ references.md
├─ official-doc.md
├─ experiment.md
└─ benchmark.md
```

Constraint:

- Evidence should help distinguish fact, experience, inference, and opinion.

### `assets/`

Purpose:

- Store small visual or content assets used by the topic.

Put here:

- Diagrams.
- Small screenshots.
- Small image source files.
- DrawIO files.
- SVGs.
- Thumbnail source files if reasonably small.

Do not put here:

- Raw video footage.
- Large PSD or project files.
- Large model files.
- Large customer screenshots or private data.

Constraint:

- Large visual/media assets should live in the external asset store, with a `media://` pointer recorded in `external-assets.md`.

### `demo/`

Purpose:

- Store minimal reproducible code that supports the topic.

Put here:

- Minimal demos.
- Reproducers.
- Small benchmark programs.
- Example scripts.
- `README.md` explaining how to run the demo.

Do not put here:

- Full commercial projects.
- Customer source code.
- Build outputs.
- Vendored third-party SDKs.
- Large dependencies.

Constraint:

- Demo code should be publishable after sanitization.
- Prefer small, focused examples over copied real-world projects.

### `data/`

Purpose:

- Store small data needed to reproduce examples or explain results.

Put here:

- Small CSV files.
- Small JSON files.
- Small sample input.
- Lightweight benchmark output.

Do not put here:

- Large datasets.
- Customer raw data.
- Large meshes or models.
- Binary dumps.

Constraint:

- If the data cannot be reviewed comfortably in Git, put it in the external asset store and leave a `media://` pointer in `external-assets.md`.

### `review/`

Purpose:

- Store human and AI review records for the topic.

Put here:

- Fact-check notes.
- Missing-point reviews.
- Technical risk reviews.
- Reproducibility reviews.
- Privacy and sanitization checks.
- Productization suggestions.

Do not put here:

- Final technical facts unless they have been moved into `content.md`.
- Platform drafts.
- Raw capture notes.

Suggested files:

```text
review/
├─ 2026-08-31-review.md
├─ fact-check.md
├─ missing-points.md
└─ improvement.md
```

Constraint:

- Review output is advisory. It becomes part of mother content only after human judgment and, where needed, evidence.

### `publish/`

Purpose:

- Store platform-specific derived content.

Put here:

- Bilibili scripts, titles, descriptions.
- Zhihu article drafts.
- WeChat article drafts.
- Xiaohongshu notes.
- Douyin short-video copy.
- Product documentation derived from the topic.

Do not put here:

- New technical facts that do not also exist in `content.md`.
- Platform drafts that contradict the mother content.
- Large exported videos.

Suggested shape:

```text
publish/
├─ bilibili/
│  ├─ script.md
│  ├─ title.md
│  └─ description.md
├─ zhihu.md
├─ wechat.md
├─ xiaohongshu.md
└─ douyin.md
```

Constraint:

- Treat these as derived files. When facts change, update `content.md` first, then refresh platform drafts.

## `templates/`

Purpose:

- Store reusable writing and review templates.

Put here:

- Mother content template.
- Evidence template.
- Experiment template.
- Benchmark template.
- Review template.
- External asset index template.
- Video script template.
- Article template.

Do not put here:

- Topic-specific content.
- Finished drafts.
- Large assets.

Constraint:

- Templates should stay generic enough to reuse across domains.

## `skills/`

Purpose:

- Store AI working methods used for this repository.

Put here:

- Repository-specific Codex skills.
- Skill instructions that define how AI should review or transform technical content.

Do not put here:

- Technical knowledge articles.
- Platform drafts.
- Random prompts detached from a repeatable workflow.

Constraint:

- Skills should describe how to work, not become a second knowledge base.
- Keep skill instructions concise and move topic-specific knowledge to `content/`.

### `skills/mother-content-reviewer/`

Purpose:

- Review `content.md` files for correctness, evidence, reproducibility, privacy, and improvement opportunities.

Constraint:

- The reviewer should write findings into `review/`.
- It should not silently rewrite `content.md` as if suggestions were facts.

## `products/`

Purpose:

- Store reusable or sellable assets derived from accumulated content.

Put here:

- Toolkits.
- Checklists.
- Small tools.
- Demo packages.
- Course outlines.
- Technical asset bundles.
- Skills derived from repeated workflows.

Do not put here:

- Random article drafts.
- One-off experiments with no product direction.
- Large binary release packages.

Constraint:

- Each product should point back to the content topics that support it.
- Product claims should be traceable to `content/` and `evidence/`.

Example:

```text
products/
├─ linux-packaging-toolkit/
├─ osg-performance-checklist/
├─ cpp-debugging-skill/
└─ cae-postprocess-demo/
```

## `archive/`

Purpose:

- Preserve material that is obsolete, superseded, abandoned, or no longer maintained.

Put here:

- Deprecated topics.
- Old drafts replaced by newer content.
- Outdated technology notes.
- Ideas you decided not to pursue.

Do not put here:

- Active topics.
- Large raw files.
- Private/customer material.

Constraint:

- Prefer archiving over deleting when the history may still be useful.
- Add a short note explaining why the item was archived.

## Placement Checklist

When deciding where something belongs, ask:

1. Is it a raw idea or quick capture? Put it in `inbox/`.
2. Is it the maintained source of truth for a technical problem? Put it in `content/<domain>/<topic>/content.md`.
3. Is it a large external file? Keep it outside Git and record a `media://` pointer in `external-assets.md`.
4. Does it support a claim? Put it in `evidence/`.
5. Is it a small visual asset? Put it in `assets/`.
6. Is it minimal reproducible code? Put it in `demo/`.
7. Is it small reproducibility data? Put it in `data/`.
8. Is it AI or human critique? Put it in `review/`.
9. Is it a platform draft? Put it in `publish/`.
10. Is it reusable or sellable as an asset? Put it in `products/`.
11. Is it outdated but still worth keeping? Put it in `archive/`.
12. Is it private? Keep it outside this repository and record only a sanitized pointer.
