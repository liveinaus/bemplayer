<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.6.11**, released 2026-09-24. Requires Android 7.0 or newer
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
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.6.11/bemplayer-0.6.11-universal.apk) | Works on every Android TV device | 19.4 MB |

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
adb install -r bemplayer-0.6.11-universal.apk
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

- 应用可以在 Chromium 66（2018 年）的 WebView 上运行，此前需要 99。Android 9 出厂自带的 WebView 正是这个版本，因此没有应用商店、WebView 从未更新过的电视（小米、荣耀、华为等）现在都能用了。新电视上的界面不变。 / The app runs on a WebView as old as Chromium 66 (2018); it needed 99 before. That is exactly the WebView Android 9 shipped with, so sets that never had a store to update it — Xiaomi, Honor, Huawei — can now run it. Nothing changes on a newer TV.
- ASS/SSA 字幕由 libass 绘制，而 libass 的 wasm 需要比应用底线更新的引擎；在这类老电视上会自动改用普通字幕，而不是留下一块空白。 / ASS and SSA subtitles are drawn by libass, whose wasm build needs a newer engine than the app's floor; on a set that old the plain cue overlay is used instead of leaving an empty canvas.
- 启动前先在系统层检查电视的 WebView。太旧或没有 WebView 的电视会看到一个原生界面，写明电视现有的版本、需要的版本和可以怎么做，中英文随电视语言；以前这种电视只能停在白屏或看到英文的一行字。 / The TV's WebView is checked natively before the app is loaded. A TV whose WebView is too old, or has none, gets a native screen saying what it has, what is needed and what to do, in the TV's language; before, such a TV stayed on a white page or Capacitor's one English line.
- 该界面可以直接下载并安装 Google WebView（校验后交给系统安装器；只对使用 Google WebView 的电视有效），并显示下载页面的二维码。 / That screen can download and install Google's WebView itself (checked against its checksum, then handed to the installer; only a TV whose WebView is Google's accepts it), and shows a QR code to the download page.
- 详情页：电影和剧集多了「加入收藏」按钮，收藏记在服务器上、跟随账号，其他客户端同样可见；已收藏的显示「取消收藏」。 / Detail: a film or a series has an "Add to favourites" button; the favourite is kept on the server under the account, so every other client of that server sees it too, and one already kept shows "Remove from favourites".
- 详情页：演职人员的头像可以点开，列出这位演员在本服务器上参与的全部电影和剧集，按年份从新到旧排列；每一部都可以直接打开。 / Detail: a face in the cast row opens a screen of every film and series on this server that person is credited on, newest first, each of which opens as usual.
- 首页和媒体库推荐页多了「我的收藏」一行：账号在服务器上收藏过的电影和剧集（在任何客户端收藏的都算），按名称排列；没有收藏时这一行不显示。 / Home and a library's recommended tab have a "Favourites" row: the films and series the account has starred on the server, from any client, by name; absent when there are none.
- 播放器加载时（「正在加载…」）显示当前下载速度，和播放中右上角的是同一个数字。等待的时候最想知道的就是「到底有没有在下」：慢的线路会慢慢往上走，服务器卡住了就一直是 0 kbps。换下一集时会先清空，不会显示上一部的速度。 / Player: the loading screen shows the current download speed under "Loading…", the same figure the corner shows once the picture is up. During that wait the only question is whether anything is arriving at all: a slow line counts up, a server that has stalled sits at 0 kbps. It is cleared between items, so the speed of the film that just finished is never shown as this one's.
- 媒体库列表滚到底部时自动加载下一页，不用再按「加载更多」；按钮仍在（遥控器要有地方可落），加载时变成「加载中…」。 / A library loads its next page when you reach the end of what is there, instead of waiting for Load more to be pressed. The button stays — a remote has to be able to land on something — and says "Loading more…" while the page is on its way.
- 跳过片头片尾多了「数据源」设置：服务器自己没有标记时，向公共数据库（TheIntroDB 或 IntroDB）查询正在播放的这一集。开始播放时查一次，只发送该剧的 TMDb/TVDB/IMDb 编号和集数，不发送账号、服务器地址或任何身份信息；设为「关闭」则除你自己的服务器外不联系任何第三方。服务器的标记和你手动标的都优先于它。TheIntroDB 按 TMDb 编号查，IntroDB 按 IMDb 编号查，媒体库得刮削到相应编号才查得到。两家对中文内容的收录目前都不多，抽查了十几部，IntroDB 命中 3 部、TheIntroDB 命中 1 部，可以两个都试试。 / Skipping intros and credits gains a "Marks from" setting: where your server has none of its own, a public database — TheIntroDB or IntroDB — is asked about the episode playing. Once as it starts, sending the series' TMDb/TVDB/IMDb id and the episode number — no account, no server address, nothing identifying. Off means nothing outside your own server is contacted. Your server's marks and any you set by hand both win over it. TheIntroDB is asked by TMDb id and IntroDB by IMDb id, so a library needs the one its source wants. Coverage of Chinese-language titles is thin in both: of fourteen series sampled from real libraries, IntroDB had three and TheIntroDB one, so both are worth trying.
- 高级设置里的客户端标识不只可以改 User-Agent，还可以分别设置客户端名称、版本号和设备名称；可以直接点选常见播放器的预设，也可以扫码在手机上填写，保存后电视立即生效。留空的项会自动推算。这一项移到了「系统」页。 / The client identity in the advanced settings covers more than the User-Agent now: the client name, version and device name can each be set, a known player can be picked from presets, and the whole thing can be typed on a phone through a QR code, taking effect on the TV as it is saved. Anything left empty is worked out from the rest. It has moved to the System tab.
- 设置 → 关于 加了 Telegram 群组 @bemplayer 的二维码，问题反馈、功能建议或随便聊聊都可以；版本发布页的二维码仍在旁边。 / Settings → About has a QR code for the Telegram group @bemplayer, for bug reports, suggestions or a chat, beside the one for the releases page.

