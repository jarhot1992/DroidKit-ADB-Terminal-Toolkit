# DroidKit: ADB Terminal Toolkit

<a id="droidkitadb-terminal-toolkit"></a>

**Your Android command center.**

Manage apps, run shell commands, control Android TV, transfer files, and troubleshoot Android devices.

## Download

- [ADB Shell - Debug Toolbox Pro](https://play.google.com/store/apps/details?id=com.github.superadb)
- [DroidKit: ADB Terminal Toolkit](https://play.google.com/store/apps/details?id=com.nextaix.androidtoolbox)
- [ADB Shell - Debug Toolbox](https://play.google.com/store/apps/details?id=com.github.standardadb)

<a id="-for-android-gamers"></a>

## 🔥 Level Up Your Android Gaming

**Related app: Mr. Zero: ADB Game Booster**

**Tune smarter. Know your FPS. Take control of your game.**

Optimize your settings and track your gaming performance with a game booster & FPS monitor built for Android gamers.

[**Get Mr. Zero on Google Play →**](https://play.google.com/store/apps/details?id=com.nextaix.game_booster)

## Enable Wireless Debugging from a Computer (Android 5.0+)

Open Wireless Debugging (ADB USB to Wi-Fi) lets you turn on wireless ADB from a Windows, macOS, or Linux computer without typing commands.

1. Turn on **USB debugging** on your phone, connect it with a USB data cable, and tap **Allow** when prompted.
2. Open the desktop tool, select your phone, and click **Enable wireless debugging**. Wait for **Wireless debugging is on**, then unplug the cable.
3. Open the Android ADB app, turn off pairing, and connect on port `5555`. To connect to another phone, use that phone's IP address and put both phones on the same Wi-Fi network. To connect to the phone you're using, enter `127.0.0.1`.

[Download on GitHub](https://github.com/jarhot1992/adb-usb-to-wifi) · [Setup guide](https://nextaix.com/adb-help/tutorials/open-wireless-debugging)

The phone you connect to must run Android 5.0 or later and allow USB debugging. The current Android app requires Android 7.0 or later. To connect to an Android 5 or 6 phone, install the app on another phone running Android 7.0 or later.

This tool enables ADB over TCP/IP on port `5555`. Android 11+ also offers wireless pairing in Settings, which uses the ports shown on the phone. For DroidKit's connection settings, follow [the traditional connection guide](md/ConnectADBText.md#enable-wireless-debugging-from-a-computer-android-50).

## Why DroidKit?

Use DroidKit's built-in controls to manage devices, or open Terminal to run commands.

- Keep several terminal tabs open. Rerun commands from history, use suggestions and path completion to save typing, and reuse your shell environment profiles.
- Inspect running apps and processes, manage startup and background activity, and use advanced app controls.
- Use your phone to navigate Android TV, type in multiple languages, and adjust the volume.
- Monitor CPU and memory in real time, take screenshots, check storage usage, and run diagnostics.

This repository includes connection guides, FAQs, release notes, and ways to send feedback.

## Complete Feature Set

### Device Connections and Management

Connect to the device running DroidKit or manage another Android device over ADB.

- Choose **Terminal**, **Universal**, or **Shizuku** connection methods. Shizuku is a local connection option with an Android 11+ guide.
- Pair through wireless debugging on supported devices, or use the traditional ADB TCP/IP workflow.
- Add, select, switch, and disconnect devices, with visibility into the current connection status.
- If DroidKit can't detect the connection port automatically when you use wireless debugging, enter the port shown on the **Wireless debugging** screen.

### Professional Terminal

Move from a quick command to a full debugging session without leaving DroidKit.

- Run ADB and shell commands to inspect the device, read logs, and troubleshoot issues.
- Keep multiple terminal tabs open and switch to a full-screen terminal when you need more room.
- Reuse command history, enter multiple lines, and access common symbols through quick input controls.
- Use smart command suggestions and command/path completion to reduce repetitive typing.
- Create and select shell environment profiles for recurring workflows.

### Application Management

Take control of installed apps and inspect the details behind each package.

- Install, launch, uninstall, or force-stop applications.
- Enable or disable apps, clear application data, and export APK files.
- Archive supported apps, suspend them temporarily, or restore them from suspension.
- Inspect version, size, permissions, installation source, and detailed package information.
- Use the **`uninstall --user 0`** option when you need to remove an app for the primary Android user.
- Open app settings and access or share the app's Google Play listing.

Advanced actions depend on the Android version, device permissions, and package. Some actions are restricted for protected system apps.

### Running Apps, Processes, and Startup Management

Understand what is running and manage how applications behave in the background.

- View running applications and app processes, and stop related apps when needed.
- Inspect background activity while investigating lag or unexpected resource usage.
- Manage background running, background autostart, and boot startup where the device supports these controls.
- Manage disabled and suspended states from the startup management tools.

Availability varies by device and Android version; system restrictions can prevent individual startup or background controls.

### Files and Storage

- Browse files on the connected device or on the device running DroidKit.
- Pull files from the connected device or push files to it from the device running DroidKit.
- Inspect file details and sort files to find the content you need.
- View total, used, and free storage, with usage grouped by content category.
- Locate large files and clear supported caches to reclaim storage.

### Screenshots

Capture a result, record a device state, or collect evidence for a bug report.

- Take an immediate screenshot or set a delay before capture.
- Capture screenshots repeatedly with a custom interval.
- Choose a save folder, save captures, and share screenshots.

### Android TV Remote, Text Input, and Volume

- Use **TV Remote** on your phone to control Android TV and TV boxes with directional controls and remote buttons. Change the remote layout in Settings.
- Type in Chinese and other languages on your phone instead of selecting characters with the TV remote.
- Adjust media, ringtone, call, and other supported volume channels.

The target device must accept an authorized ADB connection. Input and volume capabilities depend on the target device.

### Screen Configuration

Tune the display for testing, orientation changes, or a better TV layout.

- Set custom resolution and screen density (DPI).
- Choose screen rotation, control automatic rotation, and adjust supported screen margins.
- Restore default resolution and density.
- Confirm resolution and density changes, with automatic reversion if you do not keep them.

Supported display controls vary by Android version and device firmware.

### Battery Information and Simulation

Check battery details and test behavior under different simulated power conditions.

- Inspect battery level, charging state, charging type, and available battery details.
- Simulate battery level and charging status for testing.
- Reset simulation to return to the device's actual battery state.

### Device Actions

Reach common device controls without typing each command yourself.

- Lock or wake the screen and send a known password to an authorized device.
- Keep the screen on or set the screen timeout to 30 seconds.
- Shut down, reboot, or reboot into Recovery or Bootloader mode.
- Toggle supported mobile data, Bluetooth, Wi-Fi, and NFC controls.
- Open system settings directly.

These actions depend on device support and permissions. Password input requires the known password; see the [device access FAQ](md/FAQ.md#how-do-i-unlock-my-device).

### System Monitoring and Diagnostics

Get a quick overview, then inspect the system in depth.

- Monitor CPU and memory usage in real time.
- Inspect hardware, model, Android version, build details, battery, and storage information.
- Export system information for troubleshooting and documentation.
- Run diagnostics for battery, display, power, applications, memory, CPU, connectivity, Wi-Fi, Bluetooth, sensors, audio, and other Android services.
- Run system inspection commands such as `dumpsys`, `df`, `mount`, and `uptime`, and read system information from `/proc`.

Diagnostic output depends on the services and permissions available on the connected device.

### System Properties and Android Settings

Inspect and configure the system values behind device behavior.

- View, search, favorite, and edit supported system properties.
- Browse **System**, **Secure**, and **Global** Android settings.
- Search settings by key or value, and add, edit, or delete supported entries.

Editing depends on shell permissions; some properties and settings are read-only or restricted by the system.

### Personalization, Pro, and Support

- Find tools through feature navigation and keep frequently used pages in favorites.
- Use dark mode and multilingual interfaces.
- Customize connection, terminal, screenshot, file, and remote-control preferences.
- Access connection videos, tutorials, troubleshooting answers, and in-app feedback.
- Explore Pro options in the app for advanced tools, pro-level actions, and ad removal. Check the in-app offer for the benefits and access available in your edition.

## Built for Your Workflow

| You want to… | Start with… |
| --- | --- |
| Debug an app or investigate a device issue | Terminal, app details, processes, and diagnostics |
| Understand background activity | Running apps, startup management, and system monitoring |
| Maintain a phone, tablet, or TV box | Application management, file transfers, and storage analysis |
| Make Android TV navigation and typing easier | TV Remote, text input, and volume controls |
| Test display or power-related behavior | Screen configuration and battery simulation |
| Share useful evidence with support | Screenshots, system information, and diagnostic output |

## Enable ADB

**Local connection** means working with the device running DroidKit. **Remote connection** means managing another Android device, such as a phone or TV box, over an authorized ADB connection.

Choose the tutorial that matches the target device and connection method. The Android versions below describe connection workflows, not DroidKit's minimum installation requirements.

[Open Wireless Debugging (ADB USB to Wi-Fi)](https://github.com/jarhot1992/adb-usb-to-wifi) turns on wireless ADB from a Windows, macOS, or Linux computer. Connect your phone over USB for setup, then use port `5555` with pairing turned off.

Follow the [setup guide](https://nextaix.com/adb-help/tutorials/open-wireless-debugging), then [connect in DroidKit](md/ConnectADBText.md#enable-wireless-debugging-from-a-computer-android-50). The connection guide explains how to allow USB debugging, which Android versions are supported, and how to connect to your own phone or another phone.

<a id="android11"></a>

### Android 11+

For supported phones, Android 11+ offers wireless debugging with pairing. Follow the setup guide for the current pairing and connection ports.

| Connection | Method | Video tutorial |
| --- | --- | --- |
| Local | Shizuku (Android 11+) | [Connect locally with Shizuku](https://youtube.com/shorts/5k7PbHxuu_8) |
| Local | Terminal (original method, Android 4.x+) | [Connect locally with Terminal](https://youtube.com/shorts/PPmwlESYqkw) |
| Remote | Terminal (original method, Android 4.x+) | [Connect remotely with Terminal](https://youtube.com/shorts/07cEMJ6YHII) |
| Local | Universal (newer method, Android 4.x+) | [Connect locally with Universal](https://youtube.com/shorts/ePioznkFEVg) |
| Remote | Universal (newer method, Android 4.x+) | [Connect remotely with Universal](https://youtube.com/shorts/zF-EuqXL35c) |

- [Official ADB documentation](https://developer.android.com/studio/command-line/adb)
- [Complete text setup guide](md/ConnectADBText.md)
- [Additional general video guide](https://www.youtube.com/watch?v=_JjpbufTMew)
- [Illustrated Android 11+ setup guide](https://github.com/jarhot1992/Remote-ADB/blob/main/md/openMobileADB11_13.md)

<a id="android4x"></a>

### Android 4.x+

For older devices, follow the USB setup and traditional TCP/IP instructions. The Terminal and Universal video guides above also cover Android 4.x+ connection workflows.

- [Official ADB documentation](https://developer.android.com/studio/command-line/adb)
- [Complete text setup guide](md/ConnectADBText.md)
- [Illustrated Android 4.x+ setup guide](https://github.com/jarhot1992/Remote-ADB/blob/main/md/openMobileADB4x_13.md)

### TV Box / Smart TV

Enable debugging on the TV or box, then connect to it remotely in DroidKit. Menu names and wireless debugging availability vary by model and Android version.

- [Official ADB documentation](https://developer.android.com/studio/command-line/adb)
- [Complete text setup guide](md/ConnectADBText.md)
- [Illustrated TV debugging setup guide](https://github.com/jarhot1992/Remote-ADB/blob/main/md/openTVADB.md)

<a id="faq"></a>
<a id="changelog"></a>

## FAQ and Changelog

- [Frequently asked questions](md/FAQ.md): connection help, editions, ads, privacy, and supported use cases.
- [Changelog](md/Changelog.md): published release notes and improvements.

### Learn ADB

- [Official ADB guide and command reference](https://developer.android.com/studio/command-line/adb)
- [awesome-adb: useful ADB commands and examples](https://github.com/mzlogin/awesome-adb/blob/master/README.en.md)

## Feedback

Questions, bug reports, and feature ideas are welcome. Use the in-app feedback page or email [support@nextaix.com](mailto:support@nextaix.com).

For troubleshooting, include your device model, Android version, app version, connection method, and the steps that reproduce the issue. Screenshots or relevant diagnostic output help us understand the problem.
