# TechContentHub 目录说明

这个文档规定每个目录放什么、不放什么，以及内容在仓库中的流转方式。

## 全局规则

### 一个事实源

每个具体技术主题只能有一个母内容文件：

```text
content/<domain>/<topic>/content.md
```

`content.md` 保存当前对这个技术主题最完整、最稳定的理解。平台稿、产品文档和视频脚本都应该从它派生。

### 按技术问题组织

正式内容使用这个结构：

```text
content/<technical-domain>/<specific-topic>/
```

不要把主内容库按平台拆成：

```text
bilibili/
zhihu/
wechat/
xiaohongshu/
```

平台稿应该放在具体主题目录下的 `publish/`。

### Git 保持轻量

这个仓库主要保存文本、小型可复现代码、小图、小数据、模板、脚本和可审查的技术资产。

大型原始视频、大型数据集、SDK、安装包、构建产物、第三方二进制包、客户或公司私有原始材料不要放进 Git。

需要大文件时，把文件放进外部资产库，并在 Markdown 中记录逻辑链接。

推荐的外部资产库结构：

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

### 使用逻辑媒体链接

Markdown 中使用 `media://assets/...` 引用大型外部文件。

示例：

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

`media://assets/` 通过下面的配置解析：

```text
config/media-roots.local.yaml
```

这个配置文件会提交到 Git。换电脑后，修改其中的 `path`，让它指向那台电脑上的百度网盘同步目录。

### 区分事实和建议

AI 生成的建议不能自动变成技术事实。

正确流程：

```text
AI 建议 -> review/ -> 人工判断 -> 证据或实验 -> content.md
```

如果某个结论有价值但尚未验证，在 `content.md` 中明确标记为 `待验证`。

## 根目录文件

### `README.md`

用途：

- 说明 `TechContentHub` 是什么。
- 展示核心工作流。
- 链接最重要的文档。

适合放：

- 仓库定位。
- 高层规则。
- 指向 `INDEX.md`、`CONTEXT.md` 和 `docs/` 的链接。

不适合放：

- 很长的技术笔记。
- 完整平台稿。
- 临时想法。

### `INDEX.md`

用途：

- 作为成熟主题的总导航。

适合放：

- 已经从 `inbox/` 移入 `content/` 的稳定主题。
- 按领域整理的短链接或主题名。

不适合放：

- `inbox/` 里的所有临时想法。
- 未验证结论。
- 重复 `content.md` 的长摘要。

维护规则：

- 当一个主题稳定到值得以后重新找到时，再加入索引。

### `CONTEXT.md`

用途：

- 定义仓库内的核心术语。

适合放：

- 母内容、主题、领域、证据、审查、派生内容、产品化资产、外部资产库等术语。

不适合放：

- 实施步骤。
- 逐目录操作规则。
- 技术研究笔记。

操作规则放在 `docs/directory-guide.md`。

### `config/media-roots.local.yaml`

用途：

- 把 `media://` 逻辑根映射到本机磁盘路径。

适合放：

- `media://assets/` 对应的本机路径。
- 存储类型，例如 `baidu-netdisk-sync`。
- 这个根目录保存什么资产的简短说明。

不适合放：

- 密码。
- Access Token。
- 私密分享链接。
- 每个主题的资产列表。

约束：

- 这个文件为了简单会提交到 Git。
- 换电脑后，直接修改 `path` 为当前电脑的百度网盘同步目录。
- 保持 `uri_prefix` 稳定，这样已有 Markdown 链接不需要改。

示例：

```yaml
version: 1

roots:
  assets:
    uri_prefix: "media://assets/"
    storage: "baidu-netdisk-sync"
    path: "D:/BaiduSyncdisk/TechContentHub-Assets"
```

### `.gitignore`

用途：

- 防止大型文件、生成文件、私有文件和工具噪声进入 Git。

适合放：

- 构建产物模式。
- 二进制和压缩包模式。
- 大模型、大数据、大媒体文件模式。
- 缓存和临时文件模式。

约束：

- 如果确实需要提交一个通常会被忽略的小文件，在使用它的主题附近说明原因。

## `docs/`

用途：

- 保存仓库级文档。

适合放：

- `design.md`：总体设计。
- `directory-guide.md`：目录职责和约束。
- `media-links.md`：`media://` 使用规则。
- 后续的工作流说明、ADR 或维护文档。

不适合放：

- 具体主题的技术研究。应放在 `content/<domain>/<topic>/`。
- 平台稿。应放在主题的 `publish/`。
- 临时捕获笔记。应放在 `inbox/`。

建议后续结构：

```text
docs/
├─ design.md
├─ directory-guide.md
├─ media-links.md
├─ workflow.md
└─ adr/
```

## `inbox/`

用途：

- 快速收集原始想法和还没整理的材料。

适合放：

- 工作中遇到、值得后续研究的问题。
- 粗略文章或视频选题。
- AI 对话摘录。
- 官方文档、Issue、Stack Overflow、论文等链接。
- 小截图。
- 小型 CSV 或 JSON 片段。
- 临时 benchmark 笔记。

