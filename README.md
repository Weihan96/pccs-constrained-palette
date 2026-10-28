# PCCS 约束配色 · Constrained Palette

柜板已选、窗框不能改，只能从几款真实饰面里选框架？这个技能先锁定条件，再用 PCCS 解释颜色关系，并检查放回空间后谁主谁次，最后交付一张 PCCS 名称与编号优先、HEX 单独成列的推荐表。

Already chose the cabinet finish and need to work around a fixed window frame? This skill compares the finishes you can actually choose, explains their PCCS relationships, and checks visual hierarchy in context. It returns a recommendation with PCCS names/codes, separate HEX references, and evidence quality.

## 中文

### 前置条件

- [ ] 已安装支持本地技能的 Codex；尚未安装可从下方官方入口安装并登录。
- [ ] 使用 Bun 安装命令时，需要 Bun。macOS 可运行 `brew install oven-sh/bun/bun`，Windows 可运行 `powershell -c "irm bun.sh/install.ps1|iex"`；用 `bun --version` 验证。已有 Bun 可跳过。
- [ ] 准备已选材料、固定环境与可选饰面。照片、色卡或样板记录都可使用；证据不足的字段会标为待确认。

[Codex 官方入口](https://developers.openai.com/codex/)

[Bun 官方安装说明](https://bun.sh/docs/installation)

技能本身是 Markdown 指令与参考资料，不需要 API 密钥、付费色彩数据库、Python 或额外 MCP 服务。

### 安装

1. 打开终端，运行 `bun --version`，确认 Bun 可用。
2. 执行 `bunx --bun skills add Weihan96/pccs-constrained-palette --global --agent codex --yes`。
3. 执行 `bunx --bun skills list --global`，确认列表出现 `pccs-constrained-palette`。
4. 在 Codex 下一轮消息调用 `$pccs-constrained-palette`。若当前技能列表未刷新，重新加载 App 或新开聊天后再检查。

macOS/Linux 默认个人目录使用 `~`；Windows 使用用户主目录。上面的技能管理命令负责选择安装位置，无需把示例中的本机绝对路径复制到另一台机器。若维护者已有指向源码的个人技能链接，应先检查其目标，避免用另一份副本覆盖正在维护的技能。

### 使用示例

- “柜板和窗框不变，只从这三款框架饰面里选一款，用 PCCS 给我推荐表。”
- “这组中差色相能用吗？请分别检查共同色调、空间主次和我想要的柔和差异。”
- “根据这些样板照片做近似映射，把 PCCS 名称、编号、HEX 和映射依据分开列。”

内部工作：锁定条件 → 映射固定项与候选 → 筛选并组织配色 → 检查空间主次。

汇报顺序：一句明确推荐 → 材料色样与 PCCS 参考色并置、主方案表 → 约束、未选理由、来源与不确定性。映射方法灵活，以用户对并置色样的视觉反馈核对接近程度；未确认标暂定，已确认且未变化不重复审批。屏幕确认不等于实物验收或官方标准映射。

| PCCS 名称与编号 | 应用位置 | 材料／饰面 | HEX 屏幕参考 | 视觉角色 | 配色关系 | 映射依据／状态 |
|---|---|---|---|---|---|---|
| 色调名、色相名与编号，或待确认 | 实际位置 | 真实可选材料 | 有依据的六位色值，或待确认 | 重点／背景／过渡 | 与明确对象比较：共同点、变化及作用 | 来源、近似性质、视觉确认状态与限制 |

[查看含并置色样的报告样例](references/report-example.html)

### 限制

不内置官方 PCCS—HEX 对照。照片映射是近似判断，单个 HEX 不能表达金属反射、皮革方向或纹理。邻近／中差的筛选优先级是可被项目目标覆盖的个人默认偏好；“中差更依赖主次”是待验证假说。技能不自动购买材料、修改场景或生成效果图；这些动作仍依当前任务授权。公开包不含私人聊天记录。

### 常见问题

| 问题 | 处理 |
|---|---|
| `bun: command not found` | 完成上面的 Bun 安装，重新打开终端，用 `bun --version` 检查 PATH |
| 安装后找不到技能 | 用 `bunx --bun skills list --global` 确认安装；再刷新 Codex 会话，确认使用同一系统账户 |
| 安装目录已有同名技能 | 检查旧目录或符号链接，不盲目覆盖；维护者可直接更新已有源码目录 |
| 表格里 PCCS 或 HEX 为待确认 | 提供具体色卡、样板或可信数值来源；营销名称本身不足以生成精确值 |
| HEX 没显示成色块 | 渲染取决于客户端；六位色值仍保留，可用于后续色样预览 |

## English

### Requirements and installation

- [ ] Install and sign into Codex using the official link above.
- [ ] Install Bun if needed: `brew install oven-sh/bun/bun` on macOS or `powershell -c "irm bun.sh/install.ps1|iex"` on Windows. Verify with `bun --version`; the official Bun guide covers other setups.
- [ ] Supply fixed materials, surrounding constraints, available finishes, and the intended focal point. Photos are acceptable, with uncertainty retained.

1. Run `bun --version`.
2. Run `bunx --bun skills add Weihan96/pccs-constrained-palette --global --agent codex --yes`.
3. Verify with `bunx --bun skills list --global`.
4. Invoke `$pccs-constrained-palette` in your next Codex turn. Reload the app or start a new chat if discovery is stale.

The installer handles platform-specific home directories. Check an existing installation or source symlink before replacing it. The skill itself needs no API key, paid colour database, Python runtime, or additional MCP service.

### Try it

- “Keep the cabinet panels and window frame fixed. Pick one of these three frame finishes and provide a PCCS table.”
- “Can this medium hue-distance pairing work? Check shared tone and visual hierarchy separately.”
- “Map these sample photos approximately, with separate PCCS, HEX, and evidence columns.”

The report starts with one recommendation, then side-by-side material and proposed PCCS swatches and the main palette table, followed by constraints, rejected alternatives and evidence. Each relationship names its comparison target; visual role and colour relationship have separate columns. Mapping methods remain flexible. Ask whether the swatches feel close, keep unconfirmed matches provisional, and reuse unchanged confirmations. Screen confirmation is neither physical sample acceptance nor an official standard mapping. The result records PCCS names/codes, location, actual material, screen HEX and mapping evidence. It distinguishes colour discrimination, similarity, harmony, preference, and hierarchy. Missing evidence remains unknown rather than becoming a fabricated standard code.

### Limits and troubleshooting

There is no official PCCS-to-HEX lookup bundled here. Photos and screen values do not establish physical colour standards; metallic reflections and texture require additional observations. The hue-selection preferences are adjustable design heuristics, and the hierarchy explanation remains a hypothesis. Purchases, scene edits, and image generation are not automatically authorized. Private conversation archives are excluded from the public release.

| Issue | Resolution |
|---|---|
| Bun is not found | Install it, reopen the terminal, and check `bun --version` |
| Skill is missing after installation | Check `bunx --bun skills list --global`, then reload Codex under the same account |
| A skill with this name already exists | Inspect the existing directory or symlink before replacing it |
| PCCS or HEX is unknown | Supply an actual colour sample or traceable reference; a marketing name is insufficient |
| HEX does not render as a swatch | Swatch rendering depends on the client; the numeric reference remains available |

## Sources and acknowledgements · 来源与致谢

PCCS originates with the Japan Color Research Institute. The hue-distance teaching discussed here comes from 歪角 色彩實驗室; it is not presented as a universal scientific prohibition. Research by Karen B. Schloss and Stephen E. Palmer motivates keeping preference and harmony judgments distinct. This skill is an independent workflow, not an official PCCS product or endorsement.

[日本色彩研究所 · PCCS](https://www.jcri.jp/achievement_1)

[歪角 色彩實驗室 · EP.005](https://www.youtube.com/watch?v=O-sx-BL0_-U)

[Schloss & Palmer (2011)](https://pubmed.ncbi.nlm.nih.gov/21264737/)

[Evidence and scope / 依据与适用边界](references/evidence.md)

## License

MIT for the skill's original text and instructions. Referenced third-party sources retain their own rights; no official colour dataset is redistributed.
