# Advanced Multi-Agent AI Framework 用户指南

本指南旨在全面介绍如何使用 Advanced Multi-Agent AI Framework (高级多智能体 AI 框架) 进行各种开发和调试任务。它将概述框架的核心机制，并结合具体示例，指导您如何高效地利用这个框架。

## 1. 简介

Advanced Multi-Agent AI Framework 专为 AI 开发中的专业团队协作而设计。通过其结构化的方法和专业化的智能体（Agent），该框架能够系统地处理复杂的任务，从项目规划、代码实现到问题调试和知识管理。

本指南将向您展示如何有效地协调和使用这个框架，以实现卓越的开发成果。

## 2. 框架核心机制详解

理解这些关键组件和流程对于有效使用框架至关重要。

### 2.1. 智能体 (Agent) 专业化

框架由一组专业化的智能体组成，每个智能体都针对特定任务进行了优化：

*   **🪃 Orchestrator (编排者)**: 项目经理。负责整个工作流程的协调。它分解问题，将任务分配给合适的智能体，通过 Boomerang 模式管理信息流，并整合结果。这是所有复杂任务的起点。
*   **🏛️ Architect (架构师)**: 系统架构师。负责系统设计、架构文档和战略性规划。擅长 `visual-documentation-generation` (可视化文档生成) 和 `tree-of-thoughts` (思维树) 等技术。
*   **🗓️ Planner (规划师)**: 产品规划师。负责定义产品特性、管理产品待办事项列表 (Backlog) 和编写用户故事。使用 `user-story-prompting` (用户故事提示) 和 `stakeholder-perspective-analysis` (利益相关者视角分析)。
*   **🧱 Builder (构建者)**: 软件开发人员。负责实现功能、编写和测试代码。专注于 `code-generation-agents` (代码生成代理) 和 `test-based-iterative-flow` (基于测试的迭代流程)。
*   **💻 Code (代码专家)**: 高级编码专家。负责复杂功能实现、代码优化和算法挑战。使用 `modular-code-generation` (模块化代码生成) 和 `program-of-thoughts` (程序思维链)。
*   **🛡️ Guardian (守护者)**: 基础设施与 CI/CD 专家。负责管理基础设施、CI/CD 管道和自动化开发工作流。应用 `automated-development-workflows` (自动化开发工作流) 和 `flow-engineering` (流工程)。
*   **❓ Ask (询问者)**: 信息发现专家。负责查找信息、进行研究。利用 `rag` (检索增强生成) 和 `iterative-retrieval-augmentation` (迭代检索增强)。
*   **🪲 Debug (调试者)**: 技术诊断专家。负责查找和解决错误。擅长 `five-whys-prompting` (五问法) 和 `chain-of-verification` (验证链)。
*   **📁 Memory (记忆者)**: 知识管理专家。负责组织文档和构建知识库。使用 `knowledge-graph-construction` (知识图谱构建) 和 `semantic-clustering` (语义聚类)。
*   **🔍 Deep Research (深度研究者)**: 深度分析专家。负责综合分析和竞争情报。应用 `multi-perspective-analysis` (多视角分析) 和 `systematic-literature-review` (系统性文献回顾)。
*   **🔎 Deep Scope (深度范围界定者)**: 问题范围界定专家。负责分析 GitHub issue 并评估代码库影响。使用 `issue-decomposition-analysis` (问题分解分析) 和 `codebase-impact-mapping` (代码库影响映射)。

### 2.2. SPARC + Boomerang 工作流

*   **SPARC 框架**: 一个结构化的开发生命周期，包括 Specification (规范)、Pseudocode (伪代码)、Architecture (架构)、Refinement (精炼)、Completion (完成)。框架中的所有活动都遵循这个宏观流程。
*   **Boomerang 任务委派**:
    1.  **任务创建与分配**: `Orchestrator` 根据项目需求创建结构化任务，并将其分配给合适的智能体（如 `Deep Scope` 或 `Debug`）。
    2.  **执行**: 被分配的智能体执行其专业化的分析或任务。
    3.  **返回与集成**: 智能体 **必须** 以结构化格式（即 "boomerang"）将其发现或结果返回给 `Orchestrator`。`Orchestrator` 随后验证结果并规划后续步骤。
    4.  **关键原则**: 所有任务都必须通过 Boomerang 模式返回给 Orchestrator，确保集中控制和信息整合。智能体之间不进行直接的、未协调的通信。

