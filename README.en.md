<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.17**, released 2026-09-28. Requires Android 7.0 or newer
(API 24).

## Screenshots

On a television, at 1080p.

<table>
<tr>
<td><img src="docs/screenshots/en/home.jpg" alt="Home" width="460"></td>
<td><img src="docs/screenshots/en/library.jpg" alt="A library" width="460"></td>
</tr>
<tr>
<td><img src="docs/screenshots/en/detail.jpg" alt="A title" width="460"></td>
<td><img src="docs/screenshots/en/player.jpg" alt="The player, with the episode list" width="460"></td>
</tr>
<tr>
<td><img src="docs/screenshots/en/search.jpg" alt="Search" width="460"></td>
<td><img src="docs/screenshots/en/settings.jpg" alt="Settings" width="460"></td>
</tr>
</table>

## Download

| Download | Best for | Size |
| --- | --- | --- |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.17/bemplayer-0.6.17-universal.apk) | Works on every Android TV device | 25.1 MB |

`universal` is the one to take: it works on every device. If Bemplayer opens with a screen
saying the TV's WebView is too old, that screen says what can be done, and on a TV with
Google's WebView it can download and install a newer one itself. A newer WebView is a
system component shared by every app on the TV, and Settings → Apps → Android System
WebView → Uninstall updates puts the old one back.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.6.17-universal.apk
```

Then open Bemplayer from the Android TV home screen and enter your Emby server address,
for example `http://192.168.1.10:8096`.

## Updates

Bemplayer checks for new versions on its own and can install them without a computer.
Settings, then Updates, then Check now. Auto check is on by default and can be turned off
on the same screen.

The first update asks you to allow Bemplayer to install apps. That permission is what lets
it replace itself, and the app takes you straight to the setting.

## Using the remote

| Key                | In the player                                                              |
| ------------------ | -------------------------------------------------------------------------- |
| Centre, play/pause | Play or pause                                                              |
| Left, right        | Seek. Hold to go faster: 10s, 30s, 1m, 5m                                  |
| Up                 | Up a row of buttons; from the top row, hide the controls                   |
| Down               | Down a row of buttons; again for the episode strip; hold for the list      |
| Back               | Close the menu or QR code, then the episode strip, then ask before leaving |

Anywhere else, Back goes back one screen and never closes the app on its own. At the
screen with nothing behind it, Back asks whether to quit Bemplayer; holding Back leaves
at once, without asking.

The green button opens the logs from any screen (Settings › System › Logs on a remote
without one), which is the quickest way to get
information for a bug report.

## What is in this release

### 新增 / Added

- 杜比视界 Profile 7（UHD 蓝光原盘转封装常见的格式）兼容播放：电视不能按杜比视界解码 Profile 7 时，改为播放它底下的 HDR10 画面，不再无法播放或让服务器转码。电视能直接解码 Profile 7 的，照常按杜比视界播放。 / Dolby Vision profile 7, the one UHD Blu-ray remuxes carry, now plays on televisions that cannot decode it as Dolby Vision: the HDR10 picture underneath is shown instead of the file failing or the server converting it. A set that does decode profile 7 plays it as Dolby Vision as before.
- 告诉服务器：没有杜比视界的 HDR10 电视也能直接播放带 HDR10 或 SDR 底层的杜比视界文件（Profile 7、8），不必转码。 / The server is told that an HDR10 television without Dolby Vision can take Dolby Vision files with an HDR10 or SDR base layer (profiles 7 and 8) as they are, rather than converting them.

### 变更 / Changed

- 杜比（AC3、E-AC3、TrueHD）和 DTS 音频默认由 FFmpeg 解码，不再用电视自带的解码器；能原码输出给功放的照常原码输出。有些电视列着杜比解码器，没有授权时却只放出静音，也不报错。 / Dolby (AC3, E-AC3, TrueHD) and DTS audio are decoded by FFmpeg by default rather than by the TV's own decoder; where it can go to an amplifier untouched, it still does. Some sets list a Dolby decoder that, without a licence, plays silence and reports nothing.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
caaa8e99f1068665db9d5e0784ae3f0024bfed3eadd8e0d9bcce0188c2e1457a  bemplayer-0.6.17-universal.apk
```

Check one with `sha256sum bemplayer-0.6.17-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote (or open Settings › System ›
Logs), then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

For bug reports, suggestions or a chat, there is also the Telegram group
[@bemplayer](https://t.me/bemplayer). Its QR code is under Settings → About in the app.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `bde5e6e`.

Version 0.6.17 is build 617.
