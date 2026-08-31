# 媒体链接

`media://` 链接是 `TechContentHub` 用来引用外部大文件的逻辑链接。

它是仓库内部约定，不是操作系统协议。普通浏览器或编辑器不一定能直接打开 `media://` 链接，除非有工具读取 `config/media-roots.local.yaml` 并完成路径解析。

## 为什么使用 `media://`

大型原始视频、大模型、大型数据集、源素材、安装包和生成的二进制包应该留在 Git 仓库外。

文档里不要到处写某台电脑的绝对路径，而应该写稳定的逻辑 URI：

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

这个 URI 通过下面的配置文件解析：

```text
config/media-roots.local.yaml
```

示例配置：

```yaml
version: 1

roots:
  assets:
    uri_prefix: "media://assets/"
    storage: "baidu-netdisk-sync"
    path: "D:/BaiduSyncdisk/TechContentHub-Assets"
```

在这个配置下：

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

对应本机路径：

```text
D:/BaiduSyncdisk/TechContentHub-Assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

## 使用位置

`media://` 主要写在每个主题的外部资产索引中：

```text
content/<domain>/<topic>/external-assets.md
```

如果某个技术结论依赖外部文件，也可以在 `content.md` 或 `evidence/` 中引用对应的 `media://` 链接。

## 规则

- 大型外部资产使用 `media://assets/...`。
- 适合进入 Git 的小文件仍然放在 `assets/`、`data/`、`demo/` 或 `evidence/`。
- 大文件不进入 Git，只在 `external-assets.md` 中记录索引。
- `media://assets/` 后面的路径尽量和主题路径保持一致。
- 换电脑后修改 `config/media-roots.local.yaml` 的 `path`。

## 推荐的外部资产库结构

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

## 示例

```markdown
# 外部资产

## 原始录屏

- 名称：1000 万实例性能测试原始录屏
- 类型：video
- URI：media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
- 存储：百度网盘同步目录
- 用途：B 站视频素材、性能测试证据

## 大型测试场景

- 名称：1000 万实例测试场景
- 类型：dataset
- URI：media://assets/content/osg/osg-instance-rendering/large-model/10m-instance-scene.zip
- 存储：百度网盘同步目录
- 用途：复现 benchmark 数据
```

