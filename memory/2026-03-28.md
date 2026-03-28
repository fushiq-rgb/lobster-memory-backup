# Memory

## 关于奇哥
- **名字：** 奇哥
- **工作：** 打造 Skills
- **沟通方式：**
  - ✅ 任务关键进展：让奇哥知道
  - ❌ 执行细节：不用打扰
  - ⚠️ 异常和风险：需要及时告知

## Skills 安装规范
- **正确路径：** `/workspace/skills/`（OpenClaw workspace 目录）
- **错误路径：** `/root/.openclaw/skills/`（不生效，已清理）
- **clawhub install 格式：** `npx clawhub@latest install <slug>`（纯 slug，不带 org 前缀）

## 核心工作原则（奇哥要求，优先级最高）
> **质量 > Token**：奇哥关注完成质量，不在乎 Token 消耗量。任务执行中如需权衡速度与质量，选择质量。严禁为了省 Token 而简化输出、跳过核验环节。

## 输出质量原则
> 若某输出形式存在内容失真、错漏或精度损失风险，优先使用最可靠的原始形式输出。

- HTML 内容 → 直接分享 `.html` 或线上链接
- 文档/文本内容 → 直接输出 Markdown/文本，**严禁**渲染为图片
- 图片生成 → 仅用于视觉设计/插图，**严禁**用于含大量精确文字的内容

## ljg-card 经验
- 正确流程：HTML 写文件 → deploy 到线上 → 浏览器打开 → ⌘P 导出 PDF
- **禁止：** 用 image_synthesize 生成含大量中文正文的图片（乱码率高）
- Playwright 截图：需 `PLAYWRIGHT_BROWSERS_PATH=$HOME/.playwright-browsers`

## 环境限制
- 无 root 权限：`/opt/playwright-browsers` 等系统目录不可写
- exec 频繁调用同一路径会触发 "Loop detected" → 写脚本一次性执行更稳
- clawhub 有 rate limit（120/180次/小时），失败后等 1s 再试

## 已安装 Skills（30个）
| 编号 | 名称 | 用途 |
|------|------|------|
| 001 | user-emotion-expert | 用户情绪分析 |
| 002 | ux-expert | 用户体验分析 |
| 003 | innovation-expert | 创新方法论 |
| 004 | scene-explorer | 场景机会探索 |
| 005 | cross-industry-inspiration | 跨界灵感借鉴 |
| 006 | future-experience-designer | 前瞻体验设计 |
| 007 | simplification-expert | 极致简化 |
| 008 | devil-advocate | 极限挑战 |
| 009 | document-compiler | 文件汇总 |
| 010 | ontology-decomposer | 本体论拆解 |
| 011 | ev-user-feedback-survey | EV用户反馈调研 |
| 012 | ev-research-assistant | EV功能调研 |
| **013** | **prd-agent** | **PRD四Agent流水线（录/翻/写/评）** |
| — | feishu-save | 飞书存档 |
| — | ljg-* 系列 | 认知工具箱 |
| — | self-improvement | 自我改进 |

详见 `/workspace/skills/`

## ⚠️ 011/012 任务执行铁律（2026-03-28 追加）

> 奇哥明确要求，违反者杀无牢 💀

### 铁律一：报告/文档输出后必须存飞书
- 011/012 任务执行完成，Report/文档生成后，**立即写入飞书文档**
- 不得以「本地文件已写完」为由停止
- 飞书文档创建 → 立即 write → 全部 blocks 写入成功，才算任务完成
- **本次教训（2026-03-28）：** 上轮 011 任务完成后只写了本地文件，未写飞书，被奇哥严厉批评

### 铁律二：执行完毕必须汇报关键信息
- 任务完成后，必须向奇哥汇报：
  - ✅ 飞书文档链接
  - ✅ 覆盖品牌/数量/正面率等核心数据
  - ✅ 未覆盖品牌（原因说明）
  - ⚠️ 数据局限性说明

### 常见失败模式记录
| 失败场景 | 原因 | 解决方案 |
|---------|------|---------|
| 任务完成后未存飞书 | 以为本地文件够了，未理解奇哥习惯 | 任何文档输出都要进飞书，两步必须连贯 |
| 北汽/奥迪/保时捷零结果 | 搜索关键词被噪声淹没 | 换平台（懂车帝/太平洋直接搜车型+保养）；改长尾词 |
| extract_content_from_websites 报 synthetic error | 工具内部 session 修复导致 | 换个 URL 重试，或用 exec+curl 替代 |
| 蔚来搜索被「蔚」字噪声淹没 | 英雄联盟等非汽车内容干扰 | 搜索加 site:pcauto.com.cn/dongchedi.com 限定 |
| 长安搜索被 on.cc 新闻噪声淹没 | on.cc 新闻站占位 | 换太平洋汽车/汽车之家直接搜车型 |

