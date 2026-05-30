---
title: "CHPO: Constrained Hybrid-action Policy Optimization for Reinforcement Learning"
title_zh: CHPO：用于强化学习的约束混合动作策略优化
authors: "Ao Zhou, Jiayi Guan, Li Shen, Fan Lu, Sanqing Qu, Junqiao Zhao, Ziqiao Wang, Ya Wu, Guang Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=KMaBmPHkVj"
tags: ["query:uav-drl"]
score: 9.0
evidence: 提出面向离散-连续混合动作空间的约束混合动作策略优化
tldr: 针对现有混合动作强化学习仅追求奖励最大化、难以处理安全约束型混合动作空间任务的问题，本文提出约束混合动作策略优化算法CHPO。CHPO重新构建了约束混合动作RL的目标，使其在参数化离散-连续动作空间中能同时满足成本约束。实验表明CHPO在安全关键任务中优于现有方法，为混合动作空间的约束策略学习提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1426, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1440, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1438, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1442, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1420, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1444, \"height\": 460, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-kmabmphkvj/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-kmabmphkvj/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1035, \"height\": 722, \"label\": \"Table\"}]"
motivation: 现有混合动作强化学习算法难以处理同时需要满足成本约束的任务，限制了其在安全关键应用中的使用。
method: 提出约束混合动作策略优化算法CHPO，重新设计目标函数以在参数化动作空间中整合成本约束与奖励最大化。
result: CHPO在多种安全关键任务中实现了约束满足和性能提升，优于仅优化奖励的混合动作RL方法。
conclusion: CHPO有效解决了约束混合动作RL问题，为安全关键系统中的策略学习提供了实用方案。
---

## Abstract
Constrained hybrid-action reinforcement learning (RL) promises to learn a safe policy within a parameterized action space, which is particularly valuable for safety-critical applications involving discrete-continuous hybrid action spaces. However, existing hybrid-action RL algorithms primarily focus on reward maximization, which faces significant challenges for tasks involving both cost constraints and hybrid action spaces. In this work, we propose a novel Constrained Hybrid-action Policy Optimization algorithm (CHPO) to address the problems of constrained hybrid-action RL. Concretely, we rethink the limitations of hybrid-action RL in handling safe tasks with parameterized action spaces and reframe the objective of constrained hybrid-action RL by introducing the concept of Constrained Parameterized-action Markov Decision Process (CPMDP). Subsequently, we present a constrained hybrid-action policy optimization algorithm to confront the constrained hybrid-action problems and conduct theoretical analyses demonstrating that the CHPO converges to the optimal solution while satisfying safety constraints. Finally, extensive experiments demonstrate that the CHPO achieves competitive performance across multiple experimental tasks.

---

## 论文详细总结（自动生成）

好的，以下是对论文《CHPO: Constrained Hybrid-action Policy Optimization for Reinforcement Learning》的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：在许多现实世界的安全关键应用中，智能体需要在一个同时包含离散动作和连续参数的混合动作空间（Parameterized Action Space）中做出决策。例如，自动驾驶车辆需要选择行驶方向（离散）并决定在该方向上行驶多远的距离（连续），同时必须避免碰撞（安全约束）。
*   **核心问题**：现有的混合动作强化学习（RL）算法主要专注于奖励最大化，无法有效处理同时存在的成本（安全）约束。将这些算法直接应用于有约束的混合动作任务时，要么会为了高奖励而严重违反安全约束，要么（如引入奖励惩罚后）会因收敛困难而获得次优性能。
*   **整体含义**：该论文首次正式定义了约束混合动作强化学习任务，并提出了一个名为CHPO的算法。该算法旨在解决在参数化动作空间中，如何学习一个既能最大化奖励，又能满足给定安全约束的策略的难题。

### 2. 方法论