### 2.3. "Scalpel, not Hammer" (精准而非蛮力) 哲学

这是框架操作的核心原则，旨在优化资源（特别是 Token）的使用：

*   **从简单任务开始**: 优先处理消耗较少 Token 的任务，然后逐步过渡到更复杂的任务。
*   **控制上下文窗口**: 将上下文窗口的使用率始终保持在 40% 以下。
*   **选择最专业的智能体**: 为每个子任务选择最合适的专业智能体。
*   **精确打包上下文**: 为每个操作精确地打包所需的上下文信息。
*   **原子化任务**: 将复杂任务分解成边界清晰的原子组件。

## 3. 框架配置与自定义

框架的灵活性和强大功能来源于其可配置性。

### 3.1. 自定义模式 (`custom_modes.yaml`)

*   **位置**: `templates/custom_modes.yaml`
*   **作用**: 定义所有自定义智能体模式。
*   **结构**: 每个模式定义包括：
    *   `slug`: 模式的唯一标识符。
    *   `name`: 模式的显示名称。
    *   `roleDefinition`: 模式的角色定义，描述其身份和专业领域。
    *   `whenToUse`: 描述何时使用此模式。
    *   `groups`: 定义该模式可以访问的工具组 (如 read, edit, browser, command, mcp)。
    *   `customInstructions`: 该模式的**核心**。这里包含了该智能体的所有自定义指令，详细说明了其应遵循的流程、使用的提示工程技术、核心职责和报告协议。

### 3.2. 统一系统指令 (`custom-instructions-for-all-modes.md`)

*   **位置**: `templates/custom-instructions-for-all-modes.md`
*   **作用**: 为框架中的**所有**模式提供通用的、系统级的指令。
*   **内容**: 包括全局操作原则（如 Token 优化协议）、多智能体模式架构、跨模式通信协议 (Boomerang 逻辑)、可追溯性文档、伦理层、标准化子任务创建协议、搜索和引用协议、文件结构标准、模式交互和升级策略等。

### 3.3. 增强提示模板 (`enhance-prompt-template.md`)

*   **位置**: `templates/enhance-prompt-template.md`
*   **作用**: 定义了 `Orchestrator` 模式使用的 "增强提示 (✨)" 功能的模板。它指导 `Orchestrator` 如何智能地分析用户输入，并将其转换为结构化的任务地图 (Markdown Task Map)。

## 4. 80+ 高级提示工程技术详解

框架为每个智能体集成了多种高级提示工程技术，以提升其在特定领域的表现。以下是一些关键技术的列表和简要说明：

*   **`workflow-template-prompting` (工作流模板提示)**: 用于标准化流程执行和任务结构化。常用于 `Orchestrator`。
*   **`boomerang-task-delegation` (回旋镖任务委派)**: 用于结构化的任务分配和返回验证。核心机制之一。
*   **`visual-documentation-generation` (可视化文档生成)**: 用于创建清晰的架构图和系统文档。常用于 `Architect`。
*   **`tree-of-thoughts` (思维树)**: 用于复杂设计决策分析和选项评估。常用于 `Architect` 和 `Deep Research`。
*   **`user-story-prompting` (用户故事提示)**: 用于清晰、可操作的特性定义。常用于 `Planner`。
*   **`code-generation-agents` (代码生成代理)**: 用于结构化、系统化的代码实现。常用于 `Builder` 和 `Code`。
*   **`test-based-iterative-flow` (基于测试的迭代流程)**: 用于质量驱动的开发和全面测试。常用于 `Builder` 和 `Code`。
*   **`rag` (Retrieval-Augmented Generation, 检索增强生成)**: 用于从多个来源综合信息。常用于 `Ask` 和 `Deep Research`。
*   **`five-whys-prompting` (五问法)**: 用于系统性地识别根本原因。常用于 `Debug`。
*   **`chain-of-verification` (验证链)**: 用于多步解决方案验证。常用于 `Debug`。
*   **`knowledge-graph-construction` (知识图谱构建)**: 用于创建互联的信息网络。常用于 `Memory`。
*   **`multi-perspective-analysis` (多视角分析)**: 用于全面的视点评估。常用于 `Deep Research`。
*   **`issue-decomposition-analysis` (问题分解分析)**: 用于系统性的问题拆解。常用于 `Deep Scope`。
*   **`codebase-impact-mapping` (代码库影响映射)**: 用于全面的范围评估。常用于 `Deep Scope`。
*   **`automated-development-workflows` (自动化开发工作流)**: 用于 CI/CD 优化。常用于 `Guardian`。
*   **`flow-engineering` (流工程)**: 用于高效的管道设计。常用于 `Guardian`。
*   ... (还有更多技术应用于不同智能体)

