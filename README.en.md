<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.14**, released 2026-09-24. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.14/bemplayer-0.6.14-universal.apk) | Works on every Android TV device | 19.4 MB |

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
adb install -r bemplayer-0.6.14-universal.apk
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

The green button opens diagnostics from any screen, which is the quickest way to get
information for a bug report.

## What is in this release

### 新增 / Added

- 设置里多了「代理」页，可以设置一个 HTTP 代理（主机:端口，可选用户名和密码），应用的所有请求都经过它：Emby 服务器、视频、海报、字幕、弹幕和更新检查；本机和局域网地址不经过代理。「测试连接」会通过代理访问当前服务器并显示结果。WebView 太旧、自己不能走代理的电视（Chromium 72 以前，例如荣耀电视），海报和弹幕改由应用转发，同样经过代理。 / Settings has a Proxy tab for one HTTP proxy (host:port, with an optional username and password), which everything the app fetches goes through: the Emby server, the video, posters, subtitles, danmaku and update checks. This device and its own network are always reached directly. Test asks the current server for its details through the proxy and says how it went. On a TV whose WebView is too old to follow a proxy itself (before Chromium 72, such as the Honor sets), posters and danmaku are sent through the app instead, and so through the proxy too.
- 代理也可以扫码在手机上填写：二维码在「代理」页左上角，键盘弹出也挡不住。手机上会带出现有的地址和用户名，密码不会发到手机上，留空即保留电视上已保存的；手机上也可以关闭代理。 / The proxy can be typed on a phone too, through a QR code at the top left of the Proxy tab, where the TV's keyboard cannot cover it. The phone is given the address and username already set; the saved password is never sent to it, so leaving it empty keeps the one on the TV. The phone can turn the proxy off as well.

### 变更 / Changed

- 所有弹出窗口（菜单、确认框、切换服务器、播放器里的字幕/音轨/选集菜单和手机导入弹幕）都有了页眉和页脚：标题在页眉，操作和按键提示在页脚，两者用更深的底色，中间的内容更突出。切换服务器的「添加另一个服务器」移到了页脚。 / Every popup — the menus, the questions, the server switcher, and the player's subtitle, audio, episode and phone danmaku ones — has a header and a footer on a darker ground, the title in one and the actions and remote keys in the other, so the body between them stands out. The server switcher's "Add another server" is in its footer now.

### 修复 / Fixed

- 在电视上用遥控器「下」键移到输入框、弹出系统键盘后，应用会一直当作「下」键还按着，焦点不停往下跑，什么都输入不了，离开这一页也停不下来。原因是键盘把按键抬起的信号收走了。现在输入框一获得焦点，应用就不再替遥控器补发按住的按键。 / On a TV, moving onto a text field with Down and having the system keyboard open left the app treating Down as held: focus kept running down, nothing could be typed, and it went on after leaving the screen. The keyboard had taken the key's release. The app now stops repeating a held button for a remote as soon as a text field has focus.
- 启动时显示大小总是默认值，要打开一次设置才变成自己选的，字体会突然变大或变小。语言、客户端标识和详细日志也一样，在此之前首页发给服务器的是默认标识。现在应用一启动就读取全部设置。 / The display size always opened at the default and only became the chosen one once Settings was opened, so the text jumped in size. The language, the client identity and verbose logging were the same, so until then home spoke to the server under the default identity. Every setting is now read as the app starts.
- 显示大小不是「大」时，边栏的图标没有对齐：图标用的是固定像素，边栏和间距却随显示大小缩放。现在所有图标都随显示大小缩放，每一种大小下边栏图标都在同一条线上，其他页面的图标也和旁边的文字保持比例。 / At any display size other than Large the sidebar's icons were out of line: the icons were fixed pixels while the sidebar and its spacing scaled with the setting. Every icon scales with the display size now, so the sidebar's icons share one line at every size, and icons everywhere else keep in proportion with the text beside them.
- 切换服务器列表是两列时，在右列按「下」会跳到左列。现在上下只在同一列里移动，右列最后一个再往下是「添加另一个服务器」。 / In the server switcher's two columns, Down from the right column could jump across to the left one. Up and down keep to the column now, and Down past the last server on the right goes to "Add another server".

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
a528b9ea73374e811ef819eb861be5d83f5ad889905ba669a4afda64f0abab7c  bemplayer-0.6.14-universal.apk
```

Check one with `sha256sum bemplayer-0.6.14-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

For bug reports, suggestions or a chat, there is also the Telegram group
[@bemplayer](https://t.me/bemplayer). Its QR code is under Settings → About in the app.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `525d9ed`.

Version 0.6.14 is build 614.
