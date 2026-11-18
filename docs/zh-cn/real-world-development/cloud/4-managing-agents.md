---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几节练习中，你让 Copilot 云智能体执行了三项任务，以改善用户体验并添加新功能。云智能体可以异步自主工作，但监控任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个控制中心，可以查看所有带有未关闭拉取请求 (PR) 的智能体任务，了解它们执行的操作，甚至在会话进行中引导智能体。

本课将介绍如何：

- 使用智能体页面监控云智能体任务。
- 在会话进行时引导智能体添加新功能。

## 场景

将实现高对比度模式的任务分配给智能体后，团队意识到也可以顺便添加浅色模式。既然正在更新网站样式并添加切换功能，将这项功能一并实现就很合理。现在需要引导智能体，让它在添加高对比度模式的同时也实现浅色模式。

## 查看 Copilot 云智能体任务

先查看分配给 Copilot 云智能体的所有任务的当前状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。应能看到分配给 Copilot 的任务，包括：
   - 更新代码文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建工作环境。
   - 设置 MCP 服务器。
   - 执行完成任务所需的其他步骤。

> [!NOTE]
> 列出的具体步骤会因 Copilot 工作进度和采用的方法而异。

4. 同时留意右侧出现的 PR 面板。可以通过它查看 PR 和已更改的文件，以便进一步监控。

## 引导云智能体

现在已经查看了正在执行的任务，接下来要求 Copilot 在实现高对比度模式时也添加浅色模式切换开关。

1. 选择标题中提到添加高对比度模式的会话。确切标题会因 Copilot 使用的名称和当前工作状态而异。

   ![控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 继续查看会话几分钟，直到会话显示已完成设置并开始工作。此时会出现类似下方的消息。
3. 在 **Steer active session while Copilot is working** 对话框中，输入以下提示：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![智能体页面中的云智能体任务截图，突出显示 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认收到提示并将其纳入工作流程。

## 等待 Copilot 完成工作

与之前一样，Copilot 会继续处理更新后的任务！发送消息时，它正在进行的步骤完成后，就会将新请求纳入工作流程。

这也需要几分钟。可以利用这段时间回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，它是监控和引导 GitHub Copilot 云智能体任务的中心位置。在此控制中心中，你可以跟踪所有活动和已完成的任务、审查工作，也可以重定向正在运行的任务以调整范围或补充指导。

本课中，你了解了以下内容：

- 使用控制中心和智能体页面监控云智能体任务。
- 在会话进行时重定向智能体并请求添加新功能。

Copilot 正在完成无障碍功能。接下来，你将[迭代改进 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
