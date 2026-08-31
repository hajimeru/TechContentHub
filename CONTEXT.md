# TechContentHub Context

This file defines the core language used in this repository. Keep it as a glossary, not an implementation plan.

## Glossary

### Mother Content

The canonical knowledge asset for one concrete technical topic. In this repository, mother content is stored as `content.md` inside a topic folder.

### Topic

A concrete technical problem or knowledge unit worth maintaining over time, such as `osg-opengl-version` or `linux-rpath-packaging`.

### Domain

A broad technical area under `content/`, such as `osg`, `cmake`, `linux`, or `cae`.

### Evidence

Material that supports or challenges claims in mother content: official documentation, standards, release notes, issue links, experiment notes, benchmark results, and reproducibility details.

### Derived Content

Platform-specific output generated from mother content, such as Bilibili scripts, Zhihu articles, WeChat posts, short-video copy, or product documentation.

### Review

AI or human critique of mother content. Review notes can identify missing evidence, unclear logic, factual risk, reproducibility gaps, privacy risk, or productization opportunities.

### Productized Asset

A reusable or sellable artifact derived from accumulated content, such as a checklist, toolkit, demo package, script, course material, template, skill, or small software tool.

### External Asset Store

A separate location for large binary assets that should not live in Git, such as raw videos, large models, source footage, heavy datasets, SDKs, archives, and installers.

### Media URI

A logical `media://` reference used in Markdown to point to a file in an external asset store without hard-coding a machine-specific disk path.

### Media Root Config

The tracked `config/media-roots.local.yaml` file that maps a media URI root, such as `media://assets/`, to a local disk path. Edit it after cloning the repository on another computer.

### External Asset Index

The `external-assets.md` file inside a topic folder. It records large external files used by the topic, usually with `media://assets/...` URIs.
