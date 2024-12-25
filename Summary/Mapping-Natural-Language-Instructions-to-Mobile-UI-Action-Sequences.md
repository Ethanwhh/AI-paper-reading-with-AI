# Mapping Natural Language Instructions to Mobile UI Action Sequences

## 思维导图
![思维导图](/imgs/Mapping-Natural-Language-Instructions-to-Mobile-UI-Action-Sequences.jpg)

## 全文总结

“Mapping Natural Language Instructions to Mobile UI Action Sequences” 一文主要研究将自然语言指令映射到移动用户界面（UI）操作序列的问题，创建了新数据集并提出了模型架构，在相关任务上取得了一定成果。

### 1.研究背景与目标

- **背景**：在人机交互中，将自然语言指令转化为图形用户界面中的操作序列具有重要意义，尤其在辅助视障或行动不便用户方面。然而，现有的网络搜索虽能提供多步骤指令，但缺乏将其自动映射为设备可执行操作序列的能力。

- **目标**：构建能将自然语言指令转换为移动触摸屏 UI 上可自动执行的操作序列的计算模型，减少用户在操作 UI 时的细节处理，提高任务执行效率。
  
### 2.问题表述：

给定多步骤任务的指令，要在一系列用户界面屏幕上生成可自动执行的动作序列。动作包含操作、对象和参数，通过计算条件概率来确定最佳动作序列，该过程分为动作短语提取和 grounding 两个步骤，分别由和模型实现。

### 3.数据

- **PIXELHELP 数据集**：从 Pixel Phone 帮助页面提取可自动执行的多步骤指令，由标注人员在模拟器上执行并记录操作，包含 187 个指令，涉及 4 类任务，用于评估完整任务性能。

- **ANDROIDHOWTO 数据集**：通过网络爬虫获取 Android 操作指令，经标注人员筛选和标注动作描述跨度，有 32,436 个数据点，用于训练和评估动作短语提取模型。

- **RICOSCA 数据集**：基于 Rico 语料库合成操作 UI 元素的单步命令数据集，包含 295,476 个命令，用于训练 grounding 模型。

### 4.模型架构

- **短语元组提取模型**：基于 Transformer 架构，编码器对指令编码，解码器生成查询向量定位动作短语元组，考虑多种跨度表示方法，通过最小化 softmax 交叉熵损失训练。

- **grounding 模型**：将提取的短语元组连接到可执行动作，假设操作、对象和参数概率相互独立，分别用前馈神经网络和深度神经网络参数化，通过 Transformer 编码器对 UI 对象进行上下文表示，最小化交叉熵损失训练。

### 5.实验

- **数据集和指标**：使用完全匹配和部分匹配指标，在 ANDROIDHOWTO 和 RICOSCA 上训练验证，在 PIXELHELP 上评估。

- **模型配置和结果**：在动作短语提取任务中，Area Attention 等跨度表示方法表现良好；在 grounding 任务中，Transformer 屏幕编码器效果最佳，相比基于图卷积网络的方法，其在完全匹配和部分匹配上的准确率更高。

- **分析**：分析指令中位置词与 UI 屏幕实际位置的相关性，发现部分位置词相关性明显，但存在模糊区域；探讨了短语提取错误对 grounding 模型的影响，以及不同数据集语言风格差异导致的错误原因。

### 6.研究贡献与局限

- **贡献**：提出新问题并创建数据集，模型在任务上取得一定准确率，为后续研究奠定基础，分解问题的方式有助于分别改进各部分性能。

- **局限**：仍有提升空间，如从无配对数据学习时使用隐藏状态进行 grounding 存在挑战，不同数据集语言风格差异导致的错误有待解决。