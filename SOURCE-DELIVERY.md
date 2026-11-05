# r5 双工具对应源与重建入口

本页对应第一代 Z50 C2.60 的 r5 双工具交付。下载入口为 [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases)；只有同一发行条目实际提供下列两个同版附件时才按本页使用。旧 r10.1 发行与新 r5 分开，新附件是否已上传以实际页面为准，不因本地准备完成而视为已公开。

| 附件 | 用途 |
|---|---|
| `Z50-Lab-Windows-Tools-r5.zip` | 固件构建器、音效制作工具、两个根入口、必要运行/构建依赖、原许可和用户说明 |
| `Z50-Lab-Sources-r5.zip` | 与程序匹配的完整项目首选源码、对应第三方源、许可、固定输入锁和重建/重装箱控制 |
| 外部 `SHA256SUMS.txt` 与发行说明 | 核对两 ZIP 的实际身份和验证范围，避免在附件内嵌其自身最终摘要 |

**普通运行无需下载或解压 Sources。** 开发、审查、修改或再分发时，完整 Sources 是实际供源材料；它应与运行包在同一发行处清晰、等价且不另收源访问费用地提供。GitHub 自动 Source code 归档只含这份小型说明仓库，不能替代完整 Sources。原厂或生成的完整固件不上传，合法兼容输入仍由使用者自行取得。

## 完整 Sources 的实际布局

以下均为 **Sources 附件内部路径**，不是本仓库内链接：

| 路径 | 实体材料 |
|---|---|
| `project/` | 当前构建器、菜单组件、首选汇编/派生控制、音效应用、测试、包装脚本与项目原通知；不是只有网页索引 |
| `third-party/python/archives/` | Python 3.14.10、Tcl/Tk 及合并组件的 13 份不同源档，保留各原身份 |
| `third-party/packaging/wheels/` | 构建锁指定的 7 个实际 wheel；具体文件及许可按锁和原通知处理 |
| `third-party/zig/zig-bootstrap-0.15.2.tar.xz` | 完整锁定 Zig bootstrap 对应源，不能用运行包固定 reader 子集替代 |
| `ffmpeg/FFmpeg-Corresponding-Source.zip` | 唯一一份完整 120 成员供源档，含四份原源归档、构建配方、身份记录和原许可；不再在运行 ZIP 或 Sources 另放一套展开副本 |
| `third-party/notices/` | 原组件许可、来源记录、锁与配套说明；历史相对路径不被冒充当前下载位置 |
| `runtime-readme/README.zh-CN.txt` | 与运行包对应的用户教程 |

先读 Sources 根 `README.txt`、`SOURCE-COMPONENTS.json`、`SOURCE-FILES.json` 与 `BUILD-INPUTS.json`，核对实际成员与固定输入。原出处材料中的旧路径用于历史来源追溯，当前物理位置以这些索引为准。

## 构建与公开重装箱

本版的公开重装箱入口是 Sources 内 `project/packaging/assemble_toolkit.py`，步骤在 `project/packaging/README.md`。以同版公开运行包提供现有 Builder、SoundTool 和实际运行依赖，以 Sources 提供当前项目源、源档、许可、7 个 wheel 及用户教程，分别指定两档解压目录和新的 stage/dist 输出。**不要求私人旧包或私有开发仓库。** 可先使用该入口的只读 `--check-inputs-only` 核输入；完整参数以同版源码说明为准。

重装箱复用匹配的固定程序，不能冒称从 C 或全部第三方源重新编译了所有二进制。Builder 源/EXE 构建的独立配方为 `project/packaging/README.md`，固定输入见其 `dependency-lock/official-python.json`、`dependency-lock/builder-wheels.json` 及同版构建控制。官方 Python embed Windows 二进制归档、完整官方 Zig Windows 维护者二进制归档仍须按锁定的官方来源/版本/摘要另取；Sources 已包含对应 Python 源、Zig bootstrap 及指定 wheel，**不宣称整个工具链完全离线**。普通使用者无需做这些维护步骤。

音效应用入口在 `project/sound-tool/`；当前供源与运行环境映射见 `project/sound-tool-package/REBUILD.md` 的当前版说明，保留的旧装箱段落仅属历史配方。FFmpeg 重建则解开唯一内档，依 `FFmpeg-selfbuild/README.md`、`build/BUILDING-NEUTRAL.md`、原构建控制与身份清单执行；四份固定源归档已在该内档内。重建或修改后摘要可能改变，需按源控制同步维护 manifest/固定校验并重新验证；这是技术一致性要求，不是额外剥夺组件修改权。

现有程序对应、公开重组和构建控制的检查不等于每台电脑重新冷编译通过，不保证跨机器 EXE 或整 ZIP 同哈希，也不产生新的机身、GUI 屏幕或救砖验证。具体结果以同版发行说明和 [已知限制](KNOWN-LIMITATIONS.md) 为准。

## 许可边界

完整源、实际二进制与原通知应保持同版对应；GPL 恢复/组合义务、FFmpeg 和运行依赖的各自条款继续适用，不统一改为 MIT。精选原许可见 [LICENSES](LICENSES/README.md)，总体范围见 [LICENSE-SCOPE](LICENSE-SCOPE.md)。来源、阴性检查、免责声明和本地上传准备不授予 Nikon 或其他权利人的权利，也不代替具体未闭合条件或实际公开批准。
