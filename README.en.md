# Nikon Z50 Lab — Custom sound and Windows tools

[中文](README.md) · [Download](https://github.com/chen001-design/nikon-z50-downloads/releases) · [Tutorial](#tutorial) · [Risks](#risks-and-known-limitations)

## About

Z50 Lab is an experimental custom shooting-sound project for the **original Nikon Z50 with official C2.60 firmware**. Version **r10.1** contains an eight-slot sound preparation application and an M5 module builder.

The sound application converts WAV, MP3, AAC and M4A into numbered SND files and computer-preview WAVs. The builder validates a matching official input you supply and creates an independent EG module and report. The companion camera design has eight fixed SD slots, a built-in three-beep fallback and a separate enable switch. Sounds load on normal startup; selection then uses cached sounds. Each startup returns to Built-in/Off; selection and enable state are not retained across restarts.

This project is independent of Nikon. **The ZIP is a computer tool package, not a complete Nikon update ready to install.** Official firmware and generated EG files are not supplied. Creating sound files does not install the companion camera functionality.

## Download

**One download location: [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases).** Open the **r10.1** entry and obtain these **Assets**:

1. `Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip`
2. `SHA256SUMS.txt`

Automatic `Source code (zip)` / `Source code (tar.gz)` downloads contain this documentation repository, not the Windows tools. Find the experimental prerelease by version in Releases.

> Status on 2026-11-03: the repository remains private and r10.1 remains a draft. Public downloads are not open. The link above is the fixed download location, not a claim of public availability.

The Windows ZIP is **430,722,516 bytes**. In its download directory, PowerShell can check it with:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath '.\Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip'
```

Expected SHA256:

```text
5f28a65e5655a55bd7d5139ea333a1c3450d78f56bc0384b3958d7447e725870
```

## Tutorial

### 1. Extract and prepare

Extract the whole Windows ZIP, keeping every subdirectory. Its root contains `启动多音源制作工具.cmd` and `PublicBuildM5/`. Do not move only an EXE.

Launch prerequisites are **Windows 10/11 x64**, system UCRT and Microsoft VC v14 x64 runtime at least `14.51.36247.0`. No separate Python, FFmpeg, Zig or Keystone installation is needed. Missing runtimes stop startup and show the Microsoft acquisition location; they are not installed automatically.

Read the displayed applicable conditions yourself. Enter `Y` to continue; `N` or Enter cancels. This does not accept Nikon's download agreement or another installer's terms for you.

### 2. Prepare and listen to sounds

1. Double-click the root **`启动多音源制作工具.cmd`** to open the Chinese “制作存储卡多音源” window.
2. Use **“选择声音…”** in the desired numbered slots for audio you have the right to process. Select at least one slot; all eight are not required.
3. Click **“制作所选槽位音源包”**. Long sounds prompt to keep roughly the first half-second; declining cancels the entire job. Short sounds receive silence padding.
4. Select a save location on the computer. The tool creates a new package there and refuses to overwrite an existing same-named package; choose another location if necessary.
5. Listen to the WAVs under **`previews/`** first. **`sd-card/`** contains only the selected numbered `SOUND01.SND` through `SOUND08.SND`, with a manifest and instructions alongside.

Camera use of SND files requires the compatible multi-sound implementation. Selecting a sound does not enable shooting sound; enable it separately. The built-in three beeps are a project fallback, not the original shutter sound. Rescanning new files while powered on and remembering selections across restarts are not supported.

### 3. Build an M5 module on the computer

Supply an unmodified official **Z50 C2.60** complete input that you have the right to use, such as `Z_50_0260.bin`. The tool does not acquire it or accept its terms. Other models, versions or modified inputs are not substitutes.

Open PowerShell in the extracted **`PublicBuildM5`** folder, replacing both example paths with your own:

```powershell
.\Start-PublicBuildM5.cmd --source "D:\Firmware\Z_50_0260.bin" --output "D:\Builds\Z50-M5-new"
```

The parent `D:\Builds` must already exist and be writable; the final `Z50-M5-new` directory must not exist. Keep quotation marks around paths. **This builder is a command-line tool, not a firmware file chooser. Double-clicking or omitting the required arguments cannot complete a build.**

A successful new output directory contains **`EG163060.BIN`** and **`build-report.json`**. Resolve version, file or directory errors rather than bypassing checks. The baseline M5 is 31,665,490 bytes; see [VERSION.json](VERSION.json) for its full identity.

EG is an independent module, not a complete official update. Do not transfer installation procedures from another model. This tutorial ends at computer generation and verification: the tool does not install, write a card or connect to a camera. A successful build does not establish installation safety or recoverability. The package's `PublicBuildM5/user-guide/BUILD.md` documents the matching commands.

## Risks and known limitations

- Firmware-related processing or later use can cause an unbootable camera, damaged files or data loss. Back up important material; do not make an experimental setup your only provision for irreplaceable work.
- Unbricking, failed-start recovery and a general recovery route have not been verified. Returning to stock is not a recovery guarantee.
- `CA-M5-STRESS-01`: sound may stop after dozens of continuous shots. Cause, exact threshold and probability are unknown; it remains unresolved.
- Eight fixed slots load at normal startup. This is not an arbitrary-file browser; each startup returns to Built-in/Off, selection does not enable sound, and state is not persistent.
- Existing r10.1 audio checks, complete M5 byte identity and overall manual interface/listening acceptance do not certify every Windows host, camera, card, mode or sustained burst.

See [KNOWN-LIMITATIONS.md](KNOWN-LIMITATIONS.md) and [VALIDATION.json](VALIDATION.json). Pending wording in the unchanged package is an earlier sealing snapshot; it does not replace later overall feedback or invent additional tests.

## Disclaimer and licensing

Maintained by Z50 Lab contributors, independently of Nikon, without Nikon affiliation, sponsorship or endorsement. Product names identify interoperability targets; their owners retain their rights.

Software and documentation are provided as-is, without promises of fitness, continued availability, device safety or recovery. Assess your circumstances before use. Warranty and liability scope follows applicable law and each component's license; this statement does not exclude liability that cannot lawfully be excluded or guarantee the same effect in every jurisdiction.

Project licensing grants no rights to Nikon firmware, input-derived material, trademarks or other third-party content. Obtain the rights needed for your firmware/audio processing and observe applicable terms. A disclaimer, passing tests or a public repository is not a third-party authorization. Specific Nikon/Windows rights applicability remains unresolved and public release requires separate approval.

See [LICENSE](LICENSE) and [LICENSE-SCOPE.md](LICENSE-SCOPE.md). Qualified documentation MIT terms do not make the entire software bundle MIT; recovery/combined-program GPL and other component terms remain. This text adds no restriction to modification or redistribution rights granted by those licenses.

Matching release attachments include Builder, SoundTool and FFmpeg corresponding-source archives; additional Python/Tcl/Tk, Zig sources and original licenses remain in the complete Windows ZIP. Locations and component build instructions are in [SOURCE-DELIVERY.md](SOURCE-DELIVERY.md).
