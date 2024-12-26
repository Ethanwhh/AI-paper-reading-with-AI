# Navigating the Digital World as Humans Do: Universal Visual Grounding for GUI Agents

## 思维导图
![思维导图](/imgs/Navigating-the-Digital-World-as-Humans-Do-Universal-Visual-Grounding-for-GUI-Agents.jpg)

## 全文总结
“Navigating the Digital World as Humans Do: UNIVERSAL VISUAL GROUNDING FOR GUI AGENTS” 一文提出了一种类似人类的 GUI 智能体实现方式，通过视觉感知和像素级操作在不同平台的 GUI 环境中执行任务，并介绍了用于训练的大规模数据集和通用视觉 grounding 模型 UGround，实验表明该模型性能优异，为相关领域研究提供了新方向和有力支持。

### 1.研究背景与动机

GUI 智能体在大型语言模型推动下发展，但当前智能体多依赖文本表示（如 HTML、辅助功能树）进行感知和操作，存在噪声、不完整及计算开销大等问题。人类主要通过视觉感知和像素级操作与数字世界交互，因此研究仅基于视觉的 GUI 智能体具有重要意义，但现有视觉 grounding 方法无法满足准确性、泛化性和灵活性要求，限制了其发展。

### 2.方法

- SeeAct-V 框架：基于 SeeAct 框架改进，仅用屏幕截图进行环境观察，通过 MLLM 生成文本计划，再由专门的视觉 grounding 模型将计划映射到截图坐标，实现像素级操作。关键在于强大的视觉 grounding 模型，需跨平台、处理多种元素引用并易于与不同 MLLM 集成。

- 数据构建：以网页为基础合成大规模、高质量且多样的〈截图，引用表达式，坐标〉三元组训练数据。将 GUI 元素引用表达式分为视觉、位置和功能三类及组合类型，通过提取 HTML 元素属性、利用 MLLM 和规则生成丰富表达式，并从 Common Crawl 收集数据应用合成管道得到主数据集 Web-Hybrid，同时补充其他相关数据集，共涵盖 10M UI 元素。

- 模型设计：采用 7B LLaVA-NeXT 为骨干模型并调整。输入输出上，要求模型用自然语言回答元素坐标；图像分辨率方面，扩大输入尺寸，用 CLIP@224px 编码，结合 Vicuna-1.5-7b-16k 处理长视觉上下文，并舍弃低分辨率图像融合模块。

### 4.实验

- GUI 视觉 grounding：在 ScreenSpot 基准测试的标准和智能体设置下评估 UGround，与多种模型比较。结果显示 UGround 在各设置和平台上大幅优于现有模型，在标准设置下平均绝对提升约 20%，智能体设置下约 29%，尤其在图标和小部件定位上表现突出，证明其跨平台和规划器的通用 grounding 能力。

- 离线智能体评估：在 Multimodal-Mind2Web（网页）、AndroidControl（移动）和 OmniACT（桌面）三个基准测试中，SeeAct-V 与 UGround 组合均优于使用额外文本输入的基线方法，且 UGround 性能优于 SeeClick，有力支持了仅视觉的智能体实现方式和 UGround 的有效性。

- 在线智能体评估：在 Mind2Web-Live（网页）和 AndroidWorld（移动）两个在线基准测试中，SeeAct-V 与 UGround 组合性能与基线相当或更高，再次证明其可行性和有效性。

- 错误分析：对 SeeAct-V 与 UGround 进行手动错误分析，发现规划错误是主要失败原因，同时在部分测试中 grounding 错误也占一定比例，主要源于长尾巴图标的特殊语义难以捕捉，但在实际任务中 UGround 仍较稳健。

- 训练数据分析：通过缩放分析和消融研究，发现随着 Web-Hybrid 数据量增加 UGround 性能提升，100K 截图后收益递减；Web-Hybrid 数据对模型训练至关重要，与补充数据结合可获最佳性能。

### 5.结论与局限

提出的 UGround 模型和 SeeAct-V 框架在跨平台任务中表现出色，优于现有方法，但 UGround 训练数据效率有待提高，长尾巴元素和桌面 UI 数据问题需解决，且依赖外部规划器不能独立作为智能体，未来研究可在此基础上进一步探索。
