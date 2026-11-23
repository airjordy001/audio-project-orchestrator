# 音频软件项目总统筹 Skill

**推进方式**：每个重要环节按 SKILL.md 的「逐环节审批」执行 grill-me 访谈，取得用户对具体下一步的明确同意。本文中的自主执行、超时替代与里程碑安排均受该规则约束。

本仓库提供一个通用、开源的 Agent Skill：把本地音频软件项目从立项推进到本机可验证交付。它适用于效果器或乐器插件、DSP 原型、采样音源、本机独立应用，以及本地工具链或 SDK。

本 Skill **不是**发行经理手册。它默认不考虑商店上架、商业分发、市场推广或对外客服。但「非商业 / 仅本地」并不意味着可以忽略第三方依赖的许可证与版权义务。

## 范围与限制

**适用**

- 一人 Sponsor + 本地 AI 团队的本机音频软件项目
- 立项、范围控制、任务拆解、RACI、卡点处理、质量门禁、本机安装与回滚、跨会话交接
- VST3 / AU 等本机可加载格式（仅在项目明确要求时才纳入其他格式）

**默认不适用（除非变更单明确扩大范围）**

- 商店上架、公证发行、安装器商业分发
- AAX、DRM、授权服务器、防逆向加固
- 官网、账户系统、对外客服、社区与市场运营
- 把某一家 Agent、某个运营商或某套内部工具写死为前置条件

**硬限制（摘录）**

- 可逆决策不等于已授权访问账户、发送消息或安装软件
- 没有相应工具或权限时，不得声称已经执行构建、测试、安装或验收
- 听力安全与数据完整性风险不得当作 P1 例外放行
- 音频线程禁止内存分配、文件 I/O、阻塞锁和网络 I/O；实测指标须事先商定
- 收到停工指令必须立即停止，禁止无限重试，并遵守资源预算

完整规则见 [`references/handbook.zh-CN.md`](references/handbook.zh-CN.md)。

## 目录结构

```text
audio-project-orchestrator/
  SKILL.md                      # Skill 入口（YAML + 硬性规则与读取策略）
  references/
    handbook.zh-CN.md           # 完整本地执行手册与模板
  README.md                     # 本说明
  LICENSE                       # MIT，Copyright (c) 2026 Audio Project Orchestrator contributors
  CHANGELOG.md                  # 版本记录
```

安装后，Agent 应先读 `SKILL.md`，再按需打开手册对应章节，而不是每次把全文塞进上下文。

## 安装

把**整个** `audio-project-orchestrator` 目录复制到你所使用的 Agent 的 skills 目录中，并保持该文件夹名称不变。不要只复制 `SKILL.md`，否则将找不到手册。

若你拿到的是 `audio-project-orchestrator-skill.zip`，先解压：

```bash
unzip audio-project-orchestrator-skill.zip
# 解压后应得到 audio-project-orchestrator/SKILL.md
```

然后按你的工具复制目录。以下为常见安装位置示例，**以各工具当前官方文档为准**，路径可能随版本变化：

```bash
# 通用：复制到当前 Agent 文档所指定的 skills 目录
cp -R audio-project-orchestrator /path/to/your-agent/skills/audio-project-orchestrator

# Claude Code 用户技能目录示例
cp -R audio-project-orchestrator ~/.claude/skills/audio-project-orchestrator

# 项目内技能目录示例（若工具支持仓库级 skills）
cp -R audio-project-orchestrator .claude/skills/audio-project-orchestrator
cp -R audio-project-orchestrator .cursor/skills/audio-project-orchestrator
cp -R audio-project-orchestrator .agents/skills/audio-project-orchestrator
```

复制后确认下列文件都在目标目录中：

- `SKILL.md`
- `references/handbook.zh-CN.md`
- `LICENSE`
- `README.md`
- `CHANGELOG.md`

部分环境需要重新打开应用或重新加载技能后才能识别。本 Skill 不要求、也不绑定任何专有内部工具。

## 触发示例

安装后，可用如下说法激活（中英文均可）：

- 「用音频项目总统筹帮我立项一个本机效果器插件」
- 「按本地执行手册推进这个 DSP 原型，先写一页纸和 RACI」
- 「这个插件项目卡在宿主加载，按总统筹规则处理卡点」
- 「准备本机验收和回滚安装」
- "Use the audio project orchestrator to kick off a local VST3/AU instrument."
- "Orchestrate this JUCE plugin to a verifiable local delivery, not a store release."

若 Agent 提供 `/` 或 `@` 技能列表，也可直接选择 `audio-project-orchestrator`。

## 使用方式

1. Sponsor 说明项目类型（效果器、乐器或音源、本机应用、工具链、预研原型）、目标机器与宿主、已有代码位置（如有）。
2. 总统筹先做能力检测，再写入项目目录：一页纸、精简计划、岗位映射、里程碑、风险、决策日志。
3. 事先商定质量底线与实测指标，而不是测试后再补合格线。
4. 按关键路径推进；不可逆事项升级人类；停工前更新事实源及其状态标记（已确认 / 待核验 / 冲突未决）。

项目目录建议结构见手册第 7.6 节。

## 许可证

本 Skill 文本与配套文件以 [MIT License](LICENSE) 发布。

Copyright (c) 2026 Audio Project Orchestrator contributors。

将本 Skill 用于某个具体软件项目时，该项目自身的源码许可证、以及所引入第三方依赖的许可证，仍须单独遵守。
