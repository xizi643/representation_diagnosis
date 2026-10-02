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
\[
o_0^i
\rightarrow
h_t^i
\rightarrow
a_t^i
\rightarrow
\text{joint behaviour}.
\]
对其在MARL上进行扩展

## 实验流程

## 数据分析

## 结果展示

# 参考文献
[1] Ni, Tianwei, et al. "When do transformers shine in rl? decoupling memory from credit assignment." Advances in Neural Information Processing Systems 36 (2023): 50429-50452.
[2] Morad, Steven, et al. "Popgym: Benchmarking partially observable reinforcement learning." arXiv preprint arXiv:2303.01859 (2023).  Accepted by ICLR 2023
