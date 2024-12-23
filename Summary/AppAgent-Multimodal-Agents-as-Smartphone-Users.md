# AppAgent: Multimodal Agents as Smartphone Users

## 思维导图
![思维导图](/imgs/AppAgent-Multimodal-Agents-as-Smartphone-Users.jpg)

## 全文总结
用多模态智能体 AppAgent 像人类用户一样操作智能手机应用。
### 1. 引言
#### 1.1 研究背景与意义
大型语言模型（LLMs）如 ChatGPT 和 GPT - 4 的出现是人工智能领域的重要里程碑，其不仅能处理语言任务，还能执行复杂任务。但基于 LLM 的智能体多依赖文本信息，限制了对环境的感知和交互。而具备视觉能力的模型如 GPT - 4V 的出现是突破，它能处理视觉信息，提供更全面的交互体验。作者团队聚焦于构建多模态智能体，利用多模态大语言模型的视觉能力，操作智能手机应用，旨在解决现有模型在处理新应用及其非典型用户界面时的问题。
#### 1.2 研究目标与创新点
目标：构建能像人类用户一样操作智能手机应用的多模态智能体框架，提升其在不同应用中的适应性和任务处理能力。
创新点：提出创新的探索策略，使智能体通过自主交互或观察人类演示学习使用新应用；开源多模态智能体框架，定义独特的操作空间；通过多应用实验验证框架优势。
### 2. 方法
#### 2.1 实验环境与动作空间
实验环境：基于命令行界面（CLI），在 Android 操作系统上进行。智能体接收实时截图和 XML 文件作为输入，为交互元素分配唯一标识符，以半透明数字形式覆盖在截图上，辅助智能体准确交互。
动作空间：模拟人类与智能手机的常见交互，包括点击（Tap）、长按（Long_press）、滑动（Swipe）、输入文本（Text）、返回（Back）和退出（Exit）等功能，简化智能体与手机的交互过程。
#### 2.2 探索阶段
自主交互探索：智能体通过试错学习应用功能，依据大语言模型分析操作前后截图，理解 UI 元素功能和操作效果，记录信息并更新文档。若当前 UI 页面与任务无关，智能体将返回上一页面，这种目标导向的探索方式可提高效率。
观察演示学习：智能体通过观察人类操作应用来学习，记录操作元素和动作，缩小探索空间，避免无关页面，比自主交互更高效。
#### 2.3 部署阶段
智能体根据探索阶段积累的经验执行复杂任务。任务执行中，智能体按步骤操作，每步根据当前 UI 截图、动态文档和可用操作提示，进行观察、思考、执行动作并总结交互历史，这些信息用于下一步决策，直至任务完成后通过 Exit () 退出。
### 3. 实验
#### 3.1 实验设置
构建包含 10 个不同用途流行应用（如谷歌地图、推特、Gmail 等）的基准，对智能体进行全面评估。在 Adobe Lightroom 应用中进行深入案例研究，以评估智能体视觉任务处理能力。实验采用 GPT - 4 作为多模态大语言模型，在探索阶段限制最大步数为 40，测试阶段为 10。
#### 3.2 设计与分析
基线对比：评估不同设计选择对智能体性能的影响，包括 GPT - 4 在不同参考文档和动作空间下的表现，以及不同方式生成的引导文档（自主探索、观察演示、手动制作）的效果。
结果评估：采用成功率（SR）、奖励（Reward）和平均步骤（Average Steps）作为评估指标。实验结果表明，简化动作空间可提高 GPT - 4 基线性能，自主探索和观察演示生成的文档有效，与手动制作文档结果相当。定性分析展示了智能体在不同任务中的执行过程，体现其准确感知、推理和执行任务的能力。
#### 3.3 案例研究
在 Lightroom 图像编辑应用中进行案例研究，准备存在视觉问题的图像，让不同模型进行编辑，通过用户研究对编辑结果排名并报告使用工具的平均数量。结果显示，带有文档的智能体模型优于 GPT - 4 基线，观察演示生成的文档与手动制作文档结果可比，且带文档的智能体倾向使用更多工具提升图像质量。
### 4. 研究结论与局限
#### 4.1 结论
提出的多模态智能体框架利用大语言模型的视觉能力，以类人方式操作智能手机应用，无需系统后端访问，具有安全、适应和灵活优势。探索式学习策略使智能体快速适应新应用，多应用实验证明其处理多样化高级任务的能力。
#### 4.2 局限
采用简化动作空间，不支持多点触控和不规则手势等高级控制，限制了智能体在某些复杂场景的适用性，这是未来研究的改进方向。
