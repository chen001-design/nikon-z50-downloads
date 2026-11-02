# Z50 Lab Windows tools — r10.1

[中文](README.zh-CN.md)

Experimental Windows tools for Nikon Z50 C2.60: prepare sounds in eight slots and build an independent M5 EG module from a matching official input supplied by the user. **The Windows ZIP is a computer tool package, not a complete Nikon firmware updater for direct camera installation.**

Preparation snapshot, 2026-11-02: the repository name `chen001-design/nikon-z50-downloads` is confirmed. The release target below is planned; these links do not claim that the repository or attachments are already public. Check the actual [Releases](https://github.com/chen001-design/nikon-z50-downloads/releases) state and the intended [r10.1 release](https://github.com/chen001-design/nikon-z50-downloads/releases/tag/r10.1). A prerelease may not appear under “latest”.

## Windows users

Download `Z50-Lab-Windows-Tools-r10.1-local-privacy-candidate.zip` and `SHA256SUMS.txt` from the matching release. Verify the archive and extract the entire ZIP. Ordinary use needs no separate Python, FFmpeg, Zig or Keystone installation. Existing Windows runtime prerequisites are checked by the launchers; read and decide the displayed conditions yourself.

| Task | Extracted package entry |
|---|---|
| Prepare WAV/MP3/AAC/M4A sounds for eight slots | Root `启动多音源制作工具.cmd` |
| Build an M5 EG on the computer | `PublicBuildM5/Start-PublicBuildM5.cmd`; read `PublicBuildM5/user-guide/BUILD.md` |

See the [Chinese quick start](QUICKSTART.zh-CN.md). The package includes neither official firmware nor a generated EG. Input checks must pass; the tool does not install firmware or establish a recovery procedure.

Windows ZIP: **430,722,516 bytes**, SHA256:

```text
5f28a65e5655a55bd7d5139ea333a1c3450d78f56bc0384b3958d7447e725870
```

## Developers and corresponding source

The release plan has six assets: the Windows ZIP, `Corresponding-Source.zip`, `SoundTool-Corresponding-Source.zip`, `FFmpeg-Corresponding-Source.zip`, a four-archive `SHA256SUMS.txt`, and `RELEASE-NOTES.zh-CN.md`. The three source ZIPs are byte-identical copies of the corresponding Windows ZIP members.

**This Git repository contains download documentation, licenses and identity records; its automatic GitHub “Source code” ZIP does not contain the component sources.** Obtain the physical source assets and the additional Python/Tcl/Tk and tool materials inside the Windows ZIP as explained in [SOURCE-DELIVERY.md](SOURCE-DELIVERY.md). No access to a private development repository is required. Component build controls are supplied; a fresh-machine cold rebuild or an identical complete Windows ZIP is not promised.

## Evidence and limits

The retained r10.1 checks passed 375 audio assertions, 40 golden byte comparisons, 24 historical PCM hashes and complete M5 byte identity. On 2026-11-02, the user reported that the r10.1 interface and listening tests all passed. This is an overall user report, not invented per-case, Windows-version or cross-machine evidence. Pending wording inside the unchanged package records the earlier sealing state.

The release is experimental. A reported burst-photography sound failure remains unresolved; camera installation/recovery and all Windows environments are not certified. Read [KNOWN-LIMITATIONS.md](KNOWN-LIMITATIONS.md).

[LICENSE](LICENSE) applies only within its stated scope. Project documentation terms do not relicense the programs: the recovery/combined-host GPL obligations, FFmpeg and other component terms remain separate. See [LICENSE-SCOPE.md](LICENSE-SCOPE.md). An independent download repository does not clear Nikon/Windows rights conditions or authorize publication.
