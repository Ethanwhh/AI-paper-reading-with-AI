# Ferret-UI: Grounded Mobile UI Understanding with Multimodal LLMs

## 思维导图
![思维导图](/imgs/Ferret-UI-Grounded-Mobile-UI-Understanding-with-Multimodal-LLMs.jpg)

## 全文总结
该文档主要是关于一个名为 Ferret - UI 的项目，其旨在通过多模态大语言模型实现对移动 UI 的理解。

文档涵盖了项目的各个方面，包括相关技术、功能实现、资源加载、性能监测以及页面布局和样式等内容。
### 1.项目概述
#### 目标：
利用多模态大语言模型实现对移动 UI 的理解，提升用户体验。
#### 功能：
涉及多方面功能，如不同页面的布局与交互、资源的加载与管理、性能监测等。
### 2.技术实现细节
#### 脚本加载与错误处理：
通过一系列script标签加载各种脚本，如sdk - glue.js、webmssdk.es5.js、pure.umd.production.new.js等，并对加载过程中的错误进行监测和处理。
#### 模块化与依赖管理：
使用模块化的方式组织代码，通过r.m、r.n、r.t等函数实现模块的定义、导入和导出，以及依赖关系的管理。
#### 资源加载与路径处理：
根据不同的模块或资源，通过r.u函数确定其加载路径，如 JavaScript 文件和 CSS 文件的路径处理，同时利用r.l函数进行资源的加载。
#### 性能监测：
使用inlineSlardarInstance进行性能监测，记录如html_render_start、window_onload等事件，同时通过e函数监测sdk_glue的加载状态和错误来源。
### 3.页面布局与样式
#### 整体结构：
页面主要包含id="root"的根元素和用于显示骨架屏的.flow - web - skeleton元素，根元素用于承载实际内容，骨架屏在页面加载时展示占位信息。
#### 骨架屏样式：
骨架屏包含__logo和__chat两部分，__chat部分又分为侧边栏和聊天主区域，各区域内的元素如聊天项、输入框等都有特定的样式和布局规则，包括尺寸、边距、背景色、透明度等样式设置，以及弹性布局、绝对定位等布局方式。
### 4.页面交互逻辑
#### 页面路径判断：
根据location.pathname判断当前页面路径，确定是否显示骨架屏的特定部分，以及是否隐藏聊天输入框等元素。
#### 设备适配：
根据设备宽度（如小于 599px）和设备类型（如 iPad、iPhone、iPod 或 Macintosh 且支持触摸事件）调整页面元素的显示，如隐藏侧边栏或为聊天消息列表添加特定类名。
### 5.其他功能
#### 用户登录相关：
通过accountInfoPromise获取账户信息，判断用户是否登录，并根据登录状态进行相应操作，如设置本地存储中的登录标识。
#### 引导与配置获取：
使用guidancePromise和skillListPromise分别获取引导信息和技能列表，同时通过guestLayoutModePromise获取访客布局模式相关配置。

Ferret - UI 项目在技术实现上注重模块化、资源管理和性能监测，在页面设计上考虑了布局、样式和交互逻辑，同时兼顾了用户登录和设备适配等功能，以提供良好的移动 UI 体验。



