---
title: "Divide and Conquer: Grounding LLMs as Efficient Decision-Making Agents via Offline Hierarchical Reinforcement Learning"
title_zh: 分而治之：通过离线分层强化学习将大语言模型落地为高效决策智能体
authors: "Zican Hu, Wei Liu, Xiaoye Qu, Xiangyu Yue, Chunlin Chen, Zhi Wang, Yu Cheng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=pdNtji3ktF"
tags: ["query:uav-drl"]
score: 9.0
evidence: 采用分层强化学习解决稀疏奖励场景下的长时域决策与长期信用分配问题
tldr: 大语言模型在长时域决策任务中常受限于探索不足与长期信用分配困难，尤其在稀疏奖励环境下。本文提出GLIDER框架，通过离线分层强化学习为LLM策略引入高效的分层结构：高层策略学习分解任务，低层策略执行具体行动，从而将长时域信用分配转化为多层子目标学习。实验表明，该方法在多个基准测试中显著优于现有方法，证明了层次化设计对解决稀疏奖励长时域决策的有效性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pdntji3ktf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 742, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pdntji3ktf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1747, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pdntji3ktf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pdntji3ktf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 866, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pdntji3ktf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 476, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pdntji3ktf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1680, \"height\": 829, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pdntji3ktf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pdntji3ktf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pdntji3ktf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1418, \"height\": 1139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pdntji3ktf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1229, \"height\": 606, \"label\": \"Table\"}]"
motivation: 长时域稀疏奖励下LLM决策的探索与信用分配挑战严重制约性能。
method: 提出GLIDER框架，通过离线分层强化学习构造高层规划与低层执行策略，将长任务分解为子任务序列。
result: 在多个长时域决策基准上，GLIDER显著提升样本效率，超越现有LLM决策方法。
conclusion: 分层结构有效缓解了长时域信用分配，为LLM在真实世界序列决策中的应用提供了可行路径。
---

## Abstract
While showing sophisticated reasoning abilities, large language models (LLMs) still struggle with long-horizon decision-making tasks due to deficient exploration and long-term credit assignment, especially in sparse-reward scenarios. Inspired by the divide-and-conquer principle, we propose an innovative framework **GLIDER** (**G**rounding **L**anguage Models as Eff**I**cient **D**ecision-Making Agents via Offline Hi**E**rarchical **R**einforcement Learning) that introduces a parameter-efficient and generally applicable hierarchy to LLM policies. We develop a scheme where the low-level controller is supervised with abstract, step-by-step plans that are learned and instructed by the high-level policy. This design decomposes complicated problems into a series of coherent chain-of-thought reasoning sub-tasks, providing flexible temporal abstraction to significantly enhance exploration and learning for long-horizon tasks. Furthermore, GLIDER facilitates fast online adaptation to non-stationary environments owing to the strong transferability of its task-agnostic low-level skills. Experiments on ScienceWorld and ALFWorld benchmarks show that GLIDER achieves consistent performance gains, along with enhanced generalization capabilities.

---

## 论文详细总结（自动生成）

好的，请查收以下基于您提供的论文内容生成的结构化中文总结。

### **1. 论文的核心问题与整体含义**

*   **核心问题**：大型语言模型（LLMs）在长时域（long-horizon）决策任务中表现不佳，尤其是在奖励稀疏（sparse-reward）的环境下。其根本挑战在于：
    *   **探索不足（Deficient Exploration）**：由于动作空间巨大，LLM难以有效探索环境。
    *   **长期信用分配困难（Difficult Long-Term Credit Assignment）**：模型很难将最终的成功或失败归因到很久以前的某个具体行动上。
*   **整体含义**：论文旨在通过“分而治之”的思路，将复杂的长时域任务分解为一系列更容易解决的子任务，从而克服上述挑战，将LLM落地为更高效的决策智能体。

### **2. 论文提出的方法论**

*   **核心思想**：提出**GLIDER**框架，通过**离线分层强化学习（Offline Hierarchical RL）**，为LLM智能体引入一种参数高效且通用性强的层级结构。
*   **关键技术细节与架构**:
    *   **双层策略结构**：设计一个高层策略（High-level Policy)和一个低层策略（Low-level Policy）。两个策略共享同一个LLM骨干网络，仅通过不同的提示（Prompts）来区分角色，实现参数高效。
    *   **高层规划器**：以较粗的时间粒度（每`c`步）运行。它接收任务描述和当前环境状态，生成一个抽象的子目标/子任务。
    *   **低层执行器**：接收高层规划器设定的子目标，以原始动作与环境交互，逐步完成该子目标。
    *   **奖励机制**：
        *   **低层内在奖励**：由高层策略提供，指示子任务是否完成（完成为1，否则为0）。
        *   **高层环境奖励**：累积低层执行`c`步期间从环境中获得的总奖励。
*   **训练流程（三阶段）**:
    1.  **行为克隆（SFT）**: 利用专家演示数据集，通过监督学习（最大化对数似然）对高层和低层Actor进行初步训练，构建一个基础智能体（Base Agent）。
    2.  **离线强化学习（ORL）**: 在奖励标注的数据集上，进一步训练分层Actor-Critic模型。Actor在Token级别生成动作，Critic在句子级别评估策略。
        *   **Critic更新**: 使用时序差分（TD）学习训练Q函数和V函数，并采用不对称损失（expectile loss）来防止价值估计过于乐观。
        *   **Actor更新**: 采用类似AWAC算法的优势加权回归（Advantage-Weighted Regression）方法，将策略优化转化为加权最大似然估计问题，以此约束策略更新，减轻分布偏移。
    3.  **离线到在线自适应（O2O）**: 面对新任务时，冻结具有高度泛化能力的低层技能，仅在线微调高层策略，从而快速适应非平稳环境。

