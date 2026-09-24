<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.6.14**，发布于 2026-09-24。需要 Android 7.0
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.14/bemplayer-0.6.14-universal.apk) | 适用于所有 Android TV 设备 | 19.4 MB |

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
adb install -r bemplayer-0.6.14-universal.apk
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

绿色按键在任何界面都能打开诊断信息，这是拿到反馈问题所需资料最快的办法。

## 这个版本有什么

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

以前每个版本改了什么，见 [更新日志](CHANGELOG.md)。

## 校验下载的文件

```
a528b9ea73374e811ef819eb861be5d83f5ad889905ba669a4afda64f0abab7c  bemplayer-0.6.14-universal.apk
```

用 `sha256sum bemplayer-0.6.14-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键，然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

问题反馈、功能建议或随便聊聊，也可以加入 Telegram 群组 [@bemplayer](https://t.me/bemplayer)。
应用里 设置 → 关于 有它的二维码。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`525d9ed`。

版本 0.6.14 是第 614 号构建。