## 5. 通用任务执行步骤

遵循这个结构化的方法来执行复杂任务：

1.  **启动 Orchestrator**:
    *   在您的环境（例如 Kilo Code）中切换到 `Orchestrator` 模式。
    *   **清晰地阐述您的目标**: 详细描述您想要完成的任务。

2.  **生成任务地图 (Task Map)**:
    *   请求 `Orchestrator` 为您要执行的任务创建一个 **Markdown 任务地图**。
    *   该地图应使用复选框来划分阶段（如 "问题分析", "范围定义", "执行", "验证"），并将任务明确分配给 `Deep Scope`、`Debug`、`Builder` 等智能体。

3.  **执行任务地图中的任务**:
    *   `Orchestrator` 会根据任务地图，通过 Boomerang 模式将任务逐一委派给相应的智能体。
    *   **切换到被分配的智能体模式** (如 `Deep Scope`, `Debug`, `Ask` 等)。
    *   向该智能体提供任务描述和所需的上下文信息。
    *   智能体执行任务后，会通过 Boomerang 将结果返回给 `Orchestrator`。
    *   `Orchestrator` 验证结果并分配下一个任务。

4.  **审查和整合发现**:
    *   `Orchestrator` 会整合所有报告，并向您呈现最终结果。

## 6. 详细示例：调试 `Cli.py` 的错误输出

让我们通过一个具体示例来演示调试流程：运行 `Cli.py` 脚本得到了错误的结果，但脚本执行过程中没有报错，并且有详细的日志。

### 6.1. 向 Orchestrator 描述初始问题

切换到 `Orchestrator` 模式并提出问题：

> "我遇到了一个复杂的问题。当我运行脚本 `Cli.py` 时，它最终产生的输出根据我们的规范是不正确的。关键在于，脚本执行过程中没有抛出任何错误或异常。我有详细的日志文件，记录了应用程序在每个主要执行步骤的状态和输出。我的目标是找出这个错误输出的根本原因并实施修复。请生成一个调试任务地图来系统性地解决这个问题。"

### 6.2. Orchestrator 生成任务地图

`Orchestrator` 会响应一个类似如下的计划：

```markdown
# Project: Debug Cli.py Incorrect Output

## Phase 1: Problem Analysis & Scoping
- [ ] **Task 1.1**: Analyze the problem description and initial logs to define the scope of investigation.
  - **Agent**: Deep Scope
  - **Dependencies**: None
  - **Outputs**: [`cli_debug_scope.md` - Scope document detailing suspected components and initial hypotheses]
  - **Validation**: Scope document reviewed for completeness and logical breakdown of the problem.
  - **Human Checkpoint**: NO
  - **Scope**: Review the user's problem statement, understand the role of `Cli.py`, and perform an initial analysis of the codebase and log structure to hypothesize where the issue might originate. The output is a structured scope document.

## Phase 2: Root Cause Diagnosis
- [ ] **Task 2.1**: Perform in-depth investigation based on the scope document and detailed log analysis to identify the root cause of the incorrect output.
  - **Agent**: Debug
  - **Dependencies**: 1.1
  - **Outputs**: [`cli_debug_diagnosis.md` - Diagnostic report with identified root cause, code location, and fix recommendations]
  - **Validation**: Diagnostic report must clearly link the identified code/logic flaw to the observed incorrect output, validated against the provided logs.
  - **Human Checkpoint**: YES
  - **Scope**: Utilize the scope document from Task 1.1. Deep dive into the `Cli.py` script and correlated log entries. Apply advanced debugging techniques to prove the root cause. Document findings comprehensively.

## Phase 3: Fix Implementation & Verification (Optional/Next Steps)
- [ ] **Task 3.1**: (Example) Implement the fix identified in Task 2.1.
  - **Agent**: Builder
  - **Dependencies**: 2.1
  - **Outputs**: [Modified `Cli.py`]
  - **Validation**: Code changes align with the diagnostic report and follow project standards.
  - **Human Checkpoint**: NO
  - **Scope**: Apply the specific code change recommended by the `Debug` agent.

- [ ] **Task 3.2**: (Example) Verify the fix resolves the issue and does not introduce regressions.
  - **Agent**: Debug
  - **Dependencies**: 3.1
  - **Outputs**: [Verification report confirming correct output and no new issues]
  - **Validation**: Re-run the scenario and confirm the output is now correct. Perform checks for side effects.
  - **Human Checkpoint**: NO
  - **Scope**: Re-execute the `Cli.py` script under the same conditions as the original bug report. Analyze new logs to confirm the fix.
```

