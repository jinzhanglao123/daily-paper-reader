---
title: "Outcome-Based Online Reinforcement Learning: Algorithms and Fundamental Limits"
title_zh: 基于结果的在线强化学习：算法与基本极限
authors: "Fan Chen, Zeyu Jia, Alexander Rakhlin, Tengyang Xie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=sYfIpZzojf"
tags: ["query:uav-drl"]
score: 9.0
evidence: 直接解决基于结果反馈的长时序功劳分配，提出样本高效的算法
tldr: 首次全面分析了一般函数逼近下仅轨迹终点有奖励的在线强化学习问题，提出了样本复杂度为Õ(CCov H³/ε²)的算法，填补了该问题的理论空白，在大型状态空间中有效工作。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-syfipzzojf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1442, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-syfipzzojf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 737, \"height\": 234, \"label\": \"Table\"}]"
motivation: 基于结果反馈的强化学习中，如何将终点奖励正确分配给每个动作是关键挑战，缺乏理论分析。
method: 提出首个针对一般函数逼近的样本高效算法，利用覆盖系数保证采样效率。
result: 算法达到Õ(CCov H³/ε²)的样本复杂度，在大型状态空间中有效。
conclusion: 该工作为基于结果反馈的在线RL提供了算法和理论极限，推动了长时序功劳分配的研究。
---

## Abstract
Reinforcement learning with outcome-based feedback faces a fundamental challenge: when rewards are only observed at trajectory endpoints, how do we assign credit to the right actions? This paper provides the first comprehensive analysis of this problem in online RL with general function approximation. We develop a provably sample-efficient algorithm achieving $\widetilde{O}({C_{\rm cov} H^3}/{\varepsilon^2})$ sample complexity, where $C_{\rm cov}$ is the coverability coefficient of the underlying MDP. By leveraging general function approximation, our approach works effectively in large or infinite state spaces where tabular methods fail, requiring only that value functions and reward functions can be represented by appropriate function classes. Our results also characterize when outcome-based feedback is statistically separated from per-step rewards, revealing an unavoidable exponential separation for certain MDPs. For deterministic MDPs, we show how to eliminate the completeness assumption, dramatically simplifying the algorithm. We further extend our approach to preference-based feedback settings, proving that equivalent statistical efficiency can be achieved even under more limited information. Together, these results constitute a theoretical foundation for understanding the statistical properties of outcome-based reinforcement learning.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义

*   **研究动机**：在实际应用中，智能体往往只能在完整轨迹结束后获得一个总的结果奖励（如，大语言模型训练中人类对整个回答的偏好、临床试验中疗程结束后的最终疗效），而无法获得针对每一步动作的即时奖励反馈。这导致了严重的“功劳分配”问题，即难以判断哪个具体动作导致了最终的好或坏结果。
*   **核心问题**：本文旨在从理论层面，首次全面分析在**结果导向反馈**下的**在线强化学习**问题。核心是探究“仅依靠轨迹层面的奖励，何时能实现高效的在线探索？”这与传统强化学习中即时获得每一步奖励的情景形成对比。
*   **整体含义**：本文为结果导向在线强化学习提供了算法基础与理论极限。证明了在特定条件下，通过精心设计的算法，即使没有中间步骤的奖励，也能在多项式样本复杂度内学到近似最优策略；同时，也揭示了在某些情况下，结果导向反馈与过程奖励反馈之间存在着不可避免的指数级统计分离。

### 方法论：核心思想与技术细节

论文提出了基于乐观主义与模型无关的算法，其核心在于如何仅利用结果奖励进行置信区间的估计和探索。

*   **通用算法（算法1，针对随机MDP）：基于联合优化的乐观Fitted-Q迭代**
    *   **核心思想**：不再像传统方法那样先单独拟合奖励模型再优化Q函数（这种做法可能会失败，如附录F.1所示），而是**联合优化价值函数与奖励函数**。算法通过在历史数据上最小化两个关键损失函数，来构建一个乐观的置信集，从而引导探索。
    *   **关键技术细节**：
        *   **奖励模型损失（$L_{RM}$）**：衡量候选奖励模型对已观测到的轨迹总奖励的拟合误差。
        *   **贝尔曼误差损失（$L_{BE}$）**：衡量候选Q函数相对于候选奖励模型的贝尔曼方程违反程度。通过引入一个比较器函数类`G`，该损失设计解决了“双重采样”问题，即无需对同一状态-动作对进行两次独立采样。
        *   **乐观估计**：每轮迭代中，通过解决一个最大化问题 `max_{f∈F, R∈R} [λ * f₁(s₁) - L_{BE}(f; R) - L_{RM}(R)]` 来获取乐观的Q函数和奖励函数。参数`λ`用于平衡探索（鼓励高价值估计）和利用（惩罚估计误差）。
        *   **数据收集策略**：采用分层滚动探索，执行策略`π ∘_h π_ref`，即在前`h`步执行当前策略，之后执行一个固定的参考策略。这确保了收集到的数据具有足够的覆盖性。
    *   **公式（文字描述）**：算法的核心优化目标为联合最大化的公式(6)，它鼓励选择在初始状态价值估计更高，同时与历史数据中的贝尔曼方程及奖励模型更一致的Q函数和奖励函数对。
