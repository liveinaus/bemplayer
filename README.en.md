<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.18**, released 2026-10-03. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.18/bemplayer-0.6.18-universal.apk) | Works on every Android TV device | 25.1 MB |

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
adb install -r bemplayer-0.6.18-universal.apk
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

- 剧集可以倒序排列：剧集一栏旁的「正序／倒序」按钮切换，每部剧单独记住，最新一集不用再一路按到底。 / Episodes can be listed newest first: the Oldest first / Newest first button by the episode row switches it, remembered for each show on its own, so the latest episode is no longer at the far end of the row.

### 修复 / Fixed

- 集数很多的剧（比如一季一百多集），在剧集一栏里连续按右键会越来越慢、焦点跑出屏幕。现在一次只画附近的剧集，按住方向键时也不再等平滑滚动。 / On a show with a great many episodes in a season, pressing right along the episode row grew slower the further it went and the focus ran off the screen. Only the episodes near the focus are drawn now, and a held or repeated direction no longer waits on a smooth scroll.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
585c0d9829a9dd0c7f0ce5eede65e8ab0f339126a676ed0bc50c9d5bce52f82d  bemplayer-0.6.18-universal.apk
```

Check one with `sha256sum bemplayer-0.6.18-universal.apk`.

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
from: `9d65b2d`.

Version 0.6.18 is build 618.
