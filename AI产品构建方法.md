# AI 产品构建方法

## 方法页文案

主标题：

让 AI 能力真正驱动产品价值

副标题：

AI 产品不是“接入一个大模型，再做一个聊天框”，而是围绕真实任务，设计一套可评测、可控制、可持续迭代的人机协作系统。

卡片内容：

### 01/Define Value

标题：

为什么需要 AI，值不值得做？

正文：

先验证 AI 是否创造独特价值，从商业收益、用户痛点和技术可行性判断降本、提效或增收，确认 AI 是必要解而不是跟风选择。

### 02/Define Goal

标题：

先讨论需求，再定义产品目标

正文：

AI 不是目标，用户任务才是。先还原现有流程，再明确 AI 介入环节、用户结果和成功指标，同时约定质量、安全、成本与延迟的底线。

### 03/Set Boundaries

标题：

定义 AI 的身份与行动边界

正文：

明确 AI 是助手、顾问、决策者还是执行者，规定它能读取什么、调用什么、何时询问和确认。越接近外部行动，权限越小、审计越强。

### 04/Build the System

标题：

把核心能力组织成可控系统

正文：

将 AI 拆成输入、上下文、模型、工具、规则和状态，明确每一环的责任。通过结构化输出、权限控制、状态管理和失败回退，把不确定响应组织成可观察流程。

### 05/Evaluate & Attribute

标题：

用评测和归因，决定产品如何迭代

正文：

上线前用真实任务建立评测集，上线后记录过程和结果。将问题归因到需求、数据、检索、模型、工具、流程或交互，评测决定是否发布，归因决定改哪里。

### 06/Evolve with Data

标题：

让真实使用推动系统进化

正文：

让每次使用都产生可复用反馈，通过埋点、人工接管和结果记录沉淀评测样例、知识更新与流程优化，并在隐私边界内完成版本化、回归和持续监控。

## 方法论流程图

流程图按六个产品判断板块组织；板块内部展示细节节点，板块之间展示主流程。节点 ID 与 logicNotes 中的键一一对应；实线表示主流程，虚线表示反馈与迭代。

~~~mermaid
flowchart TB
    subgraph valueBlock["01 / Define Value：价值判断"]
        direction LR
        task(["真实用户任务"]) --> problem["现有流程与用户痛点"]
        problem --> baseline["现有方案与价值基线"]
        baseline --> value{"AI 是否带来独特价值？"}
        value -->|否| deterministic(["确定性产品方案"])
    end

    subgraph goalBlock["02 / Define Goal：目标定义"]
        direction LR
        goal["产品目标与成功标准"] --> contract["输入与输出契约"]
    end

    subgraph boundaryBlock["03 / Set Boundaries：边界设定"]
        direction LR
        context["知识与上下文边界"] --> identity["AI 身份与自主程度"]
        identity --> authority["权限与人工确认"]
    end

    subgraph systemBlock["04 / Build the System：系统构建"]
        direction LR
        workflow["任务流程与状态"] --> model["模型与能力策略"]
        model --> tools["工具与行动控制"]
        tools --> mvp["最小可用 AI 流程"]
    end

    subgraph evalBlock["05 / Evaluate & Attribute：评测归因"]
        direction LR
        evalset[(真实任务评测集)] --> evaluation{"是否达到上线门槛？"}
        evaluation -->|否| attribution["失败归因与修复"]
        attribution -. "修复后复测" .-> evalset
    end

    subgraph evolutionBlock["06 / Evolve with Data：持续进化"]
        direction LR
        rollout["灰度上线与运行监控"] --> feedback["使用反馈与结果数据"]
        feedback --> evolution["版本化迭代"]
    end

    value -->|是| goal
    contract --> context
    authority --> workflow
    mvp --> evalset
    evaluation -->|是| rollout
    evolution -. "目标校正" .-> goal
    evolution -. "系统优化" .-> context

    click task "#logic-task" "查看用户任务"
    click problem "#logic-problem" "查看问题定义"
    click baseline "#logic-baseline" "查看价值基线"
    click value "#logic-value" "查看价值判断"
    click deterministic "#logic-deterministic" "查看方案选择"
    click goal "#logic-goal" "查看产品目标"
    click contract "#logic-contract" "查看输入输出"
    click context "#logic-context" "查看上下文边界"
    click identity "#logic-identity" "查看 AI 身份"
    click authority "#logic-authority" "查看行动权限"
    click workflow "#logic-workflow" "查看任务流程"
    click model "#logic-model" "查看能力策略"
    click tools "#logic-tools" "查看工具控制"
    click mvp "#logic-mvp" "查看最小流程"
    click evalset "#logic-evalset" "查看评测集"
    click evaluation "#logic-evaluation" "查看上线门槛"
    click attribution "#logic-attribution" "查看失败归因"
    click rollout "#logic-rollout" "查看灰度监控"
    click feedback "#logic-feedback" "查看使用反馈"
    click evolution "#logic-evolution" "查看版本迭代"
