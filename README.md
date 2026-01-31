# mBot2 RuVector - Help Documentation

**Beginner-Friendly Guides** | **Hardware Integration** | **Troubleshooting**

Complete documentation for setting up, programming, and extending your mBot2 robot with RuVector AI companion firmware.

---

## 📚 Documentation Guides

| Guide | Description | Difficulty |
|-------|-------------|------------|
| [01. Connecting Laptop to mBot2](./01-connecting-laptop-to-mbot.md) | USB connection, driver installation, first connection | Beginner |
| [02. Downloading Apps to CyberPi](./02-downloading-apps-to-cyberpi.md) | Upload programs using mBlock, Python, or command line | Beginner → Advanced |
| [03. Adding Peripherals](./03-adding-peripherals.md) | Connect displays, GPS, cameras, and audio modules | Intermediate → Advanced |
| [04. Troubleshooting Guide](./04-troubleshooting-guide.md) | Quick solutions to common problems | All Levels |

---

## 🚀 Quick Start Path

**New to mBot2?** Follow this sequence:

1. **[Connection Guide →](./01-connecting-laptop-to-mbot.md)**
   - Connect your laptop via USB-C
   - Install drivers (Windows/Mac/Linux)
   - Test with mBlock software
   - **Time:** 15-30 minutes

2. **[Download Guide →](./02-downloading-apps-to-cyberpi.md)**
   - Upload your first program
   - Learn different upload methods
   - Understand file types (.py, .mpy, .bin)
   - **Time:** 20-40 minutes

3. **[Peripherals Guide →](./03-adding-peripherals.md)** *(Optional)*
   - Add external devices (displays, GPS, camera)
   - Build advanced integrations
   - Voice-controlled robot example
   - **Time:** 1-4 hours depending on complexity

4. **[Troubleshooting →](./04-troubleshooting-guide.md)** *(As Needed)*
   - Quick diagnostic tests
   - Problem-specific solutions
   - Reference when issues arise

---

## 🎯 Who Is This For?

### Complete Beginners
- Never programmed a robot before
- Don't know one USB cable from another
- Want step-by-step instructions with pictures

**Start here:** [Guide 01 - Connecting](./01-connecting-laptop-to-mbot.md)

### Experienced Makers
- Comfortable with electronics
- Want to add peripherals (GPS, camera, displays)
- Looking for advanced integration examples

**Jump to:** [Guide 03 - Peripherals](./03-adding-peripherals.md)

### Developers
- Coming from software background
- Want to flash Rust firmware
- Need command-line tools

