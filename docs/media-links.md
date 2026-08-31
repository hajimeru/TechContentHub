# Media Links

`media://` links are logical links used by TechContentHub to reference large files that live outside Git.

They are repository conventions, not operating-system protocols. A normal browser or editor may not open them directly unless a tool resolves them with `config/media-roots.local.yaml`.

## Why Use `media://`

Large raw videos, large models, heavy datasets, source footage, installers, and generated binary packages should stay outside this Git repository.

Instead of writing machine-specific paths everywhere, use a stable URI:

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

This URI is resolved through:

```text
config/media-roots.local.yaml
```

Example mapping:

```yaml
version: 1

roots:
  assets:
    uri_prefix: "media://assets/"
    storage: "baidu-netdisk-sync"
    path: "D:/BaiduSyncdisk/TechContentHub-Assets"
```

With that mapping, this URI:

```text
media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

points to:

```text
D:/BaiduSyncdisk/TechContentHub-Assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
```

## Where To Use It

Use `media://` mainly in each topic's external asset index:

```text
content/<domain>/<topic>/external-assets.md
```

It can also appear in `content.md` or `evidence/` when a claim depends on an external file.

## Rules

- Use `media://assets/...` for large external assets.
- Keep small files that belong in Git under `assets/`, `data/`, `demo/`, or `evidence/`.
- Keep large files out of Git and reference them through `external-assets.md`.
- Keep the path after `media://assets/` aligned with the topic path when possible.
- Edit `config/media-roots.local.yaml` after cloning on another computer.

## Recommended External Asset Layout

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

## Example

```markdown
# External Assets

## Original Recording

- Name: 10 million instance performance test recording
- Type: video
- URI: media://assets/content/osg/osg-instance-rendering/raw-video/10m-instance-test.mp4
- Storage: Baidu Netdisk sync
- Purpose: Bilibili source material and performance evidence

## Large Test Scene

- Name: 10 million instance test scene
- Type: dataset
- URI: media://assets/content/osg/osg-instance-rendering/large-model/10m-instance-scene.zip
- Storage: Baidu Netdisk sync
- Purpose: Reproducing benchmark data
```