*   **核心思想**：CHPO的核心是**直接在原始策略目标上进行优化**，摒弃了常用的拉格朗日乘子法等对超参数敏感的原始-对偶方法。
*   **关键技术/框架**：
    1.  **问题建模 (CPMDP)**：论文提出了**约束参数化动作马尔可夫决策过程（Constrained Parameterized-action Markov Decision Process, CPMDP）**框架，它在传统PAMDP的基础上引入了成本集合 $C$，用于正式定义约束混合动作RL任务的目标：在满足成本期望不超过阈值 $\bar{c}_i$ 的条件下最大化累计奖励。
    2.  **算法架构**：CHPO采用一个**约束混合动作演员-评论家（Actor-Critic）架构**。该架构包含：
        *   **两个评论家网络**：分别估计奖励状态价值 $V^r(s)$ 和成本状态价值 $V^{c_i}(s)$。
        *   **两个演员网络**：分别为离散策略 $\pi_{\theta_d}$（输出离散动作）和连续策略 $\pi_{\theta_c}$（输出连续参数），两者共同构成参数化策略 $\pi_{\theta_p}$。
    3.  **策略更新机制 (关键公式)**：策略更新并非同时优化奖励和成本，而是根据当前策略是否满足安全约束，**在奖励最大化和成本最小化这两个目标之间切换**。
        *   **评估与决策**：CHPO首先计算不加折扣因子的成本回报 $\bar{L}^{c_i}(\pi_{\theta_p^k})$。若 $\bar{L}^{c_i}(\pi_{\theta_p^k}) \le \bar{c}_i$ (满足约束)，则进入“奖励最大化”阶段；反之，则进入“成本最小化”阶段。
        *   **奖励最大化阶段** (约束已满足)：策略更新目标演变为经典的近端策略优化（PPO）目标，旨在最大化带裁剪的奖励优势函数 $\hat{A}^r$。
            $$L(\theta_p) = \arg \max_{\theta_p} \mathbb{E} \left[ \min\left( \frac{\pi_{\theta_p}(a|s)}{\pi_{\theta_p^k}(a|s)} \hat{A}^r, \text{clip}\left(\frac{\pi_{\theta_p}(a|s)}{\pi_{\theta_p^k}(a|s)}, 1-\epsilon, 1+\epsilon\right) \hat{A}^r \right) \right]$$
        *   **成本最小化阶段** (约束被违反)：策略更新目标转变为最小化带裁剪的成本优势函数 $\hat{A}^{c_i}$，以引导策略回归安全区域。
            $$L(\theta_p) = \arg \min_{\theta_p} \mathbb{E} \left[ \min\left( \frac{\pi_{\theta_p}(a|s)}{\pi_{\theta_p^k}(a|s)} \hat{A}^{c_i}, \text{clip}\left(\frac{\pi_{\theta_p}(a|s)}{\pi_{\theta_p^k}(a|s)}, 1-\epsilon, 1+\epsilon\right) \hat{A}^{c_i} \right) \right]$$
*   **理论保证**：论文从理论上证明，CHPO算法在经过 $K$ 步迭代后，其策略性能（奖励）和策略成本会分别收敛到最优解和成本阈值附近的界内，收敛速度与状态空间 $|S|$、动作空间 $|A|$ 和迭代步数 $K$ 有关。

### 3. 实验设计

*   **实验场景/数据集**：论文在四个将混合动作与安全约束相结合的仿真任务上进行了评估。
    *   **Moving**：基础任务，智能体需通过离散动作（如转向、加速）和连续参数（如转角、加速度）移动到目标区域，同时避开多个危险区。
    *   **Sliding**：在Moving任务基础上增加了惯性，使动作效果有延迟。
    *   **HardMove**：更高维度的挑战任务，智能体需控制多个执行器（每个有开/关离散动作和连续的移动距离），以在避开危险区的同时到达目标。
    *   **Parking**：一个自定义的自动驾驶泊车任务，模拟RS曲线泊车方案。智能体需选择曲线类型（离散）和行驶距离（连续），在避免碰撞的前提下成功泊入车位。
