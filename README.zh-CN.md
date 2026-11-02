# Z50 Lab Windows 工具 — r10.1

[English](README.md)

面向 Nikon Z50 C2.60 的实验性电脑工具：制作八槽音效，以及从用户自行提供的匹配官方输入生成独立 M5 EG 模块。**Windows ZIP 是电脑工具包，不是下载后可直接安装到相机的完整 Nikon 固件更新包。**

本地制备快照（2026-11-02）：仓库名称已确认为 `chen001-design/nikon-z50-downloads`，以下为拟发布入口，不表示仓库或附件现已公开。实际状态以 [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases) 和拟定的 [r10.1 发布页](https://github.com/chen001-design/nikon-z50-downloads/releases/tag/r10.1) 为准；实验性 Pre-release 不一定列入 latest。

## 普通用户：下载使用

从对应发布页下载 `Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip` 和 `SHA256SUMS.txt`，核对后完整解压。普通使用无需另装 Python、FFmpeg、Zig 或 Keystone；Windows 前置运行库由启动器检查，显示的适用条件须本人阅读决定。

| 需要做什么 | 完整解压后的入口 |
|---|---|
| 将 WAV、MP3、AAC、M4A 制作为八槽音效文件 | 根目录 `启动多音源制作工具.cmd` |
| 在电脑生成 M5 EG | `PublicBuildM5/Start-PublicBuildM5.cmd`，先读 `PublicBuildM5/user-guide/BUILD.md` |

按 [电脑端快速开始](QUICKSTART.zh-CN.md) 操作。工具包不附官方固件或生成的 EG，不替用户安装固件，也不验证救砖能力。

Windows ZIP 为 **430,722,516 字节**，SHA256：

```text
5f28a65e5655a55bd7d5139ea333a1c3450d78f56bc0384b3958d7447e725870
```

## 开发者：取得实际源码

拟定六个附件为：Windows ZIP、`Corresponding-Source.zip`、`SoundTool-Corresponding-Source.zip`、`FFmpeg-Corresponding-Source.zip`、列出四个 ZIP 哈希的 `SHA256SUMS.txt`、`RELEASE-NOTES.zh-CN.md`。三份单独源档与 Windows ZIP 中的对应成员逐字节相同。

**本仓库的 Git 目录只有下载说明、许可与身份索引；GitHub 自动生成的 Source code ZIP 不包含这些组件源码。** 实际源码从发布附件取得；Python/Tcl/Tk 等其他依赖材料仍在 Windows ZIP 内，详见 [完整供源与重建入口](SOURCE-DELIVERY.md)。所有入口都不要求访问私有开发仓库。提供组件源码与构建控制，不承诺裸克隆本说明仓库即可重打完整 Windows ZIP。

## 已有验证与限制

r10.1 已有验收为 375 项音效检查通过、40 份黄金文件同字节、24 项历史 PCM 哈希一致及完整 M5 同字节。用户于 2026-11-02 整体确认“r10.1 界面和试听全部通过”；没有据此补写逐用例、Windows 版本、跨机或相机结果。原包中的 pending/待确认文字是封包时的历史状态。

本版建议作为实验性 Pre-release。已报告的连拍后可能无音效问题尚未解决，不代表全部 Windows 环境、相机安装或恢复均已验证。请读 [已知限制](KNOWN-LIMITATIONS.md)。

根 [LICENSE](LICENSE) 只在其声明范围内适用，不能把整包称为纯 MIT。恢复/组合 host 的 GPL 义务、FFmpeg 和其他组件条款分别保留，见 [许可范围](LICENSE-SCOPE.md)。独立下载仓库不消除 Nikon/Windows 具体权利适用条件，也不等于获得公开批准。
