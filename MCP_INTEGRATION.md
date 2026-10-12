# MCP 集成说明（MCP Integration）

本文件说明「麦麦种草机」实际使用的麦当劳 MCP Server、Tool、调用流程与业务价值，用于活动资格核验。

## 使用的麦当劳 MCP Server

- Server 名称：麦当劳 MCP（官方仓库 M-China/mcd-mcp-server）
- 接入地址：`https://mcp.mcd.cn`
- 传输方式：Streamable HTTP
- 鉴权方式：Bearer Token（用户自行在 open.mcd.cn 申请的麦当劳 MCP Token，仅存于本地 WorkBuddy 配置）

## 实际使用的 Tool

本 Skill 在内容创作流程中**真实调用**以下 Tool 获取真实数据（非虚构、非占位）：

| Tool | 用途 |
|---|---|
| `campaign-calendar` | 查询当月营销活动日历（进行中 / 往期 / 未来活动），用于让种草选题契合营销节点 |
| `available-coupons` | 查询可领取的麦麦省券列表，用于种草文案中的优惠钩子 |
| `query-my-coupons` | 查询我的券，用于个性化优惠提示 |
| `list-nutrition-foods` | 餐品营养信息（能量/蛋白质/脂肪/碳水/钠/钙），用于健康/健身角度种草 |
| `query-meals` | 菜单查询，用于新品与餐品介绍 |
| `query-party-city` / `query-party-store` / `query-party-date` / `query-party-session` | 1024 主题派对预约信息，用于节日探店脚本 |
| `query-nearby-stores` | 附近门店查询，用于本地化种草 |

## 调用流程

1. 用户在 WorkBuddy 对话中描述种草需求（如"帮我写篇小红书省钱种草"）
2. Skill 触发，按 `references/mcp-mapping.md` 解析选题角度与所需 Tool
3. 调用上述麦当劳 MCP Tool 拉取真实活动 / 券 / 营养 / 门店数据
4. 数据经 `references/platform-templates.md` 与 `references/angle-playbook.md` 加工为平台原生文案
5. 输出种草草稿 + 配图分镜建议 + 话题标签，用户可直接复制发布

## 业务价值

将麦当劳官方 MCP 能力从"工具调用"升级为"内容生产流水线"：数据来自官方（真实、合规），产出是可直接发布的小红书 / 公众号 / 抖音种草草稿，显著降低创作者的生产门槛，契合本次活动"用创意解决实际问题"的宗旨。