不适合放：

- 大视频。
- 大型数据集。
- SDK 或安装包。
- 完整商业项目。
- 客户或公司私有原始数据。
- 构建产物。
- 已经明确属于稳定主题的材料。

约束：

- `inbox/` 允许内容状态比较乱，但文件体积仍然要轻量。
- 大型原始材料不要直接放进 `inbox/`，只放一个 Markdown 说明，指向外部资产位置。

示例：

```markdown
# OSG 渲染问题

状态：原始捕获

大型资产：

- media://assets/inbox/osg-rendering-issue/raw-video/
- media://assets/inbox/osg-rendering-issue/source-model/
```

转入正式内容的规则：

```text
inbox/<rough-note>.md
  -> content/<domain>/<topic>/content.md
```

当材料具备下面条件时，可以移出 `inbox/`：

- 技术问题已经清楚。
- 大致领域已经清楚。
- 有长期维护价值。

### `inbox/tmp/`

用途：

- 存放短期草稿和临时记录。

约束：

- 仍然有价值的内容应尽快移动到 `inbox/` 或 `content/`。
- 不要把这个目录当长期存储。

## `content/`

用途：

- 主母内容资产库。

适合放：

- 已验证或正在长期维护的技术主题。
- 每个领域一个目录。
- 每个具体主题一个目录。

不适合放：

- 随手捕获的零散笔记。
- 没有母内容的平台稿。
- 大型二进制资产。
- 完整商业源码。
- 没有脱敏的客户或公司资料。

领域示例：

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

主题命名：

- 使用小写英文 slug。
- 优先使用 `kebab-case`。
- 名称要具体，能表达技术问题。

推荐：

```text
osg-opengl-version/
linux-rpath-packaging/
cmake-find-package-debugging/
```

不推荐：

```text
notes/
misc/
final/
article/
```

## 标准主题目录

成熟主题统一使用下面结构：

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

用途：

- 主题的母内容，也是唯一事实源。

适合放：

- 问题背景。
- 技术原理。
- 自己的理解。
- 已验证结论。
- 版本和平台边界。
- 复现步骤。
- Demo 说明。
- 常见错误。
- 性能问题。
- 适用范围和不适用范围。
- 后续开放问题。

不适合放：

- 以平台话术为主结构的文章稿。
- 未审查的 AI 建议。
- 客户私有细节。
- 公司内部路径、主机名、IP、凭据、License 信息或专有类名。

约束：

- 结论依赖版本、平台、驱动、编译器、操作系统或硬件时，必须写清边界。
- 缺少证据的结论要标记为 `待验证`。

### `external-assets.md`

用途：

- 索引该主题使用的大型外部文件。

适合放：

- 原始视频、大模型、大型数据集、源素材、大型压缩包、安装包等外部文件的 `media://assets/...` URI。
- 文件名、存储位置、类型、用途，以及它和证据或发布工作的关系。

不适合放：

- 大文件本体。
- 私密凭据或分享密码。
- 应直接放入 `assets/` 或 `data/` 的小文件。

建议条目：

```markdown
## 原始录屏

- 名称：1000 万实例性能测试原始录屏
- 类型：video
- URI：media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
- 存储：百度网盘同步目录
- 用途：B 站视频素材、性能测试证据
```

约束：

- 每个主题优先维护一个 `external-assets.md`。
- 外部资产路径尽量和主题路径保持一致。
- 如果外部文件支撑某个技术结论，要注明关联的证据文件。

### `evidence/`

用途：

- 保存技术结论背后的证据材料。

适合放：

- 官方文档笔记。
- 标准引用。
- Release Note 链接。
- GitHub Issue 链接。
- 实验记录。
- Benchmark 方法和结果。
- 环境细节。
- 复现记录。

不适合放：

- 随机想法。
- 未验证的 AI 建议。
- 大型原始数据集。
- 大段复制的版权文档。

建议文件：

```text
evidence/
├─ references.md
├─ official-doc.md
├─ experiment.md
└─ benchmark.md
```

约束：

- 证据应该帮助区分事实、经验、推断和观点。

### `assets/`

用途：

- 保存主题使用的小型视觉素材或内容素材。

适合放：

- 技术图。
- 小截图。
- 小型图片源文件。
- DrawIO 文件。
- SVG 文件。
- 体积合理的封面源文件。

不适合放：

- 原始视频素材。
- 大型 PSD 或工程文件。
- 大模型文件。
- 大量客户截图或私有数据。

约束：

- 大型视觉或媒体素材放进外部资产库，并在 `external-assets.md` 中记录 `media://` 链接。

### `demo/`

用途：

- 保存支撑主题结论的最小可复现代码。

适合放：

- 最小 Demo。
- Reproducer。
- 小型 benchmark 程序。
- 示例脚本。
- 说明如何运行 Demo 的 `README.md`。

不适合放：

- 完整商业项目。
- 客户源码。
- 构建产物。
- 第三方 SDK 副本。
- 大型依赖。

