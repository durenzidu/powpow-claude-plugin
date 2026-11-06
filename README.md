# PowPow

**附近发现，交给 AI 助手。** 泡泡（PowPow）是一款基于位置的社交应用 —— 用户在地图上发布带位置的帖子、创建可对话的数字人（AI 角色）、参与线下打卡活动。这个插件把 PowPow 的能力开放给你的 AI 助手。

English below · 中文在上

---

## 它能做什么

插件挂载了 **PowPow 远程 MCP 服务**，共 **34 个工具**（20 个只读 + 14 个写）：

| 分组 | 能做的事 |
| --- | --- |
| 附近发现 | 按地名解析坐标、找附近的数字人 / 帖子 / 景点商圈 |
| 账号与社交 | 读资料与发帖记录、看关注与收藏、查徽章历史 |
| 内容创作 | 起草并发布带地点标签的帖子、点赞、关注、收藏、回复 |
| 数字人 | 创建可对话的 AI 角色、匹配已有角色、删除自己创建的 |
| 活动与会员 | 查线下打卡活动、账号会员状态与到期时间 |

## 安装

### 方式一：分两步（通用，推荐）

```bash
claude plugin marketplace add durenzidu/powpow-claude-plugin
claude plugin install powpow@powpow
```

### 方式二：Claude Code 会话内一步完成（需 v2.1.275+）

```
/plugin install powpow --marketplace durenzidu/powpow-claude-plugin
```

### 方式三：shell 内一步完成（需 v2.1.292+）

```bash
claude plugin install powpow --marketplace durenzidu/powpow-claude-plugin
```

> 只想在 Claude Code 里连 MCP、不装插件也可以：
> `claude mcp add --transport http powpow https://global.powpow.online/api/mcp`

## 登录

首次调用工具时会打开浏览器，授权你的 PowPow 账号。认证走 **OAuth 2.1 + PKCE**，支持动态客户端注册（不需要手工申请 client_id）。

授权页会显示这个插件要访问的内容，你可以随时在浏览器里拒绝。

## 权限与数据说明

**这个插件会连到哪里（全部目的地，仅此两处）：**

| 目的地 | 用途 |
| --- | --- |
| `https://global.powpow.online` | PowPow 官方站点 —— MCP 端点、OAuth 同意页、账号注册 |
| `https://xhahsqbaohraqrdhtvay.supabase.co` | PowPow 的认证服务（Supabase Auth）—— 账号登录与令牌签发 |

**它会做什么：**

- 读取你的 PowPow 账号资料、帖子、关注、收藏、徽章与会员状态
- 在你确认后发布帖子、点赞、关注、收藏、回复、创建数字人

**它不会做什么：**

- 不上传本地文件、不读取你的硬盘、不读环境变量
- 不做任何埋点或第三方分析
- 不提供购买、订阅或支付操作（`get_my_account` 会返回会员等级与到期时间，但**不会**有任何购买入口）

**写操作的两道保险：**

1. 发帖永远是「先出草稿 → 你确认 → 才发出」，由服务端强制，不由提示词保证
2. 通过 AI 创建的帖子或数字人，**24 小时内**可由 AI 撤销；更早的内容请在 PowPow App 里管理

**限流：** 三个公开搜索工具（`find_nearby`、`geocode_place`、`nearby_attractions`）每个访问令牌 60 秒内限 12 次，其余工具不限流。

**数据范围：** 覆盖主要集中在中国大陆；帖子仅支持纯文字，不能上传照片；头像、私信、通知、订阅与支付不在插件能力范围内。

## 隐私与条款

- 隐私政策：https://global.powpow.online/privacy-policy
- 服务条款：https://global.powpow.online/terms-of-service
- 支持：https://global.powpow.online/support

## 文档

- MCP 完整文档（34 个工具逐一说明）：https://global.powpow.online/mcp-docs
- 官方网站：https://www.powpow.online/

---

# PowPow (English)

**Nearby discovery, handed to your AI assistant.** PowPow is a location-based social app where people publish geotagged posts, create talkable digital humans (AI characters), and join offline events. This plugin exposes PowPow's capabilities to your assistant.

## What it does

The plugin bundles the **PowPow remote MCP server** with **34 tools** (20 read-only, 14 write):

- **Nearby discovery** — resolve a place name to coordinates, then find digital humans, posts, attractions and business districts around it
- **Account and social** — read your profile, posts, follows, favorites, badge history and membership status
- **Content** — draft and publish geotagged posts, like, follow, favorite, reply
- **Digital humans** — create talkable AI characters, match existing ones, delete ones you created
- **Events and membership** — look up offline check-in campaigns and your subscription status

## Install

```bash
claude plugin marketplace add durenzidu/powpow-claude-plugin
claude plugin install powpow@powpow
```

In a Claude Code session (v2.1.275 or later):

```
/plugin install powpow --marketplace durenzidu/powpow-claude-plugin
```

Prefer a plain MCP connection without the plugin?

```bash
claude mcp add --transport http powpow https://global.powpow.online/api/mcp
```

## Sign in

The first tool call opens your browser to authorize your PowPow account. Authentication uses **OAuth 2.1 with PKCE** and dynamic client registration, so no manual client ID is needed. The consent page shows exactly what the plugin asks for, and you can decline at any time.

## Permissions and data

**Network destinations — these two, and nothing else:**

| Destination | Purpose |
| --- | --- |
| `https://global.powpow.online` | The PowPow site — MCP endpoint, OAuth consent page, account sign-up |
| `https://xhahsqbaohraqrdhtvay.supabase.co` | PowPow's authentication service (Supabase Auth) — sign-in and token issuance |

**What it does:** reads your PowPow profile, posts, follows, favorites, badges and membership; and on your confirmation publishes posts, likes, follows, favorites, replies and creates digital humans.

**What it does not do:** it uploads no local files, reads no files from your disk, reads no environment variables, performs no third-party analytics, and exposes no purchase or subscription action. `get_my_account` returns your membership tier and expiry date, but there is no way to buy anything through it.

**Two safeguards on writes:** posting is always two-step — draft first, publish only after you confirm, enforced server-side — and anything the assistant creates can be undone through the assistant within 24 hours.

**Rate limits:** the three public search tools (`find_nearby`, `geocode_place`, `nearby_attractions`) allow 12 calls per 60 seconds per access token. The other tools are not rate limited.

**Scope:** coverage is concentrated in mainland China; posts are text-only with no photo upload; avatars, direct messages, notifications, subscriptions and payments are out of scope.

## Legal

- Privacy policy: https://global.powpow.online/privacy-policy
- Terms of service: https://global.powpow.online/terms-of-service
- Support: https://global.powpow.online/support
- Full MCP documentation: https://global.powpow.online/mcp-docs

## License

MIT — see [LICENSE](./LICENSE).
