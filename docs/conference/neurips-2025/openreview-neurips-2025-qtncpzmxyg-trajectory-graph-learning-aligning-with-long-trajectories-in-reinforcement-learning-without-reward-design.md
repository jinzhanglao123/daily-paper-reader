---
title: "Trajectory Graph Learning: Aligning with Long Trajectories in Reinforcement Learning Without Reward Design"
title_zh: 轨迹图学习：无需奖励设计的长时序轨迹对齐强化学习
authors: "Yunfan Li, Eric Liu, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=QtnCPZMxYg"
tags: ["query:uav-drl"]
score: 7.0
evidence: 直接解决强化学习中长时序对齐问题，无需奖励设计，保持长轨迹连贯性。
tldr: 针对长时序强化学习中奖励函数设计困难且易引发奖励黑客问题，本文提出轨迹图学习，利用专家演示直接将策略与长轨迹对齐，通过图结构保持状态间长时序连贯性，无需显式奖励建模。实验表明，该方法在多个长时序任务上比逆强化学习和偏好学习取得更高回报，并更好地保持任务长时序特性，为长距离信用分配提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-qtncpzmxyg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 926, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qtncpzmxyg/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1133, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qtncpzmxyg/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 953, \"label\": \"Table\"}]"
motivation: 人工设计奖励函数困难，尤其长时序任务易导致子优行为及奖励黑客问题，现有逆强化学习与偏好学习存在歧义与分布不匹配。
method: 提出轨迹图学习，利用专家演示直接对齐策略与长轨迹，图结构保持状态间的长时序连贯性，避免奖励建模。
result: 在多种长时序任务上，轨迹图学习方法比逆强化学习和偏好学习取得更高回报，并更好地保持任务的长时序特性。
conclusion: 轨迹图学习为长时序强化学习提供了一种无需奖励设计的高效范式，对长距离信用分配问题有重要启示。
---

## Abstract
Reinforcement learning (RL) often relies on manually designed reward functions, which are difficult to specify and can lead to issues such as reward hacking and suboptimal behavior. Alternatives like inverse RL and preference-based RL attempt to infer surrogate rewards from demonstrations or preferences but suffer from ambiguity and distribution mismatch. A more direct approach, inspired by imitation learning, avoids reward modeling by leveraging expert demonstrations. However, most existing methods align actions only at individual states, failing to capture the coherence of long-horizon trajectories.

In this work, we study the problem of directly aligning policies with expert-labeled trajectories to preserve long-horizon behavior without relying on reward signals. Specifically, we aim to learn a policy that maximizes the probability of generating the expert trajectories. Nevertheless, we prove that, in its general form, this trajectory alignment problem is NP-complete. 
To address this, we propose Trajectory Graph Learning (TGL), a framework that leverages structural assumptions commonly satisfied in practice—such as bounded realizability of expert trajectories or a tree-structured MDP. These enable a graph-based policy planning algorithm that computes optimal policies in polynomial time under known dynamics. For settings with unknown dynamics, we develop a sample-efficient algorithm based on UCB-style exploration and establish sub-linear regret. Experiments on grid-world tasks demonstrate that TGL substantially outperforms standard imitation learning methods for long-trajectory planning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机与背景**  
  强化学习（RL）的成功严重依赖人工设计的奖励函数，但手工奖励不仅设计困难，还容易引发“奖励黑客”和次优行为。  
  现有替代方法（如逆向强化学习、偏好式强化学习）通过演示或偏好推断替代奖励，却面临歧义、分布偏移、过拟合等问题。  
  模仿学习中的行为克隆（BC）虽然避免奖励建模，但仅对齐**单步状态-动作**，忽视了长序列轨迹的连贯性，导致累积误差。

- **核心问题**  
  本文研究**直接轨迹对齐**（Direct Trajectory Alignment）：**在不依赖任何奖励信号**的情况下，让策略最大化**完整生成专家标注轨迹**的概率。  
  论文首先证明该问题的一般形式是 **NP-完全** 的；进而提出 **轨迹图学习（Trajectory Graph Learning, TGL）** 框架，借助常见结构假设（专家轨迹有界可实现性、树形MDP）设计多项式时间算法，并在未知环境动态下给出具有次线性遗憾的在线学习算法。

### 2. 论文提出的方法论
- **核心思想**  
  将直接轨迹对齐问题规约为冲突图上的**最大权重独立集（MWIS）问题**：  
  - 每个专家轨迹为一个节点，权重为轨迹在环境中的实现概率乘积。  
  - 若两条轨迹在同一时间步处于相同状态但要求不同动作，则它们之间存在冲突（连边）。  
  - 最优策略等价于选取一个最大权重的无冲突轨迹子集，并按其动作执行。

