# Design Native macOS Apps

一个面向 Codex 的原生 macOS 应用设计 Skill，用于设计、审查、迁移和实现 Mac 应用的用户界面与交互层。

它不把“Apple 风格”简化成毛玻璃、圆角卡片或固定视觉参数，而是从窗口与场景结构、菜单与命令、键盘和指针操作、SwiftUI/AppKit 映射、无障碍能力以及真实运行证据出发，帮助 Codex 做出可解释、可实现、可验证的 Mac 原生设计决策。

## 适用场景

- **设计**：规划窗口、侧边栏、工具栏、检查器、设置和多窗口状态归属。
- **审查**：区分已观察事实、源码推断、未知项和可选优化，避免把构建成功误判为视觉或无障碍验收通过。
- **迁移**：把 Figma、iOS 或 Web 方案按产品意图转换为 Mac 原生的信息结构、命令路径和交互模型。
- **实现**：将设计决策映射到 SwiftUI/AppKit，并要求与改动风险相称的构建、截图、交互和无障碍验证。
- **发布验收**：通过 Apple 参考原型、运行时截图矩阵和交互验证记录判断 Apple-native fit 是否真正成立。

## 不适用范围

这个 Skill 不处理纯 Swift 业务逻辑、存储、网络、构建系统、CI、签名与打包，也不为 iPhone/iPad 专属界面或 Web/Electron 样式提供原生 macOS 结论。

## 安装

Codex 会从 `~/.agents/skills` 加载个人 Skill。将仓库克隆到该目录：

```bash
mkdir -p "$HOME/.agents/skills"
git clone git@github.com:ChenZeBin/design-macos-apps.git "$HOME/.agents/skills/design-macos-apps"
```

Codex 通常会自动发现 Skill 变更；若未出现，重启 Codex。Skill 的结构、发现位置和调用方式可参考 OpenAI 官方的 [Build skills 文档](https://learn.chatgpt.com/docs/build-skills)。

显式调用：

```text
$design-macos-apps 审查这个 Mac 窗口是否符合原生交互习惯
```

也可以直接描述符合适用范围的任务，由 Codex 根据 `SKILL.md` 中的 `description` 自动选择。

## 仓库结构

- `SKILL.md`：任务路由、证据边界、完成门槛和各模式工作流。
- `references/`：macOS 设计、实现、无障碍、动效和审查方法。
- `assets/`：可复用的 macOS 设计规格模板。
- `scripts/`：确定性的规格结构校验工具。
- `evals/`：确定性与语义评测用例、评分器和回归测试。
- `agents/openai.yaml`：Codex 展示元数据和默认提示词。

## 验证

```bash
python3 scripts/validate_spec.py --template assets/macos-design-spec-template.md
python3 -m unittest discover -s evals/regressions -p 'test_*.py' -v
skill-up validate evals/eval.yaml
skill-up validate evals/eval-semantic.yaml
```

只有运行评测套件时才需要 `skill-up`。隔离评测环境的要求见 `evals/README.md`。

## 来源与分发边界

本仓库是独立编写的综合成果，不包含 Apple HIG 原文、第三方 Skill、研究快照、登录凭据或历史本地评测工作区。资料取舍和固定的上游版本记录在 `references/source-provenance.md`。

本仓库暂未授予开源许可证。超出 GitHub 访问权限所允许范围的再分发或修改，需要先取得版权所有者许可。