### 6.3. 执行："范围定义" 任务 (通过 Deep Scope 智能体)

1.  **Orchestrator 行动**: 将 Task 1.1 分配给 `Deep Scope` 智能体。
2.  **您的操作**: 切换到 `Deep Scope` 模式。
3.  **向 Deep Scope 提供上下文**:
    *   粘贴任务地图中的任务描述。
    *   提供 `Cli.py` 脚本用途的摘要。
    *   分享显示开始、关键中间步骤和最终（错误）输出的相关日志摘录。
4.  **Deep Scope 智能体流程**:
    *   使用 `issue-decomposition-analysis` (问题分解分析) 来拆解问题："为什么输出是错的？" -> "哪个计算或数据转换步骤出错了？"
    *   使用 `codebase-impact-mapping` (代码库影响映射) 来识别 `Cli.py` 及其依赖项中所有可能影响最终输出的函数、模块和数据流。
    *   将日志条目与代码部分关联起来，形成初步假设（例如，"在函数 Y 执行后，数据 X 不正确"）。
5.  **Deep Scope 输出 (Boomerang)**: 智能体生成 `cli_debug_scope.md`，其内容可能如下所示：
    ```markdown
    # Scope Document: Debugging Cli.py Incorrect Output

    ## 1. Objective
    Define the scope and initial hypotheses for the incorrect output produced by Cli.py.

    ## 2. Context & Background
    User report: Cli.py runs without error but produces incorrect final output. Detailed logs are available.

    ## 3. Scope
    ### In Scope:
    - Analysis of `Cli.py` script logic.
    - Review of log files for data state tracking.
    - Investigation of data processing functions: `process_data()`, `calculate_result()`.
    ### Out of Scope:
    - External API calls (logs indicate these are successful).
    - Syntax or runtime errors (none reported).

    ## 4. Initial Hypotheses & Areas for Investigation
    1.  **Hypothesis**: Incorrect data filtering in `process_data()` function.
        **Evidence from logs**: Data set Z passed to `calculate_result()` is smaller than expected.
    2.  **Hypothesis**: Flawed logic in the `calculate_result()` function.
        **Evidence from logs**: Intermediate values within `calculate_result()` seem inconsistent with expected algorithm.
    3.  **Hypothesis**: Misinterpretation of a configuration flag read at the beginning.
        **Evidence from logs**: A specific config value is logged; its impact needs verification.

    ## 5. Recommended Next Steps
    - Debug Agent should prioritize investigation of Hypotheses 1 and 2, focusing on the `process_data()` and `calculate_result()` functions, using the detailed logs to trace data flow and state.
    ```

### 6.4. 执行："根本原因诊断" 任务 (通过 Debug 智能体)

1.  **Orchestrator 行动**: 接收 `cli_debug_scope.md`。创建一个详细的诊断任务 Task 2.1 分配给 `Debug` 智能体，并将范围界定文档作为上下文。
2.  **您的操作**: 切换到 `Debug` 模式。
3.  **向 Debug 提供上下文**:
    *   粘贴任务地图中的任务描述。
    *   提供 `cli_debug_scope.md` 的全部内容。
    *   **至关重要**: 授予智能体访问 **完整日志文件** 和 `Cli.py` 脚本本身的权限。
