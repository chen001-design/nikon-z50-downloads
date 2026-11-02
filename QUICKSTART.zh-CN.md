# r10.1 电脑端快速开始

本页介绍电脑端使用。声音文件的机内使用需要匹配的相机端方案；此下载和电脑测试不构成相机安装、完整 Nikon 更新包或故障恢复保证。当前发布入口和制备状态见 [首页](README.zh-CN.md)。

## 取得并解压工具

1. 在 [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases) 找到实验性 `r10.1` 的已发布附件。此处是拟定发布目标；若没有可公开取得的对应附件，就尚无该目标的公众下载。
2. 普通使用下载 Windows ZIP 和 `SHA256SUMS.txt`。校验文件列出四个 ZIP 的哈希，不是所有单独文件或发布说明的清单。
3. 在 PowerShell 对下载文件执行以下只读校验，结果应与校验文件及首页的 `5f28a65e…25870` 完整哈希一致：

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath '.\Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip'
```

4. 完整解压到电脑普通文件夹，保留所有子目录。包的启动条件面向 Windows 10/11 x64，并检查系统 UCRT 与指定 Microsoft VC v14 x64 运行库。若缺依赖，按启动器显示的官方入口自行处理；程序会停止，不自动安装或代为接受条款。上述条件不表示所有 Windows 环境均已实测。

## 制作自己的声音

双击根目录 `启动多音源制作工具.cmd`，本人阅读并决定是否满足显示的条件。窗口为“制作存储卡多音源”，提供八个固定槽位，可选择 WAV、MP3、AAC、M4A。只使用自己有权处理的音源。

为需要的槽位选择声音后，点“制作所选槽位音源包”。较长声音会询问是否截取约半秒；按自己的需要决定。选择电脑上的新保存位置，已有制作包不会被覆盖。

输出包含所选槽位的 `SOUND01.SND` 至 `SOUND08.SND`、`previews` 中的试听 WAV，以及制作清单/说明。先在电脑试听，核对所选槽位和输出内容。本页到电脑文件检查为止，不要求操作相机或真实存储卡。

## 在电脑构建 M5

先读解压包内 `PublicBuildM5/user-guide/BUILD.md`，再用 `PublicBuildM5/Start-PublicBuildM5.cmd`，自行提供匹配且未修改的官方 Z50 C2.60 输入并选用新的电脑输出目录。本项目不附该官方输入，不代为下载或同意其协议。

输入校验失败时，核对版本和文件完整性，不绕过校验。成功时检查 `build-report.json` 与 `EG163060.BIN`；EG 是独立模块，不是完整官方更新包，工具不会安装到相机。基准完整 M5 的身份见 [已知限制与验证范围](KNOWN-LIMITATIONS.md)。

## 阅读当前说明

用户已于 2026-11-02 整体确认本版界面和试听全部通过。原包内检查表、README 或源档中的“待用户/PENDING”保留封包前状态；当前整体反馈没有补充逐用例或其他机器的测量结果。本次下载入口准备没有再次运行产品测试或改变程序。

需要查看、修改或构建组件源码时，按 [SOURCE-DELIVERY.md](SOURCE-DELIVERY.md) 取得实际源档；普通使用不需要编译工具。请同时阅读 [许可范围](LICENSE-SCOPE.md) 和 [已知限制](KNOWN-LIMITATIONS.md)。
