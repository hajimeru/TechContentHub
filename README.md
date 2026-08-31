# TechContentHub

`TechContentHub` 是一个个人长期技术内容资产库，也是一个 AI 辅助的内容生产工作区。

这个仓库按“技术领域”和“具体技术问题”组织，而不是按发布平台组织。

核心流转：

```text
inbox -> content/<domain>/<topic>/content.md -> evidence/review/demo -> publish/products
```

最重要的规则：

```text
每个技术主题只有一个事实源：content.md
```

平台稿、视频脚本、短内容、工具和产品都应该从母内容派生，而不是各自维护一堆互相分叉的“最终版”。

## 关键文档

- [INDEX.md](INDEX.md)：整个内容库的总索引。
- [CONTEXT.md](CONTEXT.md)：核心概念术语表。
- [docs/design.md](docs/design.md)：总体设计摘要。
- [docs/directory-guide.md](docs/directory-guide.md)：每个目录放什么、不放什么、有哪些约束。
- [docs/media-links.md](docs/media-links.md)：外部大文件的 `media://` 引用规则。

## 大文件规则

保持这个 Git 仓库轻量、可审查、可长期维护。大型二进制资产、原始视频、大型数据集、SDK、构建产物和第三方包不要放进仓库。

外部大文件使用 `media://assets/...` 逻辑链接引用，本机路径在 [config/media-roots.local.yaml](config/media-roots.local.yaml) 中配置。