*   **对比的基准方法**：由于缺乏同领域的标准算法，论文将现有的混合动作RL算法与约束处理方法结合，构建了三个基线。
    *   **PADDPG-Lag**：将离散动作空间松弛为连续空间，并结合拉格朗日乘子法处理约束的PADDPG算法。
    *   **HPPO-Lag**：在混合动作的HPPO算法中引入拉格朗日乘子法。
    *   **PDQN-Rco**：将成本作为负奖励（Reward-Constrained方法）与PDQN（结合DQN和DDPG的算法）结合。

### 4. 资源与算力

*   文中仅在附录D.3中简要说明实验是在**AMD Ryzen Threadripper 3960X 核心和NVIDIA RTX 3090 GPU**上运行的，但**未提供**任何关于模型训练时长、GPU内存消耗或总计算量的具体信息。

### 5. 实验数量与充分性

*   **实验组数**: 论文进行了较为全面的实验验证，主要包括：
    *   **主对比实验**：在四个任务上，将CHPO与三个基线算法在默认成本阈值（$\bar{c}_i = 1$）下的性能（奖励与成本曲线）进行对比。
    *   **不同成本阈值下的性能对比**：设置了三个不同的成本阈值（$\bar{c}_i = 1, 1.5, 2$），分别对比CHPO与各基线的最终奖励和成本均值（表格1）。
    *   **消融实验**：
        1.  **移除约束模块（HPO）**：在四个任务上对比有无策略切换机制的CHPO算法，以验证约束模块的有效性。
        2.  **不同C/A比率的影响**：研究了用于成本最小化的策略更新步数与总步数之比（C/A比率）对算法性能的影响。
*   **充分性与公平性**：
    *   **充分性**：实验覆盖了四个不同特性和维度的任务，并包含了不同安全要求的场景，评估维度（奖励 vs. 成本, 均值 vs. 方差）也较为全面。
    *   **公平性**：基线选择合理，均为现有最佳方法的组合；所有实验结果均报告了三个随机种子下的均值和方差/标准差，保证了结果的统计可靠性。实验设置和超参数在附录中公开。

### 6. 主要结论与发现

*   **有效性**：CHPO在所有四个任务中，均能在确保平均成本满足安全约束的前提下，取得最高的奖励，性能优于其他所有基线方法。
*   **稳定性**：与基于拉格朗日乘子法的基线（HPPO-Lag, PADDPG-Lag）相比，CHPO的训练过程显示出更高的稳定性和更小的方差。
*   **适应性**：CHPO能有效适应不同的成本阈值，并相应调整策略，在最大程度上追求奖励。
*   **机制有效性**：消融实验证明，其核心的“奖励/成本目标切换”机制是保证安全的关键，去除该模块会导致严重的安全性违规。

### 7. 优点

*   **首创性**：首次明确定义并解决了约束混合动作强化学习问题，填补了这一研究方向的空白。
*   **方法新颖且有效**：提出的CHPO算法通过巧妙的策略更新切换机制，避开了拉格朗日乘子法调参困难的痛点，方法简洁且理论上有保证。
*   **实验设计全面**：从多个任务、多个成本约束、多个C/A比率和消融研究等角度进行了充分验证，结果令人信服。
*   **理论支撑**：提供了收敛性和安全性的理论分析，增强了方法的可靠性。

### 8. 不足与局限

*   **资源消耗说明不足**：论文未提供训练时长等具体的算力消耗信息，使得其他研究者难以评估其计算成本。
*   **实验环境相对简单**：所有实验均在仿真环境中进行，尚未在真实的机器人或自动驾驶平台上验证，其在实际物理环境中的泛化能力和实时性有待考证。
*   **依赖在线交互**：作为一个在线安全RL算法，其训练样本效率可能较低，且仍需通过与环境的交互探索来学习安全策略，在探索阶段存在发生安全事故的风险。
*   **C/A比率需手动设定**：尽管算法对C/A比率具有一定鲁棒性，但此关键参数仍需根据任务进行经验性调整，并非完全自适应。

（完）
