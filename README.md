<img src="docs/logo.png" alt="Bemplayer" width="420">

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.1.2**, released 2026-09-17. Requires Android 6.0 or newer
(API 23).

## Download

| Download | Best for | Size |
| --- | --- | --- |
| [armeabi-v7a](https://github.com/liveinaus/bemplayer/releases/download/v0.1.2/bemplayer-0.1.2-armeabi-v7a.apk) | Most Android TV boxes and sticks, including older Fire TV | 7.1 MB |
| [arm64-v8a](https://github.com/liveinaus/bemplayer/releases/download/v0.1.2/bemplayer-0.1.2-arm64-v8a.apk) | Newer 64 bit devices, Shield TV, recent Fire TV and Chromecast | 8.1 MB |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.1.2/bemplayer-0.1.2-universal.apk) | Works everywhere, larger download. Use if unsure | 13.4 MB |

Not sure which one? Take `universal`. It is a larger download and works on everything.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.1.2-universal.apk
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

The green button opens diagnostics from any screen, which is the quickest way to get
information for a bug report.

## What is in this release

Publish a dev channel alongside the stable one

A dev release is tagged dev-0.2.0 and calls itself 0.2.0-dev, so an
installed APK always names the stream it came from. It is published as a
prerelease, which is what keeps it out of the releases/latest URL every
stable install reads, and it never rewrites the front page.

Driven from the source repo by ./scripts/release.sh --dev 0.2.0.

Co-Authored-By: Claude Opus 5 (1M context) <noreply@anthropic.com>

## Verifying a download

```
e05681e99a700af3af772ee257384537d3869bf7960be0b132ab0bc92718001c  bemplayer-0.1.2-armeabi-v7a.apk
bb94219b49f485a556a15dba886ca88fe9cba706247a44e2670af1df7c3f5b7e  bemplayer-0.1.2-arm64-v8a.apk
f6b21b1c862994a25bb9046719f92a6303fd3e1e6901030e58a8c6e55ff6d31c  bemplayer-0.1.2-universal.apk
```

Check one with `sha256sum bemplayer-0.1.2-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `6d6e8e4`.

Version 0.1.2 is build 102.