4.  **Debug 智能体流程**:
    *   **问题范围界定**: 查看范围界定文档以了解关注领域。
    *   **证据收集**: 深入分析日志，将时间戳和数据状态与 `Cli.py` 中的代码（特别是 `process_data()` 和 `calculate_result()`）进行关联。
    *   **假设形成与测试 (五问法 + 验证链)**:
        *   **聚焦假设 1 (process_data)**:
            *   Q: 为什么数据集 Z 更小？A: 因为某些项目的过滤条件不满足。
            *   Q: 为什么过滤条件不满足？A: 条件检查 `item.status == 'active'`。
            *   Q: 为什么这些项目的 `item.status` 不是 'active'？A: 日志显示 `item.status` 是 'active_pending'。
            *   Q: 为什么代码只检查 'active'？A: 查看 `process_data()` 中的代码逻辑。**发现了 bug！** 过滤条件 `if item.status == 'active'` 太严格了。它也应该包括 'active_pending'。
            *   Q: 为什么会遗漏？(bug 产生的根本原因，也许是为了未来预防)。
        *   **验证链**:
            *   验证显示 'active_pending' 状态的日志条目。
            *   确认代码中的确切过滤条件。
            *   使用样本数据模拟过滤逻辑，证明它排除了 'active_pending' 项目。
            *   追踪这种排除如何导致较小的数据集 Z。
            *   追踪较小的数据集 Z 如何导致最终的错误输出。
    *   智能体现在形成了一个强大且经过验证的假设。
5.  **Debug 输出 (Boomerang)**: 智能体生成 `cli_debug_diagnosis.md`：
    ```markdown
    # Diagnostic Report: Cli.py Incorrect Output

    ## 1. Objective
    Identify the root cause of the incorrect output from Cli.py.

    ## 2. Context & Background
    Based on the scope document `cli_debug_scope.md` and analysis of `Cli.py` source code and execution logs.

    ## 3. Diagnosis
    ### Root Cause
    The root cause is an **incorrect filtering condition** in the `process_data()` function within `Cli.py`.

    **Location**: `Cli.py`, line 45 (approx.)
    **Code**:
    ```python
    # Incorrect code
    filtered_data = [item for item in raw_data if item.status == 'active']
    ```
    **Problem**: This condition only includes items with `status` exactly equal to `'active'`. However, logs show that some relevant items have a `status` of `'active_pending'`, which should also be considered active for this process.

    ### Link to Symptom
    1.  The overly strict filter excludes `'active_pending'` items from `filtered_data`.
    2.  This results in a smaller dataset being passed to the `calculate_result()` function.
    3.  `calculate_result()` processes this incomplete dataset.
    4.  The final calculation, based on incomplete data, produces the observed incorrect output.

    ## 4. Solution
    Modify the filtering condition in `process_data()` to include both `'active'` and `'active_pending'` statuses.

    **Recommended Fix**:
    ```python
    # Corrected code
    filtered_data = [item for item in raw_data if item.status in ['active', 'active_pending']]
    ```

    ## 5. Verification Plan
    1.  Apply the code fix.
    2.  Re-run `Cli.py` with the same input that produced the error.
    3.  Observe the logs to ensure `'active_pending'` items are now included in `filtered_data`.
    4.  Confirm the final output matches the expected, correct result.
    ```

### 6.5. 示例结论

`Orchestrator` 接收到诊断报告。它确认任务已完成，并且已识别出根本原因并提出了修复方案。您现在可以继续在 `Cli.py` 中实施修复，并使用 `Debug` 智能体提供的计划进行验证。

## 7. 最佳实践与提示

*   **具体明确**: 在向智能体（尤其是 `Deep Scope` 和 `Debug`）交接任务时，尽可能提供具体的上下文（日志摘录、代码片段、清晰的问题描述）。
*   **利用日志**: 日志对于调试不可见的逻辑错误至关重要。让智能体可以轻松访问这些日志。
*   **信任流程**: 让 `Orchestrator` 管理工作流。不要在不通过它的情况下直接在 `Deep Scope` 和 `Debug` 之间跳转。
*   **必要时迭代**: 复杂问题可能需要多轮范围界定和诊断。该框架支持迭代优化。
*   **记录一切**: 范围界定文档和诊断报告都是宝贵的知识资产。为将来参考而存储它们。

通过遵循本指南并利用 `Orchestrator`、`Deep Scope` 和 `Debug` 智能体在框架的结构化 SPARC + Boomerang 工作流中的专业化能力，您可以系统地解决最棘手的软件问题。

## 8. 附录：智能评估与复用现有资源

使用 AI 助手时的一个常见挑战是确保它们能利用现有的项目功能，而不是重新发明轮子。Advanced Multi-Agent AI Framework 提供了一种结构化的方法来实现这一目标。

