<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.6.2**，发布于 2026-09-21。需要 Android 7.0
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.2/bemplayer-0.6.2-universal.apk) | 适用于所有 Android TV 设备 | 19.3 MB |

只有一个安装包，所有设备都用它。

## 安装

Android TV 默认不允许安装来自文件的应用。第一次安装时会弹出提示，并直接指向对应的设置页面。

**用文件管理器或投送工具**，例如 Downloader 或 Send Files to TV：把 APK 传到电视上，打开
它，同意安装提示。

**用 adb**，在同一网络的电脑上执行：

```bash
adb connect <电视的IP>:5555
adb install -r bemplayer-0.6.2-universal.apk
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

在其他界面，返回键是返回上一层，永远不会直接关掉应用。长按返回键才会询问是否退出，这是离开应
用的唯一方式。

绿色按键在任何界面都能打开诊断信息，这是拿到反馈问题所需资料最快的办法。

## 这个版本有什么

### 新增 / Added

- 播放器：短按下键到按钮最下一行之外，会在控制栏下方展开本剧全部剧集的缩略图条（和剧集页一样），落在正在播放的一集上，左右浏览、中键切换；上键或返回收起。长按下键的选集列表保持不变。 / Player: a tap of Down off the bottom row of buttons opens a strip of the series' episode stills under the controls, as the series screen shows them, on the one playing; Left and Right browse it, OK switches, Up or Back puts it away. The list a held Down opens is unchanged.
- 播放器：右上角时间旁显示实时下载速度，即此刻真正从服务器收到的数据速率；不足 1 Mbps 时以 kbps 显示，没有数据到达时显示 0 kbps。电视上此前一直不显示，已修复。 / Player: the live download speed sits beside the clock in the top corner, the bytes actually arriving from the server at that moment; under a megabit it is written in kbps, and nothing arriving reads 0 kbps. On a TV it never showed before; fixed.

### 变更 / Changed

- 播放器：按返回不再直接退出播放，而是先询问「停止播放？」，中键确认离开，再按返回则继续看；控制栏上的返回按钮同样询问。播放尚未开始或已出错时直接离开。 / Player: Back no longer leaves the video outright; it asks "Stop watching?", OK leaves and Back again stays, and the bar's Back button asks too. A stream that never started or has failed is left without asking.

### 修复 / Fixed

- 播放器：从手机导入弹幕的二维码弹出后无法关闭，按返回会直接退出播放；现在按返回（或点击）关闭二维码，弹窗上也写明了。 / Player: the QR code for importing danmaku from a phone could not be dismissed, and Back left the video instead; Back (or a click) now closes it, and the card says so.
- 播放器：长按下键打开选集后，按住期间的连按不再让高亮从正在播放的一集往下走。 / Player: the repeats of the held Down that opens the episodes no longer walk the highlight down off the one playing.
- 播放器：控制栏显示期间按任意键都会重新计时，不会在浏览按钮或剧集条时中途消失。 / Player: any press while the bar is up keeps it up a while longer, so it no longer fades mid-way through walking the buttons or the episode strip.

以前每个版本改了什么，见 [更新日志](CHANGELOG.md)。

## 校验下载的文件

```
c70c024c60f4414b85cb078c1bd65e7de95d6be4a48748c8af15e4ea8d01947a  bemplayer-0.6.2-universal.apk
```

用 `sha256sum bemplayer-0.6.2-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键，然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`2aa342c`。

版本 0.6.2 是第 602 号构建。
