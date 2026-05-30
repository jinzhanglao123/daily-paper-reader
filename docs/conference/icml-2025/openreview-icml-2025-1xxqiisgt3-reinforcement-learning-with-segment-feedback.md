---
title: Reinforcement Learning with Segment Feedback
title_zh: 基于分段反馈的强化学习
authors: "Yihan Du, Anna Winnicki, Gal Dalal, Shie Mannor, R. Srikant"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=1XXqIIsgT3"
tags: ["query:uav-drl"]
score: 7.0
evidence: 面向长时域奖励分配的分段反馈模型
tldr: 针对实际应用中每步状态-动作对奖励难以获取的挑战，本文提出分段反馈强化学习模型，将回合划分为多个区间，智能体仅在每个区间结束时观测奖励。该模型填补了逐步反馈与轨迹反馈之间的空白，并通过理论分析建立了算法的采样复杂度保证，为长时域任务的奖励分配提供了新思路。此外，研究了两种算法并证明其有效性，为在长时域场景中高效学习提供了通用范式。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 525, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1496, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1225, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1356, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1196, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1xxqiisgt3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 571, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-1xxqiisgt3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1771, \"height\": 467, \"label\": \"Table\"}]"
motivation: 长序列任务中每步奖励获取成本高，轨迹反馈学习效率低。
method: 提出分段反馈强化学习模型，将回合划分为区间，区间结束时给予奖励，并设计算法。
result: 理论上证明了算法的采样复杂度保证，改善了长时域任务的学习效率。
conclusion: 分段反馈是逐步与轨迹反馈的有效折衷，为实际应用中的长时域强化学习提供了可行方案。
---

## Abstract
Standard reinforcement learning (RL) assumes that an agent can observe a reward for each state-action pair. However, in practical applications, it is often difficult and costly to collect a reward for each state-action pair. While there have been several works considering RL with trajectory feedback, it is unclear if trajectory feedback is inefficient for learning when trajectories are long. In this work, we consider a model named RL with segment feedback, which offers a general paradigm filling the gap between per-state-action feedback and trajectory feedback. In this model, we consider an episodic Markov decision process (MDP), where each episode is divided into $m$ segments, and the agent observes reward feedback only at the end of each segment. Under this model, we study two popular feedback settings: binary feedback and sum feedback, where the agent observes a binary outcome and a reward sum according to the underlying reward function, respectively. To investigate the impact of the number of segments $m$ on learning performance, we design efficient algorithms and establish regret upper and lower bounds for both feedback settings. Our theoretical and experimental results show that: under binary feedback, increasing the number of segments $m$ decreases the regret at an exponential rate; in contrast, surprisingly, under sum feedback, increasing $m$ does not reduce the regret significantly.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容，生成的结构化中文总结。

### 1. 研究动机与核心问题

*   **核心问题**：在传统强化学习（RL）中，智能体需要在每一步（状态-动作对）之后都获得即时奖励。然而，这在现实世界的许多应用中（如机器人、自动驾驶）往往成本高昂或难以实现。现有工作尝试使用“轨迹反馈”（即仅在回合结束时给予一次反馈），但对于长序列任务，这种反馈可能效率低下。本论文的核心问题是：**在极稀疏的每步奖励和过于粗糙的轨迹奖励之间，是否存在一种更优的折衷方案？反馈的频率如何系统性地影响学习效率？**
*   **研究动机**：作者旨在填补“逐步反馈”和“轨迹反馈”之间的理论空白，提出一个名为“**基于分段反馈的强化学习（RL with Segment Feedback）**”的通用范式。该模型允许将一个完整的交互轨迹（回合）划分为多个区段（segments），智能体仅在每个区段结束时获得关于该区段表现的反馈。这为解决长时域任务中的奖励分配难题提供了一个更具普遍性和理论深度的视角。

### 2. 方法论

*   **核心模型**：将经典的回合制马尔可夫决策过程（MDP），其中每个回合被均等划分为 \( m \) 个区段。智能体在每个区段结束时，而非每一步，获得一次关于该区段的奖励反馈。
*   **研究的两种反馈设置**：
    1.  **二元反馈**：智能体观察到一个二元结果（如“好”/“坏”），它由该区段累积奖励的 Sigmoid 函数生成。目标是学习底层奖励函数并最大化期望累积奖励。
    2.  **求和反馈**：智能体观察到该区段内所有步骤奖励的总和（叠加了随机噪声）。目标是最大化期望奖励总和。
*   **关键算法与理论分析**：
    *   **二元反馈**：
        *   提出 **SegBiTS** (已知转移) 和 **SegBiTS-Tran** (未知转移) 算法。它们基于**汤普森采样**框架，采用最大似然估计（MLE）从二元观测中学习奖励，并加入高斯噪声进行后验采样。SegBiTS-Tran 还引入了转移概率的置信度奖励项（transition bonus）。
        *   **理论贡献**：建立了悔恨值（Regret）的上界和下界，两者都包含指数项 \( \exp\left(\frac{Hr_{\max}}{2m}\right) \)。下界通过巧妙的 KL 散度分析证明了该指数依赖的**不可避免性**。结论表明，**增加区段数量 \( m \) 能指数级地加速学习**。
    *   **求和反馈**：
        *   提出 **E-LinUCB** (已知转移) 和 **LinUCB-Tran** (未知转移) 算法。E-LinUCB 将问题视作线性赌博机，并采用了**E-最优实验设计**进行初始化探索，以优化协方差矩阵的特征值，从而大幅收紧置信区间。LinUCB-Tran 则引入了一种基于方差的转移不确定性边界来处理未知转移。
        *   **理论贡献**：证明了悔恨值的上界和下界与区段数量 \( m \) **无关**，且 E-LinUCB 的悔恨上界在 \( H \) 的依赖上达到了最优。结论揭示了，**增加区段数量 \( m \) 并不能显著提升求和反馈设置下的学习速度**。

