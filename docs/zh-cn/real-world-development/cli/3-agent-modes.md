---
title: "第 3 课 - 智能体模式：Plan 和 Autopilot"
description: "使用 Plan 确定方案、使用 Autopilot 根据议题构建筛选功能，再使用 Interactive 模式审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们先为项目添加了一项小功能，但更复杂的更改需要更完善的流程。GitHub Copilot CLI 支持组织现有的工作方式，帮助我们用合适的方法构建正确的功能。从本课开始，你将通过几节课遵循典型的智能体驱动开发流程：从议题着手构建新功能，确认代码有效、功能行为符合预期，最终成功将更改合并到项目中。

> [!NOTE]
> 继续完成该功能时，你会沿用同一个对话和分支。通常，不同文件类型的工作会使用不同分支或 PR；这里会采用简化方式，以便专注于核心概念。

本课将介绍如何：

- 从 GitHub 议题启动新的 Copilot 对话。
- 在 Plan 模式中定义需求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续完成该功能时，你将更新存储库指令、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体并打开功能 PR。

## 场景

Tailspin Toys 的目录不断扩大，访客需要按类别和发行商筛选游戏。待办事项中的议题描述了该功能，但组合多个类别等细节需要在编码前达成共识。你将使用 Plan 模式确定这些决策，然后授权 Autopilot 在明确范围内实现功能。

## 背景

将 AI 编码智能体引入开发流程不会改变基本原则。事实上，这些原则变得更加重要！大多数开发者遵循类似以下的流程：

1. 从已创建的议题开始，确认需要完成的工作。
2. 制定构建方案。
3. 编写并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求 (PR)。
7. 代码通过审查且持续集成流程成功后，合并代码。

> [!NOTE]
> 具体流程会因团队和组织而异，但大多数流程都与上述主题类似。

遵循这种标准方法，可以确保 AI 生成的代码满足既定要求，并经过与手写代码相同的审查流程。

## 对话模式

**对话模式**控制智能体拥有多少自主权。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协同工作。智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先创建计划，但不能编辑项目文件。
- **Autopilot**：智能体自主工作，包括编写代码、运行测试并不断迭代，直至任务完成。

先使用 Plan 模式审查计划，再使用 Autopilot 实现。

## 从议题开始

开始筛选功能工作前，返回 Codespace，确认存储库和终端已准备就绪。

1. 返回 Codespace。如果它已停止，请先重新启动。
2. 确认星级评分 PR 已合并。
3. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为筛选功能创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有议题。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd> 将议题添加到提示中，然后返回 **Session** 选项卡。

请注意，提示现在以 `#7`（或类似编号）开头。`#` 可将 GitHub 上的议题或拉取请求 (PR) 引入上下文。

## 规划筛选功能

规划让你在交由 Copilot 实施前，先确定功能或任务的实现方式。对于复杂工作，花些时间规划总是值得的。切换到 Plan 模式，并要求 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式。确认提示下方的模式指示器显示 **Plan**。
2. 在上一步添加的议题引用后输入以下提示：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 会开始制定计划：先探索项目，再确定最佳方案。

3. 过程中 Copilot 可能会询问筛选功能应如何工作。根据你的偏好作答，没有唯一正确答案。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动以审查计划。
6. 如果计划中的任何部分不符合你的决定，请要求 Copilot 修改。

## 批准 Autopilot

计划已编写并审查完毕，现在可以开始实施。使用 Autopilot 让 Copilot 按计划完成工作。

Autopilot 会让 Copilot 持续处理问题，直至它认为任务已经完成。

1. 选择 **Accept plan and build on autopilot (recommended)**，或已安装版本中名称相近的选项。
2. 确认提示下方的模式指示器显示 **Autopilot**。
3. 查看 Copilot 如何按照计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实施，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，应先解决设置问题，再认定检查已完成。

## 审查并验证实现

生成的代码与其他代码一样，需要在合并前审查。现在检查代码并运行网站，确认一切正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查筛选功能的实现和测试。
3. 对照议题和规划时作出的决定检查结果。
4. 审查完成后，按 <kbd>Esc</kbd> 退出差异视图。
5. 查看项目检查的输出，并要求 Copilot 修复任何失败项。

## 体验新功能

代码看起来没问题，但能否正常运行？像之前一样启动应用，通过 Codespaces 转发端口打开网站。

1. 使用以下提示让 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别筛选、按发行商筛选，以及计划中约定的组合方式。
4. 确认重置和无结果时的行为符合议题要求和你的决定。
5. 返回 Codespace，要求 Copilot 停止它启动的开发服务器。

## 总结和后续步骤

你已使用不同的对话模式构建并审查功能。本课中，你：

- 从 GitHub 议题启动了新的 Copilot 对话。
- 在 Plan 模式中定义了需求。
- 使用 Autopilot 模式实现了新功能。
- 审查了代码。
- 在转发的浏览器中手动验证了功能。

接下来，我们将深入了解代码的生成方式，确保代码遵循已记录的实践，并[使用自定义指令][next-lesson]。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
