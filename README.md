<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.6.15**，发布于 2026-09-27。需要 Android 7.0
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.15/bemplayer-0.6.15-universal.apk) | 适用于所有 Android TV 设备 | 19.4 MB |

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
adb install -r bemplayer-0.6.15-universal.apk
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

- 服务器可以有多条线路。手机登录页多了一个"其他线路"框，服务器公布的备用地址每行填一个；设置 › 服务器 › 线路可以用手机增删、调整顺序，也可以在电视上直接选一条。正在用的线路完全没有响应（连不上或超时）时，会按顺序问下一条线路是不是同一台服务器，是就换过去并一直用它，图片和播放也跟着换。服务器返回错误状态不会触发换线；所有线路都没响应后，一分钟内不再重试。 / A server can have several addresses. The phone sign-in page has an "Other addresses" box for the backups a server announces, one per line, and Settings › Servers › Addresses changes them from a phone, reorders them, or picks one on the TV. When the address in use gets no answer at all (refused or timed out), the next is asked whether it is the same server, and if so it takes over and stays in use, images and playback with it. A server answering with an error status never causes a switch, and once no address answers none is tried again for a minute.
- 切换服务器列表里每个服务器都显示它有多少部电影和剧集。打开列表时向每个服务器问一次，用的是服务器自己记着的总数，不会遍历媒体库；一小时内再打开不会重复问。连不上的服务器不显示数字。 / The server switcher shows how many films and series each server has. Each server is asked once as the list opens, for the totals it already keeps, so no library is read through; opening it again within the hour asks nothing. A server that does not answer shows no figures.

### 变更 / Changed

- 服务器多于六个时，切换服务器列表改为三列的卡片：名称和状态点在上，电影和剧集数量在下，不显示地址，这样十一个服务器在电视上一屏放得下，不用滚动。六个及以下时数量显示在名称右边，地址照旧。 / With more than six servers the switcher is three columns of tiles — the name and its dot, with the film and series counts beneath and no address — so eleven servers fit on a TV screen without scrolling. With six or fewer the counts sit at the right of the name and the address stays.

### 修复 / Fixed

- 遥控器绿色按钮其实从来没有接上，按了什么都不会发生。现在在任意界面（包括播放中）按它都会打开运行日志；遥控器没有绿色按钮时，设置 › 系统 › 运行日志 是同一个界面。 / The green remote button was never actually wired up and did nothing. It now opens the logs from any screen, playback included; on a remote without one, Settings › System › Logs is the same screen.
- 有的电视把 E-AC3（杜比数字+）解成 5.1 声道后拒绝打开音频输出，报 ERROR_CODE_AUDIO_TRACK_INIT_FAILED，画面有、声音没有。现在遇到这种情况会自动重试：先关掉隧道播放，还不行就把声音缩混成立体声；本次运行里之后的影片直接沿用。 / Some televisions decode E-AC3 (Dolby Digital Plus) to 5.1 and then refuse to open an audio output for it, reporting ERROR_CODE_AUDIO_TRACK_INIT_FAILED and leaving the film silent. Playback now retries by itself, first without tunnelling and then downmixed to stereo, and later films in the same session start that way.

以前每个版本改了什么，见 [更新日志](CHANGELOG.md)。

## 校验下载的文件

```
89ecaf1f74d26da7efdd422d7412d6a9e1fbf9f54965fd06c4ec7779d64e8928  bemplayer-0.6.15-universal.apk
```

用 `sha256sum bemplayer-0.6.15-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键（或 设置 › 系统 › 运行日志），然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

问题反馈、功能建议或随便聊聊，也可以加入 Telegram 群组 [@bemplayer](https://t.me/bemplayer)。
应用里 设置 → 关于 有它的二维码。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`9f99809`。

版本 0.6.15 是第 615 号构建。
