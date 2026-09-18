<img src="docs/logo.png" alt="Bemplayer" width="420">

简体中文 | [English](README.en.md)

一款为 Android TV 打造的 Emby 客户端，为遥控器而设计，而不是触摸屏。

**最新版本 0.2.0**，发布于 2026-09-18。需要 Android 6.0
或更高版本（API 23）。

## 下载

| 下载 | 适合 | 大小 |
| --- | --- | --- |
| [armeabi-v7a](https://github.com/liveinaus/bemplayer/releases/download/v0.2.0/bemplayer-0.2.0-armeabi-v7a.apk) | 多数 Android TV 盒子和电视棒，包括较老的 Fire TV | 9.8 MB |
| [arm64-v8a](https://github.com/liveinaus/bemplayer/releases/download/v0.2.0/bemplayer-0.2.0-arm64-v8a.apk) | 较新的 64 位设备、Shield TV、近几代 Fire TV 和 Chromecast | 10.8 MB |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.2.0/bemplayer-0.2.0-universal.apk) | 所有设备都能用，下载大一些。拿不准就选它 | 16.1 MB |

不确定选哪个？选 `universal`。它下载起来大一些，但在所有设备上都能用。

## 安装

Android TV 默认不允许安装来自文件的应用。第一次安装时会弹出提示，并直接指向对应的设置页面。

**用文件管理器或投送工具**，例如 Downloader 或 Send Files to TV：把 APK 传到电视上，打开
它，同意安装提示。

**用 adb**，在同一网络的电脑上执行：

```bash
adb connect <电视的IP>:5555
adb install -r bemplayer-0.2.0-universal.apk
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
| 上                | 播放诊断信息                                   |
| 下                | 音轨与字幕                                     |
| 返回              | 先关菜单，再收起控制栏，最后离开播放器         |

在其他界面，返回键是返回上一层，永远不会直接关掉应用。长按返回键才会询问是否退出，这是离开应
用的唯一方式。

绿色按键在任何界面都能打开诊断信息，这是拿到反馈问题所需资料最快的办法。

## 这个版本有什么

Publish v0.1.9

## 校验下载的文件

```
77e0e260201979c2782fce35cabdea1a2c790c2920946a0ab881c4cbd5bf0edd  bemplayer-0.2.0-armeabi-v7a.apk
272c66493b9b5eaea8da27370d83e4512136d0c08eac017b64e7ec93bf94d11e  bemplayer-0.2.0-arm64-v8a.apk
ea4dd9775eee03d4741a1150e998565a528cc01c23f39f03a7952560bd885936  bemplayer-0.2.0-universal.apk
```

用 `sha256sum bemplayer-0.2.0-universal.apk` 校验其中一个。

## 反馈问题

到 https://github.com/liveinaus/bemplayer/issues 提交 issue。最有用的附件是日志导出：按遥控器上的绿色
按键，然后选导出，屏幕上会告诉你文件放在哪里。

请一并附上设备型号、Android 版本和 Emby 服务器版本。

## 关于这个仓库

这个仓库只发布构建产物。它存放各个发行版、这个页面，以及 `update.json`，也就是应用用来发现新
版本的那个文件。源代码放在另一个私有仓库里，每次发布都会记录它构建自哪个提交：
`7a4bb01`。

版本 0.2.0 是第 200 号构建。