*   **简化算法（算法2，针对确定性MDP）：基于贝尔曼残差最小化的乐观探索**
    *   **核心思想**：当环境动态是确定性时，任何Q函数`f`都能推导出一个天然的结果奖励模型`R_f(τ) = Σ_h [f_h(s_h, a_h) - f_{h+1}(s_{h+1})]`。因此，无需单独的奖励函数类，可以直接最小化Q函数自身的贝尔曼残差。
    *   **关键技术细节**：
        *   **贝尔曼残差损失（$L_{BR}$）**：直接衡量由Q函数推导出的奖励模型与真实结果奖励的平方误差。
        *   **简化探索**：每轮只需执行一次由乐观Q函数导出的贪婪策略，数据收集效率更高。
    *   **假设放松**：该算法仅需Q函数类具有可实现性，无需贝尔曼完备性假设，显著简化了算法和理论。
*   **扩展到基于偏好的强化学习（算法3）**
    *   **核心思想**：将算法1推广到只能获得成对轨迹偏好反馈（而非数值奖励）的场景，这更贴近RLHF的实际应用。
    *   **关键技术细节**：将奖励模型损失（$L_{RM}$）替换为基于Bradley-Terry-Luce模型的偏好奖励模型损失（$L_{PbRM}$, 即逻辑损失），并在优化目标中加入一个参考策略的价值估计项`bV_ref`，用以校准因偏好信号仅反映相对差异而可能产生的过估计。

### 实验设计

*   **本文是一个纯理论性工作，没有进行任何实验验证。** 所有的结论均通过数学推导和证明得到，因此不涉及数据集、基准方法或对比实验。

### 资源与算力

*   由于本文为纯理论研究，**文中未提及任何计算资源（GPU型号、数量、训练时长等）的使用情况。**

### 实验数量与充分性

*   本文未进行实验，因此**不涉及实验数量和充分性的讨论**。论文结论的可靠性依赖于其严谨的数学假设、定理陈述与证明过程。

### 论文的主要结论与发现

1.  **正面结果（算法上界）**：
    *   提出了首个在结果奖励下，具有样本效率保证的通用函数逼近在线RL算法，其样本复杂度为$\widetilde{O}(C_{\rm cov} H^3 / ε^2)$，其中$C_{\rm cov}$为刻画MDP内在难度的覆盖性系数。
    *   对于确定性MDP，提出了一个更简单、计算效率更高的算法，且其理论保证所需的假设更弱。
    *   将方法和理论成功拓展至基于偏好反馈的强化学习问题，展示了该技术路线在更受限信息下的有效性。
2.  **负面结果（下界与分离）**：
    *   揭示了结果奖励与过程奖励之间存在根本性的统计分离。具体地，论文构造了一个二维MDP，在该MDP上，使用过程奖励能以$\widetilde{O}(d^2/ε^2)$样本高效学习，但仅凭结果奖励则至少需要$\widetilde{\Omega}(d)$个样本，呈指数级差距。
    *   该下界证明了，当只有结果奖励时，某些依赖于过程奖励细微结构的精巧分析方法是失效的。

### 优点

*   **理论贡献完整且深刻**：首次为结果导向在线RL提供了从算法设计、上界分析到下界证明的闭环理论框架。
*   **算法设计新颖**：提出了联合优化而非分步优化的核心思想，解决了结果奖励下奖励模型误设可能导致探索失败的关键难题。
*   **拓展性强**：方法不仅适用于随机和确定性MDP，还顺利拓展到更实际的偏好反馈设定，显示出其理论框架的普适性。
*   **界限清晰**：结果明确量化了不同反馈类型（结果vs.过程）之间的统计难度差异，为未来算法设计提供了理论指导。

### 不足与局限

*   **缺乏实验验证**：作为纯理论文章，其实际算法性能，如在高维复杂环境中的表现、对近似误差的容忍度等，未经验证。
*   **计算可行性**：核心的通用算法（算法1, 3）依赖于解决一个可能非常困难的极大极小优化问题（如公式(6)和(12)），其在实际大规模问题中的计算效率和可行性是一大挑战。
*   **奖励函数限制**：本文结果严格局限于总奖励为每一步奖励之和的情况，没有扩展到其他类型的结果奖励函数（如最小值、最大值等）。
*   **理论假设较强**：算法的样本效率保证依赖于可实现性和贝尔曼完备性等强假设，这些假设在复杂实际问题中可能难以满足。尽管确定性MDP算法放松了完备性假设，但其适用范围有限。

（完）
