# 更新日志 / Changelog

每次修改都在 **Unreleased** 下记一条要点，中文在前、英文在后。发布时
`scripts/release.sh` 会把这一节作为该版本的发布说明，并把它归到版本号下面。
完整的历史都在这里；GitHub 上每个发行版只带自己那一节。

Every change adds a line under **Unreleased**, Chinese first then English.
`scripts/release.sh` takes that section as the release notes and files it under
the version. The whole history lives here; each GitHub release carries only its
own section.

## [Unreleased]

## [0.6.14] - 2026-09-24

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

## [0.6.11] - 2026-09-24

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

## [0.6.2] - 2026-09-21

### 新增 / Added

- 播放器：短按下键到按钮最下一行之外，会在控制栏下方展开本剧全部剧集的缩略图条（和剧集页一样），落在正在播放的一集上，左右浏览、中键切换；上键或返回收起。长按下键的选集列表保持不变。 / Player: a tap of Down off the bottom row of buttons opens a strip of the series' episode stills under the controls, as the series screen shows them, on the one playing; Left and Right browse it, OK switches, Up or Back puts it away. The list a held Down opens is unchanged.
- 播放器：右上角时间旁显示实时下载速度，即此刻真正从服务器收到的数据速率；不足 1 Mbps 时以 kbps 显示，没有数据到达时显示 0 kbps。电视上此前一直不显示，已修复。 / Player: the live download speed sits beside the clock in the top corner, the bytes actually arriving from the server at that moment; under a megabit it is written in kbps, and nothing arriving reads 0 kbps. On a TV it never showed before; fixed.

### 变更 / Changed

- 播放器：按返回不再直接退出播放，而是先询问「停止播放？」，中键确认离开，再按返回则继续看；控制栏上的返回按钮同样询问。播放尚未开始或已出错时直接离开。 / Player: Back no longer leaves the video outright; it asks "Stop watching?", OK leaves and Back again stays, and the bar's Back button asks too. A stream that never started or has failed is left without asking.

### 修复 / Fixed

- 播放器：从手机导入弹幕的二维码弹出后无法关闭，按返回会直接退出播放；现在按返回（或点击）关闭二维码，弹窗上也写明了。 / Player: the QR code for importing danmaku from a phone could not be dismissed, and Back left the video instead; Back (or a click) now closes it, and the card says so.
- 播放器：长按下键打开选集后，按住期间的连按不再让高亮从正在播放的一集往下走。 / Player: the repeats of the held Down that opens the episodes no longer walk the highlight down off the one playing.
- 播放器：控制栏显示期间按任意键都会重新计时，不会在浏览按钮或剧集条时中途消失。 / Player: any press while the bar is up keeps it up a while longer, so it no longer fades mid-way through walking the buttons or the episode strip.

## [0.6.1] - 2026-09-21

### 变更 / Changed

- 播放器：弹幕相关按钮统一为带圈的 D 图标，不再带文字；选集改为长按下键（短按下键到达第二行按钮，按上键回到第一行）。 / Player: the danmaku buttons are a D in a ring with no text; the episodes open on a held Down, while a tap of Down reaches the bar's second row of buttons and Up returns to the first.

### 修复 / Fixed

- 切换服务器后按返回，会回到上一个服务器的页面并报错（如「Could not load item … failed with 500」）；现在切换、登录后的返回止于首页。 / Back after switching servers reopened the previous server's screens and failed (such as "Could not load item … failed with 500"); after a switch or a sign in, Back now stops at home.
- 服务器超过四个时切换列表是两列，方向键无法从左列移到右列；现已修复。 / With more than four servers the switcher is two columns, and the D-pad could not move from the left column to the right; fixed.
- 检查更新时，版本说明很长会把「安装并重启」按钮挤到屏幕外；现在只显示前几行，「展开全文」可以看全部（按上到达，按下逐段滚动），按钮始终在屏幕上。 / Long release notes on a found update pushed the Install button off the screen; the notes now show a few lines with a Read more (Up reaches it, Down scrolls the opened notes), and the button stays on screen.

## [0.6.0] - 2026-09-20

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

## [0.5.0] - 2026-09-20

### 新增 / Added

- 多季的剧集可以按季筛选，默认显示最新一季，选过的季会被记住。 / A series with several seasons can be filtered by season; it opens on the latest, and a chosen season is remembered.
- 单集页面上的剧名和季名可以点击，分别打开该剧和该季。 / On an episode, the series name and the season are links: one opens the series, the other opens it on that season.
- 可以把单集、整季或整部剧标为已看（或未看），已看的内容不再被推荐；卡片上会显示已看标记。 / An episode, a season or a whole series can be marked watched (or unwatched), so it stops being recommended; cards show a watched tick.
- 媒体库页面分为「推荐」和「媒体库」两个标签，推荐页按本库展示继续观看、接下来、最近添加、最新上映、高分作品和为你推荐。 / A library opens on two tabs, Recommended and Library; Recommended shows continue watching, next up, recently added, recently released, top rated and suggestions for that library alone.
- 侧边栏可以整理：每个媒体库左侧有 ⋮ 按钮，可移动顺序或从侧边栏移除，顺序会被记住。 / The sidebar can be arranged: each library has a ⋮ handle to move it up or down or unpin it, and the order is kept.
- 设置页新增「关于」，含项目说明、版本号、GitHub 链接和二维码。 / Settings has an About section with a description, the version, the GitHub link and a QR code for it.
- 点击侧边栏顶部的 Bemplayer 标志可直接打开设置。 / The Bemplayer logo at the top of the sidebar opens Settings.
- 检查更新发现新版本时会弹出对话框，确定安装、取消忽略。 / Finding an update opens a dialog: OK installs, Cancel dismisses.
- 系统 WebView 过旧（低于 Chrome 99）时，启动页会说明原因和解决办法，而不是停在白屏。 / A TV whose WebView is older than Chrome 99 sees an explanation and what to do about it instead of a blank white screen.

