# DigiRL: Training In-The-Wild Device-Control Agents with Autonomous Reinforcement Learning

## 思维导图
![思维导图](/imgs/DigiRL-Training-In-The-Wild-Device-Control-Agents-with-Autonomous-Reinforcement-Learning.jpg)

## 全文总结
“DigiRL: Training In-The-Wild Device-Control Agents with Autonomous Reinforcement Learning” 介绍了一种名为 DigiRL 的新型自主强化学习方法，用于训练野外设备控制智能体。该方法通过微调预训练的视觉语言模型（VLM），在两个阶段进行训练：离线强化学习初始化模型，然后进行离线到在线强化学习。
### 1.研究背景
视觉语言模型在常识、推理和泛化能力方面取得进展，但在设备控制任务中仍存在不足。  

现有方法如构建复杂包装器或使用静态演示进行微调，效果有限。  

### 2.问题设定与准备
研究基于安卓设备的像素级交互控制，任务包括信息收集和网络购物等。  
现实设备控制存在网站和应用的非平稳性、不可预测的干扰因素以及技术挑战等随机性问题。  
为实现可靠和可扩展的在线强化学习，构建了可并行化的安卓学习环境和基于 VLM 的通用评估器。  
### 3.DigiRL 方法
将设备控制问题建模为马尔可夫决策过程（MDP），基于优势加权回归（AWR）算法进行改进。
通过双鲁棒估计器获得可靠的优势估计，以应对环境随机性。
使用指令级价值函数自动课程学习，优先选择最有信息的任务进行训练，以提高学习效果。
实验评估
与多种现有方法进行比较，包括基于专有 VLM 的智能体、模仿学习方法和过滤行为克隆方法等。
DigiRL 在安卓设备控制任务上显著优于现有方法，成功率提高了 49.5%。
对 DigiRL 的各个组件进行消融实验，证明了所有组件的必要性。
贡献与局限
提出的 DigiRL 方法为设备控制问题建立了新的最先进性能。
由于计算限制，智能体仅在 AitW 数据集的部分任务上进行训练。
