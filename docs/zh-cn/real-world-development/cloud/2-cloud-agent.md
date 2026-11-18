---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

许多组织都面临技术债务问题，例如未解决的安全问题、需要更新的旧代码，或因时间不足而长期搁置的功能请求。GitHub Copilot 云智能体可以自主执行更新代码和添加功能等任务。任务完成后，智能体会创建草稿 PR，供开发者审查。这样可以将繁琐任务交给智能体，加快开发流程，让开发者专注于更宏观的工作。

本课将使用 Copilot 云智能体探索以下内容：

- 自定义代码生成环境。
- 确保安全执行操作。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初受聘创建网站的承包商没有留下完善的文档，事实上，代码完全缺少文档。团队希望首先为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队准备改善游戏发现体验。他们希望在每款游戏的详情页显示同类别的其他游戏，方便用户继续浏览。团队目前不要求完善的实现，只需要能用于用户体验验收测试的版本。这项任务目前阻碍了其他工作，但优先级低于其他议题。

这些都是容易被延后的任务，也很适合交给 Copilot 云智能体。云智能体可以异步处理任务，让开发者专注于其他工作，之后再回来审查 Copilot 的结果并确认是否符合预期。

## 认识 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发者一样在后台执行任务。可以通过多种方式与它协作，包括[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配任务后，Copilot 会创建草稿拉取请求来跟踪进度，设置工作环境并开始处理任务。你可以在 Copilot 会话进行时或完成后查看它的工作。解决方案准备好接受审查时，Copilot 会在拉取请求中提及你。

## 明确界定指令范围的重要性

GitHub Copilot 并没有魔法，使用它并不意味着可以跳过思考。即使看似简单的操作，深入分析后也会发现复杂性，因此要[谨慎确定 Copilot 云智能体任务范围][cloud-agent-best-practices]。将它视作 AI 结对程序员：分阶段工作、学习、试验，并根据结果调整。引入生成式 AI 并不会改变软件开发的基本原则。

## 本存储库中的自定义指令

前面的练习介绍了自定义指令及其如何引导 Copilot。如果已经完成自定义指令练习，就会看到 `.github/copilot-instructions.md` 的实际效果；否则，现在可以快速查看。将任务分配给 Copilot 云智能体前，先只读查看存储库中的指令文件，稍后便能观察它们的影响。

在 GitHub Web 界面或已启动的 Codespace 中打开以下文件：

- `.github/copilot-instructions.md`：查看 **Code standards** 部分，尤其是 TypeScript 约定和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：留意 `applyTo` frontmatter，它将指令限定为 `**/*.test.ts` 文件。

下一部分将 `Code lacks documentation` 议题分配给云智能体时，留意生成的拉取请求中是否包含 TSDoc 文档注释、TypeScript 约定和文件注释头。这些内容来自上述指令文件。后续练习审查 PR 时还会再次检查。

## 为 Copilot 云智能体设置开发环境

无论由谁编写代码，通常都需要特定环境和一些设置脚本，以确保环境准备就绪。将任务分配给 Copilot 时也一样，因为它会以类似软件工程师的方式执行任务。

云智能体使用 [GitHub Actions][github-actions] 环境开展工作。你可以在 `.github/workflows/copilot-setup-steps.yml` 文件中创建[专用设置工作流][setup-workflow]，在云智能体开始工作前运行，以便安装所需的开发工具和依赖项。为确保练习顺利并提供相关学习机会，项目已经预先配置了该工作流。它会为 Copilot 安装 Node.js、项目依赖项、端到端测试所需的浏览器，以及用于这个单体 Astro 应用的迁移并填充数据的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

此文件与其他 GitHub 工作流类似，但有几个关键点：

- 它包含一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，GitHub Actions 会运行此作业。
- 留意 `workflow_dispatch` 触发器。它允许你从存储库的 **Actions** 选项卡手动运行工作流，这样可以在等待 Copilot 运行前先验证工作流是否成功。

## 添加文档

大家都知道文档的重要性，但大多数项目的信息要么已过时，要么完全缺失。这类技术债务往往长期得不到处理，降低工作效率，也让维护代码库或引入新开发者变得更加困难。Copilot 擅长创建文档，因此非常适合处理这类议题。它会在后台生成所需的文档。后续练习将审查它的工作。

1. 在新的浏览器选项卡中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建新议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开新生成的拉取请求 (PR)，标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中尚未出现新 PR，请等待一两分钟并刷新浏览器。
12. 几分钟后，Copilot 应会创建待办事项列表。

> [!NOTE]
> Copilot 生成待办事项列表可能需要几分钟。Copilot 正在创建环境（运行前面介绍的工作流）、分析项目并确定解决问题的最佳方法。

13. 查看列表和即将执行的任务。
14. 向下滚动 PR 时间线，查看 Copilot 已开始处理议题的消息。
15. 选择 **View session** 按钮。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新页面才能看到更新后的状态指示器。

16. 查看实时会话，了解 Copilot 如何解决问题，包括探索代码、了解当前状态、暂停思考并确定合适方案，以及编写代码。

整个过程可能需要几分钟。Copilot 云智能体的主要优势之一是可以异步执行任务，让我们专注于其他工作。现在就利用这一点：再分配一项任务给 Copilot 云智能体，然后转而为应用添加功能。

## 在游戏详情页添加相关游戏

如前所述，GitHub Copilot 云智能体的优势之一是可以拆分工作：你专注于一组任务，它则处理另一组。为设计团队添加相关游戏部分也许不会花费太多时间，但这段时间仍可用于其他任务。现在将任务分配给 Copilot 云智能体。

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 将 **Description** 设置为：

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

不久后，议题的第一条评论中会出现 👀，表示 Copilot 已开始处理。

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在处理第二项请求！Copilot 云智能体的工作方式类似软件工程师，因此无需一直监控；等它完成后再审查即可。现在可以转而创建和使用自定义智能体。

## 总结和后续步骤

本课介绍了 [GitHub Copilot 云智能体][copilot-agents]。可以将议题分配给云智能体，让它异步处理任务。Copilot 可以用于处理技术债务、创建新功能，或协助将代码从一种框架迁移到另一种框架。

本课中，你了解了以下内容：

- 自定义代码生成环境。
- 确保安全执行操作。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

Copilot 云智能体正在后台处理任务。接下来可以创建并使用自定义智能体。[Copilot 云智能体还可以使用 MCP 服务器][cloud-agent-mcp]，并且可以获取前面模块介绍过的自定义指令。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
