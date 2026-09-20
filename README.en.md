<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.5.0**, released 2026-09-19. Requires Android 7.0 or newer
(API 24).

## Download

| Download | Best for | Size |
| --- | --- | --- |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.5.0/bemplayer-0.5.0-universal.apk) | Works on every Android TV device | 16.2 MB |

There is one APK, and it works on every device.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.5.0-universal.apk
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

| Key                | In the player                                      |
| ------------------ | -------------------------------------------------- |
| Centre, play/pause | Play or pause                                      |
| Left, right        | Seek. Hold to go faster: 10s, 30s, 1m, 5m          |
| Up                 | Playback diagnostics                               |
| Down               | Audio and subtitle tracks                          |
| Back               | Close the menu, then hide the controls, then leave |

Anywhere else, Back goes back one screen and never closes the app. Hold Back to be asked
whether to quit, which is the only way out.

The green button opens diagnostics from any screen, which is the quickest way to get
information for a bug report.

## What is in this release

### 新增 / Added

- 多季的剧集可以按季筛选，默认显示最新一季，选过的季会被记住。 / A series with several seasons can be filtered by season; it opens on the latest, and a chosen season is remembered.
- 单集页面上的剧名和季名可以点击，分别打开该剧和该季。 / On an episode, the series name and the season are links: one opens the series, the other opens it on that season.
- 可以把单集、整季或整部剧标为已看（或未看），已看的内容不再被推荐；卡片上会显示已看标记。 / An episode, a season or a whole series can be marked watched (or unwatched), so it stops being recommended; cards show a watched tick.
- 媒体库页面分为「推荐」和「媒体库」两个标签，推荐页按本库展示继续观看、接下来、最近添加、最新上映、高分作品和为你推荐。 / A library opens on two tabs, Recommended and Library; Recommended shows continue watching, next up, recently added, recently released, top rated and suggestions for that library alone.
- 侧边栏可以整理：每个媒体库左侧有 ⋮ 按钮，可移动顺序或从侧边栏移除，顺序会被记住。 / The sidebar can be arranged: each library has a ⋮ handle to move it up or down or unpin it, and the order is kept.
- 设置页新增「关于」，含项目说明、版本号、GitHub 链接和二维码。 / Settings has an About section with a description, the version, the GitHub link and a QR code for it.
- 点击侧边栏顶部的 Bemplayer 标志可直接打开设置。 / The Bemplayer logo at the top of the sidebar opens Settings.
- 检查更新发现新版本时会弹出对话框，确定安装、取消忽略。 / Finding an update opens a dialog: OK installs, Cancel dismisses.
- 系统 WebView 过旧（低于 Chrome 99）时，启动页会说明原因和解决办法，而不是停在白屏。 / A TV whose WebView is older than Chrome 99 sees an explanation and what to do about it instead of a blank white screen.

### 变更 / Changed

- 侧边栏默认收起为图标栏，遥控器移入或鼠标悬停时展开，不再挤占内容区。 / The sidebar is a rail of icons that opens when the D-pad moves into it or the mouse hovers, leaving the screen to the content.
- 剧集以横向的画面缩略图卡片展示，带观看进度，而不是纯文字列表。 / Episodes are shown as a horizontal shelf of stills with progress, not a list of titles.
- 媒体库和搜索结果按行均匀铺满屏幕宽度。 / Library and search grids share each row out evenly across the screen.
- 切换视频时先显示黑屏和「正在加载…」，不再残留上一个视频的画面。 / Switching videos shows a black screen and "Loading…" until the new one has a picture, instead of the last frame of the previous one.
- 搜索范围的控件分成两行：一个开关，下面是各服务器的包含状态。 / The search scope controls are split into the switch and, under it, which servers are included.
- 焦点白框改为画在元素内部，电视上不再缺边。 / The focus ring is drawn inside the element, so it no longer loses its sides on a TV.
- 只发布 universal 版 APK，不再区分 CPU 架构。 / Only the universal APK is published, no more per-architecture builds.
- 播放器：快进快退连按或按住会累加，屏幕中央显示总变化量（如 +3:30）和落点，停止按键后才真正跳转；按住会逐级加速。 / Player: forward and back presses add up, the sum (+3:30) and where it lands are shown in the middle of the screen, and the seek happens once the presses stop; a held button climbs through larger steps.
- 播放器：控制栏右上角显示当前时间；按「上」可收起控制栏。 / Player: the bar shows the time of day in its corner, and Up takes the bar away.
- 播放器：下载速度改为实时传输速率，不再是估算值。 / Player: the download rate is what is arriving now, not an estimate of the line.

### 修复 / Fixed

- 快退和快进按钮的图标方向反了。 / The rewind and forward icons curled the wrong way.
- 打开一部剧时焦点落在「返回」上，现在落在「播放」或「继续」上。 / Opening a series landed focus on Back; it now lands on Play or Resume.
- 搜索页的侧边栏有时不显示媒体库。 / The sidebar on the search screen sometimes showed no libraries.
- 每次启动时的白色闪屏。 / The white flash on every launch.
- 发布说明取错了来源，显示成上一个版本的提交信息。 / Release notes were taken from the wrong place and showed the previous version's commit message.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
98e359bc5411dd796e100a0b963c46719f4551f114c94284ee3a9bb84fd478fe  bemplayer-0.5.0-universal.apk
```

Check one with `sha256sum bemplayer-0.5.0-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `5de1e64`.

Version 0.5.0 is build 500.
