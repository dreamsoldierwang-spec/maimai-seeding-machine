# 🍔 麦麦种草机 · Maimai Seeding Machine

> 把麦当劳 MCP 里的「真实数据」变成创作者手里的「爆款草稿」。
> 你负责拍板，机器负责把活动页、优惠券、营养表翻译成人话。

**麦麦种草机** 是一个基于 [麦当劳中国 MCP（`mcd-mcp`）](https://github.com/M-China/mcd-mcp-server) 的 WorkBuddy 创意 Skill，参加 **2026 麦当劳程序员创意开发大赛**。

它解决的真实痛点：创作者面对麦当劳的活动日历、优惠券、营养数据、主题派对时，常常「数据很多、却不知道怎么写成能发的内容」。麦麦种草机自动取数 → 选题 → 成稿 → 排版，一键产出小红书 / 公众号 / 抖音 可发布草稿。

---

## ✨ 为什么是「种草机」而不是「领券器」

市面上的麦当劳 MCP 项目大多扎在「领券 / Token 管理 / 响应式 UI」这口红海里。
**麦麦种草机换了个战场**：把同样的 MCP 能力，接进创作者的内容工作流——

- 别人做「工具」，我们做「内容生产流水线」；
- 数据来自官方 MCP（真实、合规），产出是平台原生种草稿（可直接发）；
- 覆盖 7 大选题角度：省钱 / 健身减脂 / 节日(1024) / 探店 / 新品 / 亲子 / 夜宵。

---

## 🎯 核心功能

1. **真实取数**：按选题调用对应 MCP 工具（`campaign-calendar`、`available-coupons`、`list-nutrition-foods`、`query-party-*` 等 44 个工具中相关者），绝不编造。
2. **智能选题**：基于真实数据提炼 3–5 个可写角度，每个说明「凭什么能火」。
3. **多平台成稿**：小红书（标题+正文+标签+分镜）、公众号（标题备选+结构+排版建议）、抖音（口播分镜脚本）。
4. **离线工作台**：`demo/麦麦种草机-预览工作台.html` 单文件离线可用，粘贴 MCP 返回的 JSON 即生成草稿，评委与创作者都能直接体验。

---

## 🔌 麦当劳 MCP 接入说明（必看）

> 本 Skill 依赖用户已在 WorkBuddy 接入麦当劳 MCP。步骤如下（详见官方仓库）：

### 1. 申请 MCP Token
- 打开 [麦当劳 MCP 开放平台](https://open.mcd.cn/mcp)，点右上角【登录】→ 手机号验证登录。
- 登录后点【控制台】→ 激活 → 申请 MCP Token → 同意协议 → 一键复制 Token。

### 2. 在 WorkBuddy 配置 MCP
WorkBuddy 的 MCP 配置文件（`~/.workbuddy/mcp.json`）中新增：

```json
{
  "mcpServers": {
    "mcd-mcp": {
      "type": "streamablehttp",
      "url": "https://mcp.mcd.cn",
      "headers": {
        "Authorization": "Bearer 你的_MCP_TOKEN"
      }
    }
  }
}
```

> 接入地址 `https://mcp.mcd.cn`，协议 **Streamable HTTP**，请求头 `Authorization: Bearer <TOKEN>`。
> 频率限制：每 Token 600 次/分钟（超了返回 429）。请妥善保管 Token，勿泄露。

### 3. 启用 Skill
将本仓库的 `SKILL.md` 及 `references/`、`assets/` 放入 WorkBuddy 用户级或项目级 `skills/maimai-seeding-machine/` 目录，对话中直接用自然语言触发即可（如「帮我用麦当劳数据写篇小红书种草」）。

---

## 📂 目录结构

```
maimai-seeding-machine/
├── SKILL.md                      # 核心 Skill 定义（参赛主交付物）
├── README.md                     # 本文件：介绍 + MCP 接入说明
├── references/
│   ├── platform-templates.md      # 小红书/公众号/抖音 文案模板与范例
│   ├── mcp-mapping.md             # 选题角度 → MCP 工具 → 关键字段 映射
│   └── angle-playbook.md          # 七大选题角度玩法库
├── assets/
│   └── brand-kit.md               # 视觉设计参考（配色/字体/风格，非商标授权）
├── demo/
│   └── 麦麦种草机-预览工作台.html   # 单文件离线演示 / 实用伴侣
├── examples/
│   └── 示例输出.md                # 一次完整调用示例（mock 数据，仅演示）
└── 参赛声明.md                    # 原创性与合规声明
```

---

## 🚀 快速体验（无需 Token）

打开 `demo/麦麦种草机-预览工作台.html`：
1. 选择平台（小红书 / 公众号 / 抖音）与角度；
2. 粘贴麦当劳 MCP 工具返回的 JSON（或点「载入示例」）；
3. 一键生成草稿 + 配图分镜 + 话题标签，支持复制 / 导出 Markdown / JSON。

---

## ⚠️ 合规声明（摘要）

- 本工具为**第三方创作辅助**，与麦当劳无官方关联，不暗示官方背书、合作或授权。
- 遵守《麦当劳 MCP 服务规则》与《使用条款》，仅用于**非商业**个人创作。
- 所有活动 / 优惠 / 价格 / 营养数据均来自 MCP 真实返回，缺数据处标注「以官方/门店实际为准」，不编造。
- 麦当劳商标、Logo 仅作「被描述对象」出现，不构成任何授权。详见 `参赛声明.md`。

---

## 🏆 参赛信息

- **赛事**：2026 麦当劳程序员创意开发大赛（麦当劳中国 × WorkBuddy）
- **时间**：2026/10/9 10:30 – 2026/10/25 23:59
- **赛道**：基于麦当劳 MCP 的创意 Skill 开发
- **开发方式**：全程使用 WorkBuddy 辅助开发（享专项积分奖励）

> 用 WorkBuddy 开发参赛可获得 3000 积分专项奖励；本作品即在此流程下完成。
