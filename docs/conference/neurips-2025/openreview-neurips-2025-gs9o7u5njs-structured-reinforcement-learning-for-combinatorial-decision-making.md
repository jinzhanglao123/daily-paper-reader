---
title: Structured Reinforcement Learning for Combinatorial Decision-Making
title_zh: 面向组合决策的结构化强化学习
authors: "Heiko Hoppe, Léo Baty, Louis Bouvier, Axel Parmentier, Maximilian Schiffer"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GS9o7u5njS"
tags: ["query:uav-drl"]
score: 4.0
evidence: 解决具有组合动作空间的强化学习，一种与混合动作空间需求相关的结构化动作空间
tldr: 针对标准强化学习在组合动作空间中难以扩展和利用结构的问题，提出结构化强化学习（SRL），将组合优化层嵌入行动者网络并通过Fenchel-Young损失端到端训练。在六个具有不同不确定性的环境中，SRL达到了与现有方法相当或更优的性能，为复杂动作空间决策提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1457, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1300, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1313, \"height\": 232, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1438, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1423, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1432, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1440, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gs9o7u5njs/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1425, \"height\": 630, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1190, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1034, \"height\": 618, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1276, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1174, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1236, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1463, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1344, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1362, \"height\": 618, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1159, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1070, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gs9o7u5njs/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1011, \"height\": 358, \"label\": \"Table\"}]"
motivation: 强化学习面临组合动作空间的扩展性和泛化挑战，标准算法难以利用问题结构。
method: 提出SRL框架，在Actor网络中嵌入组合优化层，通过Fenchel-Young损失实现端到端训练。
result: 在六个环境中，SRL性能与或优于现有方法，有效处理不确定性。
conclusion: SRL为组合决策问题提供了有前景的强化学习方案，通过嵌入优化层实现结构化探索。
---

## Abstract
Reinforcement learning (RL) is increasingly applied to real-world problems involving complex and structured decisions, such as routing, scheduling, and assortment planning. These settings challenge standard RL algorithms, which struggle to scale, generalize, and exploit structure in the presence of combinatorial action spaces. We propose Structured Reinforcement Learning (SRL), a novel actor-critic paradigm that embeds combinatorial optimization-layers into the actor neural network. We enable end-to-end learning of the actor via Fenchel-Young losses and provide a geometric interpretation of SRL as a primal-dual algorithm in the dual of the moment polytope. Across six environments with exogenous and endogenous uncertainty, SRL matches or surpasses the performance of unstructured RL and imitation learning on static tasks and improves over these baselines by up to 92\% on dynamic problems, with improved stability and convergence speed.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
* **核心问题**：强化学习（RL）应用于车辆路径、库存规划、机器调度等现实工业问题时，常常遇到**组合动作空间（Combinatorial MDPs）** 的挑战。标准 RL 算法难以在指数级大小的动作空间中有效探索、泛化和利用组合结构，导致训练不稳定、收敛缓慢。
* **整体含义**：提出**结构化强化学习（Structured Reinforcement Learning, SRL）**，将组合优化层嵌入 actor 网络，通过 Fenchel‑Young 损失实现端到端训练，使 agent 能够利用问题结构进行高效决策，从而在静态和动态环境中均取得显著性能提升，尤其在没有专家演示的动态场景下大幅超越现有方法。

## 2. 方法论
* **核心思想**：构建一个**组合优化增强的机器学习管道（COAML‑pipeline）** 作为 actor：神经统计模型 \(\phi_w\) 将状态 \(s\) 映射为评分向量 \(\theta\)，然后由组合优化层 \(f\)（如最短路径、调度、排序求解器）根据 \(\theta\) 选择最优动作 \(a = \arg\max_{\tilde{a}\in\mathcal{A}(s)} \langle\theta,\tilde{a}\rangle\)。
* **关键技术细节**：
    * **Fenchel‑Young 损失**：由于 \(f\) 是分段常数、梯度为零，SRL 使用 Fenchel‑Young 损失 \(L_\Omega(\theta;\hat{a}) = \Omega^*(\theta) + \Omega(\hat{a}) - \langle\theta,\hat{a}\rangle\) 来平滑优化。通过在评分向量上加高斯噪声 \(Z\sim\mathcal{N}(0,\varepsilon)\) 使损失可微，从而通过随机梯度下降更新 actor 参数。
    * **在线目标动作构造**：不依赖专家演示，而是利用 critic 构造局部目标动作 \(\hat{a}\)。具体做法：对评分 \(\theta\) 加扰动采样多个噪声 \(\eta\)，经组合层得到候选动作集合，再用 critic 评估的 Q 值进行 softmax 加权聚合：\(\hat{a} = \text{softmax}_{a'}\big(\frac{1}{\tau}Q_{\psi_\beta}(s,a')\big)\)。
    * **几何解释**：在静态情形下，SRL 可视为在矩多面体的对偶空间中一种基于采样的原‑对偶算法，通过采样步骤避免对 critic 的显式组合优化。
