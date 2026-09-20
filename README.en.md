<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.0**, released 2026-09-20. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.0/bemplayer-0.6.0-universal.apk) | Works on every Android TV device | 19.2 MB |

There is one APK, and it works on every device.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.6.0-universal.apk
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

- 弹幕：视频上方可显示弹幕，控制栏按钮开关，选择会被记住。支持 Bilibili 风格的 XML 和常见的 JSON 格式。 / Danmaku: comments can scroll over the video, toggled from a bar button and remembered. Bilibili-style XML and the common JSON formats are read.
- 弹幕：可以从文件导入（浏览器），或在电视上通过配对页面从手机上传；导入过的弹幕会按影片保存，不用重复导入。 / Danmaku: import from a file in a browser, or on a TV from a phone through the pairing page; imported comments are kept against the title so they are not imported twice.
- 弹幕：设置里可以填写弹幕来源地址模板，播放器上的「获取」按钮只为正在播放的这一部拉取一次。没有预设来源。 / Danmaku: a source URL template in Settings, and a Fetch button on the player that pulls comments once for the one title playing. No source is preset.
- 弹幕：透明度、速度、字号、显示区域、显示哪些类型和屏蔽词都可以在播放设置里调整。 / Danmaku: opacity, speed, font size, coverage, which modes to show and a blocked-word list are in the playback settings.
- 字幕：可以设置字号、颜色、描边或底色、显示在上方或下方，设置会被记住。 / Subtitles: size, colour, an outline or a panel background, and top or bottom placement, all remembered.
- 字幕：控制栏上有「提前」和「延后」按钮，按半秒微调字幕时间（目前仅浏览器）。 / Subtitles: Earlier and Later buttons on the bar nudge the timing in half-second steps (browser only for now).
- 字幕：可以再选一条字幕显示在第一条下方，用于学语言；需要服务器以独立文件提供外挂字幕。 / Subtitles: a second subtitle can be shown under the first, for learning a language; it needs the server to deliver external subtitles as their own file.
- 字幕：支持 ASS 和 SSA 格式，保留定位、颜色和卡拉 OK 效果；只在选中这类字幕时才加载。 / Subtitles: ASS and SSA are rendered with their positioning, colours and karaoke effects, loaded only when such a subtitle is chosen.
- 字幕和弹幕可以在显示时做简繁转换（关、转繁体、转简体）。 / Subtitles and danmaku can be converted between Simplified and Traditional Chinese as they are drawn (off, to Traditional, to Simplified).
- 密码锁：可以设置四位或六位密码，启动和离开一段时间后需要输入；输错会越来越慢。忘记密码只能退出所有服务器重新开始。 / Passcode: a four- or six-digit passcode asked for on launch and after long enough away; wrong entries slow down. A forgotten passcode means signing the servers out and starting again.
- 密码锁：在隐私设置中选中的媒体库会从侧边栏隐藏，输入密码后才显示。 / Passcode: libraries chosen in the Privacy settings are hidden from the sidebar until the passcode is entered.
- 片头片尾：服务器标记了片头或片尾时，控制栏显示「跳过片头」「跳过片尾」按钮。片头和片尾各有三档设置：关闭、自动跳过、显示按钮，默认显示按钮；关闭时连手动标记也不显示。跳过剧集的片尾会直接播放下一集。 / Intro and credits: a Skip intro or Skip credits button appears when the server has marked them. Intro and credits each have three settings, Off, Auto and Button, with Button the default; Off hides the marking buttons too. Skipping a series' credits plays the next episode.
- 片头片尾：服务器没有标记时，可以在控制栏末尾手动标记片头和片尾，标记会用于同一部剧的其他集；只有还有下一集时才显示。按钮上显示已设的时间（片头从开头算，片尾从结尾算）；在开头 3 秒内标记片头或结尾 3 秒内标记片尾即为清除。只保存在本机。 / Intro and credits: where the server has no marks, the end of the bar can mark them by hand, and the marks carry to the series' other episodes; shown only while there is a next episode. Each button shows the time set (the intro from the start, the credits from the end); marking within 3 s of the start or the end clears that mark. Kept on the device only.
- 详情页显示演员和工作人员，以及「更多类似」推荐。 / A title's page shows the cast and crew, and a More like this row.
- 一个标题有多个文件时，详情页的「版本」按钮可按容器和码率选择要播放的文件。 / A title held as more than one file has a Version button on its page to pick which one plays, named by container and bitrate.
- 电视上可以切换音轨和字幕；引擎无法切换音轨时会从服务器以所选音轨重新播放。 / Audio and subtitle switching works on a TV; where the engine cannot switch audio itself, playback restarts from the server on the chosen track.
- 电视的日志页有「在手机上查看」按钮，扫码后手机上就能读取和复制日志。 / The Logs screen on a TV has a Show on phone button: scan the code and the phone can read and copy the log.
- 设置新增「备份」页：所有服务器（含登录凭据）和全部设置可导出为一份加密备份，密码自设；导入时可选择合并或替换设置，服务器只会并入不会移除。电视上扫码后可在手机上完成导出和导入，也可用文件或粘贴文本。 / Settings has a Backup tab: every server, sign in and all, and every setting export as one encrypted backup under a password of your choosing, and import on another TV, merging or replacing the settings; servers are only ever added. On a TV, a phone does both through the code on screen; a file or the pasted text works too.
- 搜索：最近搜索过的关键词列在搜索框下方（最多十个），按一下就能再搜，可一键清除。 / Search: the last ten keywords sit under the field, one press to search again, and can be cleared.
- 搜索：搜索框右侧有二维码，手机扫码后可以在手机上输入要搜索的内容。 / Search: a QR code beside the field lets a phone type the search.
- 显示大小新增「特小」和「小」两档，共五档；原来的三档换了名字，大小不变。 / Two display sizes below the old smallest, five in all; the three that were there kept their size under new names.
- 服务器可以在设置里上下调整顺序，切换列表和搜索范围都按这个顺序；超过四个服务器时，切换列表改为两列网格。 / Servers can be arranged in Settings, and the switcher and the search scope follow that order; past four servers the switcher becomes a two-column grid.
- 服务器图标：管理员在 Emby 自定义 CSS 里指定了 logo 的服务器，会以它的 logo 作为图标。 / A server whose administrator named a logo in Emby's custom CSS is shown with that logo as its icon.