### 3. 实验设计

*   **场景与数据集**：实验使用了**自行设计的 MDP 环境**。
    *   对于二元反馈，设计了一个包含 9 个状态、5 个动作的 MDP，并定义了好/坏状态和最优/次优动作。
    *   对于求和反馈（因其算法侧重于理论揭示，计算复杂度较高），使用了更小的 3 状态、5 动作 MDP。
*   **Benchmark 与对比方法**：实验主要是为了**验证理论发现的正确性**，即揭示区段数量 \( m \) 对不同反馈设置下悔恨值的影响。对比在**已知转移**和**未知转移**两种情形下，所提出算法的累积悔恨值随 \( m \) 变化的曲线。
*   **实验参数**：设置了不同的区段数量 \( m \in \{1, 2, 4, 5, 10, 20, 25, 50, 100\} \)，固定 \( K \) 值（二元反馈 \( K=30000 \)，求和反馈 \( K=1000 \)），并对每种算法进行了 **20 次独立运行**，绘制了带有 95% 置信区间的平均累积悔恨曲线。

### 4. 资源与算力

*   论文中**未明确提及**所使用的计算资源（如 GPU 型号、数量）或总训练时长。

### 5. 实验数量与充分性

*   **实验数量**：在两种反馈设置下，各针对已知和未知转移情况运行了算法，总计 **四组主要实验**。每组实验都改变了区段数量 \( m \)（从 1 到 100，覆盖了逐步和轨迹反馈两种极端情况），共 9 种不同配置。
*   **充分性与客观性**：
    *   **优点**：实验设计紧扣理论核心——验证 \( m \) 的影响。通过绘制带有置信区间的悔恨曲线，并对比极端情况（\( m=1 \) vs. \( m=H \)），直观且有力地证实了理论分析出的指数衰减和无关性趋势。
    *   **不足**：实验仅在人工构建的、规模较小的 MDP 上进行，缺乏在标准强化学习基准（如 Atari, MuJoCo）或更复杂真实场景下的验证。对比方法也仅限于验证自身理论，未与其他非分段反馈的基线方法进行对比。

### 6. 主要结论与发现

*   **分段反馈是一个通用且有效的范式**，它平滑地连接了经典 RL 和轨迹反馈 RL。
*   **反馈类型与分段效益的关联**：分段数量 \( m \) 的收益**高度依赖于反馈类型**。
    *   **二元反馈**：增加 \( m \) 能带来 **指数级的学习效率提升**。原因在于，当区段变短，累积奖励的尺度变小，Sigmoid 函数处于梯度更大的“陡峭”区域，从而更容易区分好/坏区段。
    *   **求和反馈**：**增加 \( m \) 无法显著帮助学习**。这是因为虽然获得了更多观测，但每个观测的信息量（区段特征向量）等比例缩小，导致协方差矩阵的估计不确定性增加。在以回合总奖励为优化目标时，这两个效应恰好相互抵消。
*   在求和反馈的特例（\( m=1 \)）下，E-LinUCB 将前人（Efroni et al., 2021）的悔恨上界提升了一个 \( \sqrt{H} \) 因子，实现了理论最优。

### 7. 优点

*   **理论深度与原创性**：首次系统性地量化了区段数量对学习效率的影响，建立了上下界匹配的指数悔恨界（二元）和与 \( m \) 无关的最优悔恨界（求和），理论贡献扎实。
*   **方法新颖**：针对二元反馈的指数下界证明（使用 KL 散度和 Pinsker 不等式）和求和反馈的 E-最优实验设计初始化技巧，为分析此类问题提供了新工具和见解。
*   **问题架构清晰**：提出的分段反馈框架具有很好的泛化能力，能够涵盖从逐步到轨迹反馈的所有情况，为后续研究奠定了坚实基础。

### 8. 不足与局限

*   **计算复杂度**：为揭示理论最优性而设计的 E-LinUCB 和 LinUCB-Tran 算法，在状态空间较大时计算代价高昂，限制了其直接应用于大规模问题。
*   **实验验证范围有限**：实验仅在小型、合成环境上进行，缺乏在更复杂、高维或真实世界模拟器（如自动驾驶、机器人操控）上的验证，其结论的普适性有待进一步检验。
*   **等长区段假设**：模型假设每个回合被均等地划分，但在许多实际任务中，非等长或自适应的区段划分可能更自然、更高效。论文虽将此作为未来方向，但在本工作中并未涉及。
*   **对比基线缺失**：实验未与处理稀疏奖励或偏好反馈的其他相关强化学习方法进行对比，难以横向评估所提算法的绝对性能。

（完）
