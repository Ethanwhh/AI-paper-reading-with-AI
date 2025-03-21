# You Only Look at Screens: Multimodal Chain-of-Action Agents

## 思维导图
![思维导图](/imgs/You-Only-Look-at-Screens-Multimodal-Chain-of-Action-Agents.jpg)

## 全文总结

论文 “You Only Look at Screens: Multimodal Chain-of-Action Agents” 由 Zhuosheng Zhang 和 Aston Zhang 撰写，旨在解决自主图形用户界面（GUI）代理在与用户界面交互时面临的挑战，提出了 Auto-GUI 及相关技术，在 AITW 基准测试上取得优异性能，为 GUI 自动化任务提供新方案。

### 1.研究背景与挑战

- 构建能在特定环境中进行任务规划、决策和执行的智能自主代理是人工智能的长期目标，大语言模型（LLMs）的出现为其带来机遇，但现有方法存在局限。

- 现有方法多依赖外部工具（如 OCR 和图标检测器）将环境解析为文本元素作为语言模型输入，导致推理效率低和错误传播风险，且多在沙盒环境下依赖特定 API 与环境交互，在第三方应用中 API 接口常不可用。

### 2.相关工作

- 语言代理：分为自主代理（如 AutoGPT、BabyAGI 等）和通信代理，本文关注自主代理，旨在辅助用户完成多步任务。

- 用自然语言进行 GUI 控制：LLMs 在构建自主 GUI 代理方面有潜力，但现有方法受限于沙盒设置，需将 GUI 状态和操作转换为文本格式，依赖环境解析和特定 API，存在推理效率和错误传播问题。

### 3.Auto-GUI 方法

- 问题形式化：给定用户指令，代理需通过多次交互完成任务，每个交互步骤提供截图，代理预测动作直至任务完成。

- 框架概述：Auto-GUI 是多模态代理，通过动作链（包括先前动作历史和未来动作计划）预测动作。模型架构包括编码、交互和解码三个阶段，分别获取视觉和语言特征、融合特征并生成动作预测。

- 坐标归一化：考虑六种动作类型，对点击和滚动动作的坐标进行归一化，以加速收敛和减少坐标歧义。

### 4.实验

- 数据集：使用 AITW 基准数据集，包含 715K 个情节、30K 条独特指令，涵盖应用操作、网页搜索和购物等多步任务，分为五个子集，按 80/10/10% 划分为训练、验证和测试集。

- 基线方法：包括基于上下文学习的 LLMs（如 Few-shot PaLM 2、ChatGPT 等）、微调的 LLMs（如 Llama - 2 - 7B）和专门的 GUI 代理（如行为克隆 BC）。

- 评估指标：主要指标是屏幕动作匹配得分，即正确动作数除以情节长度，还比较点击区域、滚动方向、动作类型和输入文本的准确性。

- 实现细节：采用编码器 - 解码器架构，在小、基、大三种设置下进行实验，用 FLAN - Alpaca 初始化模型权重，使用 BLIP - 2 获取视觉特征，训练 10 个 epoch，学习率为 1e - 4，最大输入序列长度 512，批大小 4，在 8 个 NVIDIA Tesla V100 32G GPU 上运行。

- 主要结果：Auto - GUI_unified 在所有基线方法中性能最佳，动作链和坐标归一化对整体性能有积极贡献，LLMs 的提示或微调技术相比多模态方法性能欠佳。

### 5.分析

按类别分析 Auto-GUI：Auto-GUI 平均动作类型准确率超 90%，但点击区域和滚动方向预测存在挑战，未来需提升对屏幕布局的理解能力。

与 ICL 按类别比较：ICL 方法（如 ChatGPT）预测动作类型有一定准确性，但在低级执行（如点击位置和滚动方向）表现差，Auto-GUI 利用多模态感知和动作链技术具有优势。

泛化能力：Auto-GUI 基于第一性原理设计，不依赖预定义内部 API，在不同子集上有不错表现，统一模型 Auto - GUI_unified 因训练数据覆盖广有应用潜力。

综合分析：BLIP - 2 视觉特征和 FLAN - Alpaca 语言模型权重性能较好；模型规模扩大对性能提升作用相对较小，本文主要关注基础和大型模型。
计算成本：Auto-GUI 能在不到一秒内推断动作，GPU 内存小于 10GB，推理速度比 Llama 2 快 10 倍以上。

### 6.结论与局限

- 提出 Auto-GUI 和动作链技术，在 AITW 上性能优异，能直接与屏幕交互，无需环境解析和特定 API，推理速度快。

- 局限在于未扩展到极大模型，实验仅在 AITW 数据集进行，未来需探索在其他数据集上的应用。
