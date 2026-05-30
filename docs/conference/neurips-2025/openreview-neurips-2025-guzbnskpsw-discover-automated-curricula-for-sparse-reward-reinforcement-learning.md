---
title: "DISCOVER: Automated Curricula for Sparse-Reward Reinforcement Learning"
title_zh: DISCOVER：稀疏奖励强化学习的自动课程
authors: "Leander Diaz-Bone, Marco Bagatella, Jonas Hübotter, Andreas Krause"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=guZBnsKPsw"
tags: ["query:uav-drl"]
score: 9.0
evidence: 通过自动课程解决稀疏奖励强化学习中的长时序功劳分配，可直接应用于无人机巡检
tldr: 针对稀疏奖励强化学习中高效探索与长时序功劳分配的挑战，提出DISCOVER方法，从现有强化学习算法中提取方向信息，自动生成相关简化任务课程引导探索，在复杂高维长时域任务上显著提升学习效率，为自提升智能体奠定基础。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1306, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1455, \"height\": 884, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1429, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 600, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 602, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 664, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1259, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 673, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1460, \"height\": 996, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1451, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1462, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 568, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1433, \"height\": 1196, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1432, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-guzbnskpsw/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1466, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-guzbnskpsw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1440, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-guzbnskpsw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 597, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-guzbnskpsw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1192, \"height\": 619, \"label\": \"Table\"}]"
motivation: 稀疏奖励任务需要高效探索和长时域功劳分配，但手动设计课程困难且难以扩展。
method: 提出DISCOVER，利用已有强化学习算法的方向信息自动构建相关简化任务课程，引导探索。
result: 在高维长时域任务上，DISCOVER有效提升了探索效率和最终性能。
conclusion: 自动课程学习能够显著改善稀疏奖励环境下的强化学习效率，为复杂任务提供可行路径。
---

## Abstract
Sparse-reward reinforcement learning (RL) can model a wide range of highly complex tasks.
Solving sparse-reward tasks is RL's core premise — requiring efficient exploration coupled with long-horizon credit assignment — and overcoming these challenges is key for building self-improving agents with superhuman ability.
We argue that solving complex and high-dimensional tasks requires solving simpler tasks that are *relevant* to the target task.
In contrast, most prior work designs strategies for selecting exploratory tasks with the objective of solving *any* task, making exploration of challenging high-dimensional, long-horizon tasks intractable.
We find that the sense of direction, necessary for effective exploration, can be extracted from existing reinforcement learning algorithms, without needing any prior information.
Based on this finding, we propose a method for _**di**rected **s**parse-reward goal-**co**nditioned **ve**ry long-horizon **R**L_ (DISCOVER), which selects exploratory goals in the direction of the target task.
We connect DISCOVER to principled exploration in bandits, formally bounding the time until the target task becomes achievable in terms of the agent's initial distance to the target, but independent of the volume of the space of all tasks.
Empirically, we perform a thorough evaluation in high-dimensional simulated environments. We find that the directed goal selection of DISCOVER solves exploration problems that are beyond the reach of prior state-of-the-art exploration methods in RL.

---

## 论文详细总结（自动生成）

好的，以下是根据论文《DISCOVER: Automated Curricula for Sparse-Reward Reinforcement Learning》生成的结构化中文总结。

### 1. 核心问题与整体含义
- **核心问题**：稀疏奖励强化学习任务中，由于智能体只有在完成任务后才获得奖励，导致高效探索和长时域信用分配极为困难。传统方法在高维、长时域任务中往往因无法获得奖励信号而失效。
- **整体含义**：论文认为，解决一个困难的最终任务需要先解决一系列与之**相关**且更简单的中间任务，从而习得必要技能。基于此，论文提出一种自动构建“课程”的方法，引导智能体从易到难、有方向性地探索，最终解决近乎不可能的复杂任务。

### 2. 方法论
#### 核心思想
提出 **DISCOVER**（Directed Sparse-reward Goal-Conditioned Very Long-horizon RL）目标选择策略，在每个探索回合从已达成目标集合 \( G_{\text{ach}} \) 中选择一个子目标，使其能够同时平衡三个原则：**可达性**（Achievability）、**新颖性**（Novelty）与**相关性**（Relevance）。

#### 关键技术细节
- **目标选择公式**：选择一个目标 \( g_t \) 最大化：
  \[
  g_t = \arg\max_{g \in G_{\text{ach}}} \left[ \alpha_t \big( V(s_0, g) + \beta_t \sigma(s_0, g) \big) + (1-\alpha_t) \big( V(g, g^\star) + \beta_t \sigma(g, g^\star) \big) \right]
  \]
  其中 \( V \) 和 \( \sigma \) 分别是价值网络集合的均值与标准差。\( V(s_0, g) \) 衡量从初始状态出发达成 \( g \) 的可达性，\( \sigma(s_0, g) \) 鼓励探索新颖区域；\( V(g, g^\star) \) 衡量子目标 \( g \) 与最终目标 \( g^\star \) 的相关性。
