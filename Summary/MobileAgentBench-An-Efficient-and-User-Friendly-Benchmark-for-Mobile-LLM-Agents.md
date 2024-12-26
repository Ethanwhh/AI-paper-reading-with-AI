# MobileAgentBench: An Efficient and User-Friendly Benchmark for Mobile LLM Agents

## 思维导图
![思维导图](/imgs/MobileAgentBench-An-Efficient-and-User-Friendly-Benchmark-for-Mobile-LLM-Agents.jpg)

## 全文总结
“MobileAgentBench: An Efficient and User - Friendly Benchmark for Mobile LLM Agents” 由 Guodong Mao、Qinmin Wang 等人撰写。随着基于大语言模型（LLM）的移动智能体兴起，但相关性能评估基准存在不足。本文提出 MobileAgentBench 基准，其在真实安卓设备上运行，通过匹配最终 UI 状态判断任务成功与否，简化了扩展过程，支持多种测试任务。实验对 5 种流行移动 LLM 智能体进行评估，结果显示 AppAgent 成功率最高，CogAgent 最低等，为移动 LLM 智能体发展提供了基线数据。

### 研究背景

- 大语言模型促使各领域自主智能体发展，其中移动智能体因能提升用户体验受关注。传统数字助手虽提供语音交互，但对第三方应用功能调用受限。LLM 智能体可直接操作图形用户界面（GUI），理论上能完成复杂任务，但目前缺乏有效的性能评估基准。

- 现有基准存在问题：可扩展性和可用性差，开发者需深入了解复杂数据结构和工具；健壮性和灵活性不足，仅考虑单一任务完成路径；部分基于静态截图评估，未在真实设备运行。
  
### MobileAgentBench 基准介绍

- 方法：在真实安卓设备或模拟器上运行，自动判断任务成功状态，无需人工监督。通过匹配最终 UI 状态和结合应用事件（如按钮点击信号）判断任务是否成功，利用 Android Accessibility Service 捕获应用事件。其架构包括设备端运行的应用、与主机和智能体通信的模块以及事件监听器等，各模块协同工作完成基准测试流程。

- 任务描述：涵盖 10 个开源应用的 100 个任务，任务难度分为易、中、难三个级别，由专家根据完成任务的最小步骤交叉验证定义，旨在模拟用户日常活动。

- 使用方法：基准 API 设计友好，对标准智能体集成只需不到 10 行额外代码。开发者需导入相关 Python 库并初始化任务编排器，定义智能体入口函数，在函数中调用 LLM 生成动作并执行，编排器在动作前后收集信息，最后通过编排器运行函数启动测试。

### 实验与智能体评估

- 指标：定义了成功率（SR）、逐步效率（SE）、延迟、令牌数、误报率（FP）和漏报率（FN）6 个指标，全面评估移动智能体性能。

- 环境设置：选择 Google Pixel 3a 模拟器和 Android 14 操作系统（AutoDroid 用 Android 9），部分智能体在 Macbook Pro（M1 Max 芯片）执行，部分在配备 Nvidia RTX 4090 GPU 的工作站执行，并对各智能体进行相应配置。

- 结果：AppAgent 成功率最高，得益于自探索机制；CogAgent 成功率最低，可能因实现方式简单。AutoDroid 虽成功率与 MobileAgent 相近，但逐步效率低。在延迟方面，AutoDroid 和 CogAgent 较低，AppAgent 因需查找文档消耗更多令牌。AutoDroid 和 CogAgent 误报率高，AppAgent 误报率也较高。不同难度任务中，多数智能体处理简单任务成功率高，AppAgent 在中等任务表现突出；基于不同 LLM 模型，AutoDroid 使用 GPT - 3.5 模型却在某些方面优于使用 GPT - 4V 模型的智能体，表明文本视图层次结构对 GUI 导航任务的重要性。

### 研究局限与未来工作

- 对于无技术背景人员，使用 Python 代码片段配置任务成功条件仍有难度，未来将探索无需代码的自动构建方法。

- UIAutomator 在处理有动态屏幕内容的应用时无法获取视图层次结构，考虑用其他框架替代以获取视图信息。
