# Surge Claude 补充规则

为现有 AI 规则补充 Claude / Anthropic 相关域名，共 22 条。覆盖新增产品域名、社区收录域名、部分 Artifact 脚本库、更新检查和可选服务。

## 添加到 Surge

在配置的 `[Rule]` 区域添加一行：

```ini
RULE-SET,https://raw.githubusercontent.com/Aryous/surge-claude-rules/main/ClaudeSupplement.list,OpenAI
```

`OpenAI` 是接收这些请求的策略或策略组名称；使用其他名称时，替换最后一项即可。规则集中的域名不会自动选择节点，实际出口由这个策略决定。

**将这一行放在广告、跟踪及其他拦截规则之后，普通服务分流和 `FINAL` 之前。** 如果原配置按“广告规则 → AI 规则 → 其他服务 → FINAL”排列，放在 AI 规则区域即可。Surge 按顺序匹配，先命中的拦截规则应继续生效。

规则文件每行只写类型和域名；统一策略在上述引用行中指定。语法说明见 [Surge Rule Sets](https://manual.nssurge.com/rules/ruleset.html)。

## 域名范围

| 分类 | 条数 | 域名 |
| --- | ---: | --- |
| 官方 Desktop 域名 | 2 | `claude.app`、`claudemcpcontent.com` 及其子域名 |
| 社区收录域名 | 12 | `ant.dev`、`anthropic.team`、`antspace.dev`、`chatbotclaude.com`、`claude.dev`、`claude.new`、`claude.site`、`claudeacademy.com`、`claudemcpclient.com`、`claudepages.dev`、`claudestudio.com` 及其子域名；`servd-anthropic-website.b-cdn.net` |
| Artifact 脚本库 | 3 | `cdn.tailwindcss.com`、`code.jquery.com`、`unpkg.com` |
| Homebrew 更新检查 | 1 | `formulae.brew.sh` |
| 可选运行遥测 | 2 | `http-intake.logs.us5.datadoghq.com`、`browser-intake-us5-datadoghq.com` |
| 社区收录的功能配置服务 | 1 | `cdn.growthbook.io` |
| MCP 文档与生态 | 1 | `modelcontextprotocol.io` 及其子域名 |

`claude.app` 和 `claudemcpcontent.com` 已列入官方 Desktop 网络要求。Artifact 脚本库仅在内容使用相应依赖时需要；Homebrew 域名用于对应安装方式的版本检查；两个 Datadog 域名用于可选运行遥测。

社区条目来自维护者的域名分类，具体产品用途和必要性尚未逐项获得官方说明。`cdn.growthbook.io` 来自社区对客户端的分析，当前官方必需网络清单未列出该域名。共享服务使用精确域名规则，避免将整个 CDN、Google 或 Datadog 服务纳入同一策略。

## 与现有规则配合

本文件是补充清单。主站和 API 的 `anthropic.com`、`claude.ai`、`claude.com`、`clau.de`、`claudeusercontent.com` 应由已有 AI 规则覆盖，使用前可查看相应规则集的内容。

以下域名不纳入本清单，继续由原有拦截规则处理：

- `statsig.anthropic.com`
- `api.statsig.com`
- `events.statsigapi.net`
- `cdn.usefathom.com`
- `sentry.io`

本清单不包含上述域名的父级后缀放行规则。新增的两个 Datadog 条目是另一组可选服务；若已有规则拦截它们，也应让拦截规则排在本清单之前。

## 来源

核对日期：2026-10-29。

- [Anthropic Desktop 网络要求](https://code.claude.com/docs/en/desktop#network-access-requirements)
- [Claude Code 网络要求](https://code.claude.com/docs/en/network-config#network-access-requirements)
- [v2fly Anthropic 域名分类](https://github.com/v2fly/domain-list-community/blob/master/data/anthropic)
- [MetaCubeX Anthropic 域名分类](https://github.com/MetaCubeX/meta-rules-dat/blob/meta/geo/geosite/anthropic.list)
- [Anthropic / Claude 社区域名登记及用途说明](https://github.com/xiaolai/anthropic-claude-surge-rules-set/blob/main/domains.yaml)
- [Sukka AI 规则](https://ruleset.skk.moe/List/non_ip/ai.conf)
- [EAlyce AI 规则](https://github.com/EAlyce/conf/blob/main/Rule/OpenAI.list)

维护时可直接编辑 `ClaudeSupplement.list`；引用地址保持不变。远程规则的下载和缓存由 Surge 管理。
