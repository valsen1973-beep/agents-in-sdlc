---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或 Copilot 需要了解一些背景信息，应确保它能够获取这些上下文。[指令文件][instruction-files]可以提供此类指导，让 Copilot 不仅了解你想让它做什么，也了解应该如何完成。

本练习将介绍如何：

- 了解项目上下文、编码指南和文档标准如何通过存储库自定义指令及按路径应用的指令文件传递给 Copilot。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 练习路径不同，这里不会运行更改前后的提示进行对比。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。之后审查云智能体创建的拉取请求时，可以看到指令文件的影响。

## 指令文件

### 场景

Tailspin Toys 与其他优秀的开发团队一样，有一套开发实践规范和要求，包括：

- 数据层始终需要单元测试。
- UI 应使用深色模式并具有现代风格。
- 应通过 TSDoc 文档注释为代码添加说明。
- 每个文件开头都应有一段注释，说明文件的用途。

通过使用指令文件，可以确保 Copilot 获得正确的信息，并按照这些实践完成任务。

### 自定义指令

自定义指令可为 Copilot 提供上下文和偏好，帮助它了解你的编码风格和要求。它可以指导 Copilot 使用首选的编码约定和库，甚至规定注释的写法。你可以为整个存储库创建指令，也可以为特定类型的文件创建任务级上下文。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个指令文件。内容应包括与大多数请求相关的项目级信息，例如技术栈、项目概述、最佳实践和全局指南。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建的指令文件。例如，可以提供 TypeScript 或 Astro 等特定语言的指南，也可以提供创建 UI 组件或一组单元测试的指南。

> [!NOTE]
> 在 IDE 中使用时，指令文件只用于 Copilot Chat 的代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用存储库级指令文件和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

完整讨论如何创建指令文件超出本工作坊的范围。示例项目展示了一种有代表性的方法，主要原则如下：

- 在 `copilot-instructions.md` 中集中描述项目级指南，例如项目内容、项目结构和全局编码标准。
- 使用 `*.instructions.md` 文件提供针对特定文件类型（单元测试、Astro 组件、数据层）或特定任务的指令。
- 使用自然语言，确保指南清楚易懂。提供代码应如何编写以及不应如何编写的示例。

创建指令文件没有唯一的方法，使用 AI 也是如此。通过试验，可以找到最适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一组完善的指令文件。查看本项目中的文件时，会发现其中涵盖了多种任务，包括 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 还可以帮助你生成指令文件。不同产品界面的操作方式各有不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相应界面的课程会在相关处说明。
>
> 需要模板或起点？可以查看 [awesome-copilot][awesome-copilot]，其中包含大量指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

花些时间阅读存储库中提供的指令文件：一个核心 `copilot-instructions.md`，以及一组适用于各种任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub Web 界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 查看文件，留意项目的简要说明，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。**Code standards** 下还有 **GitHub Actions Workflows** 指南。这些信息适用于你与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并查看其中内容。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它设置了相对于存储库根目录的 glob，用于确定指令适用的文件。这里会匹配任何 TypeScript 测试文件，例如符合 `**/*.test.ts` 的文件。
5. 留意本项目专门用于创建单元测试的指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到文件底部。留意其中指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并让 Copilot 参考相关示例。（这里的路径是相对于指令文件，而不是存储库根目录。）

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码标准，但尚未要求添加代码文档。接下来会添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来要进行本练习唯一的一项编辑：添加一条项目级规则，要求在代码中使用 TSDoc 文档注释和文件级注释头。云智能体之后处理分配给它的议题时会读取此规则。

开始编辑前，先创建一个分支（云智能体会读取议题目标分支中的指令；同时，创建分支可以让你的更改以整洁的方式提交）：

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在补充存储库编码标准，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，约在第 27 行。留意其中记录的项目编码标准；目前没有关于代码文档的规则，这也是生成的辅助函数没有文档注释的原因。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可以在存储库级文件 (`.github/copilot-instructions.md`) 中设置全局指南，也可以使用 `*.instructions.md` 文件设置特定语言、文件类型或任务的指南。刚添加的文档注释规则属于项目级标准，因此存储库级文件是合适的位置。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支上的指令。下一练习中将议题分配给 Copilot 时，它会从 `main` 分支创建新分支。因此，必须先将指令更改合并到 `main`，云智能体才能使用它们。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求，并合并该 PR。下一练习中处理分配的议题时，云智能体便会读取这些指令。

> [!TIP]
> 如果希望在本工作坊中直接使用 `main`，也可以跳过分支步骤并直接提交到 `main`。此处保留分支步骤是为了模拟真实项目中的工作方式。

## 总结和后续步骤

你了解了 Copilot 如何从项目中的指令文件获取上下文，并在 `.github/copilot-instructions.md` 中添加了新的存储库级标准。后续练习中，可以在云智能体创建的拉取请求里看到此标准的应用效果。

接下来，将[第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更有效 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源合集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
