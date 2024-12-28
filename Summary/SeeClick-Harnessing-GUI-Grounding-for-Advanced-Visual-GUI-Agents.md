# SeeClick: Harnessing GUI Grounding for Advanced Visual GUI Agents

## 思维导图
![思维导图](/imgs/SeeClick-Harnessing-GUI-Grounding-for-Advanced-Visual-GUI-Agents.jpg)

## 全文总结

“SeeClick: Harnessing GUI Grounding for Advanced Visual GUI Agents” 一文提出了仅依赖截图进行任务自动化的视觉 GUI 代理 SeeClick，通过 GUI 基础预训练和创建基准数据集 ScreenSpot 等方法，有效提升了在 GUI 任务中的性能，并探讨了其在不同任务中的应用及相关伦理问题。

### 1.研究背景与动机

- GUI 代理旨在自动化数字设备任务，但现有基于结构化文本交互的方法存在局限，如文本获取困难、信息冗余或缺失、需定制任务空间等。

- 视觉 GUI 代理可绕过这些问题，但面临 GUI 定位挑战，即依据指令准确定位屏幕元素的能力缺失。

### 2.SeeClick 模型

- **GUI 定位训练**：将 LVLM 定位任务形式化为根据界面截图和元素文本描述预测元素位置，采用直观方式处理坐标数值，通过交叉熵损失优化模型。

- **数据构建**：使用网络 UI 数据（从网页爬取，含文本和特定属性元素）、移动 UI 数据（包括部件标注、定位及总结数据）和通用视觉语言指令数据训练 SeeClick，混合后生成 1M 数据集，并为每个 GUI 任务设计 30 个特定提示。

- **训练过程**：在 Qwen - VL 上持续预训练约 10k 步（约 1 个 epoch），用 LoRA 微调视觉编码器和 LLM，采用 AdamW 优化器和余弦退火调度器，在 8 个 NVIDIA A100 GPU 上训练约 24 小时。

### 3.ScreenSpot 基准

- 涵盖移动（iOS、Android）、桌面（macOS、Windows）和网页平台超 600 张截图及 1200 多条指令，含多种图标和部件，样本新颖，由经验丰富的注释者标注。

- 用于评估视觉语言模型基于指令定位屏幕元素能力，推动 GUI 定位研究。

### 4.实验结果

- **GUI 定位能力**：在 ScreenSpot 上，通用 LVLMs 因 GUI 与自然图像差异大定位性能差，GUI 特定 LVLMs 表现更好，SeeClick 平均性能最佳，在定位图标 / 部件方面仍有挑战。

- **视觉 GUI 代理任务**：在 MiniWob 任务中，SeeClick 作为纯视觉模型，用少量数据超越强基线，如超 WebGUM 和 Pix2Act，且比 LVLM 基线 Qwen - VL 高近 20 个百分点，在动态布局任务表现突出；在 AITW 任务中，采用指令级分割训练，SeeClick 在 API 基 LLM 和训练 LVLMs 中平均性能最佳，点击准确率比 Qwen - VL 高 9%；在 Mind2Web 任务中，SeeClick 比 Qwen - VL 的元素准确率和步骤成功率近乎翻倍，但性能仍低于基于 HTML 的方法；总体上，GUI 定位能力提升与代理任务性能增强呈正相关，统一训练模型性能略有下降。

### 5.研究贡献与局限

- 贡献包括开发 SeeClick、探索 GUI 定位、创建 ScreenSpot 基准及验证定位与任务性能关系。

- 局限是动作空间简化，执行多步任务需特定数据训练；同时存在隐私、安全和偏差等伦理问题需解决。