- **已知模型下的算法**  
  - **TGL‑CP（冲突规划器）**：建图后调用 MWIS 预言机（例如穷举法，在 ε0‑可实现条件下时间复杂度 O(M^2H + M^{⌊1/ε0⌋})）。  
  - **树形 MDP 下的 TGL‑PrunedTree**：利用树结构的“无后续交叉、无回访”特性，从叶子向根动态规划：对每个状态-动作对聚合权重，保留各状态下总权重最大的动作，在 O(H·M·|A|) 时间内得到最优策略。  

- **未知动态下的算法**  
  **TGL‑UCB**：  
  - 为每个轨迹节点维护经验实现概率 ^μ_i，并计算 UCB 值 u_i = ^μ_i + sqrt(3 log t / (2 T_i))。  
  - 每轮调用 MWIS 预言机选出 UCB 总和最大的独立集，执行对应策略，采样后更新统计量。  
  - 理论保证：期望累积遗憾为 O( (M^3 log K · Δ_max) / (Δ_min^2) )，即次线性遗憾。

### 3. 实验设计
- **环境**  
  修改版 4×4 Frozen Lake（洞不终止，目标+1，其余‑1，10% 随机转移），水平线 H=10，无奖励信号用于训练。
- **专家轨迹集合构造**  
  来自确定性专家（PPO 训练）与随机专家的不同比例混合，涵盖 14 种不同数量组合（如 15 确定性 + 5 随机、纯确定性、纯随机等）。
- **对比方法**  
  - TGL‑UCB（本方法）  
  - 行为克隆（BC，有监督学习，batch size 8，20 epochs）  
  - PPO 专家（提供确定性演示的策略）
- **评估指标**  
  **轨迹匹配概率**：10,000 次 rollout 中生成的整条轨迹恰好属于演示集的比例，并报告 95% 置信区间。

### 4. 资源与算力
- 计算平台：单个 Google Colab 实例，配备 NVIDIA T4（16 GB GPU RAM）。  
- 训练耗时：  
  - PPO 专家训练 50k 步约 1 分 20 秒；  
  - 一次 TGL‑UCB 运行（50 次迭代，20 个轨迹节点）约 45 秒；  
  - 三种方法评估共约 1 分 30 秒。  
- 大多数代码未利用 GPU 加速，CPU 亦可运行。

### 5. 实验数量与充分性
- 表 1 展示了 14 种不同演示组合下的匹配概率，每种组合均独立训练和评估，提供了置信区间。  
- 实验仅在一个小型离散网格世界（4×4 Frozen Lake）上开展，**未涉及连续控制、高维状态或更复杂的环境**。  
- 对比基线包括 BC 和 PPO 专家，比较方式公平，但**未进行消融实验**（如 UCb 参数、初始采样量对性能的影响），也未与历史条件 BC 或循环序列模型比较。  
- 因此，实验虽能初步验证方法的有效性，但**充分性和泛化性仍有待加强**。

### 6. 论文的主要结论与发现
- 直接轨迹对齐问题一般情形是 NP‑完全，揭示了其本质计算难度。  
- 通过结构假设（ε‑可实现性、树形 MDP）可将问题转化为可多项式时间求解的 MWIS，并在未知动态下通过 UCB 探索实现次线性遗憾的在线学习。  
- 在网格世界实验中，**TGL‑UCB 在所有演示组合下均达到或超越行为克隆**，尤其在演示稀缺或混合强烈时表现突出，且常超过 PPO 专家，表明直接对齐长轨迹比单步模仿更有效。

### 7. 优点
- **理论严谨性强**：给出了 NP‑完全性证明、多项式时间结构算法、以及未知动态下的遗憾界。  
- **问题转化巧妙**：将长轨迹对齐抽象为冲突图上的 MWIS，统一了规划和学习视角。  
- **结构化高效求解**：在树形 MDP 下给出了线性时间复杂度算法，为实际应用（如 LLM 文本生成、自动驾驶）提供了直观依据。  
- **无需奖励设计**：完全绕开奖励建模，直接针对轨迹级目标优化，减轻了人工设计负担。  
- **实验直观**：通过匹配概率这一直接指标衡量长程行为一致性，比单纯奖励比较更能反映对齐质量。

### 8. 不足与局限
- **实验范围狭窄**：仅在 4×4 离散迷宫中测试，未扩展到连续状态/动作空间或更复杂的任务（如机器人控制、语言生成）。  
- **对比不够全面**：未纳入历史条件 BC、Transformer 序列模型等更现代的模仿学习方法，无法凸显 TGL 的相对优势。  
- **计算瓶颈未缓解**：依赖求解 MWIS，尽管在小型图上可行，大规模时计算开销高，文中未提供近似求解或加速方法。  
- **理论假设较强**：多项式时间算法依赖 ε‑可实现性或严格树结构，实际环境中可能难以满足；UCB 遗憾分析基于组合多臂老虎机规约，gap 条件较强。  
- **评估单一**：仅用轨迹匹配概率评估，未考察策略在扰动、泛化到新初始分布等场景下的鲁棒性。  
- 数据构造中确定性专家轨迹本身无冲突，混合随机轨迹才产生冲突，实际应用中冲突模式可能更复杂。

（完）
