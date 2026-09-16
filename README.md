# Bemplayer

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.1.0**, released 2026-09-16. Requires Android 6.0 or newer
(API 23).

## Download

| Download | Best for | Size |
| --- | --- | --- |
| [armeabi-v7a](https://github.com/liveinaus/bemplayer/releases/download/v0.1.0/bemplayer-0.1.0-armeabi-v7a.apk) | Most Android TV boxes and sticks, including older Fire TV | 3.2 MB |
| [arm64-v8a](https://github.com/liveinaus/bemplayer/releases/download/v0.1.0/bemplayer-0.1.0-arm64-v8a.apk) | Newer 64 bit devices, Shield TV, recent Fire TV and Chromecast | 3.2 MB |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.1.0/bemplayer-0.1.0-universal.apk) | Works everywhere, larger download. Use if unsure | 3.3 MB |

Not sure which one? Take `universal`. It is a larger download and works on everything.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.1.0-universal.apk
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

| Key | In the player |
| --- | --- |
| Centre, play/pause | Play or pause |
| Left, right | Seek. Hold to go faster: 10s, 30s, 1m, 5m |
| Up | Playback diagnostics |
| Down | Audio and subtitle tracks |
| Back | Close the menu, then hide the controls, then leave |

The green button opens diagnostics from any screen, which is the quickest way to get
information for a bug report.

## What is in this release

Check the signing key the way the packaging step does

keytool ignores -keypass on a PKCS12 keystore, which cannot hold a key password
of its own, so the check passed a key password that Gradle then rejected with
"Given final block not properly padded". The check now loads the keystore and
calls getKey through the JDK, which is what packaging does, and falls back to
the store password when the key password secret does not decrypt the key.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>

## Verifying a download

```
dc1c4eaf694a49ce83c54fc434dc95a5f2bf4942ef920c126bfc21c2ede6abf9  bemplayer-0.1.0-armeabi-v7a.apk
ae0b59146d27d2f73b40e3b8bd59e7fb17f90659e7582fd385d2470add89e746  bemplayer-0.1.0-arm64-v8a.apk
379ad2b31f5d4a4f6cfa8df2aa22ac0b2af1844dfba23c5de587436ed3ae3d85  bemplayer-0.1.0-universal.apk
```

Check one with `sha256sum bemplayer-0.1.0-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `ba8926c`.

Version 0.1.0 is build 100.
