---
layout: default
title: 1. Connecting to mBot2
nav_order: 2
description: "Step-by-step USB connection, driver installation, and connection testing"
---

# Connecting Your Laptop to mBot2
{: .no_toc }

**Beginner-Friendly Guide** | **No Prior Experience Required**
{: .fs-6 .fw-300 }

This guide walks you through connecting your laptop to your mBot2 robot step by step, as if you've never done this before.

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What You'll Need

Before you start, gather these items:

- **mBot2 Robot** - The wheeled robot with the blue "brain" on top
- **CyberPi** - The blue rectangular computer on top of the robot (this is the "brain")
- **USB-C Cable** - A cable with a flat oval connector (looks like a phone charger)
- **Laptop/Computer** - Windows, Mac, or Linux
- **Charged Batteries** - The robot needs 3 18650 batteries installed and charged

> **💡 First Time Tip:** The CyberPi is the blue computer on top of your mBot2. It has a screen, buttons, and a USB-C port on the side. This is what we'll plug into your laptop.

---

## Step 1: Prepare Your mBot2

### Check the Batteries

1. **Turn the robot over** - Flip it upside down carefully
2. **Locate the battery compartment** - It's the long black box on the bottom
3. **Check battery installation** - You should see 3 cylindrical batteries
4. **Check the charge level**:
   - Turn robot right-side up
   - Press the **power button** on CyberPi (big button on top-left)
   - Look at the screen - battery icon should show charge level
   - If battery is low (red icon), charge the batteries first

### Power On the Robot

1. Press and **hold the power button** for 2 seconds
2. You'll see the screen light up with the Makeblock logo
3. Wait for the home screen to appear (shows battery, WiFi, etc.)

> **⚠️ Troubleshooting:** If nothing happens when you press power:
> - Check batteries are installed correctly (+ and - ends match the labels)
> - Try charging the batteries
> - Make sure the battery pack connector is plugged into the CyberPi

---

## Step 2: Connect USB Cable

### Find the Right Port

1. **Look at the side of CyberPi** - There are several ports
2. **Locate the USB-C port**:
   - It's the **flat oval port** (not the small square ones)
   - Usually on the **left side** of CyberPi
   - Look for a USB icon (⎍) next to it

### Plug It In

1. **Take your USB-C cable**
2. **Plug the USB-C end** (flat oval) into CyberPi
   - It only fits one way - don't force it
   - You should hear a small "click" when it's in
3. **Plug the USB-A end** (rectangular) into your laptop
   - This is the normal USB connector
4. **Watch the CyberPi screen** - You should see a connection notification

> **💡 Cable Tip:** Not all USB-C cables work for data! If your computer doesn't detect the robot, try a different cable. Charging-only cables won't work - you need a "data cable."

---

## Step 3: Install Drivers (One-Time Setup)

Your computer needs special software called "drivers" to talk to CyberPi.

### Windows Users

1. **Wait for automatic installation** - Windows usually installs drivers automatically
2. **Check Device Manager**:
   - Press `Windows + X` on keyboard
   - Click "Device Manager"
   - Look under "Ports (COM & LPT)"
   - You should see "USB Serial Device (COMx)" where x is a number
