# 更新日志 / Changelog

每次修改都在 **Unreleased** 下记一条要点，中文在前、英文在后。发布时
`scripts/release.sh` 会把这一节作为该版本的发布说明，并把它归到版本号下面。
完整的历史都在这里；GitHub 上每个发行版只带自己那一节。

Every change adds a line under **Unreleased**, Chinese first then English.
`scripts/release.sh` takes that section as the release notes and files it under
the version. The whole history lives here; each GitHub release carries only its
own section.

## [Unreleased]

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