- **概率价值估计**：采用集成（ensemble）价值网络（默认6个）并通过成员间的不一致性来估计不确定性 \( \sigma \)。
- **在线参数自适应**：\( \alpha_t \) 和 \( \beta_t \) 根据近期目标达成率 \( p_t \) 与目标达成率 \( p^\star \)（设为50%）的偏差动态调整，以维持探索与利用的平衡。
- **理论联系**：将DISCOVER与上置信界（UCB）算法建立联系，证明在简化线性假设下，达到最终目标所需的回合数与目标空间的体积无关，仅线性依赖于初始状态到目标的“距离”。

### 3. 实验设计
#### 实验场景与基准
在三个稀疏奖励、长时域控制环境中评测：
- **点迷宫（Pointmaze）**：\( n \) 维超立方体导航任务，维度从2到6可变，评估高维探索能力。
- **蚁形迷宫（AntMaze）**：27维状态、8维动作的四足机器人迷宫导航。
- **机械臂（Arm）**：23维状态、5维动作的立方体操纵任务（可含障碍）。
每个环境均设有**简单**和**困难**两种配置（更长时序、更多障碍或更高维度）。

#### 对比方法
- **目标选择Baseline**：HER（始终选最终目标）、DISCERN（均匀随机选已达成目标）、MEGA（选低可能性的已达成目标）、Achievability + Novelty（仅DISCOVER的前两项）。
- **标准无子目标RL方法**：TD3、SAC、RND、SAC + MaxInfoRL（用于检验目标条件化的重要性）。

### 4. 资源与算力
- 所有实验在内部集群上进行，**每轮实验使用单块 NVIDIA GeForce RTX 2080 Ti GPU**。
- 单个最长实验运行时间约**50小时**，为复现所有实验需运行约**800次独立运行**，总计算量估计约**8000 GPU小时**。

### 5. 实验数量与充分性
- **主要对比实验**：在3个环境×2种难度共6个任务上，对DISCOVER与4种目标选择Baseline进行对比（共5×6=30组实验），全部使用10个随机种子并报告均值和标准误差。
- **高维扩展实验**：在点迷宫2到6维上测试，并与3种Baseline比较。
- **消融与深入分析**：包括在线参数自适应策略消融、固定\( \alpha \)与\( \beta \)值的影响、额外噪声下的鲁棒性测试、集成大小（2,4,6,8）的影响、利用先验知识（手工L2距离或预训练价值函数）的加速效果、各价值分项的视觉化分析等。
- **充分性与公平性**：实验覆盖多个复杂度和维度的环境，对比方法包含当前领先的子目标选择策略及标准RL探索算法，消融实验也较为全面。所有结果均报告标准差和种子数，基准使用原论文推荐设置，整体遵循公平原则。

### 6. 主要结论与发现
- DISCOVER在所有复杂控制任务中**始终优于**现有最先进的子目标选择策略，尤其在困难任务中性能提升显著。
- 无引导的探索策略在高维空间（>3维）中彻底失效，而DISCOVER能利用对最终目标的方向感**有效缩减搜索空间**，成功解至6维迷宫。
- DISCOVER的“方向感”完全从价值网络的自举估计中涌现，**无需任何外部先验知识**；若事先有预训练模型，则可进一步加速探索。
- 传统的基于好奇心或奖励塑形的非子目标选择RL算法**完全无法解决**实验中的长时域稀疏奖励任务，证明了有引导的子目标选择对深度探索至关重要。

### 7. 优点
- **新颖的探索范式**：首次在子目标选择中同时整合可达性、新颖性和对最终任务的相关性，平衡利用与探索。
- **理论与实证结合**：不仅提供了与多臂老虎机UCB的理论联系与收敛界，还在复杂高维连续控制任务上验证了显著优势。
- **高效的探索自举**：价值网络自行提炼出有用的距离度量，无需任何手工特征或奖励塑形，便于推广。
- **实验设计严谨**：对比全面，消融深入，代码开源，具有良好的可复现性。

### 8. 不足与局限
- **依赖值函数泛化**：方向估计完全依赖价值网络的泛化能力，当泛化较差时可能不可靠。
- **集成计算开销**：使用6个评论家网络估计不确定性，增加了约26%的训练时间，对大规模模型（如语言领域）可能带来较大负担。
- **环境内容受限**：实验限于标准导航与简单操作模拟环境，未在更大规模或不同模态（如图像、文本）任务中验证。
- **理论假设较强**：收敛性证明基于线性值函数、子目标空间测地凸性等简化假设，与实践环境存在差距。
- **仅从已达成目标中选择**：无法生成全新的、超出已达成区域的目标，在需要创造性突破的任务中可能受限于先前的经验。

（完）
