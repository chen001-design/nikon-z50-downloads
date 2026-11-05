# 风险与已知限制 / Risks and known limitations

本说明对应第一代 Nikon Z50 C2.60、默认 `m5-battery-cache` r5 组合及其双工具交付。它不是官方固件、稳定性认证或安装安全保证。

## 刷写与恢复

- 修改固件可能导致无法启动、拍摄异常、数据丢失或永久损坏；应评估维修成本和停机风险。
- `EG163060.BIN` 是独立主模块，不能改名成官方整包 `Z_50_0260.bin`。独立模块路径仅按本工程已使用的 C2.60 条件描述，不泛化首刷、降级或其它机型。
- 更新前备份并核可读取，保持充分、稳定供电；更新期间不关机、不拔卡、不取电池。识别异常或不兼容时停止，不强行改版本/型号/文件名继续。
- 删除卡上更新文件不会撤销已写入固件。正常菜单可用时的官方重装不等于故障开机状态可恢复。**没有经过验证的救砖方案。**

## 音效

- **CA-M5-STRESS-01 未修复：** 历史用户反馈连续连拍几十张后可能自定义音效失效。精确阈值、概率与根因未定；本轮不重做压力复现。不保证每帧重播、固定延迟或无限稳定。
- 启动为 Built-in/Off，选源不会自动启用，选择与On不跨重启保存。Off可试听；原厂蜂鸣音与机械快门仍按原设置工作。
- 输入WAV/MP3/AAC/M4A在电脑准备为固定短声；长声必须明确同意截取，短声补静音。48kHz/24000帧是准备约定，未作为机内播放时钟的实测校准。
- 卡声音在正常开机时加载；变更文件或卡应先正常关机。受限FAT16/FAT32/exFAT实现不认证每种卡、容量、分区或损坏状态。

## 电量与验证范围

- 电压来自原厂标称缓存u32，0按未知；非零不证明有效、新鲜或物理准确。未有实测标定系数，不换算精确容量百分比。
- 记录实际重建时读取缓存；重开菜单、滚动、确认、重画和唤醒不保证新采样。原厂图标和低电警告保留，缓存数值不能替代更新供电判断。
- 离线/构建/来源一致性结果，以及先前未逐项细分的电脑生成或M5用户反馈，不代表所有机身、卡、模式、Windows电脑或长期运行已验证。程序依赖、完整解压与VC前置仍须满足。
- 无已验证的恢复保证、整机安全结论或本轮新增实机/屏幕验证。已知路径/凭据模式的阴性检查不是对所有秘密、漏洞或权利的穷尽认证。

## 来源与再分发

运行包与同版完整Sources分开提供；Sources须与程序同时、清晰、等价可取得。保留原通知与许可，不以仅列上游主页或版本号替代实际对应源。项目条款不授予Nikon固件/资源的权利；具体第三方条件与既有适用范围保持。免责声明和技术检查不等于权利清理或公开批准。

---

**English:** This is an experimental original-Z50/C2.60 candidate, not installation-safety or stability certification. Modified firmware can fail to boot, malfunction, lose data or cause permanent damage. There is no verified unbricking procedure. Keep EG distinct from Nikon's full container; stop on recognition/compatibility errors and preserve power throughout an update.

The unresolved M5 burst-sound failure after dozens of shots remains. Startup is Built-in/Off and settings are not persisted across restart. Preview is possible while Off. Fixed short-sound preparation and bounded FAT16/FAT32/exFAT support do not qualify all clocks/cards/workflows.

Cached nominal mV is not a fresh calibrated measurement or capacity percentage. A nonzero sample, matching hash or successful computer build is not physical safety proof. No new broad camera/GUI/long-run qualification is asserted. Sources and actual licenses remain available separately with the same version; disclaimers do not grant third-party rights or publication approval.