### 变更 / Changed

- 侧边栏默认收起为图标栏，遥控器移入或鼠标悬停时展开，不再挤占内容区。 / The sidebar is a rail of icons that opens when the D-pad moves into it or the mouse hovers, leaving the screen to the content.
- 剧集以横向的画面缩略图卡片展示，带观看进度，而不是纯文字列表。 / Episodes are shown as a horizontal shelf of stills with progress, not a list of titles.
- 媒体库和搜索结果按行均匀铺满屏幕宽度。 / Library and search grids share each row out evenly across the screen.
- 切换视频时先显示黑屏和「正在加载…」，不再残留上一个视频的画面。 / Switching videos shows a black screen and "Loading…" until the new one has a picture, instead of the last frame of the previous one.
- 搜索范围的控件分成两行：一个开关，下面是各服务器的包含状态。 / The search scope controls are split into the switch and, under it, which servers are included.
- 焦点白框改为画在元素内部，电视上不再缺边。 / The focus ring is drawn inside the element, so it no longer loses its sides on a TV.
- 只发布 universal 版 APK，不再区分 CPU 架构。 / Only the universal APK is published, no more per-architecture builds.
- 播放器：快进快退连按或按住会累加，屏幕中央显示总变化量（如 +3:30）和落点，停止按键后才真正跳转；按住会逐级加速。 / Player: forward and back presses add up, the sum (+3:30) and where it lands are shown in the middle of the screen, and the seek happens once the presses stop; a held button climbs through larger steps.
- 播放器：控制栏右上角显示当前时间；按「上」可收起控制栏。 / Player: the bar shows the time of day in its corner, and Up takes the bar away.
- 播放器：下载速度改为实时传输速率，不再是估算值。 / Player: the download rate is what is arriving now, not an estimate of the line.

### 修复 / Fixed

- 快退和快进按钮的图标方向反了。 / The rewind and forward icons curled the wrong way.
- 打开一部剧时焦点落在「返回」上，现在落在「播放」或「继续」上。 / Opening a series landed focus on Back; it now lands on Play or Resume.
- 搜索页的侧边栏有时不显示媒体库。 / The sidebar on the search screen sometimes showed no libraries.
- 每次启动时的白色闪屏。 / The white flash on every launch.
- 发布说明取错了来源，显示成上一个版本的提交信息。 / Release notes were taken from the wrong place and showed the previous version's commit message.

## [0.3.3] - 2026-09-19

- 剧集、音轨和字幕选择器显示在控制栏之上。 / The episode, audio and subtitle pickers sit in front of the control bar.
- 电视端加载后明确发送播放指令，不再需要按两次播放。 / The native player is told to play after loading, so Play no longer needs two presses.
- 首页数据过期的提示旁增加重试按钮。 / A retry button beside the stale-data banner on home.
- 修复「搜索时加入另一个服务器」开关不生效。 / The "add another server to search" toggle now applies.
- 不再自行编造播放会话 ID。 / Playback no longer invents a play session id.
- 启动失败时显示原因。 / A message when the app fails to start.

## [0.3.2] - 2026-09-19

- 修复快进快退的问题。 / Forward and backward seeking fixes.
- 修复切换音轨和字幕的问题。 / Audio and subtitle switching fixes.

## [0.3.1] - 2026-09-19

- 修复定位跳转的两个问题。 / Two seek fixes.

## [0.3.0] - 2026-09-19

- 浏览器版本支持所有服务器；开发用代理可模拟电视的 User-Agent。 / The browser build works with every server; a dev proxy can present a TV's user agent.
- 修复电视端字幕问题。 / A TV subtitle fix.

## [0.2.9] - 2026-09-19

- 修复观看进度的调整。 / Watching progress adjustment fixes.

## [0.2.8] - 2026-09-19

- 可以在设置中回退到旧版本。 / Older versions can be installed from Settings.
- 更多测试。 / More tests.

## [0.2.7] - 2026-09-18

- 修复电视端观看进度调整和画面比例。 / Watching progress adjustment and picture ratio fixes on TV.

## [0.2.6] - 2026-09-18

- 可以调整观看进度。 / Watching progress can be adjusted.

## [0.2.5] - 2026-09-18

- 播放时间显示调整。 / Playback time display adjustments.

## [0.2.1] - 2026-09-18

- 修复电视端快进问题。 / A TV fast-forward fix.

## [0.2.0] - 2026-09-18

- 缓冲时长可调。 / Adjustable buffering.
- 设置页分为多个标签。 / Settings split into tabs.
- 播放体验改进；修复按下键选择项目和播放状态指示。 / Playback UX improvements; fixes for choosing an item with Down and for the play status indicator.

## [0.1.0] – [0.1.9] - 2026-09-17 to 2026-09-18

- 首批版本：浏览媒体库、排序与搜索、详情页、播放器、添加服务器的二维码、支持更多格式、错误提示、遥控器导航修复、中文说明。 / The first releases: browsing libraries, sorting and search, the detail screen, the player, a QR code for adding a server, more formats, error messages, D-pad navigation fixes and a Chinese README.