**See:** [Guide 02 - Method 4 (CLI)](./02-downloading-apps-to-cyberpi.md#method-4-using-command-line-advanced---rustc)

---

## 🔧 What You'll Learn

### Hardware Connection
- ✓ USB-C cable requirements (data vs charging)
- ✓ Driver installation (CH340)
- ✓ Serial port detection
- ✓ mBlock connection testing

### Programming Methods
- ✓ Visual block programming (mBlock)
- ✓ Python/MicroPython coding
- ✓ Rust firmware development
- ✓ Command-line flashing tools

### Peripheral Integration
- ✓ Freenove FNK0104 display (SPI, 3.3V)
- ✓ NEO-7M GPS module (UART, location tracking)
- ✓ ESP32-CAM (vision, WiFi streaming)
- ✓ Audio modules (speakers, MP3 playback)

### Advanced Topics
- ✓ Multi-device coordination
- ✓ Voice control with STT/TTS
- ✓ Claude AI integration
- ✓ Network topology design

---

## 🛠️ Required Hardware

### Minimum Setup (Guides 01-02)
- mBot2 robot with CyberPi brain
- USB-C cable (data-capable)
- Laptop/computer (Windows/Mac/Linux)
- Charged 18650 batteries (3x)

### Extended Setup (Guide 03)
- Freenove FNK0104 display *(optional)*
- NEO-7M GPS module *(optional)*
- ESP32-CAM module *(optional)*
- Speaker/audio module *(optional)*
- Raspberry Pi *(for advanced integration)*
- External 5V power supply *(for ESP32-CAM)*

---

## 📖 Documentation Features

### Beginner-Friendly
- **Plain Language** - No jargon without explanation
- **Step-by-Step** - Every action broken down
- **Visual Aids** - Wiring diagrams and connection photos
- **Glossary** - Terms explained when introduced

### Comprehensive
- **Multiple Methods** - Choose what works for you
- **Troubleshooting** - Solutions for common issues
- **Safety Guidelines** - Voltage warnings and best practices
- **Code Examples** - Working Python code included

### Tested
- **Real Hardware** - Tested on actual mBot2 robots
- **Multiple Platforms** - Windows, Mac, and Linux
- **Beginner Verified** - Written for complete newcomers

---

## 🚨 Safety First

### Power Safety
⚡ **Critical Warnings:**
- Freenove FNK0104 uses **3.3V** (NOT 5V - will damage!)
- ESP32-CAM needs **5V at 500mA** (external power required)
- NEO-7M GPS typically **3.3V-5V** (check your module!)
- Always verify voltage before connecting

### Connection Safety
🔌 **Best Practices:**
- Power off before wiring
- Use color-coded wires (Red=+, Black=-, Yellow/White=signals)
- Test with multimeter before connecting
- Secure connections with heat shrink or tape

See [Guide 03 - Safety Section](./03-adding-peripherals.md#safety-and-best-practices) for details.

---

## 🆘 Getting Help

### Quick Diagnostics
Run these three tests from [Guide 04](./04-troubleshooting-guide.md):
1. **LED Blink** - Verifies CyberPi is functional
2. **Serial Monitor** - Verifies USB and drivers
3. **Sensor Read** - Verifies sensors working

### Common Issues
- [Connection not detected →](./04-troubleshooting-guide.md#connection-issues)
- [Upload fails/timeouts →](./04-troubleshooting-guide.md#uploadflash-issues)
- [Motors don't move →](./04-troubleshooting-guide.md#hardware-issues)
- [GPS no fix →](./04-troubleshooting-guide.md#gps-issues)
- [ESP32-CAM brown-out →](./04-troubleshooting-guide.md#displaycamera-issues)

### Community Support
- **GitHub Issues:** [Report problems or ask questions](https://github.com/Hulupeep/mbot-help/issues)
- **RuVector Repo:** [Main firmware project](https://github.com/Hulupeep/mbot_ruvector)
- **Official Forum:** [Makeblock Community](https://forum.makeblock.com)

---

## 🔗 Related Projects

### RuVector Firmware
- **Repository:** [Hulupeep/mbot_ruvector](https://github.com/Hulupeep/mbot_ruvector)
- **Language:** Rust (no_std embedded)
- **Features:** Homeostasis, personality system, nervous system simulation
- **Apps:** ArtBot, GameBot, LEGOSorter, LearningLab, HelperBot

### Official Makeblock Resources
- **mBlock Software:** [mblock.makeblock.com](https://mblock.makeblock.com)
- **CyberPi Docs:** [makeblock.com/pages/cyberpi-support](https://www.makeblock.com/pages/cyberpi-support)
- **MicroPython API:** [docs.micropython.org](https://docs.micropython.org)

---

## 📝 Contributing

Found an error? Have suggestions? Want to add a peripheral guide?

1. **Report Issues:** [Create a GitHub issue](https://github.com/Hulupeep/mbot-help/issues/new)
2. **Propose Changes:** Submit a pull request
3. **Add Peripherals:** Share your integration guides

### Documentation Standards
- Beginner-friendly language
- Step-by-step instructions
- Code examples that work
- Safety warnings for voltage/power
- Tested on real hardware

---

## 📜 License

This documentation is part of the mBot RuVector open source project.

---

## 🎓 Learning Path Summary

```
START HERE
    ↓
[01. Connection] → Test USB connection
    ↓
[02. Download] → Upload first program
    ↓
[Try RuVector Apps] → ArtBot, GameBot, etc.
    ↓
[03. Peripherals] → Add sensors/displays (optional)
    ↓
[Advanced Integration] → Voice control, AI, multi-device
    ↓
[04. Troubleshoot] → Reference as needed
```

**Ready to get started?** → [Guide 01: Connecting Your Laptop](./01-connecting-laptop-to-mbot.md)

---

**Last Updated:** January 2026
**Documentation Version:** 1.0.0
**Compatible with:** mBot2 (CyberPi STM32F405)
