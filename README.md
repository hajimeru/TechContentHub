# TechContentHub

`TechContentHub` is a personal long-term technical content asset library and AI-assisted content production workspace.

The repository is organized around technical domains and concrete technical problems, not publishing platforms.

Core flow:

```text
inbox -> content/<domain>/<topic>/content.md -> evidence/review/demo -> publish/products
```

The most important rule:

```text
Each technical topic has one source of truth: content.md
```

Platform drafts, video scripts, short posts, tools, and products should be derived from the mother content rather than maintained as independent final versions.

## Key Documents

- [INDEX.md](INDEX.md): repository-wide content index.
- [CONTEXT.md](CONTEXT.md): glossary for core concepts.
- [docs/design.md](docs/design.md): high-level design summary.
- [docs/directory-guide.md](docs/directory-guide.md): detailed folder responsibilities and constraints.
- [docs/media-links.md](docs/media-links.md): `media://` URI rules for external Baidu Netdisk assets.

## Large File Rule

Keep this repository lightweight and reviewable. Store large binary assets, raw videos, large datasets, SDKs, generated build outputs, and third-party packages outside this repository. Record their paths or links in Markdown instead.

Use `media://assets/...` links for external large assets, with the local root path defined in [config/media-roots.local.yaml](config/media-roots.local.yaml).
