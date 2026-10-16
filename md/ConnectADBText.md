# Complete ADB Setup Guide (Android 4.x–Android 14)

ADB (Android Debug Bridge) lets you communicate with Android devices to run commands, install apps, inspect logs, transfer files, and more.

This guide covers **Android 4.x through Android 14** setup instructions for **USB debugging** and **wireless debugging**. Connection workflows and menu names depend on the target device; this version range does not describe DroidKit's minimum installation requirements.

[Back to DroidKit](../README.md) · [FAQ](FAQ.md) · [Changelog](Changelog.md)

<a id="-complete-adb-setup-guide-android-4x---android-14"></a>

## Choose Your Connection Workflow

- **Local connection:** use DroidKit to work with the Android device running the app. Follow the selected Terminal, Universal, or Shizuku method in the [video guides](../README.md#android11).
- **Remote connection:** use DroidKit to manage another Android device, such as a phone or TV box. Follow the remote Terminal or Universal video guide and enable debugging on the target device.
- **Computer connection:** use the Platform Tools and computer-side command examples below for a desktop ADB workflow. A computer is not a prerequisite for every DroidKit connection method.

Shizuku is a local connection option; its linked guide covers Android 11+. For TV boxes and smart TVs, also see the [illustrated TV setup guide](https://github.com/jarhot1992/Remote-ADB/blob/main/md/openTVADB.md).

<a id="-table-of-contents"></a>

## Table of Contents

1. [Choose your connection workflow](#choose-your-connection-workflow)
2. [Prerequisites](#prerequisites)
3. [Enable Developer Options](#enable-developer-options)
4. [USB Debugging Configuration](#usb-debugging-configuration)
5. [Wireless Debugging Configuration](#wireless-debugging-configuration)
6. [Brand-Specific Considerations](#brand-specific-considerations)
7. [Troubleshooting](#troubleshooting)
8. [Advanced Tips](#advanced-tips)

## Prerequisites

The computer setup below applies to desktop ADB commands. For DroidKit-only connections, follow the app's selected connection method and the linked videos.

### Computer Setup

1. **Download ADB Tools**
   - **Windows**: Download [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools).
   - **macOS**: Install with Homebrew: `brew install android-platform-tools`.
   - **Linux**:

     ```bash
     sudo apt install android-tools-adb android-tools-fastboot  # Ubuntu/Debian
     sudo yum install android-tools                            # CentOS/RHEL
     ```

2. **Verify ADB Installation**

   ```bash
   adb --version
   ```

   The output should include a version number, such as `Android Debug Bridge version 1.0.41`.

### Device Preparation

- Keep the device battery above 30%.
- Prepare a USB data cable for the initial USB setup.
- Connect the phone and computer to the same Wi-Fi network for wireless debugging.

## Enable Developer Options

### Universal Steps (All Android Versions)

These paths are common examples. Menu names and the location of Developer options vary by Android version and manufacturer.

1. **Open Settings**
   - Open **Settings** from the home screen or app drawer.

2. **Navigate to System Information**
   - Look for one of these menu paths:
     - **"About phone"** or **"About tablet"**
     - **"System"** → **"About phone"**
     - **"System & updates"** → **"About phone"**

3. **Activate Developer Mode**
   - Find **Build number** or **Build version**.
   - **Tap seven times in succession**.
   - You should see a countdown such as "X more taps to become a developer."
   - The device confirms: "You are now a developer!"

4. **Access Developer Options**
   - Return to the main Settings menu.
   - Typical **Developer options** locations include:
     - **Android 4.x-6.x**: Settings → Developer options
     - **Android 7.x-8.x**: Settings → System → Developer options
     - **Android 9.x-11**: Settings → System → Advanced → Developer options
     - **Android 12-14**: Settings → System → Developer options

### Brand-Specific Paths

| Brand | Developer Options Path |
| --- | --- |
| **Samsung** | Settings → About phone → Software information → Build number |
| **Huawei/Honor** | Settings → About phone → Build number |
| **Xiaomi** | Settings → About phone → All specs → MIUI version |
| **OPPO** | Settings → About phone → Build number |
| **vivo** | Settings → System management → About phone → Build number |
| **OnePlus** | Settings → About phone → Build number |
| **Realme** | Settings → About phone → Build number |
| **Motorola** | Settings → About phone → Build number |
| **Sony** | Settings → About phone → Build number |
| **LG** | Settings → About phone → Software info → Build number |

## USB Debugging Configuration

### Basic Configuration Steps

USB debugging is the core requirement. Additional installation and security options, and whether a file-transfer mode is needed, vary by device.

1. **Enter Developer Options**
   - Open **Settings → System → Developer options**.

2. **Enable Essential Options**
   - Enable **USB debugging** (required).
   - Enable **Install via USB** if your device offers it and requires it for app installation.
   - Enable **USB debugging (Security settings)** if available and needed for the intended operations.

3. **USB Connection Mode**
   - In Developer options, find **Select USB Configuration**.
   - Choose **File Transfer** or **MTP** mode.

<a id="-first-time-connection-setup"></a>

### First-Time Connection Setup

1. **Connect Device**
   - Connect the phone to the computer with a USB data cable.
   - Select **File Transfer** mode on the phone.

2. **Authorize Debugging**
   - The phone displays an **Allow USB debugging?** dialog.
   - Select **Always allow from this computer** for a computer you trust.
   - Tap **Allow**.

3. **Verify Connection**

   ```bash
   # Check if device is recognized
   adb devices
   ```

   A connected, authorized device appears as:

   ```text
   List of devices attached
   1234567890ABCDEF    device
   ```

## Wireless Debugging Configuration

### Android 11+ Official Wireless Debugging

Android 11 introduced wireless debugging for supported phones without an initial USB connection. Follow the target device's pairing and connection information.

#### Configuration Steps

1. **Enable Wireless Debugging**
   - Open **Settings → System → Developer options**.
   - Enable **Wireless debugging**.
   - Connect the phone and computer to the same Wi-Fi network.

2. **Pair Device**
   - Tap **Wireless debugging** to open its details.
   - Tap **Pair device with pairing code**.
   - The pairing dialog displays information such as:

     ```text
     IP address: 192.168.1.100
     Port: 12345
     Pairing code: 123456
     ```

3. **Computer-Side Pairing**

   ```bash
   # Use displayed IP and port for pairing
   adb pair 192.168.1.100:12345

   # Enter the 6-digit pairing code from phone
   Enter pairing code: 123456
   ```

4. **Connect Device**

   For Android 11+ paired wireless debugging, use the connection endpoint shown on the main **Wireless debugging** page. Its port differs from the pairing-dialog port and can change. After pairing, ADB may connect automatically; if it does not, use the current connection endpoint.

   The example below uses the traditional TCP/IP port, `5555`. For paired wireless debugging, replace that port with the current connection port. See the [official ADB wireless connection guide](https://developer.android.com/tools/adb#connect-to-a-device-over-wi-fi).

   ```bash
   # Traditional TCP/IP example; use the displayed connection port for Android 11+ pairing
   adb connect 192.168.1.100:5555

   # Verify connection
   adb devices
   ```

### Android 10 and Below Wireless Debugging

For the standard ADB workflow on Android 10 and earlier, first connect over USB to enable TCP/IP debugging. This traditional method can also be used on newer Android versions.

#### Detailed Configuration Steps

1. **Initial USB Configuration**
   - Complete [USB Debugging Configuration](#usb-debugging-configuration) first.
   - Confirm that `adb devices` lists an authorized device.

2. **Enable TCP/IP Mode**

   ```bash
   # Enable ADB TCP/IP mode on port 5555
   adb tcpip 5555
   ```

   Expected output:

   ```text
   restarting in TCP mode port: 5555
   ```

3. **Get Device IP Address**

   **Method 1: Via ADB Command**

   ```bash
   # Get device IP address
   adb shell ip route | grep wlan
   ```

   **Method 2: Check Phone Settings**

   - Open **Settings → Wi-Fi**.
   - Tap the connected Wi-Fi network.
   - View the **IP address** (for example, `192.168.1.100`).

4. **Disconnect USB**

   ```bash
   # Disconnect USB connection
   adb disconnect
   ```

   Then unplug the USB cable. `adb disconnect` closes network connections; unplugging the cable ends the physical USB connection.

5. **Connect Wirelessly**

   ```bash
   # Connect to device (replace with actual IP)
   adb connect 192.168.1.100:5555
   ```

   Expected output:

   ```text
   connected to 192.168.1.100:5555
   ```

6. **Verify Wireless Connection**

   ```bash
   # Check device status
   adb devices
   ```

   Expected output:

   ```text
   List of devices attached
   192.168.1.100:5555    device
   ```

### Restore USB Debugging Mode

This command returns a traditional TCP/IP ADB session to USB mode. Android 11+ wireless pairing is managed separately in the device's Wireless debugging settings.

To return to USB debugging mode:

```bash
# Re-enable USB debugging mode
adb usb
```

## Brand-Specific Considerations

The brand-specific options below depend on the model, firmware, and Android version; use the options that actually appear on your device. Some commands require an already authorized ADB connection or additional shell privileges.

### Samsung Devices

**Special Requirements:**

- Enable **"USB debugging"** and **"Install via USB"** in Developer options.
- Samsung USB drivers may be required on Windows.
- Some models need **"Wireless debugging"** enabled separately.

**Common Issues:**

- Knox security may interfere with debugging.
- Some Galaxy models require **"Developer options"** → **"USB debugging"** → **"Allow debugging over wireless"**.

**Solutions:**

```bash
# For Samsung devices, try this if connection fails
adb kill-server
adb start-server
adb devices
```

### Xiaomi/MIUI Devices

**Special Requirements:**

- Enable **"USB debugging (Security settings)"** in Developer options.
- A Mi account login may be required.
- Turn off **"MIUI optimization"** in Developer options.

**Common Issues:**

- MIUI security restrictions may block ADB.
- Some models require **"Install via USB"** and **"USB debugging (Security settings)"**.

**Solutions:**

```bash
# For MIUI devices with connection issues
adb shell settings put global development_settings_enabled 1
```

### Huawei/Honor Devices

**Special Requirements:**

- Enable **"Allow HiSuite to use HDB"** in Settings → Security.
- Some models need **"USB debugging"** and **"Allow debugging in charging mode"**.
- EMUI may require additional permissions.

**Common Issues:**

- HiSuite may interfere with ADB.
- Some models require disabling **"Enhanced protection"**.

**Solutions:**

```bash
# Disable HiSuite if causing conflicts
adb shell pm disable-user com.huawei.hisuite
```

### OPPO/ColorOS Devices

**Special Requirements:**

- Enable **"USB debugging"** and **"Install via USB"**.
- May need to disable **"USB debugging monitoring"**.
- Some models require **"Disable permission monitoring"**.

**Common Issues:**

- ColorOS security may block wireless debugging.
- Permission dialogs may appear frequently.

**Solutions:**

- Disable **"Permission monitoring"** in Developer options.
- Enable **"Disable permission monitoring"** if available.

### vivo Devices

**Special Requirements:**

- Enable **"USB debugging"** in Developer options.
- A vivo account login may be required.
- Some models need **"Install via USB"** enabled.

**Common Issues:**

- Funtouch OS security restrictions.
- May require **"USB debugging (Security settings)"**.

**Solutions:**

- Enable **"USB debugging (Security settings)"** if available.
- Disable **"USB debugging monitoring"**.

### OnePlus Devices

**Special Requirements:**

- Follow the standard Android debugging process.
- Some functions may require **"Advanced reboot"**.
- OxygenOS generally supports standard ADB workflows.

**Common Issues:**

- Standard ADB setup generally works without additional steps.
- Some models may require **"Install via USB"**.

### Realme Devices

**Special Requirements:**

- Enable **"USB debugging"** and **"Install via USB"**.
- May need to disable **"USB debugging monitoring"**.
- Some models require additional security permissions.

**Common Issues:**

- RealmeUI security may interfere.
- Permission monitoring can cause issues.

### Motorola Devices

**Special Requirements:**

- Follow the standard Android debugging process.
- Additional requirements are generally minimal.
- Standard ADB workflows generally apply.

**Common Issues:**

- Standard setup generally works without additional steps.
- May require **"Install via USB"** for app installation.

## Troubleshooting

<a id="-problem-1-device-not-recognized"></a>

### Problem 1: Device Not Recognized

**Symptoms:** `adb devices` shows `unauthorized`, or no device is listed.

**Solutions:**

1. Check that USB debugging is enabled.
2. Unplug and reconnect the USB cable.
3. Authorize debugging again on the phone.
4. Try another USB port.
5. Update or reinstall the device drivers.
6. Use the original USB data cable if available.

<a id="-problem-2-wireless-connection-failure"></a>

### Problem 2: Wireless Connection Failure

**Symptoms:** `adb connect` fails or times out.

**Solutions:**

1. **Check Network Connectivity**

   ```bash
   # Test network connectivity
   ping 192.168.1.100
   ```

2. **Verify Port Access**

   ```bash
   # Check if port is open
   telnet 192.168.1.100 5555
   ```

3. **Restart ADB Service**

   ```bash
   # Restart ADB service
   adb kill-server
   adb start-server
   ```

4. **Check Firewall Settings**
   - Check that the computer firewall is not blocking ADB.
   - If testing with the firewall temporarily disabled, restore it after the test.

<a id="-problem-3-unstable-connection"></a>

### Problem 3: Unstable Connection

**Symptoms:** The connection drops frequently, or the device appears as `offline`.

**Solutions:**

1. **Stable Wi-Fi Environment**
   - Check that the Wi-Fi signal is strong.
   - Avoid periods of heavy network traffic.

2. **Power Management Settings**
   - Check the phone's Wi-Fi power-saving settings; disable power saving if it interrupts the connection.
   - The existing power-management guidance also suggests turning off **Stay awake while charging** in Developer options.

3. **Fixed IP Address**
   - Assign a fixed IP address in the router settings.
   - Reconnect if an IP address change breaks the connection.

<a id="-problem-4-authorization-issues"></a>

### Problem 4: Authorization Issues

**Symptoms:** `adb devices` lists the device as `unauthorized`.

**Solutions:**

1. **Revoke USB Debugging Authorizations**
   - Open **Developer options → Revoke USB debugging authorizations**.
   - Reconnect the device and authorize debugging again.

2. **Check RSA Key Fingerprint**
   - Verify the RSA key fingerprint before approving the connection.
   - If resetting keys is necessary, remove `~/.android/adbkey*` and reconnect as shown below.

3. **Reset ADB Keys**

   The example below removes this computer's ADB keys, so previously trusted devices will need to authorize it again.

   ```bash
   # Reset ADB keys
   adb kill-server
   rm ~/.android/adbkey*
   adb start-server
   ```

## Advanced Tips

### Multi-Device Management

```bash
# View all connected devices with details
adb devices -l

# Execute command on specific device
adb -s <device_id> shell <command>

# Example:
adb -s 192.168.1.100:5555 shell ls /sdcard/
```

### Multiple Device Connections

```bash
# Connect multiple devices
adb connect 192.168.1.100:5555
adb connect 192.168.1.101:5555

# View all devices
adb devices

# Execute same command on all devices
for device in $(adb devices | tail -n +2 | cut -sf1); do
    adb -s $device shell echo "Hello from $device"
done
```

### Automation Scripts

These examples use the traditional TCP/IP workflow. Begin with an authorized USB connection and replace the sample IP address with your device's address.

**Windows batch script:**

```batch
@echo off
echo Starting ADB wireless debugging...
adb tcpip 5555
timeout /t 3
adb connect 192.168.1.100:5555
adb devices
pause
```

**Linux/macOS shell script:**

```bash
#!/bin/bash
echo "Starting ADB wireless debugging..."
adb tcpip 5555
sleep 3
adb connect 192.168.1.100:5555
adb devices
```

<a id="-network-debugging"></a>

### Network Debugging

```bash
# View network information
adb shell ip addr show wlan0

# Check ADB service status
adb shell getprop service.adb.tcp.port

# View ADB processes
adb shell ps | grep adbd
```

### Security Considerations

1. **Use wireless debugging only on trusted networks**
2. **Disable wireless debugging after use**
3. **Regularly check authorized debugging devices**
4. **Avoid using wireless debugging on public Wi-Fi**
5. **Use VPN when debugging over untrusted networks**

### Performance Optimization

**Applicability:** These commands change debugging settings and a trace-related system property. Their availability and effects depend on the device and shell permissions. The performance and buffer-size effects described in the comments have not been independently verified.

```bash
# Optimize ADB performance
adb shell settings put global development_settings_enabled 1
adb shell settings put global adb_enabled 1

# Increase ADB buffer size
adb shell setprop persist.adb.trace_mask 0
```

## Summary

Use this guide as a reference for:

- Enabling Developer options across the Android versions covered here.
- Configuring and authorizing USB debugging.
- Setting up wireless debugging on Android 11+ or traditional TCP/IP on older devices.
- Finding brand-specific settings and requirements.
- Troubleshooting common connection issues.
- Using multiple devices, automation scripts, and advanced debugging commands.

Return to [DroidKit's feature overview](../README.md#complete-feature-set) to explore the app-management, terminal, TV, file, and diagnostic tools available after connecting.

### Further Learning

- [Android Developer Documentation - ADB](https://developer.android.com/studio/command-line/adb).
- [ADB Command Reference](https://developer.android.com/studio/command-line/adb#commandsummary).
- [Android Debug Bridge Advanced Usage](https://developer.android.com/studio/command-line/adb#advanced).