3. **If you don't see it**, install CH340 driver:
   - Download from: [makeblock.com/pages/mbot2-support](https://www.makeblock.com/pages/mbot2-support)
   - Look for "CyberPi CH340 Driver"
   - Run the installer
   - Restart your computer
   - Plug robot back in

### Mac Users

1. **Check System Information**:
   - Click Apple menu > "About This Mac"
   - Click "System Report"
   - Select "USB" on the left
   - Look for "CP2102 USB to UART Bridge" or "CH340"
2. **If you don't see it**, install CH340 driver:
   - Download from: [makeblock.com/pages/mbot2-support](https://www.makeblock.com/pages/mbot2-support)
   - Open the .dmg file
   - Run the installer
   - **Important:** Go to System Preferences > Security & Privacy
   - Click "Allow" next to the CH340 driver message
   - Restart Mac
   - Plug robot back in

### Linux Users

1. **Open Terminal** - Usually Ctrl+Alt+T
2. **Check if device appears**:
   ```bash
   lsusb
   ```
   Look for "QinHeng Electronics CH340" or similar
3. **Check serial port**:
   ```bash
   ls /dev/ttyUSB*
   ```
   You should see something like `/dev/ttyUSB0`
4. **Add yourself to dialout group** (one-time):
   ```bash
   sudo usermod -a -G dialout $USER
   ```
5. **Log out and log back in** for changes to take effect

> **🐧 Linux Note:** Most modern Linux distributions include the CH340 driver by default. If not, install package `brltty` and restart.

---

## Step 4: Test the Connection

### Using mBlock Software (Recommended for Beginners)

1. **Download mBlock**:
   - Go to [mblock.makeblock.com](https://mblock.makeblock.com)
   - Click "Download" and install for your operating system
2. **Open mBlock** and create an account (free)
3. **Connect your robot**:
   - Click the "Connect" button (plug icon) in top toolbar
   - Select "CyberPi" from the device list
   - Choose "Connect via USB"
   - Select your serial port (COM3, /dev/ttyUSB0, etc.)
4. **Success!** You should see:
   - Green "Connected" status in mBlock
   - CyberPi screen shows "Connected to mBlock"

### Using Command Line (Advanced)

If you want to test the connection without installing software:

**Windows:**
```bash
# Open PowerShell and check COM ports
mode
```

**Mac/Linux:**
```bash
# Check serial port exists
ls -l /dev/tty* | grep -i usb

# Test communication (replace ttyUSB0 with your port)
screen /dev/ttyUSB0 115200
```

Press Ctrl+A then K to exit screen.

---

## Step 5: Upload Your First Program

Now that you're connected, let's test it!

### Simple LED Test

1. **In mBlock**, create a new project
2. **Drag these blocks** into the coding area:
   ```
   [When space key pressed]
   [Set all led color to (Red)]
   [Wait 1 seconds]
   [Turn off all led]
   ```
3. **Click "Upload"** button (cloud with up arrow)
4. **Wait for upload** - You'll see a progress bar
5. **Test it!** - Press spacebar on your keyboard
6. **Success!** - CyberPi LEDs should turn red then off

---

## Troubleshooting Common Issues

### "Device Not Found" Error

**Problem:** Computer can't see CyberPi when you plug it in.

**Solutions:**
1. Try a different USB-C cable (charging cables won't work)
2. Try a different USB port on your laptop
3. Restart CyberPi: Hold power button 10 seconds until it turns off, then turn back on
4. Reinstall drivers (see Step 3 above)
5. Try a different laptop to rule out hardware issues

### "Permission Denied" Error (Linux)

**Problem:** You see "Permission denied: '/dev/ttyUSB0'"

**Solution:**
```bash
# Add yourself to dialout group
sudo usermod -a -G dialout $USER

# Then log out and back in, or run:
sudo chmod 666 /dev/ttyUSB0
```

### Upload Fails or Times Out

**Problem:** Upload starts but fails halfway, or times out.

**Solutions:**
1. **Don't touch CyberPi** during upload - keep hands off buttons
2. **Check battery level** - Low battery can cause upload failures
3. **Close other programs** that might be using the serial port
4. **Reset CyberPi**: Hold power 10 seconds, turn back on, try again
5. **Try slower baud rate** in mBlock settings: 57600 instead of 115200

### CyberPi Screen Freezes

**Problem:** Screen is frozen or unresponsive.

**Solution:**
1. **Force restart**: Hold power button for 10 seconds
2. Wait for screen to go black
3. Release button
4. Press power button normally to restart
5. Reconnect USB cable

### USB Keeps Disconnecting

**Problem:** Connection drops randomly.

**Solutions:**
1. **Check cable** - Replace with a higher-quality USB-C cable
2. **Disable USB power saving** (Windows):
   - Device Manager > Universal Serial Bus controllers
   - Right-click each "USB Root Hub"
   - Properties > Power Management
   - Uncheck "Allow computer to turn off device to save power"
3. **Check laptop power settings** - Ensure laptop isn't in power-saving mode
4. **Avoid using USB hub** - Connect directly to laptop

---

## Next Steps

Once you have a solid connection:

1. **Learn the Basics** - Try the built-in tutorials in mBlock
2. **Explore Sensors** - Test ultrasonic sensor, buttons, LEDs
3. **Try Python** - Switch from blocks to Python coding
4. **Upload RuVector** - Follow the "Downloading Apps" guide to install RuVector AI

---

## Getting Help

**Still stuck?** Here's where to get help:

- **Official Support:** [makeblock.com/pages/mbot2-support](https://www.makeblock.com/pages/mbot2-support)
- **Community Forum:** [forum.makeblock.com](https://forum.makeblock.com)
- **Video Tutorials:** Search "mBot2 CyberPi connection" on YouTube
- **GitHub Issues:** [github.com/Hulupeep/mbot-help/issues](https://github.com/Hulupeep/mbot-help/issues)

---

## Glossary

**Terms you might hear:**

- **CyberPi** - The blue computer brain on top of mBot2
- **USB-C** - The flat oval connector type (newer style)
- **USB-A** - The rectangular connector type (standard USB)
- **Serial Port** - The communication channel between computer and robot (COM3, ttyUSB0, etc.)
- **Driver** - Software that lets your computer talk to hardware devices
- **Baud Rate** - Communication speed (usually 115200 or 57600)
- **CH340** - The chip inside CyberPi that handles USB communication
- **mBlock** - Makeblock's visual programming software

---

**Next Guide:** [02-downloading-apps-to-cyberpi.md](./02-downloading-apps-to-cyberpi.md)
