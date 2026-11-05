# Z50 Lab: custom sound and menu voltage

[简体中文](README.md) · [Risks and limitations](KNOWN-LIMITATIONS.md) · [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases)

Experimental local tools for the **original Nikon Z50 running C2.60**: a firmware builder and an eight-slot card-sound maker. This guide covers the **r5 candidate**. Match the version and SHA-256 in its release entry; do not combine files or instructions from older releases.

> [!CAUTION]
> **Installing modified firmware can cause loss of data, camera malfunction, failure to boot or permanent damage.** Repair costs and downtime are possible. No unbricking procedure has been verified. A successful computer build, matching hash or valid CRC identifies the checked file and process; it does not establish that installation is safe on every camera. Keep official firmware if you cannot accept these risks.

## Scope

| Item | Current behavior and limits |
|---|---|
| Camera | Original **Z50 / C2.60** only, not Z50II, Z30, Zfc, Z8, ZR or another firmware version. |
| M5 sound | The project's built-in three-beep fallback plus eight fixed card slots, selection/preview and independent Off/On. The fallback is not a factory shutter sound. Startup is **Built-in / Off**. Selecting a source does not enable it; selection and On are not retained across restart. |
| Labels | Both Off selection states use `Shot sound: Off`, retaining `[ ]` / `[x]` marks. |
| Battery icon | Factory icons and low-battery warnings remain; the earlier five-bar experiment is excluded. |
| Menu voltage | `Battery cache: … mV` after Firmware version at setup-menu level. It is a factory-nominal cached value, **not capacity percentage or a live measurement**. Zero is unknown; nonzero proves neither freshness nor physical accuracy. |
| Windows | 64-bit Windows 10/11. Required Python/Tk, audio converter and fixed build dependencies are supplied; a separately installed Microsoft VC runtime is required. |

Earlier M5 feedback covered its main sound functions but retained a failure after dozens of burst shots. Current computer-generation feedback does not qualify every body, card, mode or sustained workflow. See [limitations](KNOWN-LIMITATIONS.md).

## 1. Download and extract

