# 兼听 (IOCHunter) - 高并发 IOC 域名解析校验工具

![Version](https://img.shields.io/badge/Version-V1.0-blue.svg)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

“兼听 (IOCHunter)”是一款专为安全运营（SecOps）和威胁情报（TI）分析师打造的高性能桌面端便携工具。主要用于批量对海量 IOC（恶意域名）进行并发 DNS 解析，以快速验证这些域名是否已被内部网络、安全设备或运营商拦截，并指向了**公共 DNS/Sinkhole（黑洞）IP 池**。

**💡 核心优势：开箱即用，零依赖。专为解决“百万级解析任务下的界面卡死与内存溢出”而生。**

## 📥 下载与运行 (开箱即用)

本工具为绿色便携版，**无需安装 Python 环境或任何依赖**。

1. 前往 [Releases](#) 页面下载最新版本的`IOCHunter_v1.0.zip`。解压后即可得到`IOCHunter_v1.0.exe`。
2. 将程序放置在任意目录，双击运行即可。
3. 首次运行会自动在同级目录生成 `config.json` 配置文件。

## ✨ 核心特性

* 🚀 **极限高并发与防假死架构**
    * 采用底层线程池纯后台异步执行，支持自定义并发数、超时时间和生命周期。
    * **$O(1)$ 极速去重**：实测导入数十万条恶意域名，瞬间完成哈希去重过滤。
    * **UI 攒批渲染与熔断机制**：彻底解决 Tkinter 在海量数据下的组件崩溃问题。**实测单机 350 万并发解析任务下，主界面依然丝滑拖拽，零卡顿。**
    * **安全中断**：支持在海量任务执行中途随时“急刹车”，立即中止并结算已出结果，杜绝僵尸线程堆积。
* 🛡️ **智能分析与警报**
    * 零配置自动比对 `config.json` 中的 Public DNS 池。
    * 发现可疑 Sinkhole 命中后，界面触发**深红色高亮预警**及独立弹窗提示。
* 📊 **异步海量数据导出**
    * 支持导出**详细报告**与**唯一 IP 聚合报告**（XLSX / HTML / CSV）。
    * 导出操作被完全剥离至后台线程，几万条数据的 Excel 单元格着色与绘制全程不阻塞主界面操作。
* 🎨 **现代化桌面视觉体验**
    * 深度定制的极简“科技蓝”与深色模式（Dark Mode），全局深色标题栏自适应。
    * 底层调用 Windows API 显式声明 DPI 感知，**彻底消除高分屏/缩放下的 UI 模糊与锯齿**。

## 📸 界面预览

* ## 📸 运行截图
![主界面预览](images/1.png)

* ## 📸 风险高亮预警截图
![红色预警弹窗与高亮](images/2.png)

## 🛠️ 高级配置 (`config.json`)

程序运行后，可通过界面上的【打开配置】按钮直接编辑外部配置：
* `public_dns_servers`: 全局公共 DNS IP 池（用于判定域名是否被黑洞拦截）。
* `default_query_dns_servers`: 默认用于执行解析查询的 DNS 节点库（支持内网 DNS）。
## 🤝 贡献与反馈
欢迎提交 Issue 或 Pull Request。如果在实战情报解析中遇到新的场景需求（如自动化联动、特定代理支持），请随时反馈探讨。

---

# IOCHunter (兼听) - High-Concurrency IOC DNS Resolution & Validation Tool

![Version](https://img.shields.io/badge/Version-V1.0-blue.svg)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

**IOCHunter** is a high-performance, portable desktop tool designed for SecOps and Threat Intelligence (TI) analysts. It performs concurrent DNS resolutions on massive IOCs (malicious domains) to quickly verify if they have been intercepted by internal networks, security devices, or ISPs, and redirected to **Public DNS/Sinkhole IP pools**.

**💡 Core Value: Out-of-the-box, zero dependencies. Specifically architected to solve UI freezing and memory overflow issues under million-level resolution tasks.**

## 📥 Download & Run (Portable)

This tool is a standalone executable. **No Python environment or dependencies are required.**

1. Go to the [Releases](#) page and download the latest `IOCHunter_v1.0.exe`.
2. Place it in any directory and double-click to run.
3. A `config.json` file will be automatically generated in the same directory upon first launch.

## ✨ Key Features

* 🚀 **Extreme Concurrency & Anti-Freezing Architecture**
    * Fully asynchronous execution using a background thread pool with customizable worker limits, timeouts, and lifecycles.
    * **$O(1)$ Hash Deduplication**: Instantly deduplicates hundreds of thousands of malicious domains upon import.
    * **UI Batch Rendering & Circuit Breaker**: Completely resolves Tkinter crashes under massive data loads. **Tested with 3.5 million concurrent tasks with zero UI lag or freezing.**
    * **Safe Interrupt**: Supports a "hard brake" during massive task execution, immediately terminating pending requests and settling resolved data without zombie thread accumulation.
* 🛡️ **Smart Analysis & Alerts**
    * Zero-config matching against the Public DNS pool defined in `config.json`.
    * Triggers **dark red visual highlights** and independent popup alerts upon detecting suspicious Sinkhole hits.
* 📊 **Asynchronous Massive Data Export**
    * Export detailed logs or unique IP aggregated reports (XLSX / HTML / CSV).
    * Export operations are isolated in background threads, ensuring the main UI remains fully responsive even when rendering thousands of colored Excel cells.
* 🎨 **Modern Desktop Experience**
    * Deeply customized "Tech Blue" accent with native Dark Mode, featuring adaptive global dark title bars.
    * Explicit DPI-awareness declaration via Windows API, **completely eliminating UI blurriness and jagged text on high-resolution/scaled displays**.

## 🛠️ Advanced Configuration (`config.json`)

Click the [Open Config] button in the UI to edit the external configuration:
* `public_dns_servers`: Global Public DNS IP pool (used to determine if a domain is sinkholed).
* `default_query_dns_servers`: Default DNS nodes used for resolution queries (supports internal DNS).
