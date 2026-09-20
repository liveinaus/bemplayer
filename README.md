<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.6.1**，发布于 2026-09-20。需要 Android 7.0
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.1/bemplayer-0.6.1-universal.apk) | 适用于所有 Android TV 设备 | 19.2 MB |

只有一个安装包，所有设备都用它。

## 安装

Android TV 默认不允许安装来自文件的应用。第一次安装时会弹出提示，并直接指向对应的设置页面。

**用文件管理器或投送工具**，例如 Downloader 或 Send Files to TV：把 APK 传到电视上，打开
它，同意安装提示。

**用 adb**，在同一网络的电脑上执行：

```bash
adb connect <电视的IP>:5555
adb install -r bemplayer-0.6.1-universal.apk
```

然后在 Android TV 主界面打开 Bemplayer，填入你的 Emby 服务器地址，例如
`http://192.168.1.10:8096`。

## 更新

Bemplayer 会自行检查新版本，不用电脑也能安装。进入设置，再进更新，然后点立即检查。自动检查
默认开启，也可以在同一个页面关掉。

第一次更新会请求允许 Bemplayer 安装应用。正是这个权限让它可以替换自己，应用会直接带你到那个
设置项。

## 遥控器按键

| 按键              | 在播放器中                                     |
| ----------------- | ---------------------------------------------- |
| 确定键、播放/暂停 | 播放或暂停                                     |
| 左、右            | 快退快进。按住会加速：10 秒、30 秒、1 分、5 分 |
| 上                | 回到上一行按钮；在最上一行时收起控制栏         |
| 下                | 到达下一行按钮；长按打开选集                   |
| 返回              | 先关菜单，再收起控制栏，最后离开播放器         |

在其他界面，返回键是返回上一层，永远不会直接关掉应用。长按返回键才会询问是否退出，这是离开应
用的唯一方式。

绿色按键在任何界面都能打开诊断信息，这是拿到反馈问题所需资料最快的办法。

## 这个版本有什么

### 变更 / Changed

- 播放器：弹幕相关按钮统一为带圈的 D 图标，不再带文字；选集改为长按下键（短按下键到达第二行按钮，按上键回到第一行）。 / Player: the danmaku buttons are a D in a ring with no text; the episodes open on a held Down, while a tap of Down reaches the bar's second row of buttons and Up returns to the first.

### 修复 / Fixed

- 切换服务器后按返回，会回到上一个服务器的页面并报错（如「Could not load item … failed with 500」）；现在切换、登录后的返回止于首页。 / Back after switching servers reopened the previous server's screens and failed (such as "Could not load item … failed with 500"); after a switch or a sign in, Back now stops at home.
- 服务器超过四个时切换列表是两列，方向键无法从左列移到右列；现已修复。 / With more than four servers the switcher is two columns, and the D-pad could not move from the left column to the right; fixed.
- 检查更新时，版本说明很长会把「安装并重启」按钮挤到屏幕外；现在只显示前几行，「展开全文」可以看全部（按上到达，按下逐段滚动），按钮始终在屏幕上。 / Long release notes on a found update pushed the Install button off the screen; the notes now show a few lines with a Read more (Up reaches it, Down scrolls the opened notes), and the button stays on screen.

以前每个版本改了什么，见 [更新日志](CHANGELOG.md)。

## 校验下载的文件

```
4358990d1c83d7f5f0f3f196180d46b8492a49f08621b150e69a76f60edfd9fb  bemplayer-0.6.1-universal.apk
```

用 `sha256sum bemplayer-0.6.1-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键，然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`585d413`。

版本 0.6.1 是第 601 号构建。
