# TechContentHub Design

`TechContentHub` is not a simple notes folder and not a folder grouped by publishing platforms. It is a personal long-term technical content asset library and AI-assisted content production workspace.

The central idea is:

```text
research once
  -> create mother content
  -> improve it over time
  -> derive platform-specific content
  -> turn reusable parts into products or assets
```

## Core Principle

Each technical topic has one source of truth:

```text
content.md
```

Do not create chains of final versions such as:

```text
final.md
final-v2.md
zhihu-final.md
wechat-final-edited.md
video-script-final.md
```

Instead, maintain:

```text
content.md
  -> publish/bilibili/
  -> publish/zhihu.md
  -> publish/wechat.md
  -> publish/xiaohongshu.md
  -> publish/douyin.md
```

When a technical fact changes, update `content.md` first, then review derived drafts.

## Repository Shape

```text
TechContentHub/
├─ README.md
├─ INDEX.md
├─ CONTEXT.md
├─ .gitignore
├─ docs/
├─ inbox/
├─ content/
├─ templates/
├─ skills/
├─ products/
└─ archive/
```

## Topic Shape

```text
content/<domain>/<topic>/
├─ content.md
├─ evidence/
├─ assets/
├─ demo/
├─ data/
├─ review/
└─ publish/
```

## Long-Term Goal

The goal is not only:

```text
I wrote 100 articles.
```

The goal is:

```text
I own 100 verified technical knowledge assets.
```

Each asset can later become articles, videos, answers, demos, skills, tools, templates, courses, or small products.

