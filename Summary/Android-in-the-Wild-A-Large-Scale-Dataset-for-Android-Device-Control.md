# Android in the Wild: A Large-Scale Dataset for Android Device Control

## 思维导图
![思维导图](/imgs/Android-in-the-Wild-A-Large-Scale-Dataset-for-Android-Device-Control.jpg)

## 全文总结
这篇论文介绍了用于设备控制研究的大规模数据集 AITW，它在数量和多样性上远超现有数据集，为设备控制研究提供了丰富资源，有助于推动相关领域发展。
### 1.研究背景
#### 设备控制系统需求：
用户常通过自然语言描述任务，在无法直接操作设备（如身体残疾、特定情境）时，需设备控制系统解读指令并执行。此类系统需理解屏幕 UI 元素语义，将高级命令映射为执行计划，并在不同任务和 UI 间通用。
#### 现有数据集不足：
现有数据集在人类演示数量、任务指令多样性方面受限，且多为特定平台（安卓或网页）。部分数据集假设可从平台特定 UI 元数据获取应用 UI 的树状表示，这简化了问题但限制了系统适用性。同时，一些数据集的任务指令多为基于 UI 元素的分步命令，与用户常用的简短高级目标指令不符。
### 2.研究目的：
发布 Android in the Wild（AITW）数据集，推动设备控制研究，为训练、微调及评估相关系统提供数据，同时分析训练系统在不同条件下的性能表现。
### 3.数据集构建
#### 数据收集管道：
分两阶段，先让评估者在模拟器上执行端到端任务，然后对收集的轨迹进行事后语言重新标记，以识别和标注简单动作序列（单步任务）。
#### 动作与观察记录：
使用 AndroidEnv 记录动作，包括 TOUCH、LIFT、REPEAT 等类型，记录触摸事件的起始和结束位置（双点手势），按钮按下和输入事件也被记录。环境返回 RGB 截图及应用等元数据。
#### 屏幕特征处理：
对 RGB 截图进行后处理，映射到检测到的 UI 元素，每个元素有边界框、OCR 检测文本或图标类标签。
#### 任务指令来源：
从作者、PixelHelp 部分指令、LLM 生成的指令等多源创建高级任务指令，随机分配给评估者执行，任务执行可通过特殊 “状态” 动作结束。
### 4.数据集内容
#### 多步任务轨迹：
涉及谷歌应用（GOOGLEAPPS）、应用安装（INSTALL）、网页购物（WEBSHOPPING）、通用（GENERAL）等类别，任务需多步完成，环境随机重置起始屏幕，评估者自然操作，任务完成或无法完成时通过特定动作标记。
#### 单步任务演示：
通过事件可选的事后语言重新标记多步任务轨迹收集，评估者需标注描述动作结果的短语，避免使用特定简单词汇。
#### 数据集总结：
AITW 包含 5 个子类别，任务长度适中，Chrome 和谷歌应用常用，指令长度和内容有一定特点，数据集涵盖众多安卓应用和网站。
### 5.实验设置
#### 标准测试分割：
将每个数据集按 80/10/10% 比例随机分割为训练、验证和测试集，分别评估后取平均得分。
#### 未见安卓版本：
将安卓 10、11、12 版本收集的数据用于训练和验证（90/10%），安卓 13 版本数据用于单独测试，以评估系统在未见版本上的性能。
#### 未见主题和动词：
通过开发指令模板（掩盖动词或主题短语），将数据按模板分割，评估系统对未见语言模式和新任务的泛化能力。
#### 未见域：
根据指令推断的域（如网页购物的网站域、安装任务的应用名）将数据分割，测试系统对未见应用和网站的泛化能力，单步任务和 GOOGLEAPPS 因特定原因被排除。
### 6.实验结果
#### 模型评估：
实现了基于 Transformer 的行为克隆（BC）代理（含 BC - single 和 BC - history 两个变体）和基于预训练 LLM（PaLM 2）的模型（LLM - 0 和 LLM - hist - 5 - CoT），LLM 模型输入文本化屏幕表示，输出受限，与 BC 模型相比存在性能差距。
#### 评估方法与指标：
提出离线评估方法，通过动作匹配计算部分和完全匹配分数，与在线评估（人类标记）对比，发现部分匹配与真实成功率相关，自动化完全匹配分数是真实值下限。
#### 结果分析：
BC 代理在所有分割中表现最佳，在未见任务（尤其是主题和动词模板分割）上有较好泛化能力；LLM 模型受限于动作空间，在标准测试集上部分任务不可行，可行动作中 LLM - hist - 5 - CoT 有一定部分匹配分数。
### 7.讨论
#### 数据局限性：
评估者不具全球代表性，数据集仅含英语提示，评估者使用鼠标键盘而非原生触摸界面，数据集仅源于手机交互，可能未充分体现 UI 动态变化。
#### 伦理考量：
收集过程中评估者被要求不输入个人可识别信息，数据集无真实用户交互，但存在被恶意利用的风险。
### 8.未来工作：
探索多模态基础模型，改进评估方法，允许模型以多种方式完成任务并定义最优方式。
### 9.研究结论：
AITW 数据集规模大、多样性高，包含丰富任务指令和执行路径，通过不同实验设置可评估模型性能，有望推动设备自动化模型研究。
