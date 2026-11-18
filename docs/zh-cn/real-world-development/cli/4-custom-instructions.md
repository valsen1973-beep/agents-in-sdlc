---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "了解存储库指令，添加文档标准，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，应让 Copilot 能够获取相应指导。[指令文件][instruction-files]不仅描述想要编写什么代码，也说明代码应如何组织。现在已经实现筛选功能，接下来将了解 Copilot 使用的指令、添加一项文档标准，并将其应用于代码。

本课将介绍如何：

- 了解存储库指令和按路径应用的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码标准。
- 查看指令文件对代码的影响。

## 场景

Tailspin Toys 与其他优秀的开发团队一样，有一套开发实践规范和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明函数用途、参数和返回值（如果存在可注入的 `db` 参数，也应予以说明）。
- 可复用的 Astro 组件应记录其 `Props` 接口；相关代码更改时，注释也应保持更新。
- 应保留现有格式设置和 lint 指南。

通过使用指令文件，可以确保 Copilot 获得正确的信息，并按照上述实践完成任务。

## 指令文件

自定义指令可为 Copilot 提供上下文和偏好，帮助它了解你的编码风格和要求。它可以指导 Copilot 使用首选的编码约定和库，甚至规定注释的写法。你可以为整个存储库创建指令，也可以为特定类型的文件创建任务级上下文。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个指令文件。内容应与大多数请求相关。
- `.github/instructions/*.instructions.md`：为特定语言、文件类型或任务提供指南。

> [!NOTE]
> 不同环境支持的其他指令格式可能不同。依赖特定格式前，请参阅[自定义指令支持参考][custom-instructions-support]。

## 查看项目中的自定义指令文件

起始项目中已包含一组指令文件。先查看已有内容，再进行更改，以了解其影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看文件，留意其中简要介绍的项目和编码指南。这些指令适用于 Copilot 在此存储库中的每次交互。
4. 打开 `.github/instructions` 文件夹并查看其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它设置了一个 glob，用于确定指令适用的文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它指向其他指令文件和现有项目文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并让 Copilot 参考相关示例。

## 更新指令文件以符合团队指南

现有文件已经是很好的起点，但仍有不足。修改核心 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，该部分大约位于第 35 行。
2. 在该部分的最后添加以下条目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 使用更新后的指南

Copilot CLI 会在对话启动时加载存储库指令。保存更改后，退出并恢复筛选功能对话，让 Copilot 在保留功能上下文的同时加载新指南。

1. 如果筛选功能对话仍处于打开状态，请输入 `/exit` 关闭它。Copilot CLI 会自动保存对话。
2. 在 `game-filters-cli` 分支的存储库根目录中恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果出现提示，请选择筛选功能对话，并确认检出的是 `game-filters-cli` 分支。
3. 要求 Copilot 应用更新后的指南：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff` 并查看已更改的 TypeScript 文件。留意新生成的 TSDoc 注释，并确认其准确解释了代码。

## 总结和后续步骤

你已了解 Copilot CLI 如何获取上下文和指令文件中的内容，并将新的标准应用于功能代码。具体来说，你：

- 了解了存储库指令和按路径应用的指令文件如何传递给智能体。
- 更新了指令文件，确保遵循编码标准。
- 观察了指令文件对代码的影响。

接下来，你将[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot：指令文件及其他资源合集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
