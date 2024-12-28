# UFO: A UI-Focused Agent for Windows OS Interaction

## 思维导图
![思维导图](/imgs/UFO-A-UI-Focused-Agent-for-Windows-OS-Interaction.jpg)

## 全文总结

“UFO: A UI-Focused Agent for Windows OS Interaction” 介绍了 UFO，这是一种利用 GPT-Vision 为 Windows 操作系统设计的创新型智能体，可通过自然语言指令完成用户请求，有效提升操作效率与自动化水平。

### 1.研究背景：

大语言模型（LLM）的发展展示了强大能力，但针对 Windows 操作系统的视觉语言模型（VLM）智能体研究较少。Windows 系统具有高市场份额、多样应用和复杂任务，开发适用于其的智能体有重要意义。

### 2.相关工作

- LLM 智能体：如 AutoGPT、TaskWeaver 等，扩展了 LLM 能力，但多数未针对 Windows 系统应用。多智能体框架如 AutoGen、MetaGPT 等虽具优势，但在 Windows 系统任务完成方面仍有不足。

- 基于 LLM 的 GUI 智能：已有研究利用多模态 LLM 控制 GUI，但 UFO 是首个专门针对 Windows 系统应用 UI 操作的多模态 LLM 智能体框架。

### 3.UFO 设计

- 整体架构：采用双智能体框架，包括 HostAgent 和 AppAgent。HostAgent 负责选择应用并制定全局计划，AppAgent 执行所选应用内操作。二者借助 GPT-Vision 分析 UI 截图和控制信息，通过控制交互模块实现自动化操作。

- HostAgent：输入用户请求、桌面截图、应用信息和记忆，输出观察结果、思考过程、所选应用等。利用这些信息决策并协调任务，提高应用选择合理性。

- AppAgent：输入类似 HostAgent，但多了不同类型截图和控制信息。根据输入选择控制和操作，执行并更新计划，确保任务在应用内推进。

- 控制交互：利用 pywinauto 和 Windows UI Automation API 检测和操作应用控制，定义 10 种关键控制类型和常用操作，实现智能体对系统的有效影响。

- 特殊设计考虑：具备交互模式，支持用户迭代交互；可定制操作，满足个性化需求；采用控制过滤，精简决策；有计划反思机制，适应 UI 变化；设有安全保障，确认敏感操作，增强安全性与可靠性。

### 4.实验

- 基准、基线和指标：构建 WindowsBench 基准，含 50 个用户请求和 9 个应用。以 GPT-3.5 和 GPT-4 为基线，从成功、步骤、完成率和安全率评估 UFO。

- 性能评估：UFO 在基准测试中成功率达 86%，远超基线模型，完成率高且步骤少，安全率达 85.7%。在各应用中表现良好，跨应用任务也能保持较高性能。

- 案例研究：展示在删除 PowerPoint 笔记和跨应用邮件撰写等任务中的高效操作，体现其处理复杂任务能力。

### 5.局限与展望：

受限于当前支持的 UI 控制和操作，对特殊应用 UI 处理困难。未来计划扩展后端支持，利用外部知识增强适应性。

### 6.结论：

UFO 是 Windows 系统的创新智能体，能有效处理应用任务，双智能体设计和特殊功能提升了其通用性和安全性，为 Windows 自动化操作提供了新方案。
