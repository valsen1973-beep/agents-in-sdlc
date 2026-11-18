---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本工作坊中，你与 GitHub Copilot 协作完成了多项任务，以改善用户体验并添加新功能。你让 Copilot 为代码添加文档、为设计团队构建相关游戏功能以便他们迭代，还实现了高对比度和浅色模式切换等无障碍功能。现在来检查代码更改；如有需要，也可以向 Copilot 提供反馈，进一步改进结果。

### 场景

前面多次提到，引入生成式 AI 并不会改变软件设计和 DevOps 的基本原则。我们始终需要审查生成的代码，并遵循常规 DevOps 流程。因此，在让团队其他成员参与审查前，先检查 GitHub Copilot 为代码文档、相关游戏功能和无障碍功能生成的建议。

## GitHub Copilot 云智能体安全性

Copilot 云智能体会在后台无人监督地执行任务，因此设置了一些安全限制，确保操作安全：

- Copilot 对存储库只有读取权限；写入权限**仅限于**用于提交代码的分支。
- 云智能体在 GitHub Actions 中运行，并在独立、临时的环境中工作。
- GitHub Actions 工作流必须经过人工批准后才能运行。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，MCP 服务器也包括在内。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)，其中包含代码文档。通过 GitHub.com 上的标准 PR 界面完成审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器。你可以[自定义或禁用 Copilot 云智能体的防火墙][agent-firewall]。

1. 在浏览器中打开自己的 GitHub 存储库。
2. 选择 **Pull Requests**，打开拉取请求列表。
3. 打开标题类似 **Add missing documentation** 的拉取请求。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。此时请等待 Copilot 完成工作。这可能需要几分钟，可以趁此休息一下或回顾已学内容。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

   ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新增的 TSDoc 文档注释和其他文档。具体更改可能有所不同。

   检查更改时，留意 TSDoc 文档注释、TypeScript 约定和文件注释头。这些内容来自你在练习 2 开始时查看的自定义指令文件。

6. 审查完成且确认没有问题后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应会进入 PR 检查队列。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 修改

你不必只接受 Copilot 创建的 PR，也可以像给团队成员留言一样，在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论，并启动新会话来处理请求。由于结果并非确定，因此没有固定的提示文本。你可以让 Copilot：

- 为每个代码文件添加简短说明用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用的结构。

1. 添加评论并提及 **@copilot**，要求它修改生成的文档。可以使用上述建议，也可以提出其他文档改进请求。
2. 选择 **View Session**，观察 Copilot 执行修改。留意 Copilot 如何启动新会话来完成更新。
3. 选择 **Back to pull request** 返回 PR。

   ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中应会出现新的提交。
5. 选择 **Files changed** 选项卡，审查更改。

你可以继续迭代，直到满意为止。完成后，可将 PR 从草稿状态转为准备审查状态，然后合并到 main 分支。

![将 PR 转为准备审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

现在查看 Copilot 为解决“在游戏详情页显示相关游戏”议题而创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查完成且确认没有问题后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流提示。
7. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 工作流应会进入 PR 检查队列。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
9. **可选：**也可以在 Codespace 中切换到该分支，手动测试相关游戏功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**）：

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot 已构建相关游戏功能！与之前一样，你可以通过迭代让 Copilot 修改结果。例如，可以要求 Copilot 调整显示的相关游戏数量，或添加文件注释头和 TSDoc 文档注释（请记住，分配此任务时尚未更新自定义指令）。与之前一样，可以在 **Conversation** 选项卡中添加评论，Copilot 会看到评论并启动新会话。

## 审查无障碍功能

最后，检查使用无障碍自定义智能体实现的功能。这个 PR 应包含你在练习 3 中分配的高对比度模式，以及在练习 4 的控制中心中提出的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。此时请等待 Copilot 完成工作，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查实现，重点检查：
   - 用于切换模式的 UI 组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性，如 ARIA 标签和键盘导航。
   - 用于管理模式切换的 JavaScript/TypeScript 代码。

6. 审查完成且确认没有问题后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应会进入 PR 检查队列。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
10. **可选：**可以在 Codespace 中切换到该分支，手动测试无障碍功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称）：

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   然后启动应用，在浏览器中测试高对比度和浅色模式开关，并确认页面重新加载后设置仍然有效。

留意无障碍自定义智能体如何帮助 Copilot 按照无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可以像处理之前的 PR 一样，在评论中提及 **@copilot** 并要求更新。

## 可选练习 — 继续委派任务

云智能体适合处理待办事项，让你能腾出精力处理其他工作。可以在自己的存储库中创建更多议题并分配给 Copilot，以养成使用习惯。以下是一些想法：

- 在游戏详情页创建支持者兴趣表单。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体练习路径。通过这些课程，你：

- **查看了存储库提供的自定义指令文件**，以便之后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，并观察它如何设置环境、规划任务和异步执行。
- **创建并使用了无障碍自定义智能体**，添加高对比度和浅色模式切换功能。
- **使用 Copilot 智能体页面作为控制中心**，监控并引导无障碍会话。
- **审查并迭代改进云智能体创建的拉取请求**，通过提及 `@copilot` 请求更改并批准工作流。

## 回顾和后续步骤

云智能体练习路径已完成。若想继续探索，其他练习路径可以补充此处学到的内容：

- 🖥️ **[VS Code 练习路径](../../vscode/)** — 直接在 IDE 中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 练习路径](../../cli/)** — 在终端中交付两个经过审查的更改，体验 Plan 和 Autopilot 模式、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

在自己的存储库中，可以尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
