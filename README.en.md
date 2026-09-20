<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.1**, released 2026-09-20. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.1/bemplayer-0.6.1-universal.apk) | Works on every Android TV device | 19.2 MB |

There is one APK, and it works on every device.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.6.1-universal.apk
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

| Key                | In the player                                            |
| ------------------ | -------------------------------------------------------- |
| Centre, play/pause | Play or pause                                            |
| Left, right        | Seek. Hold to go faster: 10s, 30s, 1m, 5m                |
| Up                 | Up a row of buttons; from the top row, hide the controls |
| Down               | Down a row of buttons; hold for the episodes             |
| Back               | Close the menu, then hide the controls, then leave       |

Anywhere else, Back goes back one screen and never closes the app. Hold Back to be asked
whether to quit, which is the only way out.

The green button opens diagnostics from any screen, which is the quickest way to get
information for a bug report.

## What is in this release

### 变更 / Changed

- 播放器：弹幕相关按钮统一为带圈的 D 图标，不再带文字；选集改为长按下键（短按下键到达第二行按钮，按上键回到第一行）。 / Player: the danmaku buttons are a D in a ring with no text; the episodes open on a held Down, while a tap of Down reaches the bar's second row of buttons and Up returns to the first.

### 修复 / Fixed

- 切换服务器后按返回，会回到上一个服务器的页面并报错（如「Could not load item … failed with 500」）；现在切换、登录后的返回止于首页。 / Back after switching servers reopened the previous server's screens and failed (such as "Could not load item … failed with 500"); after a switch or a sign in, Back now stops at home.
- 服务器超过四个时切换列表是两列，方向键无法从左列移到右列；现已修复。 / With more than four servers the switcher is two columns, and the D-pad could not move from the left column to the right; fixed.
- 检查更新时，版本说明很长会把「安装并重启」按钮挤到屏幕外；现在只显示前几行，「展开全文」可以看全部（按上到达，按下逐段滚动），按钮始终在屏幕上。 / Long release notes on a found update pushed the Install button off the screen; the notes now show a few lines with a Read more (Up reaches it, Down scrolls the opened notes), and the button stays on screen.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
4358990d1c83d7f5f0f3f196180d46b8492a49f08621b150e69a76f60edfd9fb  bemplayer-0.6.1-universal.apk
```

Check one with `sha256sum bemplayer-0.6.1-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `585d413`.

Version 0.6.1 is build 601.
