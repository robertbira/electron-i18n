# autoUpdater

> Paganahin ang app na awtomatikong mag-update ang kanilang sarili.

Ang proseso: [Main](../glossary.md#main-process)

Ang`autoUpdater`modyul ay nagbibigay ng isang interface para sa [Squirrel](https://github.com/Squirrel) na balangkas.

Maaari mong mabilis na ilunsad ang isang multi-platform release server para sa pamamahagi ng iyong applikasyon sa pamamagitan ng paggamit ng isa sa mga proyektong ito:

* [nuts](https://github.com/GitbookIO/nuts):*Ang smart release server para sa iyong mga applikasyon, gamit ang Github bilang isang backend. Nag a update ng automatiko sa Squirrel (Mac & Windows)*
* [electron-release-server](https://github.com/ArekSredzki/electron-release-server):* Isang ganap at tampok, na mayroong sariling naka-host release server para sa mga aplikason ng electron, magkabagay sa auto-updater*
* [squirrel-updates-server](https://github.com/Aluxian/squirrel-updates-server):* Isang simpleng node.js server para sa Squirrel.Mac at Squirrel.Windows na kung saan gumagamit ng inilabas ng Github*
* [squirrel-release-server](https://github.com/Arcath/squirrel-release-server):*Isang simpleng PHP na applikasyon para sa Squirrel.Windows na nagbabasa ng mga update mula sa isang folder. Sinusuportahan ng mga update sa delta.*

## Babala sa plataporma

Bagama't ang `autoUpdater` ay nagbibigay ng isang magkaparehong API para sa iba't ibang plataporma, mayroon pa rin ilang mga bahagyang pagkakaiba sa bawat plataporma.

### macOS

Sa macOS, ang `autoUpdater` na modyul ay ginawa [sa Squirrel.Mac](https://github.com/Squirrel/Squirrel.Mac), ibig sabihin hindi mo kailangan ng kahit anong espesyal na set-up para mapagana ito. Para sa mga kinakailangan ng panig ng server, maari mong basahin ang [Server Support](https://github.com/Squirrel/Squirrel.Mac#server-support). Tandaan lamang na ang [App Transport Security](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW35)(ATS) ay nalalapat sa lahat ng mga kahilingan na ginawa bilang bahagi ng proseso ng pag-update. Ang mga apps na kailangan hindi isama sa ATS ay maaaring idadag sa susi ng `NSAllowsArbitraryLoads` para sa kanilang app plist.

**Tandaan:** Ang iyong applikasyon at dapat nakalagda para sa awtomatikong pag-aupdate ng macOS. Ito ay kinakailangan ng `Squirrel.Mac`.

### Windows

Sa Windows, ay kailangan mong ilagay ang iyong app sa makina ng gagamit bago mo magamamit ang `autoUpdater`, kaya't inirerekomenda na iyong gamitin ang [electron-winstaller](https://github.com/electron/windows-installer), [electron-forge](https://github.com/electron-userland/electron-forge) or the [grunt-electron-installer](https://github.com/electron/grunt-electron-installer) na pakete para mabuo ang Windows installer.

Kapag ginagamit ang [electron-winstaller](https://github.com/electron/windows-installer) o ang [electron-forge](https://github.com/electron-userland/electron-forge) siguraduhing hindi mo subukan mag-update ng iyong app[ sa unang pagkakataon na ito ay tumatakbo](https://github.com/electron/windows-installer#handling-squirrel-events)(Mangyari ring tignan [ang isyung ito para sa karagdagang impormasyon](https://github.com/electron/electron/issues/7155)). Inirerekomenda rin naming gumamit ng [electron-squirrel-startup](https://github.com/mongodb-js/electron-squirrel-startup)para makakuha ng shortcut sa desktop para sa iyong app.

Ang installer na nabuo gamit ang Squirrel ay lilikha ng isang shortcut icon na mayroong[Application User Model ID](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378459(v=vs.85).aspx) sa format ng `com.squirrel.PACKAGE_ID.YOUR_EXE_WITHOUT_DOT_EXE`,halimbawa nito ay `com.squirrel.slack.Slack` at `com.squirrel.code.Code`. Kailangan mong gamitin ang parehong ID para sa iyong app sa `app.setAppUserModelId` API, kung hindi ang Windows ay hindi magagawang ilagay ang iyong app ng wasto sa iyong task bar.

Hindi gaya ng sa Squirrel.Mac, ang Windows ay kayang mag-host ng update sa S3 o sa kahit anong static file ng host. Maari mong basahin ang dokumento ng [Squirrel.Windows](https://github.com/Squirrel/Squirrel.Windows)para makakuha pa ng higat pang detalye tungkol sa kung paano gumagana ang Squirrel.Windows.

### Linux

Walang nakalagay na suporta para sa auto-updater para sa Linux, kaya't inirerekomenda na gamitin ang distribution's package manager para i-update ang iyong app.

## Pangyayari

Ang `autoUpdater` maglalabas ng mga ganitong pangyayari:

### Pangyayari: 'error'

Magbabalik ng:

* `error` Error

Lumabas kapag mayroong mali habang ina-update.

### Pangyayari:'checking-for-update'

Lumalabas kapag sinusuri kung ang update ay nagsimula na.

### Pangyayari: 'update-available'

Lumalabas kapag mayroong pagbabago. Ang pag-update ay awtomatikong na-download.

### Pangyayari: 'update-not-available'

Napalabas kapag walang available na pag-update.

### Pangyayari: 'update-downloaded'

Magbabalik ng:

* `event` Event
* `releaseNotes` Lupid
* `releaseNotes` Lubid
* `releaseDate` Petsa
* `updateURL` Lubid

Lumalabas kung ang update ay nadownload na.

Tanging Windows lamang`releaseName` is available.

## Pamamaraan

Ang `autoUpdater` na gamit ay mayroong ibat-ibang pamamaraan:

### `autoUpdater.setFeedURL(url[, requestHeaders])`

* `url` String
* `requestHeaders` Onject *macOS* (opsyonal) - kahilingan sa ulunan ng HTTP.

Tinatakda ang `url` at nagpapasimula ng auto-updater.

### `autoUpdater.getFeedURL()`

Bumalik `String` - Ang kasalukuyang update feed URL.

### `autoUpdater.checkForUpdates()`

Itanong sa server kung merong bago. Kaylangan mong tumawag `setFeedURL` bago gamitin itong API.

### `autoUpdater.quitAndInstall()`

Uulitin ang app at iinstall ang mga update pagkatapos itong ma download. Ito ay dapat lamang tawagin pagkatapos ng `update-downloaded` ay lumabas na.

**Tandaan:** Ang `autoUpdater.quitAndInstall()`ay isasara ang lahat ng naunang applikasyon sa windows at maglalabas ng mga `bago-itigil` na pangyayari`app`pagkatapos nito. Ito ay kaiba mula sa normal na quit event sequence.