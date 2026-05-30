---
title: Minimax Optimal Regret Bound for Reinforcement Learning with Trajectory Feedback
title_zh: 轨迹反馈强化学习的极小极大最优遗憾界
authors: "Zihan Zhang, Yuxin Chen, Jason D. Lee, Simon Shaolei Du, Ruosong Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oOAICE3sY7"
tags: ["query:uav-drl"]
score: 7.0
evidence: 专注射程反馈强化学习，仅观测累积奖励，直接应对长周期信用分配
tldr: 该文针对强化学习中仅可观测轨迹累积奖励的长周期场景，提出一种面向有限期MDP的新算法。通过构建更紧的置信区间并融合轨迹反馈信息，算法在K轮学习后达到~O(√(SAH^3K))的近似极小极大最优遗憾。理论分析证明了其在轨迹反馈设置下的高效性，为长周期间奖励分配提供了坚实的理论基础与实用工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ooaice3sy7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 855, \"height\": 319, \"label\": \"Table\"}]"
motivation: 解决长周期任务中单步奖励查询代价过高或不可得时，仅凭轨迹累积奖励进行策略学习的困难。
method: 设计一种针对有限期MDP的算法，通过构造更紧的奖励函数置信区间并巧妙利用轨迹级反馈，实现极小极大最优遗憾。
result: 证明了在含S状态、A动作、H步长的MDP中，算法在K轮交互后达到~O(√(SAH^3K))的遗憾界，接近理论最优。
conclusion: 为仅靠轨迹累积反馈的RL提供了首个近似最优算法，对需要长期奖励分配的现实应用具有重要参考价值。
---

## Abstract
In this work, we study reinforcement learning (RL) with trajectory feedback. 
Compared to the standard RL setting, in RL with trajectory feedback, the agent only observes the accumulative reward along the trajectory, and therefore, this model is particularly suitable for scenarios where querying the reward in each single step incurs prohibitive cost. 
For a finite-horizon Markov Decision Process (MDP) with $S$ states, $A$ actions and a horizon length of $H$, we develop an algorithm that enjoys an asymptotically nearly optimal regret of $\tilde{O}\left(\sqrt{SAH^3K}\right)$ in $K$ episodes.
To achieve this result, our new technical ingredients include
(i) constructing a tighter confidence region for the reward function by incorporating the RL with trajectory feedback setting with techniques in linear bandits and 
 (ii) constructing a reference transition model to better guide the exploration process.

---

## 论文详细总结（自动生成）

（以下是为您生成的论文总结，基于提供的PDF文本内容，严格遵循您指定的八个要点进行组织。）

---

# 论文总结：轨迹反馈强化学习的极小极大最优遗憾界

## 1. 论文的核心问题与整体含义

- **研究背景**：在标准的强化学习（RL）中，智能体每执行一个动作就能立即收到即时奖励信号。然而，在许多现实应用中（如医疗、自动驾驶），精确估计每一步的即时奖励极其昂贵甚至不可行，而只能在整条轨迹结束后获得一个**累积奖励**的总值。
- **核心问题**：这种“**轨迹反馈**”（Trajectory Feedback）下的RL是否比标准RL在统计难度上更困难？能否达到与标准RL相同的、关于状态数$S$、动作数$A$、视界长度$H$和回合数$K$的**极小极大最优遗憾界** $\tilde{O}(\sqrt{SAH^3K})$？
- **整体含义**：本文首次证明了在轨迹反馈的RL中，可以设计算法实现与标准RL**相同**的渐近最优遗憾界，从理论上说明轨迹反馈的RL在统计上并不比标准RL更难。这为部分可观测奖励的现实场景提供了强有力的理论支撑。

## 2. 论文提出的方法论

### 2.1 核心思想
- 将轨迹反馈RL的奖励学习问题建模为**线性老虎机**（Linear Bandit）问题，但利用轨迹分布的结构（轨迹数量远小于策略数量，且状态占用度是轨迹特征向量的凸组合）**构造更紧的置信区间**，突破以往工作中对状态数$S$的次优依赖。
- 结合**基于模型消除的策略淘汰框架**（Policy Elimination），分批淘汰次优策略，并利用**参考模型**引导探索，从而高效学习未知的转移核。

### 2.2 关键技术细节与算法流程
- **更紧的轨迹级置信区间**：不直接对每个策略$(d^\pi_P)^\top (\hat{R} - R)$做联合界，而是对所有轨迹$\tau \in \mathcal{T}$构造事件：
  \[
  \mathcal{E} := \left\{ \forall \tau, \; |\phi_\tau^\top (\hat{R} - R)| \le c \cdot \min\left( \sqrt{\phi_\tau^\top \Lambda^{-1} \phi_\tau \sigma^2 \log(|\mathcal{T}|/\delta)}, H \right) \right\}
  \]
  再利用轨迹概率的凸组合性质，通过柯西‑施瓦茨不等式得到对任意策略$\pi$的奖励估计误差上界：
  \[
  |(d^\pi_P)^\top (\hat{R} - R)| \le \tilde{O}\left( H \sqrt{\sum_{\tau} \Pr^{\pi,P}[\tau] \min\{ \phi_\tau^\top \Lambda^{-1}\phi_\tau, 1\}} \right).
  \]