约束：

- Demo 代码应在脱敏后可以公开。
- 优先保留小而聚焦的示例，不直接复制真实项目。

### `data/`

用途：

- 保存复现实验或解释结果所需的小数据。

适合放：

- 小型 CSV。
- 小型 JSON。
- 小样例输入。
- 轻量 benchmark 输出。

不适合放：

- 大型数据集。
- 客户原始数据。
- 大型网格或模型。
- 二进制 dump。

约束：

- 如果数据无法舒适地在 Git 中审查，就放进外部资产库，并在 `external-assets.md` 中留下 `media://` 链接。

### `review/`

用途：

- 保存主题的人工和 AI 审查记录。

适合放：

- 事实核查记录。
- 缺失点审查。
- 技术风险审查。
- 可复现性审查。
- 隐私和脱敏检查。
- 产品化建议。

不适合放：

- 尚未进入 `content.md` 的最终技术事实。
- 平台稿。
- 原始捕获笔记。

建议文件：

```text
review/
├─ 2026-08-31-review.md
├─ fact-check.md
├─ missing-points.md
└─ improvement.md
```

约束：

- 审查结果是建议。只有经过人工判断，并在需要时补充证据后，才能进入母内容。

### `publish/`

用途：

- 保存平台化派生内容。

适合放：

- B 站脚本、标题、简介。
- 知乎文章草稿。
- 微信公众号文章草稿。
- 小红书笔记。
- 抖音短视频文案。
- 从该主题派生的产品文档。

不适合放：

- 没有同步回 `content.md` 的新技术事实。
- 与母内容矛盾的平台稿。
- 导出后的大视频。

建议结构：

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

约束：

- 这些都是派生文件。事实变化时，先改 `content.md`，再刷新平台稿。

## `templates/`

用途：

- 保存可复用的写作和审查模板。

适合放：

- 母内容模板。
- 证据模板。
- 实验模板。
- Benchmark 模板。
- 审查模板。
- 外部资产索引模板。
- 视频脚本模板。
- 文章模板。

不适合放：

- 具体主题内容。
- 已完成稿件。
- 大型素材。

约束：

- 模板要保持通用，能跨领域复用。

## `skills/`

用途：

- 保存本仓库专用的 AI 工作方法。

适合放：

- 仓库专用 Codex Skill。
- 定义 AI 如何审查或转换技术内容的工作指令。

不适合放：

- 技术知识文章。
- 平台稿。
- 不能形成重复流程的零散提示词。

约束：

- Skill 应描述“如何工作”，不要变成第二套知识库。
- 具体技术知识放进 `content/`。

### `skills/mother-content-reviewer/`

用途：

- 审查 `content.md` 的技术正确性、证据、复现性、脱敏情况和产品化机会。

约束：

- 审查结果应写入主题的 `review/`。
- 不应把建议直接当事实改进 `content.md`。

## `products/`

用途：

- 保存从内容积累中派生出来的可复用或可出售资产。

适合放：

- 工具包。
- 清单。
- 小工具。
- Demo 包。
- 课程大纲。
- 技术资料包。
- 从重复工作流中沉淀出来的 Skill。

不适合放：

- 随机文章草稿。
- 没有产品方向的一次性实验。
- 大型二进制发布包。

约束：

- 每个产品应能追溯到支撑它的 `content/` 主题。
- 产品中的技术主张应能追溯到 `content/` 和 `evidence/`。

示例：

```text
products/
├─ linux-packaging-toolkit/
├─ osg-performance-checklist/
├─ cpp-debugging-skill/
└─ cae-postprocess-demo/
```

## `archive/`

用途：

- 保存过时、被替代、放弃或不再维护的内容。

适合放：

- 废弃主题。
- 被新内容替代的旧草稿。
- 已过时的技术笔记。
- 决定不再继续的选题。

不适合放：

- 活跃主题。
- 大型原始文件。
- 客户或公司私有材料。

约束：

- 当历史可能仍有价值时，优先归档而不是删除。
- 归档内容应补一句简短说明，解释为什么归档。

## 放置检查清单

决定一个材料放哪里时，按下面顺序判断：

1. 是原始想法或快速捕获吗？放进 `inbox/`。
2. 是某个技术问题的长期事实源吗？放进 `content/<domain>/<topic>/content.md`。
3. 是大型外部文件吗？留在 Git 外，并在 `external-assets.md` 里记录 `media://` 链接。
4. 是支撑结论的证据吗？放进 `evidence/`。
5. 是小型视觉素材吗？放进 `assets/`。
6. 是最小可复现代码吗？放进 `demo/`。
7. 是小型复现数据吗？放进 `data/`。
8. 是 AI 或人工审查意见吗？放进 `review/`。
9. 是平台稿吗？放进 `publish/`。
10. 是可复用或可出售资产吗？放进 `products/`。
11. 已过时但仍值得保留吗？放进 `archive/`。
12. 包含私密信息吗？留在仓库外，只记录脱敏后的说明或逻辑链接。