* **算法流程**：
    * 收集经验 → 采样状态转移。
    * 对当前评分 \(\theta\) 加高斯扰动生成多个候选动作，评价 Q 值后计算 softmax 目标动作 \(\hat{a}\)。
    * 用 Fenchel‑Young 损失更新 actor，用标准 TD 误差更新 critic。

## 3. 实验设计
* **环境与数据集**：
    * 静态环境：Warcraft 最短路径（WSPP）、单机调度（SMSP）、随机车辆调度（SVSP），均采用文献 [Dalle et al., 2022] 的标准实例。
    * 动态环境：动态车辆调度（DVSP）、动态品类优化（DAP）、网格世界最短路径（GSPP），涵盖外生与内生不确定性。
* **基准方法**：
    * 结构化模仿学习（SIL）：使用专家状态‑动作对训练 COAML‑pipeline。
    * 无结构 RL（PPO）：将组合层视为环境的一部分，对评分向量加扰动后直接用 PPO 优化。
    * 参照：专家策略和贪心策略。
* **评估指标**：最终模型在训练集和测试集上的奖励，训练过程中的验证奖励曲线、收敛速度和稳定性（标准差）。

## 4. 资源与算力
* 所有实验均在 **MacBook Air M3** 上运行，使用 Julia 语言实现。
* 训练时长因环境和算法而异：单个环境训练耗时约 3 分钟到 90 分钟，其中 SRL 通常训练时间更长（例如 DVSP 约 31 分钟），因其需多次调用组合优化层。未使用 GPU 加速。
* 没有提到使用大规模集群或高算力 GPU。

## 5. 实验数量与充分性
* **实验规模**：在 6 个不同性质的组合决策环境中评估，每个环境均包含训练、验证、测试数据的划分。
* **重复次数与统计**：所有算法均使用 10 个不同的随机种子重复训练，结果以箱线图展示分布，并报告均值和标准差，统计可信度高。
* **公平性**：SRL 与对比方法均使用相同的 COAML‑pipeline 结构和 critic 架构（PPO 亦用相同 critic）；超参数通过网格搜索独立调优，并利用 PPO 的 episode 数统一设置，使对比公平。
* **消融/补充**：论文未进行消融实验，但通过静态和动态、外生/内生不确定性的多样场景，有效验证了方法的普适性。实验充分性较好。

## 6. 主要结论与发现
* SRL 在静态任务中性能与 SIL 相当，均接近专家策略；在动态任务中性能显著优于 SIL（最高 78%）和 PPO（最高 92%），尤其在 GSPP 中甚至超越在线最优策略。
* SRL 收敛更稳定，方差显著低于 PPO（约 1/80），且收敛速度比 PPO 更快。
* 结构化方法（SIL 和 SRL）普遍比无结构 PPO 更稳定高效，证明嵌入组合优化层的优势。
* SRL 无需专家演示，仅凭交互经验即能学得高质量策略，拓展了 COAML 的适用范围。

## 7. 优点
* **新颖的算法框架**：将 Fenchel‑Young 损失、组合优化层与在线 RL 结合，解决了组合空间中的端到端学习难题。
* **无需专家演示**：SRL 通过 critic 自动生成目标动作，克服了 SIL 依赖专家数据、无法探索非专家状态的问题。
* **理论与几何解释**：将算法解释为原‑对偶方法，加深了对结构化 RL 训练动力的理解。
* **实验全面**：覆盖静态/动态、外生/内生不确定性，比较了强基线，展示了 SRL 在缺少专家时的独特优势。

## 8. 不足与局限
* **计算开销较高**：由于需多次调用组合求解器，SRL 的训练时间显著高于 SIL 和 PPO，尤其当组合层复杂时。
* **对 critic 质量敏感**：目标动作 \(\hat{a}\) 依赖 critic 的准确性，在 critic 难以学习的复杂任务中可能影响性能。
* **未与其他 RL 范式对比**：仅与 PPO（同管道）和 SIL 对比，未涉及基于值函数分解或直接优化 Q 网络的动作选择方法（如 [Xu et al., 2025]），也未比较神经组合优化方法（如 attention‑based 模型）。
* **环境规模有限**：实验中的状态和动作维数尚属中等（如车辆调度 25 个任务），更大规模问题的扩展性未验证。

（完）
