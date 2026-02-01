# 预设技能构建与导入指南

## 构建符合 SKILL 规范的开荒技能

为了让开荒流程在 Claude Code、OpenCode 等代理框架中正确运行，我们需要将每个开荒步骤封装成一个符合 `SKILL.md` 规范的技能文件。建议使用 Claude 官方提供的 Skill Creator 元技能来快速生成草稿，并根据反馈进行调整完善。

一个 `SKILL.md` 文件通常包括：

- 前置 YAML 区块（frontmatter），定义技能名称、描述、适用平台、触发短语等关键信息；
- 技能正文部分，详细说明技能目的、实现步骤和预期输出；
- 触发示例和边界条件，帮助模型在合适场景下调用该技能，并避免误触发。

建议先通过 Skill Creator 用自然言语描述技能，例如“为新电脑安装并配置 git”，生成初稿后再根据实际表现调整描述、完善前置条件，保证技能具体、庁算。

## 安装代理框架并导入技能

项目默认推荐用户先安装支持多模型的开源代理框架（如 OpenCode），后续也可以接入 Claude Code、Gemini CLI、Qwen Code 等其他引擎。安装方式通常是通过 `curl` 拉取安装脚本并执行，例如：

```
/bin/bash -c "$(curl -fsSL https://example.com/opencode-install.sh)"
```

（具体安装链接以各框架官方文档为准）

安装完成后，用户可以通过代理提供的命令行控制界面导入我们预设的技能包。例如在 OpenCode 中：

```
opencode skill install https://raw.githubusercontent.com/Leon-Algo/dev-env-bootstrap/main/skills/setup_dev_env/SKILL.md
```

导入技能后，当用户运行开荒命令时，代理会根据技能的触发词和平台信息选择合适的技能执行相应步骤。未来支持其他引擎时，可以在配置文件中指定首选引擎，或在导入时选择对应的命令行工具。
