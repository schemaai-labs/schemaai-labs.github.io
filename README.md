# schemaai-labs.github.io

SchemaAI 的组织站点，站点地址：**https://schemaai-labs.github.io/**

## 本仓不含站点源码

它是一层**部署壳**：`.github/workflows/deploy.yml` 拉取公开的
[`schemaai-labs/showcase`](https://github.com/schemaai-labs/showcase) 仓库，
构建后发布到 GitHub Pages。

**为什么用根仓而不是 showcase 仓直接部署**：showcase 仓直接部署会落在子路径
`/showcase/`，而站内模板把素材路径写成了绝对路径（`/exhibits/assets/…`、
`/exhibits/thumbs/…`），子路径下会全部 404。放在根路径则天然成立，无需为 base 做适配。

## 部署

| 方式 | 说明 |
| --- | --- |
| 手动 | Actions → **Deploy showcase** → *Run workflow*（主路径） |
| 定时 | 每周一 04:23 UTC 兜底重跑 |
| 即时（可选） | showcase 仓 push 后发 `repository_dispatch`（`event_type=showcase-updated`）触发；需在 showcase 仓配置 PAT |

不依赖任何 secrets —— showcase 是公开仓，checkout 不需要凭据。

## 首次配置

1. **Settings → Pages → Build and deployment → Source** 选 **GitHub Actions**
2. 手动跑一次 `Deploy showcase`

## 改站点要改哪里

改站点的内容或代码**不在本仓**：

- 展示站源码 → [`schemaai-labs/showcase`](https://github.com/schemaai-labs/showcase)
- 模板资产 → 上游 monorepo 真源，经 `pnpm sync:showcase-exhibits` 同步进 showcase 仓

本仓只在需要改**部署方式**时改动（例如换自定义域名、加缓存策略）。
