---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

使用智能体模式时，GitHub Copilot 会自主探索代码库、提出更改建议、编辑文件并运行命令。由于这些工作在本机实时进行，VS Code 中的 Copilot Chat 会持续显示每次工具调用和文件编辑。你可以直接在聊天中审查每项差异、接受或拒绝单个更改，并通过后续提示引导对话，无需离开编辑器即可完善或扩展工作。

本练习将介绍如何：

- 实时监控无障碍智能体的工作。
- 审查并接受建议的文件编辑。
- 在会话进行时引导智能体添加浅色模式开关，并保留高对比度模式开关。

## 场景

你在[练习 4][previous-lesson]中使用的无障碍自定义智能体正在实现高对比度模式。工作进行期间，设计团队提出了新需求：他们也希望提供浅色模式开关，供觉得默认主题太暗的用户使用。你无需从头开始新对话，可以引导现有会话扩展工作。

## 监控 Copilot 进度

Copilot Chat 视图会显示智能体的每个步骤，包括探索的文件、运行的命令和提出的编辑。每次文件编辑都会在聊天中以内联差异的形式显示，并提供 **Keep** / **Undo** 控件。

1. 返回练习 4 中使用的 Copilot Chat 视图。
2. 智能体工作时，滚动聊天内容查看每次工具调用。你会看到文件读取、文件编辑和请求运行的终端命令。
3. 智能体提出文件编辑时，聊天中会显示差异：
   - 选择 **Keep** 接受更改。
   - 选择 **Undo** 撤销更改，让智能体重新尝试。
4. 也可以打开聊天顶部的 **Files changed** 指示器，查看该会话中智能体修改的全部文件。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你信任的命令。

5. 等待智能体完成高对比度模式的实现。完成时会显示总结更改内容的消息。

## 引导智能体添加浅色模式

高对比度模式完成后，在同一个对话中继续添加浅色模式切换开关。由于仍在同一个聊天会话中，智能体会保留之前的上下文，包括修改的组件、使用的样式方案和设置的本地存储模式。

1. 在 Copilot Chat 输入框中发送以下后续提示：

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. 智能体会继续之前的工作，探索已完成的更改并提出浅色模式的实现。
3. 每次新编辑出现时都进行审查，就像处理高对比度模式一样。使用 **Keep** 或 **Undo** 处理每项差异。
4. 如果智能体的实现方向不符合预期，例如试图以你不喜欢的方式重构开关 UI，可以选择聊天输入框旁的 **Stop** 按钮停止任务，然后发送补充说明。

> [!TIP]
> 引导进行中的会话通常比从头开始更快。可以使用后续提示要求调整（“简化 CSS，改用 CSS 变量，不要重复选择器”）、纠正方向（“不要添加第三个开关，把浅色模式集成到现有设置面板”）或扩展范围（“为两个开关都添加键盘快捷键”）。

## 审查工作集

提交工作前，快速检查智能体修改的所有内容。

1. 在 VS Code 中打开 **Source Control** 视图。
2. 审查所有已更改文件。你应该能看到 Astro 组件、样式和相关测试的更新。
3. 打开几个已更改文件，查看差异。确认其中体现了自定义智能体要求的无障碍实践：ARIA 属性、键盘导航、语义化 HTML 和本地存储持久化。
4. 确认满意后，在 Source Control 面板中暂存并提交更改。下一课会发布这些更改。

## 总结和后续步骤

你使用 Copilot Chat 智能体模式监控并引导了一个进行中的会话：逐项审查文件编辑、接受或拒绝更改，并通过后续提示扩展工作，同时保留原有上下文。

本课中，你了解了以下内容：

- 实时监控智能体工作。
- 接受或拒绝单个文件编辑。
- 使用后续提示在会话进行时引导智能体。

在[下一课][next-lesson]中，你将把无障碍工作发布为拉取请求，并审查本地自定义智能体在本工作坊中生成的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
