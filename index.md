---
layout: home
title: Home
nav_order: 1
description: "Beginner-friendly guides for setting up, programming, and extending your mBot2 robot with RuVector AI companion firmware"
permalink: /
has_children: false
---

# mBot2 RuVector Documentation
{: .fs-9 }

Complete beginner-friendly guides for your mBot2 robot
{: .fs-6 .fw-300 }

[Get Started](#quick-start){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View on GitHub](https://github.com/Hulupeep/mbot-help){: .btn .fs-5 .mb-4 .mb-md-0 }

---

{: .warning }
> **Safety First!** Always verify voltage requirements before connecting peripherals.
> - Freenove FNK0104: **3.3V only** (5V will damage!)
> - ESP32-CAM: **5V at 500mA** (needs external power)
> - NEO-7M GPS: Check your module (typically 3.3V-5V)

## Quick Start

New to mBot2? Follow this recommended path:

1. **[Connection Guide](01-connecting-laptop-to-mbot.md)** - Connect laptop via USB-C (15-30 min)
2. **[Download Guide](02-downloading-apps-to-cyberpi.md)** - Upload your first program (20-40 min)
3. **[Peripherals Guide](03-adding-peripherals.md)** - Add displays, GPS, camera *(optional)*
4. **[Troubleshooting](04-troubleshooting-guide.md)** - Quick fixes when needed

## What You'll Learn

<div class="code-example" markdown="1">

### Hardware Connection
{: .text-delta }

- USB-C cable requirements (data vs charging)
- CH340 driver installation
- Serial port detection
- Connection testing with mBlock

</div>

<div class="code-example" markdown="1">

### Programming Methods
{: .text-delta }

- Visual block programming (mBlock)
- Python/MicroPython coding
- Rust firmware development
- Command-line flashing tools

</div>

<div class="code-example" markdown="1">

### Peripheral Integration
{: .text-delta }

- Freenove FNK0104 display (SPI, 3.3V)
- NEO-7M GPS module (UART)
- ESP32-CAM (WiFi vision)
- Audio modules (speakers, MP3)

</div>

<div class="code-example" markdown="1">

### Advanced Topics
{: .text-delta }

- Multi-device coordination
- Voice control with STT/TTS
- Claude AI integration
- Network topology design

</div>

## Who Is This For?

### 🎓 Complete Beginners
Never programmed a robot before? Don't know one USB cable from another?

**Start here:** [Connection Guide](01-connecting-laptop-to-mbot.md)

### 🔧 Experienced Makers
Comfortable with electronics and want to add peripherals?

**Jump to:** [Peripherals Guide](03-adding-peripherals.md)

### 💻 Developers
Want to flash Rust firmware or use command-line tools?

**See:** [Download Guide - CLI Method](02-downloading-apps-to-cyberpi.md#method-4-using-command-line-advanced---rustc)

## Required Hardware

### Minimum Setup
- mBot2 robot with CyberPi brain
- USB-C cable (data-capable)
- Laptop (Windows/Mac/Linux)
- 3× 18650 batteries (charged)

### Extended Setup *(optional)*
- Freenove FNK0104 display
- NEO-7M GPS module
- ESP32-CAM module
- Speaker/audio module
- Raspberry Pi *(for advanced integration)*
- External 5V power supply *(for ESP32-CAM)*

## Quick Diagnostics

Having issues? Run these three tests from the [Troubleshooting Guide](04-troubleshooting-guide.md):

1. **LED Blink** - Verifies CyberPi functional
2. **Serial Monitor** - Verifies USB and drivers
3. **Sensor Read** - Verifies sensors working

## Documentation Features

{: .note }
This documentation is tested on real hardware and written for complete beginners.

- **Plain Language** - No jargon without explanation
- **Step-by-Step** - Every action broken down
- **Visual Aids** - Wiring diagrams included
- **Code Examples** - Working Python code
- **Multiple Methods** - Choose what works for you
- **Safety Guidelines** - Voltage warnings and best practices

## Related Projects

- **[RuVector Firmware](https://github.com/Hulupeep/mbot_ruvector)** - Rust-based AI companion firmware
- **[mBlock Software](https://mblock.makeblock.com)** - Visual programming environment
- **[CyberPi Official Docs](https://www.makeblock.com/pages/cyberpi-support)** - Makeblock resources

## Contributing

Found an error? Have suggestions? Want to add a peripheral guide?

- [Report Issues](https://github.com/Hulupeep/mbot-help/issues/new)
- Submit Pull Requests
- Share Integration Guides

---

**Ready to get started?** → [Connection Guide: Step 1](01-connecting-laptop-to-mbot.md)

---

{: .fs-3 }
*Last Updated: January 2026 • Documentation v1.0.0 • Compatible with mBot2 (CyberPi STM32F405)*