### 变更 / Changed

- 播放器：返回键先关闭信息面板，再退出播放器回到来处；长按返回不再弹出退出应用的提示。 / Player: Back closes the info panel first, then leaves the video for wherever it was chosen from; holding Back no longer reaches the quit prompt.
- 播放器：控制栏隐藏时，按确定键呼出控制栏并暂停，按「下」呼出控制栏但继续播放。 / Player: with the bar hidden, OK brings it up and pauses, Down brings it up and keeps playing.
- 连续播放时提前准备下一集，两集之间不再有明显的空档。 / The next item in the queue is prepared ahead of time, so there is no longer a gap between episodes.
- 播放服务器给出的地址，而不是自行拼接的地址，某些代理后的服务器因此可以播放了。 / Playback uses the stream URL the server advertises rather than one built locally, which makes servers behind certain proxies play.
- 搜索改为按确定键或「搜索」按钮后才开始，不再边输入边搜索。 / A search runs when it is submitted, with OK or the Search button, and no longer as it is typed.
- 拼音首字母搜索更准确：服务器返回的结果里，名字并不包含这些首字母的会被去掉；整个标题匹配的排最前，其次是开头匹配的，再次是中间匹配的；剧集按剧名匹配，排在剧和电影之后。 / Pinyin initials are more exact: what a server returns is dropped when none of its names holds the initials, and what is left is ordered whole title first, then a start, then inside, with episodes matched by their series and listed after titles.
- 设置页：每组设置分框显示，一眼能看出分界；「关于」独立成页；更新移到「系统」页顶部，「检查更新」和「其他版本」并排。 / Settings: each group is boxed so the eye can tell where one ends; About is its own tab; Updates lead the System tab, with Check for updates and Other versions side by side.
- 播放器控制栏：状态信息面板更详细。 / Player bar: the info panel says more about what is playing.

### 修复 / Fixed

- 在侧边栏选中一个媒体库后，焦点框会跳到「首页」；现在留在选中的媒体库上。 / Choosing a library in the sidebar sent the focus ring up to Home; it now stays on the library chosen.
- 媒体库的「推荐」页：十秒内没有加载出来，或者没有可推荐的内容时，自动切到「媒体库」页；各行请求改为同时发出，不再一行等一行。「继续观看」和「接下来」只显示本媒体库的内容：有的服务器会忽略媒体库参数而返回整个账号的记录，现在会核对后只保留属于这个媒体库的。 / A library's Recommended tab switches to the Library tab on its own when the rows have not come after ten seconds or there is nothing to recommend, and its rows are now asked for together rather than one after another. Continue watching and Next up hold only this library's items: some servers ignore the library and answer with the whole account's, so what comes back is checked and the rest left out.
- 从主页的「继续观看」进入或刷新页面后，播放器不知道还有下一集：「下一集」按钮、手动标记片头片尾的按钮都不显示，播完也不会接着播。现在播放器打开时会自行读取本剧的剧集列表。 / Opened from Continue watching on home, or after a page reload, the player did not know there was a next episode: the Next episode button and the intro and credits marking buttons were missing, and the end of the episode did not carry on. The player now reads the series' episodes itself as it opens.
- 开发用代理：服务器在响应中途断开时，整个开发服务器会随之退出，此后页面上的每个请求都显示「无法连接」；现在只有那一个请求失败。错误信息也改为显示服务器地址而不是代理路径，并在开发服务器本身没有回应时直接说明。 / Dev proxy: a server dropping the connection mid-response took the whole dev server down, after which every request on the page said it could not be reached; now only that one request fails. The message names the server rather than the proxy path, and says so when it is the dev server itself that did not answer.
- 已添加服务器时，打开应用有时会停在欢迎页而不是主页；现在总是直接进入主页。 / With a server already added, launching sometimes stopped on the welcome screen instead of home; it now always goes straight to home.
- 搜索页上，从搜索框按「下」现在会到达搜索范围开关，电视上不再被键盘挡住而跳到侧边栏。 / On the search screen, Down from the search field reaches the scope toggles instead of jumping past them to the sidebar on a TV.
- 索引指针有误的 MKV（其他播放器能放，电视上报 "Element 187 must be in a Cues"）现在能播放，也能定位；播放器会跳过错误的索引直接读取。 / An MKV whose index pointer is wrong, which other players open but a TV refused with "Element 187 must be in a Cues", now plays and seeks: the player reads past the bad index.
- 剧集列表还没从服务器到达时按「下」，选集列表打不开；现在会等列表到达再打开。 / Down while the series' episodes were still loading opened nothing; the list now waits for them.
- GitHub 上的版本说明显示的是上一版的提交信息，而不是更新内容；发布脚本已改正，旧版本的说明也已补上。 / The release notes on GitHub showed the previous release's commit message instead of what changed; the release script is fixed and the earlier releases' notes filled in.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
8eb2ea62f10eb2e691424c5c9e075a4338d4c2990b3ccc71e03ea912022e94f9  bemplayer-0.6.0-universal.apk
```

Check one with `sha256sum bemplayer-0.6.0-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `352e452`.

Version 0.6.0 is build 600.
