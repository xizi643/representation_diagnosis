# representation_diagnosis
paper链接：
研究中心：在合作 MARL 中，网络如何形成并使用影响决策的情境区别；这些决策产生的联合经验，又如何影响后续表示与协作学习？
本研究聚焦于以下研究问题：
协作所需的信息，在什么经验和学习信号下形成怎样的内部表示；这些表示何时能够被去中心化策略有效读取；读取产生的联合行为，又如何促进或限制后续学习？
在 cooperative MARL 中，决策表示与联合策略如何共同演化；什么时候这种共同演化形成有效协作抽象，什么时候形成自我确认、难以纠正的失败表示？

基本assumption：Self-confirming representation failure：当前表示丢失了某个关键区别，因此策略采取了不会暴露该区别重要性的动作；后续数据缺少反例，TD 与辅助目标便继续认为当前表示足够。

## 实验目的
在多个训练 checkpoint 和受控的后续学习分支中进行分析。公共诊断历史与匹配数据实验帮助区分网络处理方式的变化和被测数据分布的变化。从相同 checkpoint 出发的干预分支，则检验改变候选表示或经验条件是否影响即时行为及后续适应。这些实验保留各算法所需的学习条件：公共数据用于诊断比较，而同策略算法的后续学习使用适当收集的 rollout。我们计划同时研究 QMIX 与 MAPPO，追踪局部 encoder 与记忆如何进入 utility 或 policy head，并分别检查集中训练组件。对比这两种范式，能够检验哪些模式在目标和数据使用方式不同的条件下仍然出现，哪些则依赖价值分解或 actor–critic 学习。这种比较不预设二者具有相同的失败机制，也不等同于证明结论适用于所有 MARL。

## 实验设计
受控任务：
delay cue: 在单agent RL 学习中，目前已有多项研究提出一个设计简单但是可受人工管控的任务，例如such as Passive T-Maze [1] and POPGym [2].
其基本流程是agent一开始看到一个关键信息 cue → 中间经过一段没有 cue 的过程 → 最后必须根据最开始的信息做选择。单agent上，上面的相关研究主要研究的是学习的策略是否能够记住提供的这个关键的历史提示
但是在MARL我们的本研究中，关心的是：What does a MARL agent represent, preserve, and use?
<img width="477" height="48" alt="image" src="https://github.com/user-attachments/assets/32712638-fb58-41a9-8507-3f90092e6d07" />

对其在MARL上进行扩展
t = 0    Agent 0: cue
         Agent 1: cue
              ↓
      delay + distractors
              ↓
hidden representations h_t^1, h_t^2
              ↓
        joint decision
              ↓
t = 0+d  team reward
其中d是dalay的时间长度

我们首先没有直接从 SMAC 开始，因为在复杂任务中，一旦性能下降，很难判断究竟是 exploration、credit assignment、coordination 还是 representation 本身的问题。因此我们先构造一个非常简单的 two-agent delayed-cue diagnostic task。  
在 episode 开始时，两个 agent 同时看到一个随机的 binary cue。这个 cue 随后消失，agent 经过若干带 distractor 的 delay steps，而且 delay 期间只能执行 wait action，避免通过 action history 携带 cue。最后两个 agent 必须根据最初看到的信息做联合决策；只有 joint action 正确才得到 team reward。  
这样我们知道理论上唯一需要保存的 task-relevant variable 就是 cue，因此可以沿时间直接 probe hidden representation，检查 cue 信息何时进入、能保持多久，以及最终是否真的被 policy 使用。之后再通过 neuron masking、perturbation 等 intervention 区分“representation 中能解码出来的信息”和“真正对行为有因果作用的信息”。最后再看这些规律是否能在 SMAC/SMACv2 中复现。

## 实验流程

## 数据分析

## 结果展示

# 参考文献
[1] Ni, Tianwei, et al. "When do transformers shine in rl? decoupling memory from credit assignment." Advances in Neural Information Processing Systems 36 (2023): 50429-50452.
[2] Morad, Steven, et al. "Popgym: Benchmarking partially observable reinforcement learning." arXiv preprint arXiv:2303.01859 (2023).  Accepted by ICLR 2023
