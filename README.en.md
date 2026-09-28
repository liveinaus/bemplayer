<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.16**, released 2026-09-28. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.16/bemplayer-0.6.16-universal.apk) | Works on every Android TV device | 25.1 MB |

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
adb install -r bemplayer-0.6.16-universal.apk
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

- 设置 › 播放 › 音频解码：自动、本机解码（不原码输出）、FFmpeg 软件解码三选一。有的电视原码输出或自带杜比解码时只有静音、也不报错，应用无法察觉，换一种就能出声。 / Settings › Playback › Audio decoding: Automatic, Decode here (no passthrough) or FFmpeg in software. Some sets play passthrough, or their own Dolby decoding, as silence without any error the app can see, and another choice brings the sound back.
- 文件的声音本机完全无法播放（例如 WMA、RealAudio）时，在允许转码的情况下自动请服务器把声音转成这里能播放的格式；不允许转码时画面上会说明怎么打开。 / When nothing here can play a file's sound at all (WMA or RealAudio, say), the server is asked to convert it, where transcoding is allowed; where it is not, a line over the picture says how to allow it.

### 修复 / Fixed

- 很多电视没有杜比或 DTS 的解码授权，播放 AC3、E-AC3（杜比数字+）、DTS 或 TrueHD 音轨时只有画面没有声音，也不报错，例如大多数版本的《老友记》。现在应用自带 FFmpeg 软件解码，电视自己解不了的音轨由它来解。 / Many televisions have no Dolby or DTS decoder licence, so an AC3, E-AC3 (Dolby Digital Plus), DTS or TrueHD track played as picture without sound and no error, as most copies of Friends do. The app now carries FFmpeg and decodes in software whatever the set cannot.
- 电视自带的音频解码器或原码输出出错时，会自动改用软件解码重试；解出的多声道被拒绝时再缩混成立体声。0.6.15 只处理了多声道输出被拒这一种情况。 / When the set's own audio decoder or its passthrough fails, playback retries decoding in software, and downmixes to stereo if the set then refuses the surround. 0.6.15 only covered the refused surround output.
- 隧道播放只用在高于 30 帧的视频上。有的电视在隧道模式下播放的声音是静音，也不报错，而 24、25、30 帧的影片和剧集用它没有任何好处。 / Tunnelled playback is only used for video above 30 frames a second. Some sets play tunnelled audio as silence without reporting it, and film and TV at 24, 25 or 30 frames gain nothing from it.
- 告诉服务器的音频格式名称改成 Emby 自己用的：PCM 按采样格式（pcm_s16le 等）、DTS 也叫 dca，并补上 MP2、AMR 和 G.711。以前名字对不上，服务器会把本来能直接播放的文件拿去转码或拒绝。 / The audio codecs the server is told about now use Emby's own names: PCM by sample format (pcm_s16le and the rest), DTS as dca too, and MP2, AMR and G.711 added. Names that did not match had the server convert, or refuse, files that play here as they are.
- 如果一条音轨本机确实无法播放，画面上方会写明，播放信息面板的「输出」也会显示；运行日志里记下音轨的格式和用的是哪个解码器。 / If an audio track really cannot be played here, a line over the picture says so and the info panel's Output shows it; the logs name the track's format and which decoder was used.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
e7bdd648e4eeea6d12bfddbe2a11a4addd9ece6bf6a454523eeb4221048ff8a4  bemplayer-0.6.16-universal.apk
```

Check one with `sha256sum bemplayer-0.6.16-universal.apk`.

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
from: `b4e4e1d`.

Version 0.6.16 is build 616.
