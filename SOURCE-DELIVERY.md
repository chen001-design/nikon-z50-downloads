# r10.1 实际供源与组件重建入口

本说明针对 r10.1 Windows ZIP 的实际组件。拟定公开取得入口为 [r10.1 Release](https://github.com/chen001-design/nikon-z50-downloads/releases/tag/r10.1)，实际是否已发布以该页附件为准，不要求访问任何私有开发仓库。

## 四个 ZIP 与完整材料

| 发布附件 | 内容及入口 |
|---|---|
| `Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip` | 完整运行工具及其他依赖源/许可材料，430,722,516 字节；包括下列三个源 ZIP |
| `Corresponding-Source.zip` | 原构建器实际对应源，333 个成员；从 `packaging/README.md` 开始 |
| `SoundTool-Corresponding-Source.zip` | 当前音效应用、启动器、装箱说明及项目条款，30 个成员；从 `sound-tool-package/REBUILD.md` 开始 |
| `FFmpeg-Corresponding-Source.zip` | 当前 FFmpeg/FFprobe 完整供源树，120 个成员；从 `FFmpeg-selfbuild/README.md` 开始 |

三个单独源附件是从 Windows ZIP 原样取出的同一成员，没有解包重压缩或替换。`SHA256SUMS.txt` 列出以上四档的完整 SHA256；第六个附件为 `RELEASE-NOTES.zh-CN.md`。

**这三个源 ZIP 不穷尽 Windows 包的全部依赖材料。** Python/Tcl/Tk 等材料仍须从完整 Windows ZIP 取得。GitHub 自动生成的 Source code ZIP 只含本说明仓库，不能替代以上实体源档或下列包内材料。

## 构建器源码

将 `Corresponding-Source.zip` 解压到新目录，阅读 `packaging/README.md`。正式源码入口是 `packaging/portable_entry.py`，或按该说明使用 `packaging/official_runtime.py` 进入 `build_m5.py`。源档根备用 `portable_entry.py` 存在已知隔离模式路径问题；它不是本页推荐的入口，也不代表已保留的 Windows 程序有同一故障。

完整首选汇编/派生控制在源档的 `assembly/`、`maintainer/generate_assembly.py` 等位置，构建控制包括 `packaging/build_portable.py`。依赖版本和取得哈希在 `packaging/dependency-lock/official-python.json`、`builder-wheels.json`；宿主及打包轮子按其中公开固定来源自行准备，不依赖本仓库外的私有路径。构建所需官方固件输入仍由使用者自行取得并满足适用条件。

当前 Windows ZIP 可提供 `PublicBuildM5/deps/zig/` 的完整 Zig 0.15.2 工具和 `lib/` 源。另有 `Third-Party-Source/zig-bootstrap-0.15.2.tar.xz`、同名 `.minisig` 及 `Third-Party-Notices/Zig-0.15.2/` 原通知；其 `SOURCE-DELIVERY.json` 说明源范围。不要把这些原许可套成项目 MIT。

## 音效应用源码与运行环境

在 `SoundTool-Corresponding-Source.zip` 中，应用入口为 `sound-tool/launch_sound_gui.py` 和 `sound-tool/sound_cli.py`，具体运行布局见 `sound-tool-package/REBUILD.md`。

按该说明使用当前 Windows ZIP 的 `SoundTool/runtime/`，并从同一包的 `SoundTool/vendor/ffmpeg-s22/` 取得匹配解码器、原许可和 manifest，按相同相对布局放置。应用固定身份校验、manifest 与两程序必须相互一致，不混用其他构建。

历史整包装箱保全配方以特定历史基包为输入，该基包不在本发行范围。那些脚本不是本版组件源码取得、运行或独立组件编译的必需入口；不将它们当作从本说明仓库裸克隆后一键重打完整 Windows ZIP 的承诺。本页提供的是当前组件的实际源和当前运行材料。

## FFmpeg/FFprobe 源码

将 `FFmpeg-Corresponding-Source.zip` 完整解压，进入 `FFmpeg-selfbuild/`。先核对其中 `FILES.json` 和 `SHA256SUMS.txt`，再读 `build/BUILDING-NEUTRAL.md`，使用 `build/unpack-sources.py`、`build/rebuild-neutral.py` 和固定的宿主工具取得记录。

其 `archives/` 物理包含四个固定源档；无需从私有仓库补取。相同完整树也在 Windows ZIP 的 `SoundTool/dependency-materials/FFmpeg-selfbuild/`。固定 FFmpeg 源提交为 `946fcce07b6dcd0331c8cc609192aeff5e1924f8`；实际014中性路径构建保留原后端选择，七项成功探测及显式兼容策略分别留有记录，其余3139个非路径宏一致。完整原版权、组件条款和实际控制随源提供。

自行修改或重建组件后，SHA 可能改变；需按源码身份控制同步维护 manifest/固定校验值并重新验证。这个技术一致性要求不把组件修改权改成额外许可限制。公开参数化配方经过静态对应核验，没有在本次准备中再执行第二次完整冷重建，不保证跨机器 EXE 或整 ZIP 同哈希。

## Python、Tcl/Tk 与其他依赖

以下路径都相对于完整解压的 Windows ZIP：

| 材料 | 实际路径 |
|---|---|
| 当前 Python/Tcl/Tk 运行环境 | `SoundTool/runtime/`，927 个保留文件 |
| Python 3.14.10、Tcl/Tk 及合并组件的13份源档 | `SoundTool/dependency-materials/Third-Party-Source/Python/` |
| 上述源档身份锁 | `SoundTool/dependency-materials/SOURCE.lock.json` |
| 运行文件身份锁 | `SoundTool/dependency-materials/runtime-files.lock.json` |
| Python 运行来源 | `SoundTool/dependency-materials/build-info/Python-runtime-provenance.json` |
| 许可四组 | `SoundTool/dependency-materials/licenses/Python/`、`Python-Windows/`、`Python-components/`、`Python-pip-bundled/` |
| 原 Windows 许可材料 | `SoundTool/licenses/release-preflight/r6-python-ms/CPython-3.14.10-WINDOWS-LICENSE.txt` |

源档目录中包括 `Python-3.14.10.tgz`，以及 bzip2、expat、hacl-star、libffi、mpdecimal、openssl、tcl、xz、zlib-ng、zstd、tk、sqlite 的固定源包。还应保留 Windows ZIP 内各组件原通知和其他 `Third-Party-Source/`、`Third-Party-Notices/` 材料。组件取得/构建说明的存在不等于本次运行了全部依赖构建，也不构成新装系统或所有平台验证。

根目录为文档/许可/身份索引，不是另一个完整开发代码树。完整源、二进制、原条款应一起按本版固定身份使用；总体许可范围见 [LICENSE-SCOPE.md](LICENSE-SCOPE.md)。