### 变更 / Changed

- 全站界面打磨，重点是统一：标题统一为白色加粗（原本是灰色小字）；海报有了静止阴影；动画曲线、时长和分割线都成了统一的样式变量，模板里不再各写各的。浮在页面上的（菜单、确认框、服务器列表、侧边栏展开后）用同一套阴影加描边，属于页面本身的信息框（服务器行、更新提示、日志、格式列表）用同一条描边，不再一个框一个画法。详情页的背景大图加了朝左和朝下的双向渐变，白色标题和按钮不会再压在亮色剧照上；详情页的海报也有了和列表里一致的阴影。输入框有了边框，说明文字限制了每行长度。 / A pass of polish over the whole app, and mostly of consistency. Every section heading is white and bold rather than small and grey; posters carry a resting shadow, so a wall of them reads as things rather than one printed sheet; the curve, the length and the hairline are theme tokens now, so a template asks for `ease-settle`, `duration-moment` and `border-line` instead of inventing its own. There are two ways of drawing a box and no third: raised, with a shadow and an edge, for what floats over the screen — menus, questions, the server list, the opened sidebar — and a plain hairline for what belongs to the page. A detail screen's backdrop is darkened towards the left as well as the bottom, so a white title never sits on a bright still, and its poster has the same shadow as every other poster. Fields have an edge, and explanatory text is held to a readable line length instead of running the width of a television.
- 页面底色从接近纯黑（#0a0a0c）调亮为「几乎黑但不是黑」（#16161a）：纯黑在电视上像墙上的一个洞，海报像浮在虚空里。启动时先画出的几处（安卓窗口、Capacitor、index.html、「WebView 太旧」原生页）和手机配对页一起改，所以启动时不会先闪一下旧的黑色。 / The page is almost black rather than black: #16161a where it was #0a0a0c, which a television shows as a hole in the wall. Everything that paints before the stylesheet does — the Android window, Capacitor, index.html, the native "WebView too old" screen — and the phone pairing page moved with it, so a launch does not flash the old black first.
- 首页和媒体库推荐页的每一行交替使用两种底色（页面色和稍亮一点的条带），一眼就能分出一行一行，不用先找标题；条带从侧边栏一直铺到屏幕边缘，海报位置不变。侧边栏右边多了一条细边，旁边不管是哪种底色都能清楚看出边界。 / Home and a library's recommended tab alternate the ground under each row — the page, then a slightly lighter band — so the rows are told apart at a glance before any heading is read. The band runs from the sidebar to the edge of the screen without moving a poster. The sidebar gained a hairline on its right edge, so it is crisp against either colour beside it.
- 播放器进度条加粗并提亮，播放位置有了一个圆点标记：原本是一条 6 像素高、五分之一亮度的细线，坐在三米外的沙发上几乎看不清，也找不到自己看到哪了。控制栏标题也改成和其他标题一样的加粗。 / Player: the progress track is thicker and brighter, and the playhead is marked with a dot. It was a six-pixel line at a fifth of white — a hairline from a sofa three metres away, with nothing at the playhead to find. The bar's title is bold, like every other title.
- 海报上的观看进度条改成内缩的圆角进度条，和播放器的进度条一样：原来贴着图片最底边，被圆角切掉了开头，看了一成的片子只在角上露出一丝。 / A poster's progress is an inset, rounded track now, the player's scrubber at the size of a card. It ran along the very bottom of the picture, where the rounded corner cut its start away, so a film a tenth watched showed a sliver in the corner.
- 运行日志从一堆独立的圆角卡片改成一个整体：时间、级别、标签对齐成列，长地址换行时对齐在消息那一列，而不是折回时间下面；警告和错误左侧有彩色标记，翻几百条时一眼就能找到。 / The log is one panel rather than a stack of rounded cards: the time, level and tag sit in aligned columns, a long address wraps under its own message instead of back under the time, and a warning or an error carries a coloured edge so it can be found by eye among hundreds of lines.
- 侧边栏展开时，Bemplayer 的标志竖着立在服务器、首页和搜索旁边，填满了原本空着的那一列；收起时各行高度不变，展开不会让下面的内容跳动。 / The opened sidebar stands the Bemplayer logotype on end beside the server, Home and Search, filling a column that was empty; closed, the rows keep their heights, so nothing under them jumps as it opens.

