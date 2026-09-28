<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.6.16**，发布于 2026-09-28。需要 Android 7.0
或更高版本（API 24）。

## 截图

在电视上的样子（1080p）。

<table>
<tr>
<td><img src="docs/screenshots/zh/home.jpg" alt="首页" width="460"></td>
<td><img src="docs/screenshots/zh/library.jpg" alt="媒体库" width="460"></td>
</tr>
<tr>
<td><img src="docs/screenshots/zh/detail.jpg" alt="详情页" width="460"></td>
<td><img src="docs/screenshots/zh/player.jpg" alt="播放器与选集" width="460"></td>
</tr>
<tr>
<td><img src="docs/screenshots/zh/search.jpg" alt="搜索" width="460"></td>
<td><img src="docs/screenshots/zh/settings.jpg" alt="设置" width="460"></td>
</tr>
</table>

## 下载

| 下载 | 适合 | 大小 |
| --- | --- | --- |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.16/bemplayer-0.6.16-universal.apk) | 适用于所有 Android TV 设备 | 25.1 MB |

下载 `universal` 即可，所有设备都能用。如果打开 Bemplayer 后显示「此电视的 WebView 太旧」，那个界面会说明
可以怎么做；使用 Google WebView 的电视可以在界面上直接下载并安装新版。新的 WebView 是电视上所有应用共用的
系统组件，如需恢复：设置 → 应用 → Android System WebView → 卸载更新。

## 安装

Android TV 默认不允许安装来自文件的应用。第一次安装时会弹出提示，并直接指向对应的设置页面。

**用文件管理器或投送工具**，例如 Downloader 或 Send Files to TV：把 APK 传到电视上，打开
它，同意安装提示。

**用 adb**，在同一网络的电脑上执行：

```bash
adb connect <电视的IP>:5555
adb install -r bemplayer-0.6.16-universal.apk
```

然后在 Android TV 主界面打开 Bemplayer，填入你的 Emby 服务器地址，例如
`http://192.168.1.10:8096`。

## 更新

Bemplayer 会自行检查新版本，不用电脑也能安装。进入设置，再进更新，然后点立即检查。自动检查
默认开启，也可以在同一个页面关掉。

第一次更新会请求允许 Bemplayer 安装应用。正是这个权限让它可以替换自己，应用会直接带你到那个
设置项。

## 遥控器按键

| 按键              | 在播放器中                                             |
| ----------------- | ------------------------------------------------------ |
| 确定键、播放/暂停 | 播放或暂停                                             |
| 左、右            | 快退快进。按住会加速：10 秒、30 秒、1 分、5 分         |
| 上                | 回到上一行按钮；在最上一行时收起控制栏                 |
| 下                | 到达下一行按钮；再按展开剧集缩略图条；长按打开选集列表 |
| 返回              | 先关菜单或二维码，再收起剧集条，最后询问是否停止播放   |

在其他界面，返回键是返回上一层，不会自己关掉应用。回到没有上一层可回的那一屏时，按返回会询问
是否退出 Bemplayer；长按返回则直接退出，不再询问。

绿色按键在任何界面都能打开运行日志（遥控器没有绿色按键时，在 设置 › 系统 › 运行日志 打开），这是拿到反馈问题所需资料最快的办法。

## 这个版本有什么

### 新增 / Added

- 设置 › 播放 › 音频解码：自动、本机解码（不原码输出）、FFmpeg 软件解码三选一。有的电视原码输出或自带杜比解码时只有静音、也不报错，应用无法察觉，换一种就能出声。 / Settings › Playback › Audio decoding: Automatic, Decode here (no passthrough) or FFmpeg in software. Some sets play passthrough, or their own Dolby decoding, as silence without any error the app can see, and another choice brings the sound back.
- 文件的声音本机完全无法播放（例如 WMA、RealAudio）时，在允许转码的情况下自动请服务器把声音转成这里能播放的格式；不允许转码时画面上会说明怎么打开。 / When nothing here can play a file's sound at all (WMA or RealAudio, say), the server is asked to convert it, where transcoding is allowed; where it is not, a line over the picture says how to allow it.

### 修复 / Fixed

- 很多电视没有杜比或 DTS 的解码授权，播放 AC3、E-AC3（杜比数字+）、DTS 或 TrueHD 音轨时只有画面没有声音，也不报错，例如大多数版本的《老友记》。现在应用自带 FFmpeg 软件解码，电视自己解不了的音轨由它来解。 / Many televisions have no Dolby or DTS decoder licence, so an AC3, E-AC3 (Dolby Digital Plus), DTS or TrueHD track played as picture without sound and no error, as most copies of Friends do. The app now carries FFmpeg and decodes in software whatever the set cannot.
- 电视自带的音频解码器或原码输出出错时，会自动改用软件解码重试；解出的多声道被拒绝时再缩混成立体声。0.6.15 只处理了多声道输出被拒这一种情况。 / When the set's own audio decoder or its passthrough fails, playback retries decoding in software, and downmixes to stereo if the set then refuses the surround. 0.6.15 only covered the refused surround output.
- 隧道播放只用在高于 30 帧的视频上。有的电视在隧道模式下播放的声音是静音，也不报错，而 24、25、30 帧的影片和剧集用它没有任何好处。 / Tunnelled playback is only used for video above 30 frames a second. Some sets play tunnelled audio as silence without reporting it, and film and TV at 24, 25 or 30 frames gain nothing from it.
- 告诉服务器的音频格式名称改成 Emby 自己用的：PCM 按采样格式（pcm_s16le 等）、DTS 也叫 dca，并补上 MP2、AMR 和 G.711。以前名字对不上，服务器会把本来能直接播放的文件拿去转码或拒绝。 / The audio codecs the server is told about now use Emby's own names: PCM by sample format (pcm_s16le and the rest), DTS as dca too, and MP2, AMR and G.711 added. Names that did not match had the server convert, or refuse, files that play here as they are.
- 如果一条音轨本机确实无法播放，画面上方会写明，播放信息面板的「输出」也会显示；运行日志里记下音轨的格式和用的是哪个解码器。 / If an audio track really cannot be played here, a line over the picture says so and the info panel's Output shows it; the logs name the track's format and which decoder was used.

以前每个版本改了什么，见 [更新日志](CHANGELOG.md)。

## 校验下载的文件

```
e7bdd648e4eeea6d12bfddbe2a11a4addd9ece6bf6a454523eeb4221048ff8a4  bemplayer-0.6.16-universal.apk
```

用 `sha256sum bemplayer-0.6.16-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键（或 设置 › 系统 › 运行日志），然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

问题反馈、功能建议或随便聊聊，也可以加入 Telegram 群组 [@bemplayer](https://t.me/bemplayer)。
应用里 设置 → 关于 有它的二维码。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`b4e4e1d`。

版本 0.6.16 是第 616 号构建。
