---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行其他操作，例如运行测试。作为开发者，通常需要查找所有相关文件、进行更改、运行测试、调试、找出遗漏的文件、再次更新……需要完成的工作往往还有很多。

这正是 Copilot 智能体模式的用武之地。

Copilot 智能体模式可以在 IDE 中更自主地工作。它的行为类似开发者：先探索现有项目结构，再执行必要的更新，运行测试等任务，并自动修复发现的问题。现在来了解如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但它们针对两种不同的体验。智能体模式在 IDE 中执行任务，便于快速反馈和交互。云智能体则像团队成员一样异步工作，通过议题和拉取请求与你协作。

本练习将介绍如何：

- 让 Copilot 智能体模式探索项目、识别相关文件并协调更改。
- 使用 GitHub Copilot 智能体模式跨 UI 和数据层实现新功能。
- 在将代码合并到代码库之前审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断增长，你希望用户能够按类别和发行商筛选。上一练习已添加发行商辅助函数；现在将使用 Copilot 智能体模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

开始更改前，先查看 Tailspin Toys 网站，了解当前功能。

该网站是一个以开发者为主题的棋盘游戏众筹平台，用户可以浏览游戏列表并查看游戏详情。它是一个单体 Astro 应用，在构建时将页面呈现为静态 HTML。页面通过 Drizzle ORM 在 frontmatter 中直接查询本地 SQLite 数据库，没有单独的后端 API 或客户端 UI 框架。可复用的数据访问辅助函数放在 `src/lib/` 中；交互功能使用标准 DOM API 编写的小型、作用范围明确的 Astro `<script>`。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单体 Astro 开发服务器。可按以下步骤在 GitHub Codespace 中运行：

1. 返回 Codespace。上一练习结束后，你应位于 `main` 分支。
2. 在 Codespace 中按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）打开新终端。
3. 为筛选功能创建并切换到新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器准备就绪后，会显示类似以下的 URL 提示：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否要为 `http://localhost:4321` 打开浏览器窗口，请选择 **x** 将其关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），同时选择终端中的 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端中的 localhost URL 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是通往 Codespace 的私有隧道，此时 Web 服务器已在 Codespace 中运行！

### 浏览网站

网站启动后，可以查看其功能。主要功能包括：

- **主页**：显示棋盘游戏列表及其标题、图像和说明。
- **游戏详情页**：选择游戏后，会打开详情页，显示标题、说明、发行商和类别等详细信息。

## 使用 Copilot 探索待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板，并选择 **New Chat** 开始干净的新对话。不同练习所需的模式和模型可能不同；每个步骤会在相关处说明。

网站的初始实现已经可用，但我们希望添加新功能。先查看待办事项。根据模板设置项目时，系统已自动创建了一组议题；让 GitHub Copilot 显示这些议题。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。**Agent** 智能体会自主规划并跨文件实现更改、运行终端命令并调用工具。

   ![Chat 视图中智能体选择器的截图](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本工作坊作者并非推荐某个模型。编写本工作坊时使用了 Claude Sonnet 4.5，因此将它列入说明。希望这样能让代码建议相对一致，提供良好的体验。不过，LLM 具有概率性，因此你收到的建议可能与工作坊中的说明不同。这完全正常，也在预期之中。

> [!NOTE]
> 由于 LLM 具有概率性，Copilot 可能会使用不同的 MCP 命令，但仍应能完成任务。

3. 发送以下提示，让 Copilot 查看议题待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**，运行列出所有议题的命令。
5. 审查生成的议题列表。

留意 Copilot 还根据对用户的帮助程度为这些事项进行了优先级排序。

## 查看指令文件

让智能体生成代码前，先查看将用于提供上下文的指令文件。本练习会使用[用户界面 (UI) 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，其中介绍了如何为网站添加功能。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 留意其中关于添加功能的整体指南，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向各类文件专用指令的链接，包括：
     - Astro。
     - Tailwind CSS。
     - Drizzle。

> [!TIP]
> 指令文件可以引用其他指令文件和项目文件。路径相对于指令文件所在位置，因此可以复用内容、将复杂指令拆分成较小模块，并提供示例和模板。

## 实现筛选功能

要完成筛选功能，至少需要对应用进行三项更新：

- 在数据层 (`src/lib/`) 中添加或完善剩余的筛选逻辑。
- 为筛选行为添加或更新测试。
- 更新游戏列表页，添加筛选 UI。

此外，所有测试都必须通过后才能将更改合并到代码库。Copilot 智能体模式可以完成这些任务，现在来添加功能。

1. 可以继续使用当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选择了 **Agent**。

   ![Chat 视图中智能体选择器的截图](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，要求 Copilot 根据待办议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何先探索项目并查找与功能相关的文件。你会看到它查找数据层辅助函数、UI 和测试，然后开始修改文件并运行测试。

   ![Copilot 正在探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个任务，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂程度，整个过程可能需要几分钟。期间，代码编辑器中可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，所有更改都会显示这两个按钮；无需在工作进行时选择。

7. 按照 Copilot 的提示，选择 **Continue** 运行测试。

   ![Copilot Chat 面板中提示用户确认运行测试的对话框截图](../../../_images/ex3-agent-mode-run-tests.png)

8. 整个过程中可能会暂停，甚至出现测试失败。这没有关系！Copilot 会在生成代码和运行测试之间反复迭代，直到完成任务且未检测到错误。

   ![已完成的 Copilot 智能体模式聊天会话截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查找潜在问题。

> [!CAUTION]
> 请务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回网站所在的浏览器，体验新功能。
11. 确认一切正常并完成代码审查后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

恭喜！本练习中，你了解了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。你了解到：

- GitHub Copilot 智能体模式可以跨 UI 和数据层实现新功能。
- Copilot 智能体模式可以探索项目、识别相关文件并协调更改。
- 在将 Copilot 智能体模式生成的更改合并到代码库之前，应审查更改和测试。

接下来，[使用 Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 额外探索练习 - 实现分页

随着游戏列表不断增长，网站将需要分页功能。使用本练习中学到的技能，提示 Copilot 更新网站并实现分页。编写代码时可考虑：

- 遵循现有最佳实践，包括使用已有指令文件。
- 规划分页方式：允许用户选择每页大小，还是使用固定值。
- 编写提示时提供必要指南，确保 Copilot 按照预期实现功能。
- 可能需要通过多轮对话提出更改并补充上下文。这是使用 Copilot 的正常方式。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