~~~

## logicNotes（节点说明数据）

~~~json
{
  "task": {
    "title": "真实用户任务",
    "description": "从用户要完成的任务和现有流程开始，而不是从模型能力开始。"
  },
  "problem": {
    "title": "现有流程与用户痛点",
    "description": "识别用户在哪个环节受阻，以及问题是否真实、高频、刚性且值得解决。"
  },
  "baseline": {
    "title": "现有方案与价值基线",
    "description": "记录人工、传统软件或规则引擎的处理方式、成本、耗时和结果质量。"
  },
  "value": {
    "title": "AI 价值判断",
    "description": "判断 AI 是否带来独特价值，并比较确定性方案、AI 功能和 Agent 方案的投入与收益。"
  },
  "deterministic": {
    "title": "确定性产品方案",
    "description": "当规则、搜索或传统软件已经能够稳定解决问题时，优先选择更可控的确定性方案。"
  },
  "goal": {
    "title": "产品目标与成功标准",
    "description": "把用户需求转化为明确结果、衡量指标和质量、安全、成本与延迟边界。"
  },
  "contract": {
    "title": "输入与输出契约",
    "description": "定义用户提供什么、系统返回什么，以及结果必须满足的格式、质量和不确定性要求。"
  },
  "context": {
    "title": "知识与上下文边界",
    "description": "明确模型可以使用哪些数据、数据是否可靠及时，以及权限和隐私边界在哪里。"
  },
  "identity": {
    "title": "AI 身份与自主程度",
    "description": "确定 AI 是辅助、推荐、决策还是执行，并匹配相应的自动化范围。"
  },
  "authority": {
    "title": "权限与人工确认",
    "description": "规定 AI 能读取什么、调用什么，以及哪些高风险动作必须由人确认、审计和撤销。"
  },
  "workflow": {
    "title": "任务流程与状态",
    "description": "把一次交互拆成输入、处理、等待、成功、失败、转人工和恢复等可识别状态。"
  },
  "model": {
    "title": "模型与能力策略",
    "description": "根据任务难度、质量目标、延迟和成本选择模型能力与降级策略。"
  },
  "tools": {
    "title": "工具与行动控制",
    "description": "只开放完成任务所需的工具，限制参数和副作用，并为失败、重复执行和超时设计保护。"
  },
  "mvp": {
    "title": "最小可用 AI 流程",
    "description": "先打通最小闭环，让用户完成一次真实任务，再根据结果决定是否增加复杂能力。"
  },
  "evalset": {
    "title": "真实任务评测集",
    "description": "用正常、边界、失败和高风险样例组成评测集，代表产品真正要解决的任务。"
  },
  "evaluation": {
    "title": "上线门槛",
    "description": "同时检查任务效果、系统安全、用户体验、成本和延迟，决定是否进入下一阶段。"
  },
  "attribution": {
    "title": "失败归因与修复",
    "description": "将失败定位到需求、数据、检索、模型、工具、流程或交互，并形成对应修复和复测。"
  },
  "rollout": {
    "title": "灰度上线与运行监控",
    "description": "通过小范围灰度、可回滚版本和运行指标验证真实环境中的稳定性与风险。"
  },
  "feedback": {
    "title": "使用反馈与结果数据",
    "description": "记录接受、修改、拒绝、人工接管、工具调用和最终结果，观察用户是否真正完成任务。"
  },
  "evolution": {
    "title": "版本化迭代",
    "description": "将反馈沉淀为评测样例、知识更新、规则调整或流程优化，并回到目标和系统重新验证。"
  }
}
~~~

## 工作经验篇章

章节标签：

WORKING PRINCIPLES

标题：01/先确认问题

正文：

先从用户任务、现有流程和可验证材料开始，再形成产品判断，区分事实、假设与待验证问题。

标题：02/让控制匹配风险

正文：

根据任务风险分配自动化程度：低风险环节追求效率，高风险决策保留确认、回退和审计。

标题：03/沿链路做归因

正文：

从输入、上下文、模型、工具、交互到结果逐段检查，先定位影响任务成败的环节，再决定优化方向。

标题：04/用真实任务验证

正文：

用真实使用、失败样例和人工反馈校准方案，让产品判断经得起复现，而不是停留在演示效果。

标题：05/把经验沉淀为方法

正文：

将验证过的判断沉淀为规则、流程和证据，让一次项目经验转化为可复用、可持续的产品能力。