- **基于最优设计的探索策略**：为了最小化上述上界，需要最小化 $\max_{\pi \in \Pi} \sum_\tau \Pr^{\pi,P}[\tau]\phi_\tau^\top \Lambda^{-1}\phi_\tau$。作者推广了经典的 Kiefer‑Wolfowitz 定理，证明存在一个混合策略$\bar{\pi}$满足：
  \[
  \max_{\pi \in \Pi} \sum_{\tau} \Pr^{\pi,P}[\tau] \phi_\tau^\top (\Lambda_{\bar{\pi}})^{-1} \phi_\tau = SAH,
  \]
  其中$\Lambda_{\bar{\pi}} = \sum_\tau \Pr^{\bar{\pi},P}[\tau]\phi_\tau \phi_\tau^\top$。运行该探索策略$T$步后，即可将奖励估计误差控制在 $\tilde{O}(\sqrt{SAH^3/T})$。

- **分批策略淘汰（Algorithm 1，5）**：
  1. **第一阶段**（Ref‑Model）：利用Raw‑Exploration学习一个关于转移核的**粗近似模型** $\tilde{P}$（为$(3, \sigma_0)$‑近似），并初步淘汰掉明显次优的策略，得到策略集$\Pi_1$。
  2. **第二阶段**（Traj‑Learning）：分$L = O(\log\log K)$个批次，每一批$\ell$内：
     - **奖励回归**（Reward‑Regression）：基于当前策略集$\Pi_\ell$和参考模型$\tilde{P}$，通过最优设计找到探索策略$\bar{\pi}$，收集$K_\ell$条轨迹和累积奖励，使用岭回归（LSR）得到奖励估计$\hat{R}_\ell$。
     - **策略淘汰**（Plan）：根据$\hat{R}_\ell$和从$\bar{\pi}$样本中估计的经验转移核$\hat{P}$，计算每个策略的乐观值，淘汰掉满足 $W^\pi(\hat{R}_\ell, \hat{P}) < \max_{\pi'} W^{\pi'}(\hat{R}_\ell, \hat{P}) - \epsilon_\ell$ 的策略，形成$\Pi_{\ell+1}$。
  3. **最终遗憾界**：由于每批策略的次优性均被控制在$\epsilon_\ell = \tilde{O}(\sqrt{SAH^3/K_\ell})$，且批长度$K_\ell$呈指数增长，总遗憾被证明为 $\tilde{O}(\sqrt{SAH^3K} + \text{低阶项})$。

## 3. 实验设计
- **本文为纯理论论文**，未进行数值模拟或真实数据实验。所有结果均以定理、引理的形式给出，并通过严格的概率不等式进行证明。文中未涉及基准对比、数据集或实验设置。

## 4. 资源与算力
- 由于本文没有数据实验，**未提及任何计算资源**（GPU型号、数量、训练时间等）。理论算法的时间复杂度极高（需要维护指数级大小的确定性策略集合），因此作者明确指出所提算法**非计算高效**，其贡献在于统计效率（遗憾界）的最优性。

## 5. 实验数量与充分性
- 本文**未进行实验**，因此不存在实验数量、充分性、客观性或公平性的讨论。所有结论仅依赖于理论证明。

## 6. 论文的主要结论与发现
- **主定理（Theorem 5.6）**：针对任意有限视界MDP与轨迹反馈，所提算法（Algorithm 1）以概率$1-\delta$达到遗憾界
  \[
  \tilde{O}\left( \sqrt{SAH^3K} + \sqrt{S^3A^2H^3}K^{3/8} + \sqrt{S^{11}A^3H^{19}}K^{1/4} + \sqrt{S^{17}A^3H^{27}} \right),
  \]
  当$K\to\infty$时主导项为$\tilde{O}(\sqrt{SAH^3K})$，这是**渐近极小极大最优**的。
- **重要推论**：即使在只接收累积轨迹奖励的条件下，RL的统计难度也未增加，与拥有逐步奖励的标准RL享有相同的最优遗憾率。
- 技术核心在于两方面的创新：（i）利用轨迹层面的信息构造更紧的奖励置信区间；（ii）通过参考模型引导探索，实现与线性老虎机中G 最优设计的无缝衔接。

## 7. 优点
- **理论突破**：首次在轨迹反馈RL中实现了最优遗憾界，填补了该领域的理论空白。
- **方法普适**：将线性老虎机和最优设计技术创造性地融入轨迹反馈建模，为后续研究提供了新的分析工具（如推广的Kiefer‑Wolfowitz定理，Lemma B.2）。
- **严格的数学证明**：算法描述与证明层次清晰，误差界限显式依赖于所有结构参数（$S,A,H,K$），置信度高。

## 8. 不足与局限
- **计算不可行**：算法依赖维护所有确定性策略的集合（大小可达$A^{SH}$）并在其上求解优化问题，运行时间随$S$和$H$指数增长，**无法应用于任何中等规模以上的问题**。
- **仅统计最优**：理论仅关注$K\to\infty$时的渐近行为，低阶项可能在实际有限$K$下占据主导，且未提供数值验证来展示实用效果。
- **模型假设理想化**：假设MDP是表格型的（Tabular），且奖励分布为$[0,1]$有界独立噪声，对更复杂的函数逼近、对抗噪声或偏好反馈场景的扩展有待研究。
- **缺少数值证据**：作为纯理论工作，缺乏仿真或实验，使得结论的可视化和直观理解稍显不足。

---

（完）