### **3. 实验设计**

*   **数据集/场景**：
    *   **ScienceWorld**: 一个模拟基础科学实验的文本环境，包含30个任务，提供稠密奖励。
    *   **ALFWorld**: 一个模拟家庭操作的文本环境，包含6类任务，提供稀疏的二值奖励（成功为1，否则为0）。
    *   两个benchmark均设有“已见任务（Seen）”和“未见任务（Unseen）”测试集，以评估泛化能力。
*   **对比的基准方法（Baselines）**:
    *   **基于提示的方法**: ReAct, Reflexion, SwiftSage。
    *   **基于微调的方法**: NAT, ETO。
*   **LLM骨干网络**: 使用 Mistral-7B, Gemma-7B, Llama-3-8B 三种不同基座模型进行实验，以验证方法的鲁棒性。

### **4. 资源与算力**

*   论文原文**未明确提及**具体使用的GPU型号、数量及详细的训练时长等算力信息。文中仅在附录中提到了相关的超参数，如批量大小、学习率等，但未描述硬件配置。

### **5. 实验数量与充分性**

*   **实验数量充足且全面**：大概做了以下几组主要实验，覆盖了有效性验证、组件贡献分析、泛化能力测试等维度。
    *   **主实验**：在3种LLM骨干网络（Mistral-7B, Gemma-7B, Llama-3-8B）和2个基准（ScienceWorld, ALFWorld）上与5种基准方法进行对比。
    *   **消融研究**：
        *   从**模型结构**上消融层级设计，对比有无层级的性能。
        *   从**训练阶段**上消融，对比仅SFT、仅ORL、SFT+ORL的性能。
        *   从**模型规模**上消融，测试Llama-1B, 3B, 8B不同规模下的框架效果。
    *   **泛化性分析**：通过离线到在线（O2O）微调实验，在未见过的任务上对比GLIDER与AC、AWAC算法的快速适应能力。
    *   **数据混合比例分析**：研究训练数据中专家轨迹与中等质量轨迹不同混合比例对模型性能的影响。
*   **实验客观性与公平性**：实验设计较为公平，对比了同类最先进的提示方法和微调方法，并更换多种不同基座LLM来消除模型偏差。多角度的消融实验也充分验证了每个设计的有效性。

### **6. 论文的主要结论与发现**

*   GLIDER在所有主实验中均取得**一致性的性能提升**，显著超越所有对比的基线方法。
*   **层级结构至关重要**：无论是SFT还是ORL阶段，使用层级结构的模型性能都优于非层级模型，尤其是在SFT和ORL结合使用时优势最大。
*   **RL优于BC**：从零开始使用离线RL训练（ORL）的智能体性能优于仅用监督学习（SFT）的智能体，而结合两者效果最佳。
*   **泛化能力强**：GLIDER不仅在未见过的任务上表现优异（零样本泛化），还能通过O2O微调**快速适应新任务**，证明了其低层技能的高度可迁移性。
*   **数据效率高**：通过RL，智能体能够从次优数据中学习并自我进化，数据质量和多样性对构建强大智能体都至关重要。该方法甚至在较小参数规模的模型（如Llama-3B）上也能超越更大规模模型（如Mistral-7B）的性能。
*   **奖励设置有效**：论文指出，高层策略受环境奖励引导，低层策略受高层提供的子任务完成信号（从环境观测中获取）监督，整个过程**无需人工设计或领域知识**，具有广泛的适用性。

### **7. 优点**

*   **方法创新性**：将“分而治之”的层级思想巧妙地应用于LLM决策，通过高层规划与低层执行的解耦，有效应对了长时域和稀疏奖励挑战。
*   **参数效率高**：高、低层策略共享LLM骨干网络，仅通过LoRA和不同提示进行微调和区分，大大减少了参数量，优于需要独立训练多层模型的传统分层RL方法。
*   **设计通用性强**：奖励信号的设计从任务环境中自动获取，无需人工定义，使得该框架易于迁移到不同领域的任务。
*   **实验严谨扎实**：跨多个模型、多个基准的对比，加上多维度的消融实验，为结论提供了强有力的证据。
*   **泛化与适应能力出色**：通过离线预训练获得可迁移的低层技能，实现了在新任务上的零样本泛化和快速在线适应，具有重要的应用价值。

### **8. 不足与局限**

*   **训练流程复杂**：多阶段（SFT -> ORL -> O2O）的训练流程较为繁琐，论文自身也指出未来可简化。
*   **专家演示依赖**：尽管证明了RL可从非最优数据学习，但第一阶段的行为克隆仍然依赖于专家演示数据，构建此类数据成本高昂。
*   **应用领域局限**：实验目前仅限于文本交互环境（ScienceWorld, ALFWorld），其在更复杂的真实世界机器人操作或多模态任务上的效果有待验证。
*   **算力成本不透明**：论文未报告训练所需的算力资源，使得其他研究者难以估算复现的成本和门槛。

（完）
