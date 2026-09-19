<img src="docs/logo.png" alt="Bemplayer" width="420">

[简体中文](README.md) | English

An Emby client for Android TV, built for a remote control rather than a touchscreen.

**Latest version 0.3.3**, released 2026-09-19. Requires Android 6.0 or newer
(API 23).

## Download

| Download | Best for | Size |
| --- | --- | --- |
| [armeabi-v7a](https://github.com/liveinaus/bemplayer/releases/download/v0.3.3/bemplayer-0.3.3-armeabi-v7a.apk) | Most Android TV boxes and sticks, including older Fire TV | 9.8 MB |
| [arm64-v8a](https://github.com/liveinaus/bemplayer/releases/download/v0.3.3/bemplayer-0.3.3-arm64-v8a.apk) | Newer 64 bit devices, Shield TV, recent Fire TV and Chromecast | 10.8 MB |
| [universal](https://github.com/liveinaus/bemplayer/releases/download/v0.3.3/bemplayer-0.3.3-universal.apk) | Works everywhere, larger download. Use if unsure | 16.1 MB |

Not sure which one? Take `universal`. It is a larger download and works on everything.

## Install

Android TV will not install an app from a file until you allow it. The prompt appears the
first time and points at the right settings screen.

**With a file manager or sideload app** such as Downloader or Send Files to TV: copy the
APK across, open it, and accept the install prompt.

**With adb**, from a computer on the same network:

```bash
adb connect <tv-ip>:5555
adb install -r bemplayer-0.3.3-universal.apk
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

Publish v0.3.2

## Verifying a download

```
7f743c5fb3023288a6557fda2fea9b1ea283a8a45afbbe1e1939cecbfd125f0c  bemplayer-0.3.3-armeabi-v7a.apk
92efb4194ac654aaa72e101e18f23ae3b44a306beaa37cccf3919aed56ab6622  bemplayer-0.3.3-arm64-v8a.apk
493f5eb9e71d8c1f0325471e1350f6e992cff0bfe9cb6d7dea49af6c8154eafa  bemplayer-0.3.3-universal.apk
```

Check one with `sha256sum bemplayer-0.3.3-universal.apk`.

## Reporting a problem

Open an issue at https://github.com/liveinaus/bemplayer/issues. The most useful thing you can attach
is a log export: press the green button on the remote, then Export, and the screen tells
you where the files landed.

Please include your device model, the Android version and the Emby server version.

## About this repository

This repository publishes builds only. It holds the releases, this page and
`update.json`, which is the file the app polls to discover new versions. The source is
kept in a separate private repository, and each release records the commit it was built
from: `5cf47ed`.

Version 0.3.3 is build 303.
