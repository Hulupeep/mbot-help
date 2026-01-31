---
layout: default
title: 4. Troubleshooting
nav_order: 5
description: "Quick solutions to common mBot2 problems"
---

# mBot2 Troubleshooting Guide
{: .no_toc }

**Quick Solutions to Common Problems**
{: .fs-6 .fw-300 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Connection Issues

### Problem: Computer can't see CyberPi
**Try these in order:**
1. Different USB-C cable (must support data!)
2. Different USB port on computer
3. Restart CyberPi (hold power 10 sec)
4. Reinstall drivers (see Guide 01)
5. Try different computer to isolate issue

### Problem: Connection drops randomly
- Use better quality USB cable
- Disable USB power saving (Windows Device Manager)
- Ensure laptop isn't in battery-saver mode
- Connect directly (not through USB hub)

---

## Upload/Flash Issues

### Problem: Upload times out
1. Don't touch CyberPi during upload
2. Check battery > 30%
3. Put in bootloader mode (hold BOOT, press RESET)
4. Close other programs using serial port
5. Try slower baud rate (57600 instead of 115200)

### Problem: Upload succeeds but program doesn't run
- Check auto-start enabled in settings
- Look for runtime errors in serial monitor
- Test with simple LED program first
- Verify main function is called

---

## Hardware Issues

### Problem: Motors don't move
- Check battery charge
- Verify motor cables fully inserted
- Test motors individually
- Check motor power switch on base

### Problem: Sensors give wrong readings
- Clean sensor lenses
- Check wiring connections
- Verify correct sensor port in code
- Test sensor with example program

### Problem: LEDs don't light up
- Check brightness setting (not set to 0)
- Test individual LEDs
- Verify power supply
- Check for software conflicts

---

## GPS Issues

### Problem: No GPS fix
- Go outside (won't work indoors!)
- Wait 5-30 minutes for first fix
- Check antenna connection
- Verify clear sky view
- Check UART baud rate (usually 9600)

### Problem: Inaccurate position
- Wait for more satellites (need 4+ for 3D fix)
- Avoid tall buildings/trees
- Check for interference
- Use external antenna if available

---

## Display/Camera Issues

### Problem: Display stays blank
- Check power (3.3V, NOT 5V!)
- Verify SPI wiring
- Run initialization sequence
- Test with known-good code

### Problem: ESP32-CAM brown-out
- Need stable 5V at 500mA+ (USB power bank)
- Can't power from CyberPi (insufficient current)
- Use capacitor near power pins
- Check antenna connected

---

## Voice/Audio Issues

### Problem: STT not working
- Check microphone connection
- Verify Wyoming server running
- Test with `arecord -l` (Linux)
- Check audio levels (not too quiet/loud)

### Problem: TTS stutters
- Reduce model size (use "tiny" model)
- Check Pi CPU usage
- Improve WiFi signal
- Use wired connection if possible

---

## Network Issues

### Problem: ESP32-CAM won't connect to WiFi
- Check SSID and password correct
- Ensure 2.4GHz network (not 5GHz!)
- Check antenna attached
- Reduce distance to router
- Check network security (WPA2 works best)

### Problem: Raspberry Pi connection drops
- Use Ethernet instead of WiFi if available
- Assign static IP addresses
- Check for WiFi interference
- Update Pi firmware: `sudo rpi-update`

---

## Quick Diagnostics

### Test 1: LED Blink
```python
from cyberpi import *
led.on(255, 0, 0, "all")  # Red
time.sleep(1)
led.off("all")
```
**If this works:** CyberPi is functional

### Test 2: Serial Monitor
```python
print("Hello from CyberPi!")
```
**If you see output:** USB and drivers working

### Test 3: Sensor Read
```python
distance = ultrasonic2.get_distance()
print("Distance:", distance)
```
**If you get numbers:** Sensors working

---

**Previous:** [03-adding-peripherals.md](./03-adding-peripherals.md)