Select the matching [release entry](https://github.com/chen001-design/nikon-z50-downloads/releases), with both:

- `Z50-Lab-Windows-Tools-r5.zip`: the two tools, runtime/build dependencies, notices and instructions.
- `Z50-Lab-Sources-r5.zip`: complete matching corresponding source and build materials. Normal use does not require extracting it.
- `SHA256SUMS.txt` and the release notes: download identities, targets and scope.

If the two same-version ZIPs are not offered, do not assemble a substitute from different releases. Compare the runtime ZIP against its SHA256SUMS entry, for example:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath '.\Z50-Lab-Windows-Tools-r5.zip'
```

A mismatch is a stop condition. Extract the **whole ZIP** with Windows Explorer into an ordinary writable local folder. Do not launch inside an archive viewer, copy only an EXE, or merge it into an old installation. Administrator mode is not required. Preserve system-policy errors rather than disabling protection or bypassing checks.

Requirements are 64-bit Windows 10/11 and **Microsoft VC v14 x64 14.51.36247.0 or later**. The launcher checks prerequisites and points to Microsoft's official source if needed; it does not download or run an installer. No separate Python, FFmpeg or Keystone installation is needed.

## 2. Two launchers and Start-PublicBuildM5

- **`启动固件构建器.cmd`** opens the firmware-build console.
- **`启动多音源制作工具.cmd`** opens the eight-slot sound window.

Internal `PublicBuildM5/Start-PublicBuildM5.ps1` checks Windows/VC and presents the original conditions applicable to specific Microsoft code linked into the supplied official Python Windows binaries. The main build script calls it before the EXE. **Keep it; it is not a separate user action.** Declining or cancelling stops that invocation.

The older `Start-PublicBuildM5.cmd` is an alternative argument-taking EXE launcher. Only its `--dry-run` and `--check-runtime-only` branches check without starting the EXE. This combined package omits that redundant CMD and duplicate inner user launchers; the required PS1 gate and notices remain.

## 3. Generate firmware

1. Obtain original `Z_50_0260.bin` yourself from [Nikon's C2.60 page](https://downloadcenter.nikonimglib.com/en/download/fw/555.html), personally reading and deciding its terms. Do not supply another model, a modified package, generated EG, old M5 or a private recovery table.
2. Expected input: **31,972,272 bytes**, SHA-256:

   ```text
   69745c9e8f3156e936918e62a4a1fad18e7078e9ea3b95d8b8e08144b1542e49
   ```

3. Run **`启动固件构建器.cmd`**, drag the original file into the console and press Enter. Decide the per-invocation conditions yourself.
4. Wait for local recovery, compilation, composition and whole-target verification. No camera connection or physical-card scan is performed.
5. Find `EG163060.BIN` and `build-report.json` under `PublicBuildM5/Generated-Firmware/<timestamp>/`. Existing results are not overwritten.

Default r5 target:

```text
File: EG163060.BIN
Bytes: 31665490
SHA-256: eb33fab29b6ba337484961a852dd3a634f8c9573ac1b6631f1e20f692accd318
CRC16-XMODEM trailer: 665B; whole-file residue: 0
Profile: m5-battery-cache
```

The report must say `EXACT-PINNED-TARGET`, with the matching size, hash and profile. You can hash the BIN independently. Stop on failure, missing report or mismatch; do not edit check values to accept an unexplained result.

This EG is an **independent main module**, not the official complete `Z_50_0260.bin` update container. Do not rename one as the other. A valid CRC is not an official signature or approval.

The advanced `--profile m5-only` option reproduces frozen M5, SHA-256 `09f539c078676509db12f759a4a9e2fe1516b7455e031635fd60bb677876d03e`, without the voltage item and with the original wording. The normal root launcher uses the r5 combination above; no such option is needed.

## 4. Make sound files

This local step needs no connected camera/card.

1. Run **`启动多音源制作工具.cmd`**, decide the startup conditions, and use the “制作存储卡多音源” window.
2. Each of eight rows maps permanently to slot 1–8. Choose WAV, MP3, AAC or M4A for desired slots; blank slots produce no file.
3. Click “制作所选槽位音源包”. Each sound longer than about 0.5 seconds needs explicit agreement to keep its beginning. Declining any prompt cancels the entire package. Short sounds are padded with silence.
4. Choose a local parent folder. A new `Z50-多音源-<slots>-<input digest>/` is created. The same inputs/slots give the same name; select another parent if it already exists.
5. **Listen to the WAVs in `previews/` first**, then use the SNDs in `sd-card/`.

Slots produce `SOUND01.SND` through `SOUND08.SND`. Each is **96,032 bytes**. Computer preparation uses 48 kHz, stereo, 16-bit and 24,000 frames; this is not physical playback-clock calibration. Do not rename a WAV to SND or edit its header/CRC. The manifest, previews and notes are for computer inspection, not firmware installation.

## 5. Optional experimental installation

Back up photographs, required card files and settings, and verify the backups. Retain independently obtained official firmware. Use stable power, sufficient charge and a healthy readable card. If formatting is required, back up first and follow the camera instructions; formatting erases data and these tools do not perform it.

This is the project's existing **C2.60 standalone-EG route**, limited to an original Z50 already at C2.60 that can enter normal updating. It is not Nikon endorsement, a general first-install/downgrade procedure or a non-booting-camera rescue route.

1. Verify the default target. Shut down normally, wait for card access to finish, then use a reader to put **one `EG163060.BIN` at the card root**, keeping its name. Do not mix firmware candidates or copy the enclosing output folder as firmware. Existing SNDs may remain.
2. Safely eject, insert while the camera is off, then open **Setup menu → Firmware version** and check recognition.
3. Stop if no update is offered, compatibility is rejected, identification is unexpected or an error appears. Do not alter model/version/filename, rename EG as the official container, use another camera's method or enter an unknown service mode.
4. Only after accepting the risk and normal recognition, confirm using the camera's screen. **Do not power off, remove the battery or remove the card during updating.** Do not invent a forced-power-off timeout.
5. After an explicit completion message, follow its shutdown instructions, remove the update file/card and restart normally. The header remains C2.60. Check the M5 controls, shortened Off label and cached-mV entry, then cautiously check normal capture, saving and playback.

Nikon's linked page describes its official full package, not this modified module. Deleting the card update file does not undo firmware already written. An official reinstall is at most a direction while normal updating remains available; it is **not an unbricking guarantee**.

## 6. Use card sounds and menus

With compatible M5 firmware installed, power off normally and wait for card access before copying the selected **SND files themselves** from `sd-card/` to the card root. Do not copy the enclosing folder or substitute preview WAVs. The package does not generate or delete unselected slots.

Sounds load at normal startup and can then be selected repeatedly in-camera. Power off before replacing SNDs/cards; do not hot-remove a card. Bounded FAT16/FAT32/exFAT paths do not qualify every card, capacity, partition or layout.

Open **Setup menu → Beep options → `Shot sound / pitch`**:

1. Select and confirm `Built-in (3 beeps)` (the project's fallback, not a factory shutter sound) or `SD sound 1`–`8`, then inspect its mark.
2. Selection/focus can preview, **including while Off**.
3. Separately select `Shot sound: On` for custom capture sound. Selection alone does not enable it.
4. `Shot sound: Off` disables added capture sound while retaining the current-session source. Factory beeps and mechanical shutter retain factory settings. Restart returns to Built-in/Off.

For unavailable entries check the exact filename, double extensions, tool-produced 96,032-byte SND and card-root placement, then restart normally.

Find `Battery cache: … mV` after Firmware version. Zero displays unknown. Nonzero nominal cache has no guaranteed age, validity or physical calibration. The value is read only when its native text record is reconstructed; reopening, scrolling, focus, repaint or wake does not promise a new sample. Do not infer a precise percentage or use it as the sole update-power check. Factory battery icons/warnings remain.

## 7. Errors, limits, source and license

Keep full error messages. Use a new writable local output on save/existing-output errors, without administrator mode or weaker system security labels. On decoder errors, check complete extraction and a supported playable input. For ordinary capture/audio faults, stop triggering and retain diagnostics/conditions rather than repeatedly flashing, hot-removing cards or stressing the camera.

`F009:003` illustrates a colon-form fault; `F012/003` with a slash may be a normal source display. These are not photo/playback-completion counters. During an update, keep power stable and preserve its screen state rather than applying ordinary post-preview shutdown advice.

`CA-M5-STRESS-01` remains: custom sound may fail after dozens of burst shots; exact threshold, probability and cause are unresolved. Do not repeat pressure tests merely to verify this guide. No per-frame replay, fixed latency or indefinite stability is promised. [Known limitations](KNOWN-LIMITATIONS.md) remain applicable.

The public front repository carries user guides, limits, version and source/download indexes. Matching **Sources** physically supplies builder/menu/package/sound-tool preferred sources, fixed third-party sources, original notices and build controls. It is separate from the runtime ZIP. Original/recovered/modified complete firmware, private Git history, research databases, debug logs, caches and old candidates are excluded from uploads.

Keep licenses and attribution; see [LICENSE](LICENSE) and [license scope](LICENSE-SCOPE.md). Project terms cover only expression contributors can license; GPL recovery and third-party terms remain separate, without Nikon firmware/resource rights or Nikon sponsorship, approval or warranty. Read the actual licenses in Sources. Disclaimers do not replace rights or verification.

Documentation structure was informed by [NikonFirmwarePatch for Z8](https://github.com/XinmiaoZhao/NikonFirmwarePatch) and [WonderLantern Z8](https://github.com/WonderLantern/z8-qemu)/[ZR](https://github.com/WonderLantern/zr-qemu) scope/input guides. Their emulator evidence is not this project's camera qualification; their code, licensing, features and supported models remain independent.
