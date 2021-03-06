# Installation

> Tipps zum Installieren von Electron

Nutzen Sie [`npm`](https://docs.npmjs.com/) um Electron als vorgefertigtes Archiv zu installieren. Die bevorzugte Methode ist jedoch, Electron als Abhängigkeit in Ihrer App einzubinden:

```sh
npm install electron --save-dev
```

See the [Electron versioning doc](electron-versioning.md) for info on how to manage Electron versions in your apps.

## Globale Installation

Sie können den `electron`-Befehl auch global in Ihrer `$PATH`-Variable installieren:

```sh
npm install electron -g
```

## Individuelle Anpassung

Falls Sie die herunterzuladende Architektur ändern möchten (z.B. `ia32` auf einem `x64`-Rechner), dann können Sie den `--arch`-Flag verwenden oder die Umgebungsvariable `npm_config_arch` setzen:

```shell
npm install --arch=ia32 electron
```

In addition to changing the architecture, you can also specify the platform (e.g., `win32`, `linux`, etc.) using the `--platform` flag:

```shell
npm install --platform=win32 electron
```

## Proxys

Sofern Sie einen HTTP-Proxy nutzen müssen, können Sie [diese Umgebungsvariablen](https://github.com/request/request/tree/f0c4ec061141051988d1216c24936ad2e7d5c45d#controlling-proxy-behaviour-using-environment-variables) setzen.

## Custom Mirrors and Caches

During installation, the `electron` module will call out to [`electron-download`](https://github.com/electron-userland/electron-download) to download prebuilt binaries of Electron for your platform. It will do so by contacting GitHub's release download page (`https://github.com/electron/electron/releases/tag/v$VERSION`, where `$VERSION` is the exact version of Electron).

If you are unable to access GitHub or you need to provide a custom build, you can do so by either providing a mirror or an existing cache directory.

#### Mirror

You can use environment variables to override the base URL, the path at which to look for Electron binaries, and the binary filename. The url used by `electron-download` is composed as follows:

```txt
url = ELECTRON_MIRROR + ELECTRON_CUSTOM_DIR + '/' + ELECTRON_CUSTOM_FILENAME
```

For instance, to use the China mirror:

```txt
ELECTRON_MIRROR="https://npm.taobao.org/mirrors/electron/"
```

#### Cache

Alternatively, you can override the local cache. `electron-download` will cache downloaded binaries in a local directory to not stress your network. You can use that cache folder to provide custom builds of Electron or to avoid making contact with the network at all.

* Linux: `$XDG_CACHE_HOME` or `~/.cache/electron/`
* MacOS: `~/Library/Caches/electron/`
* Windows: `$LOCALAPPDATA/electron/Cache` or `~/AppData/Local/electron/Cache/`

On environments that have been using older versions of Electron, you might find the cache also in `~/.electron`.

You can also override the local cache location by providing a `ELECTRON_CACHE` environment variable.

The cache contains the version's official zip file as well as a checksum, stored as a text file. A typical cache might look like this:

```sh
├── electron-v1.7.9-darwin-x64.zip
├── electron-v1.8.1-darwin-x64.zip
├── electron-v1.8.2-beta.1-darwin-x64.zip
├── electron-v1.8.2-beta.2-darwin-x64.zip
├── electron-v1.8.2-beta.3-darwin-x64.zip
├── SHASUMS256.txt-1.7.9
├── SHASUMS256.txt-1.8.1
├── SHASUMS256.txt-1.8.2-beta.1
├── SHASUMS256.txt-1.8.2-beta.2
├── SHASUMS256.txt-1.8.2-beta.3
```

## Problemlösungen

Beim Ausführen von `npm install electron` können bei einigen Nutzern gelegentlich Installationsfehler auftreten.

In fast allen Fällen sind entstehen diese Fehler wegen Netzwerkproblemen und sind nicht mit dem `electron` npm package verbunden. Fehler wie `ELIFECYCLE`, `EAI_AGAIN`, `ECONNRESET`, and `ETIMEDOUT` weisen alle auf ein Problem mit dem Netzwerk hin. Das Problem kann am besten gelöst werden, wenn man das Netzwerk wechselt oder man eine Weile wartet und die Installation erneut versucht.

Man kann auch versuchen, Electron direkt unter [electron/electron/releases](https://github.com/electron/electron/releases) herunterzuladen, falls die Installation über `npm` weiterhin fehlschlägt.

If installation fails with an `EACCESS` error you may need to [fix your npm permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions).

Falls dieser Fehler dennoch bestehen bleibt, könnte es Abhilfe schaffen, den [unsafe-perm](https://docs.npmjs.com/misc/config#unsafe-perm)-Flag auf "true" zu setzen:

```sh
sudo npm install electron --unsafe-perm=true
```

In langsameren Netzwerken ist es ratsam den `--verbose`-Flag zu benutzen um den Downloadfortschritt anzuzeigen:

```sh
npm install --verbose electron
```

Müssen Sie die Ressourcen und die SHASUM-Datei erneut manuell herunterladen, dann setzen Sie die Umgebungsvariable `force_no_cache` auf `true`.