### 修复 / Fixed

- 侧边栏收起和展开时背景色不一样，后来改成收起时透明又看不出侧边栏在哪。现在收起和展开都是同一个面板色，和页面明显区分；展开只是变宽并投下阴影，颜色不变，所以展开时不会闪。 / The sidebar was one colour closed and another open, and then — made transparent to fix that — could not be seen at all closed. It is one panel colour in both states now, distinct from the page; opening it only widens it and casts a shadow, so nothing about its colour changes as it opens.
- 选中的海报标题和年份后面会有一块暗色阴影：焦点阴影是整张卡片投下的，连文字一起；纯黑底上看不见，底色调亮后就露出来了。现在阴影只在图片上，和焦点框一样。 / A chosen poster had a dark smudge behind its title and year: the focus shadow was cast by the whole card, words included, which was invisible on black and showed once the page was lifted off it. It falls from the picture alone now, as the focus ring already did.
- 下载速度在「19 Mbps / 0 kbps / 30 Mbps / 0 kbps」之间来回跳，没法看：播放器是把缓冲填满再停下来等，所以每隔一跳就真的没有数据在下。现在显示最近六秒的平均值，播放中和加载时是同一个数字；真的停了几秒仍然会显示 0 kbps。 / The download speed flickered between a burst and nothing — 19 Mbps, 0 kbps, 30 Mbps, 0 kbps — which reads as something broken rather than a buffer working: a player fills its buffer as fast as the line allows and then waits, so every other reading genuinely is zero. It is averaged over the last six seconds now, the same figure while loading and while playing, and still falls to 0 kbps when nothing has actually arrived for a few seconds.
- 在首页按返回键没有任何反应，有用户因此退不出应用（电视上没人用任务管理器，Home 键只是把应用放到后台）。现在到了没有上一页可回的那一屏，按返回会问「要退出 Bemplayer 吗？」，并提示下次长按返回可直接退出；长按返回仍然是立即退出，不再多问一次。 / Back on the home screen did nothing at all, and a viewer reported being unable to leave the app — a television has no task switcher anybody uses, and Home only puts it behind the launcher. Back at the screen with nothing behind it now asks "Quit Bemplayer?" and says that holding Back leaves without asking next time. Holding Back leaves at once, as before, and is no longer asked about.
- 用遥控器长按某个键在电视上没有反应（长按「下」出选集列表、长按左右加速快进、长按返回），而同样的操作用键盘在浏览器里都正常：长按原本是靠键盘的自动重复判断的，而不少电视遥控器无论按多久都只发一次按下、一次抬起。现在按住超过 400 毫秒就由应用自己开始计数，遥控器自己会重复的则照旧交给它。 / Holding a button on a TV remote did nothing — Down for the episode list, Left or Right to seek faster, Back — while the same holds all worked from a keyboard in a browser. A hold was read off the keyboard's own auto repeat, and plenty of remotes send one key down and one key up however long the button is held. A button still down after 400ms is now counted by the app itself; a remote that does repeat is left to do it.
- 「加载更多」按了没反应的真正原因：本地缓存写不进去时，把已经拿到的数据一起丢掉了。浏览器里没有 OPFS 时用的是 localStorage（只有几兆），写满后 SQLite 自己回滚，写入报错——而这个写入是夹在「取数据」中间 await 的，于是请求发出去了、结果也回来了，却什么都没显示。现在缓存写入失败只记一条日志，屏幕照常显示服务器给的内容。 / The real reason Load more did nothing: a cache write that failed threw away the data that had already been fetched. Where there is no OPFS the browser build stands a few megabytes of local storage in for a database; once it is full SQLite rolls the transaction back itself and the write throws — and that write was awaited in the middle of the fetch, so the request went out, the items came back, and nothing was drawn. A cache that cannot be written to is now one line in the log, and the screen still shows what the server sent.
- 数据库回滚失败时会盖掉真正的错误：日志里满屏「cannot rollback - no transaction is active」，而真正的原因（比如磁盘/存储写满）一条都看不到。现在保留原始错误。 / A failed rollback replaced the error that caused it: the log filled with "cannot rollback — no transaction is active" and never once said what had actually gone wrong, such as the storage being full. The original error is kept now.
- 翻页时只接收真正新的条目：服务器把第二页答成第一页时，重复的条目不再被原样接在后面；一页里一个新的都没有就说明到底了，不再继续问。 / Paging takes only genuinely new items: where a server answers the second page with the first one, the repeats are no longer appended, and a page with nothing new in it ends the asking rather than going round again.
- 翻下一页失败时，整个媒体库的封面墙会被一行红字取代。失败的是下一页，不是已经在屏幕上的那些：现在它们留着，原因写在下面。 / A next page that failed replaced the whole wall of posters with one red line. What failed was the next page, not the ones already on the screen: those stay now, and the reason goes below them.
- 媒体库的「推荐」页没有内容时，只显示一句「这个媒体库里还没有可以推荐的内容。」就停在那里。现在会直接切到「媒体库」页——整个媒体库就在旁边，本来就是要看的东西。以前只有刚打开媒体库时才会自动切换，手动点「推荐」、从某个条目返回、或十分钟缓存内再次打开时都不会。 / A library's Recommended tab with nothing on it showed one line saying so and stopped there. It now goes straight to the Library tab: the whole library is right beside it and is what was wanted. Before, that only happened when the library was first opened — choosing the tab by hand, coming back to it from a title, or opening the library again within the ten minutes the rows are cached for all landed on the same empty paragraph.
- 首页「继续观看」经常是上一次看的内容，而不是最近在看的：首页整屏缓存五分钟，从详情页或播放器返回时不会重新询问服务器。现在每次回到首页都单独刷新「继续观看」和「下一集」这两行（两个请求），其余各行仍走缓存，缓存时长从 5 分钟延长到 30 分钟——既更准，整体请求数也更少。服务器说没有在看的内容时，这一行会消失，而不是继续显示旧的。 / Home: Continue watching often showed what was watched before the last thing watched. The whole screen was cached for five minutes, so coming back from a detail screen or the player asked the server nothing. Continue watching and Next up are now refreshed on their own every time home is opened — two requests — while the rest of the screen keeps its cache, now good for thirty minutes instead of five. It is both more accurate and fewer requests overall. A row the server says is empty now goes away instead of standing there with what it held before.
- 首页卡片大量空白只显示两个字母：剧集通常没有自己的图片（除非有人为每一集都抓过图），而「继续观看」和「下一集」几乎全是剧集。现在这种情况改用剧集的海报，和其他 Emby 客户端一致。 / Home: cards were blank but for two letters. An episode usually has no picture of its own unless somebody fetched images for every episode in the library, and Continue watching and Next up are almost entirely episodes; the series' poster is now drawn instead, as every other Emby client does.
- 首页海报迟迟不出现：以前一打开首页就会把五行共一百张海报全部请求一遍，电视到服务器只有六条连接，正在看的那几张排在看不见的那些后面。现在只请求即将进入视野的卡片，相同的图片同时被要两次也只发一个请求，内存里保留的图片数量也有了上限。 / Home: posters took a long time to appear. Opening home used to request all hundred posters of its five rows at once, and a television has six connections to a server, so the ones being looked at queued behind ones nobody could see. Only a card coming near the screen is asked for now, the same picture wanted twice at once is one request, and what is held decoded in memory is capped.
- 同一个内容有时能播、有时报错说需要转码，而转码明明是关着的：一个屏幕要播完整个队列，某一集不得不回退到转码后，这个状态会留给后面每一集，于是后面全部被要求转码——不允许转码的服务器就全部拒绝。现在每换一个内容（或换一个文件）都从头来过。 / Playback: the same item played one time and failed the next with a message about converting, although converting was switched off. One screen plays a whole queue, and once a title had to fall back to converting, every title after it asked for the same thing — which a server that will not convert then refused. Each title, and each file of a title, now starts from scratch.
- 播放偶尔画面发暗、颜色不对，再播一次就正常：同上，是上一个内容遗留的转码状态让这一部被服务器转了码，HDR 片源被转成 SDR 时就会这样。 / Playback: a film occasionally came back dark and wrong in colour, and was fine when played again. Same cause: the converting left over from the title before it meant this one was converted by the server, which is what an HDR film looks like turned into SDR.
- 关掉转码后仍会把码率上限告诉服务器：码率上限是转码设置，关掉转码后它只能让内容播不了——超过上限的文件 Emby 会拒绝原样发送，而转码又不允许。现在关掉转码时不再发送上限。 / Playback: a bitrate ceiling was still being named to the server after converting was switched off. A ceiling is a converting setting; with converting off it can only stop something playing, because Emby refuses to send a file as it stands when it is above the ceiling its client named. No ceiling is sent now.
- 设置里选了「不转码」时，应用不再在任何情况下要求服务器转码——包括原来「其他办法都试过了」的兜底。服务器只能转码发送的内容，现在直接说明原因（并提示可以在设置里选一个码率上限来允许转码），而不是偷偷让服务器转码。换容器（remux）不算转码，仍会尝试：同样的视频换个封装发过来，服务器几乎不花力气。 / With No transcoding chosen in settings, the app no longer asks the server to convert anything, in any circumstance — including the last resort it used to fall back on. A file the server will only send converted now says so, and says a bitrate ceiling in settings would allow it, rather than quietly putting the server to work. Rewrapping is not converting and is still tried: it is the same video handed over in another box, which costs a server almost nothing.
- 播放请求失败时一律要求服务器转码，包括超时和连接被拒这类和格式无关的失败。现在只有服务器确实拿不出任何可播内容时才换个方式再问，并且先问「换个容器」再问「转码」。 / Playback: any failed request for a stream used to be answered by demanding a transcode, including a timeout or a refused connection, which say nothing about the format. Only a server that really had nothing to offer is asked again now, and it is asked to rewrap before it is asked to convert.
- 老电视上片名会叠在一起、盖住旁边的卡片：这类引擎不允许 `<button>` 作为 flex 容器，卡片里的文字因此按最长的一条排版，既没有被截断也没有留在卡片内。片名过长时现在会正常显示省略号。菜单、服务器列表和专辑曲目列表也有同样的问题，一并修复。 / On an older television a title was drawn over its neighbour: an engine that old will not let a `<button>` be a flex container, so the words inside a card were laid out as wide as the longest of them instead of being cut short at the card's edge. A long title now ends in an ellipsis as it should. Menus, the server list and an album's track list had the same fault and are fixed with it.
- 老电视上应用仍然打不开，只显示一行 `Uncaught SyntaxError`：浏览器版的 SQLite（wasm）被无条件打包进了启动文件，而它的代码用了 Chromium 67 才有的写法，老引擎连解析都无法完成，整个应用因此都跑不起来——尽管电视用的是自带的原生 SQLite，根本用不到它。现在只有真正需要时才加载，并且每次打包都会检查有没有超出底线的语法。 / A set at the floor still showed only `Uncaught SyntaxError` and no app: the browser's SQLite (wasm) was bundled into the launch file unconditionally, and its code is written with syntax only Chromium 67 understands, which an older engine cannot even parse — so the whole app failed, although a television uses its own native SQLite and never needs it. It is now loaded only when it is actually wanted, and every build is checked for syntax above the floor.
- 媒体库：网络慢时，冷启动后打开媒体库会先显示「还没有可以推荐的内容」而不切换到「媒体库」标签，因为十秒的等待要等媒体库列表刷新完才开始计时。现在从打开那一刻计时，等待期间显示「正在加载」，列表迟到也不会把画面拉回推荐页。 / Library: on a slow link, a library opened after a cold start said "nothing to recommend" and never switched to the Library tab, because the ten-second wait only began once the list of libraries had been refreshed. The clock now runs from the opening, the screen says it is loading meanwhile, and a list arriving late no longer pulls the screen back.
- 剧集详情页上下移动焦点反应慢：每按一次，焦点算法都要把整页每个可选的东西重新检测好几遍，剧集、演员、推荐三行加起来有六十多个。现在一次按键只测量一遍，按键后焦点移动所需的时间少了约三成。 / Moving up and down a series' detail screen was slow to respond: every press had the focus algorithm measure each of the sixty-odd things on the screen several times over — the episodes, the cast and the recommendations. One press measures the page once now, which takes about a third off the time before focus moves.
- 服务器列表里，从单独占一行的最后一个服务器按「上」，偶尔会跳到右上方那个，而不是正上方：刚离开焦点的格子还在缩回原来大小，这一点点差别就决定了去哪。现在按格子的原本大小来算。 / In the server list, Up from the last server alone on its row sometimes went to the one above and to the right rather than the one directly above: the cell focus had just left was still shrinking back, and that sliver decided it. Cells are measured at their resting size now.
- 电视上一集播完会跳过一集（看完 08 直接到 10）：播放器在结束时报了两次「播完了」，每一次都换到下一集。现在只报一次，而且每段播放最多只会换一次集。 / On a TV, an episode that finished skipped one (08 went straight to 10): the player reported the end twice, and each report moved to the next episode. It is reported once now, and a stream moves the queue on at most once.
- 正在播放的剧集在中间突然跳到下一集：服务器提前断开的流和真正播完的流在播放器看来是一样的「结束」。现在离片长还有一分钟以上就结束的，会从停下的地方重新请求；在同一处第二次停下才算这集到头。每次自动换集都会在日志里写明原因。 / An episode playing normally could jump to the next one in the middle: a stream the server stopped sending early ends the same way as one that played out. An end more than a minute short of the episode's length is now asked for again from where it stopped, and only a second stop at the same place is taken as the end. Every automatic move to the next episode says why in the log.
- 服务器转码的流拖动进度后，新位置还在加载时按「播放」，播放器可能按还没开始的流来判断新流从哪里算起。现在只听播放器自己说的状态，按钮照样立刻变化。 / On a stream the server converts, pressing Play while a seek's new stream was still loading could have the app work out where that stream counts from before it was running. Only the player's own word is used for that now; the button still changes at once.

What changed in every earlier version is in the [changelog](CHANGELOG.md).

## Verifying a download

```
30841606c0f698f549e081da35b37fb3de7e0bb0e948d2046d56c2596d9fbf66  bemplayer-0.6.11-universal.apk
```

Check one with `sha256sum bemplayer-0.6.11-universal.apk`.

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
from: `90fdcf9`.

Version 0.6.11 is build 611.
