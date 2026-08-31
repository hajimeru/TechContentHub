# TechContentHub 设计

`TechContentHub` 不是普通笔记文件夹，也不是按发布平台分类的自媒体文件夹。它的定位是：

```text
个人长期技术内容资产库 + AI 内容生产工作区
```

核心思想：

```text
一次研究
  -> 形成母内容
  -> 持续完善
  -> 派生不同平台内容
  -> 将可复用部分沉淀为产品或资产
```

## 核心原则

每个技术主题只有一个事实源：

```text
content.md
```

不要维护这种文件链：

```text
最终版.md
最终版2.md
知乎最终版.md
公众号最终修改版.md
视频脚本最终版.md
```

正确关系是：

```text
content.md
  -> publish/bilibili/
  -> publish/zhihu.md
  -> publish/wechat.md
  -> publish/xiaohongshu.md
  -> publish/douyin.md
```

技术事实发生变化时，先更新 `content.md`，再检查派生稿。

## 仓库结构

```text
TechContentHub/
├─ README.md
├─ INDEX.md
├─ CONTEXT.md
├─ .gitignore
├─ config/
├─ docs/
├─ inbox/
├─ content/
├─ templates/
├─ skills/
├─ products/
└─ archive/
```

## 主题结构

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

## 外部媒体链接

大型视频、大模型、大型数据集、原始素材、安装包和其他大型二进制资产不进入 Git。仓库使用稳定的逻辑链接引用它们：

```text
media://assets/content/<domain>/<topic>/<category>/<file>
```

`media://assets/` 对应的本机磁盘路径配置在：

```text
config/media-roots.local.yaml
```

这个配置文件会提交到 Git。换电脑后，直接把里面的 `path` 改成那台电脑上的百度网盘同步目录。

## 长期目标

目标不是：

```text
我写过 100 篇文章。
```

而是：

```text
我拥有 100 个经过验证的技术知识资产。
```

一个资产可以继续派生为文章、视频、回答、Demo、Skill、工具、模板、课程或小型产品。