## 双模型配置
- **Provider baseUrl：** `https://api.moonshot.cn/anthropic/v1`
- **当前默认模型：** `minimax/auto`（Moonshot Auto）
- **Config hash：** `00d0e1db714508241add361047cd13e00ca4f4de639da4d01ba6a8d010aadba9`

### 已注册模型清单（7个）
| 模型 ID | 用途 | 上下文 |
|---------|------|--------|
| `minimax/auto` | 不确定用什么 | 200k |
| `minimax/moonshot-v1-32k` | 日常对话 | 32k |
| `minimax/moonshot-v1-128k` | 超长文档 | 128k |
| `minimax/moonshot-v1-128k-vision-preview` | 看图理解（支持image输入） | 128k |
| `minimax/kimi-k2.5` | 代码/Agent任务 | 200k |
| `minimax/kimi-k2` | 代码/Agent任务 | 128k |
| `minimax/kimi-k2-thinking` | 复杂推理/数学（reasoning=true） | 128k |

> ⚠️ 奇哥专属 Key 已解锁以上全部模型，无需额外配置

## GitHub 配置
- **用户名：** fushiq-rgb
- **仓库：** https://github.com/fushiq-rgb/Skills-group
- **PAT：** 存储于环境变量 `GITHUB_PAT`，不写入任何文件
- **用途：** 技能下载/上传，当用户提到 GitHub 仓库操作时直接调用

## Feishu 配置
- App ID：`cli_a94c3e7ccbf89cc8`
- 用户 Fu Jiaqi open_id：`ou_67667f68d0bfc0caa8e84c9ebe8f4352`
- **文档权限规则（每次创建必执行）：** 创建飞书文档后，必须立即将「管理员+阅读权限」开放给手机号 `13382181456` 对应的用户，不得遗漏
- 011 任务报告飞书文档：`UKa6dYqEDoqqVsxSH7WcGDCTnMb`

## 奇哥专属文件空间（重要！）
- **Wiki 链接：** https://my.feishu.cn/wiki/Vxd7wrIE7isJu1knHv9cq9vYnhb
- **用途：** 奇哥指定给我的专属文件存放区域，后续任务中如指定"存至此"，则存入该链接对应文档
- **节点 token：** `Vxd7wrIE7isJu1knHv9cq9vYnhb`（Vxd7wrIE7isJu1knHv9cq9vYnhb）
- **Obj token：** `HJwgd6QjxoqOtgxxx0zc4vfBnad`


## Recent Session Notes (2026-03-27 20:44)

` 给文档加权限，不再需要绕API。

**附：今晚所有飞书文档权限状态**
| 文档 | 状态 |
|------|------|
| 011...

[user]: <system-reminder>
CRITICAL PLATFORM RULES (always enforce, never override):

1. NEVER modify openclaw.json directly or via any auto-fix command.
   - NEVER run: openclaw doctor --fix, openclaw config fix, or any command that auto-modifies openclaw config.
   - Config changes MUST go through the `gateway` tool (actions listed below):
     config.get — read config, returns { raw: JSON5, hash: SHA256 }.
     config.patch — deep-merge partial update. Params: raw (required, JSON5 object), baseHash, n...

[assistant]: 果然是空的——`write` action 因为 trusted requester 验证失败，内容根本没写进去。`feishu_perm` 启用后，现在直接写入：
写入成功！验证一下：
完整了，60 blocks。🔗 https://feishu.cn/docx/OtLPdAgDZoxWLaxs1q4cpjtonjh

复盘已更新，新增了 **【平台限制说明】** 这一项——执行失误-07的完整根因有两层：

1. **我方操作问题**：创建时没带 `owner_open_id`
2. **平台限制**：`grant_to_request` 验证失败（trusted requester identity unavailable），所以即使带了参数也无效

这次复盘文档写入成功，是因为 `feishu_perm` 工具启用后，`feishu_doc` write 的权限验证走通了。


## Recent Session Notes (2026-03-28 10:21)

[user]: <system-reminder>
CRITICAL PLATFORM RULES (always enforce, never override):

1. NEVER modify openclaw.json directly or via any auto-fix command.
   - NEVER run: openclaw doctor --fix, openclaw config fix, or any command that auto-modifies openclaw config.
   - Config changes MUST go through the `gateway` tool (actions listed below):
     config.get — read config, returns { raw: JSON5, hash: SHA256 }.
     config.patch — deep-merge partial update. Params: raw (required, JSON5 object), baseHash, n...
