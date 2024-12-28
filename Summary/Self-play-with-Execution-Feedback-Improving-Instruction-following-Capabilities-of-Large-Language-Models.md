# Self-play with Execution Feedback: Improving Instruction-following Capabilities of Large Language Models

## 思维导图
![思维导图](/imgs/Self-play-with-Execution-Feedback-Improving-Instruction-following-Capabilities-of-Large-Language-Models.jpg)

## 全文总结

Self-play with Execution Feedback: Improving Instruction-following Capabilities of Large Language Models 提出了 AUTOIF 方法，通过代码验证和执行反馈自动生成指令跟随训练数据，在多个模型和训练算法上取得显著效果，提升了大语言模型的指令跟随能力，同时探讨了相关实验结果、消融研究和分析，并提及方法的局限与伦理考虑。

### 1.研究背景

- 大语言模型的指令跟随能力至关重要，但目前增强该能力的方法存在局限。手动标注难以创建复杂多样的指令且难以规模化，行为模仿受限于源模型且数据可靠性无法保证。

- 因此需要一种可扩展且可靠的自动生成指令跟随训练数据的方法。

### 2.AUTOIF 方法

- 预备知识：定义指令跟随要求和可验证指令，AUTOIF 通过自我进化、拒绝采样和执行反馈合成数据，并整合自动化数据增强与质量验证过程。

- 指令增强与验证：手写单约束种子指令，用自指令策略扩充，让 LLM 为指令生成验证函数和测试用例，经交叉验证和回译验证确保指令和验证函数质量，得到过滤后的指令集。

- 查询增强与验证：为指令从 ShareGPT 选用户查询并扩充响应，用验证函数评估响应和查询质量，过滤后构建最终训练集。

- 训练策略：包括监督微调（SFT）、SFT + 离线直接偏好优化（Offline DPO）、SFT + 迭代在线 DPO，分别按不同目标函数对模型训练，以适应 AUTOIF 多方面监督并评估其有效性。

### 3.实验

- 实验设置：用 Qwen2 和 LLaMA3 系列模型，以 IFEval、FollowBench 等为基准，分强弱蒸馏和自对齐两种设置评估。

- 主要结果：AUTOIF 在各模型、配置和训练方法下显著提升指令跟随性能，如在 IFEval 中 Qwen2 - 72B 宽松指令准确率达 88.0%，LLaMA3 - 70B 达 90.4%。在线 DPO 比离线 DPO 好，大模型提升更明显，且未降低通用能力。

- 消融研究：强监督模型如 GPT - 4 蒸馏效果更好；提高指令验证函数通过率阈值可提升性能但减少数据量；AUTOIF 各组件都有效，交叉验证最重要，整体质量过滤协同作用强。

- 分析：少量 AUTOIF 生成数据就能使模型有不错表现，且数据量增加性能提升；AUTOIF 训练数据无污染；监督模型的编码能力影响数据合成质量和模型指令跟随能力。

### 4.结论、局限与伦理考虑

- 提出的 AUTOIF 方法有效提升指令跟随能力，有良好扩展性和泛化性。

- 局限在于未聚焦跨指令构建，未来可研究自动化和规模化跨指令任务。

- 方法虽尽力降低风险，但拒绝采样中恶意提示可能导致有害输出，应用时需遵循伦理并防范误用。
