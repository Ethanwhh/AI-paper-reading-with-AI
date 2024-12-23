# GUICourse: From General Vision Language Models to Versatile GUI Agents

## 思维导图
![思维导图](/imgs/GUICourse-From-General-Vision-Language-Models-to-Versatile-GUI-Agents.jpg)

## 全文总结
GUICourse: 从通用视觉语言模型到多功能 GUI 代理

- 作者：Wentong Chen、Junbo Cui、Jinyi Hu 等

- 发表时间：2024 年 6 月 17 日

- 论文地址：https://arxiv.org/pdf/2406.11317v1.pdf

- 代码和数据集地址：https://github.com/yiye3/GUICourse

### 研究背景

- **GUI 的重要性**：图形用户界面（GUI）是人机交互的关键媒介，在各种应用中发挥着重要作用，不同 GUI 系统的操作逻辑相似，便于用户使用，GUI 代理可帮助用户完成任务，扩展大语言模型的能力。
  
- **基于视觉的 GUI 代理优势**：与基于文本的方法相比，基于视觉的 GUI 代理具有获取容易（获取 GUI 系统截图比获取结构化文本容易）和可转移性强（不同系统中相似视觉元素表示相似功能）的优点。

- **当前 VLM 的挑战**：当前视觉语言模型（VLM）在 OCR 和定位能力以及对 GUI 元素功能和控制方法的知识方面存在不足，无法准确完成 GUI 导航任务。

### 研究目的

提出 GUICourse，一组完整的数据集，用于训练基于视觉的 GUI 代理，提升 VLM 的基本能力和 GUI 知识，包括 GUIEnv（提高 OCR 和定位能力）、GUIAct（增强 GUI 系统知识）和 GUIChat（改善交互能力）三个数据集。

### 研究方法

数据集构建

1.GUIEnv

- 数据收集：从 C4 收集 4M 个 URL，使用 Playwright 渲染得到 10M 个带注释的截图，用于 GUIEnv - global 数据；从 C4 中选择约 50k 个网站截图，处理后得到 0.7M 个指令，用于 GUIEnv - local 数据。

- 任务类型：GUIEnv - global 任务是根据截图预测所有文本及其位置；GUIEnv - local 任务包括 “text2bbox”（给定文本预测区域）和 “bbox2text”（给定区域预测文本）。

2.GUIAct

- 数据收集

  - web - single：使用 GPT - 4 收集场景和 URL，通过网络快照工具获取截图，再用 GPT - 4V 获取单步指令 - 动作对，经人工检查后得到约 67k 个单步动作指令。

  - web - multi：定义 8 个顶级网络场景，收集子场景和网站，用 LLMs 生成指令，通过众包注释得到 5,696 个多步动作指令。

  - smartphone：使用 AITW 数据集的子集，转换动作后得到 9,157 个多步动作指令。

- 任务类型：GUI 导航任务，要求代理根据任务指令与 GUI 环境交互，定义了 11 种统一动作类型，包括点击、输入、浏览等。

3.GUIChat

- 数据收集：使用 Playwright 渲染网页获取截图，提取文本信息，用 GPT - 4 构建问答对，包括约 44k 个单轮 QA 对和 6k 个多轮对话，涵盖视觉信息查询、以人为中心的问题、世界知识查询和复杂推理任务等方面。

### 实验设置

1.训练 GUI 代理：基于三个 VLM（Fuyu - 8B、Qwen - VL、MiniCPM - V）和 GUICourse 数据集训练多个 GUI 代理。

2.评估性能

- 评估数据集和指标：使用 Mind2Web（2000 个网站场景高级指令任务）和 AITW（30k 指令及 715k 操作轨迹的智能手机场景任务）数据集，采用与 SeeClick 相同的评估方法，评估指标包括步骤成功率（StepSR）、点击准确率（Cli.Acc）、类型精确匹配分数（Type EM）等。

- 消融实验：调整 GUIEnv - global 数据集的数量，分析对 MiniCPM - GUI 的影响；以 MiniCPM - V 为基线，依次添加 GUIAct 数据集、提高图像分辨率、混合 GUIChat 数据集，分析不同因素的影响。

### 研究结论

1.性能提升：GUICourse 帮助 GUI 代理在常见 GUI 任务（Mind2Web 和 AITW）上比基线 VLM 表现更好，如在 Mind2Web 任务中，Qwen - GUI 的 StepSR 相比基线 Qwen - VL 有显著提高。

2.数据集作用

- GUIEnv 数据集有助于提升 VLM 的基本能力和 GUI 导航能力，数据量增加能提高 OCR 和定位能力及导航任务性能。

- 高分辨率对 GUI 导航任务重要，提升分辨率可显著改善 “web - single” 和 “smartphone” 任务性能。

- GUIChat 数据集有助于提升网站场景任务性能，尽管其主要目标是改善交互能力。

### 未来研究方向

1.考虑使用强化学习方法（如 RLHF）进一步提升 GUI 代理能力。

2.构建或收集更多关于计算机系统和专业软件的 GUI 指令数据，以构建更通用的 GUIAgent。