### 问题所在

当您要求 AI "执行一个任务" 时，它可能会立即开始从头开始编写解决方案，即使您的项目中已经存在一个完全合适的脚本。这会浪费时间和精力。

### 解决方案：探索 -> 评估 -> 实施

关键是在任何实施开始之前，**强制进行探索和评估阶段**。这利用了框架内不同智能体的专业化能力。

### 指导框架的步骤

1.  **使用 Orchestrator 明确目标**:
    *   切换到 `Orchestrator` 模式。
    *   **清晰地陈述您的高级目标** (例如，"生成用户活动报告")。
    *   **至关重要，明确指示它优先考虑资源评估**: 添加类似这样的声明，"在实施任何事情之前，请评估并优先考虑重用项目中任何可以实现此目标的现有脚本或工具。"

2.  **生成战略性任务地图**:
    *   要求 `Orchestrator` 创建一个 **强制探索** 的任务地图。一个良好的结构包括：
        *   **第一阶段：资源探索与评估**
            *   **Task 1.1**: 指示 `Ask` 智能体搜索代码库中相关的现有脚本、工具或库。
                *   **Agent**: `Ask`
                *   **Scope**: 利用其能力 (`rag`, `comprehensive-code-analysis`) 扫描项目中匹配任务描述的文件 (例如，在 `scripts/`, `tools/`, `bin/` 中)。记录它们的位置、用途和重用潜力。
        *   **第二阶段：可行性分析与计划 (可选但推荐)**
            *   **Task 2.1**: (如果需要) 要求 `Architect` 智能体在整体系统架构的背景下评估发现的资源。
                *   **Agent**: `Architect`
                *   **Scope**: 评估现有脚本如何融入系统、它们的依赖关系以及任何潜在的集成挑战。
        *   **第三阶段：决策与执行**
            *   **Task 3.1**: 基于 Task 1.1 (以及可选的 2.1) 的发现，决定最佳行动方案。
                *   **Agent**: `Orchestrator` (或用于复杂案例的 `Architect`)
                *   **Scope**: 比较选项：a) 直接使用/重用现有脚本。b) 稍微修改/包装现有脚本。c) 从头开始构建新解决方案。记录决策和理由。
            *   **Task 3.2**: 执行所选计划。
                *   **Agent**: `Builder`/`Code` (用于新开发) 或 `Guardian` (用于 CI/CD 集成) 甚至 `Orchestrator` (提供最终指令)。
                *   **Scope**: 如果是重用，此任务是关于 "实现集成/包装器逻辑" 或 "记录用法"，而不是 "重新实现核心功能"。

### 关键策略

*   **明确指令**: 始终告诉 `Orchestrator` "评估重用" 或 "首先探索现有资源"。这能正确地启动工作流。
*   **利用 `Ask` 智能体**: `Ask` 智能体专门用于信息发现 (`rag`, `comprehensive-code-analysis`)。指示它彻底搜索代码库。如果您有线索，请提供具体的目录或搜索关键词。
*   **必要时使用 `Architect` 获取上下文**: 对于复杂项目，`Architect` 可以提供关于发现的脚本如何融入大局以及它是否是重用的好选择的宝贵见解。
*   **仔细构建任务**: 当 `Orchestrator` 创建 Task 3.2 (执行任务) 时，确保描述中清楚地说明了所选路径 (例如，"实现一个 Python 包装器脚本，使用从用户输入派生的适当参数调用现有的 `scripts/generate_report.py` 工具。")。这可以防止被分配的智能体默认进行完全重新实现。
*   **给 Orchestrator 的示例提示**:
    > "我需要从我们的数据库生成一份每周用户活动摘要报告。我的目标是让这个任务自动化。然而，我怀疑在我们的 `tools/` 或 `scripts/` 目录中可能已经有处理数据提取或报告生成的脚本。请创建一个任务地图，首先让 `Ask` 智能体彻底搜索代码库中任何相关的现有脚本。在识别出潜在候选者后，我们将评估它们是否可以被重用、修改，或者是否需要新解决方案。优先考虑利用现有工作。"

通过遵循本附录的指导，并在框架内构建您的请求以包含明确的探索阶段，您可以显著提高 Kilo Code (Roo) 智能评估和重用项目现有资源的可能性，从而带来更高效和一致的结果。