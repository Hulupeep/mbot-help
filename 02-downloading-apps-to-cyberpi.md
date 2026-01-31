# Downloading Apps to CyberPi

**Beginner-Friendly Guide** | **Learn to Install Programs on Your Robot**

This guide shows you how to put programs (apps) onto your mBot2's CyberPi brain.

---

## Understanding Apps vs Programs

Think of CyberPi like a smartphone:
- **Apps** = Programs that make your robot do things
- **Downloading** = Copying the program from your computer to the robot
- **Flashing** = Installing the program so it runs when robot starts

---

## Method 1: Using mBlock (Easiest for Beginners)

### What You Need
- mBot2 connected to laptop via USB (see Guide 01)
- mBlock software installed
- An app or program you want to install

### Step-by-Step

**1. Open Your Program in mBlock**
- Launch mBlock software
- Click "File" > "Open" to load a saved project
- OR create a new program by dragging blocks

**2. Connect to Robot**
- Click the "Connect" button (plug icon)
- Choose "CyberPi" > "Connect via USB"
- Select your port (COM3, ttyUSB0, etc.)
- Wait for "Connected" status

**3. Upload the Program**
- Click the **"Upload"** button (cloud with up arrow)
- **NOT** the green flag (that just tests without saving)
- Watch the progress bar at bottom of screen
- Wait for "Upload successful" message

**4. Test the Program**
- The program starts running immediately
- Test it! Press buttons, move robot, etc.
- Program is now saved on CyberPi - it will run every time you power on

> **💡 Tip:** Programs uploaded to CyberPi stay there even after power off. To run a different program, upload a new one.

---

## Method 2: Using Python/MicroPython

For more advanced users who want to write Python code.

### Step-by-Step

**1. Switch mBlock to Python Mode**
- In mBlock, click "Python" tab at top
- You'll see the Python code editor

**2. Write or Paste Python Code**
```python
# Example: Blink LEDs
from cyberpi import *

while True:
    led.on(255, 0, 0, "all")  # Red
    time.sleep(1)
    led.off("all")
    time.sleep(1)
```

**3. Upload Python Code**
- Click "Upload" button
- Code is converted to bytecode and sent to CyberPi
- Program runs immediately and is saved

**4. Run Python REPL (Interactive Mode)**
- Click "Connect" > "Serial Monitor"
- Type Python commands directly
- See results in real-time
- Good for testing snippets before uploading

---

## Method 3: Using Makeblock Uploader (Official Tool)

### Download the Tool

1. Go to [makeblock.com/software](https://www.makeblock.com/software)
2. Download "Makeblock Uploader" for your OS
3. Install and launch the program

### Upload Process

**1. Prepare Your File**
- You need a **.mpy** or **.py** file
- This is the compiled program file
- Get it from:
  - Exporting from mBlock ("File" > "Export")
  - Building RuVector firmware (see Guide 03)
  - Downloading from community

**2. Connect Robot**
- Plug in USB cable
- Uploader should auto-detect CyberPi
- If not, manually select your port

**3. Select File to Upload**
- Click "Choose File" button
- Navigate to your .mpy or .py file
- Select it

**4. Start Upload**
- Click "Upload" button
- Progress bar shows upload status
- Wait for "Success!" message
- **Don't unplug** during upload!

**5. Test**
- Press reset button on CyberPi (small button next to USB)
- OR power cycle (turn off and on)
- Your program should run

---

## Method 4: Using Command Line (Advanced - Rust/C++)

For RuVector firmware and advanced development.

### Prerequisites

You need these tools installed:
```bash
# Rust toolchain
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustup target add thumbv7em-none-eabihf

# Probe-rs (for flashing)
cargo install probe-rs --features cli

# OR makeblock-upload tool
pip install makeblock-upload
```

### Build the Firmware

**For RuVector (Rust):**
```bash
cd /path/to/mbot_ruvector

# Build for mBot2 (CyberPi uses STM32F405)
cargo build --release --target thumbv7em-none-eabihf

# Binary is at: target/thumbv7em-none-eabihf/release/mbot-companion
```

### Flash to CyberPi

**Option A: Using probe-rs**
```bash
# Connect robot via USB

# Flash with probe-rs
probe-rs run --chip STM32F405RGT6 \
  target/thumbv7em-none-eabihf/release/mbot-companion

# Should see upload progress and "Success"
```

**Option B: Using makeblock-upload**
```bash
# Find your serial port
ls /dev/ttyUSB*  # Linux
ls /dev/cu.*     # Mac
# Look in Device Manager (Windows)

# Flash
makeblock-upload -p /dev/ttyUSB0 -b 115200 \
  target/thumbv7em-none-eabihf/release/mbot-companion.bin
```

**Option C: Using DFU mode (if USB isn't working)**
```bash
# Put CyberPi in DFU mode:
# 1. Hold BOOT button (next to USB port)
# 2. Press RESET button (while holding BOOT)
# 3. Release RESET, then release BOOT
# 4. CyberPi is now in DFU mode

# Flash with dfu-util
dfu-util -a 0 -s 0x08000000:leave -D mbot-companion.bin
```

---

## Troubleshooting Common Issues

### Upload Fails with "Timeout"

**Causes:**
- Robot is running a program that blocks serial communication
- Low battery
- Cable issue

**Solutions:**
1. Put CyberPi in **bootloader mode**:
   - Hold BOOT button
   - Press RESET button
   - Release both
   - Try upload again
2. Charge batteries to at least 50%
3. Try a different USB cable
4. Close other programs using the serial port

### "Out of Memory" Error

**Problem:** Program is too large for CyberPi.

**Solutions:**
- Remove debug code and comments
- Optimize your code (remove unused functions)
- For Rust: Ensure you're building with `--release` flag
- Check available memory: CyberPi has ~512KB flash

### Program Doesn't Run After Upload

**Problem:** Upload succeeds but nothing happens.

**Solutions:**
1. **Check auto-start is enabled** in CyberPi settings
2. **Look for runtime errors**:
   - Connect serial monitor in mBlock
   - Watch for error messages
3. **Verify the entry point**:
   - Python programs need `if __name__ == "__main__":`
   - Check your main function is called
4. **Test with a simple program first**:
   ```python
   from cyberpi import *
   led.on(0, 255, 0, "all")  # Green = working
   ```

### Upload Works but Program Crashes

**Problem:** Program starts but crashes/freezes.

**Solutions:**
1. **Check for infinite loops** without delays
2. **Add error handling**:
   ```python
   try:
       # Your code here
   except Exception as e:
       print("Error:", e)
       led.on(255, 0, 0, "all")  # Red = error
   ```
3. **Test sensors individually** before combining
4. **Monitor serial output** for crash messages

### Can't Find Serial Port

**Problem:** Computer doesn't show CyberPi port.

**Solutions:**
1. See Guide 01 - Driver installation
2. Try different USB port on laptop
3. Restart CyberPi
4. Check cable supports data (not charge-only)

---

## File Types Explained

### .py (Python Source)
- Human-readable Python code
- Can upload directly via mBlock or makeblock-upload
- Slower execution than compiled versions

### .mpy (MicroPython Bytecode)
- Compiled Python code
- Faster execution
- Smaller file size
- Can't be edited after compilation
- Created by mBlock when you click "Export"

### .bin (Binary/Firmware)
- Low-level machine code
- For Rust, C++, or other compiled languages
- Fastest execution
- Requires probe-rs or DFU tools
- This is what RuVector uses

### .elf (Executable and Linkable Format)
- Debug version with symbols
- Larger than .bin
- Used for debugging with probe-rs
- Can be converted to .bin

---

## Best Practices

### Before Uploading
1. ✓ Save your project
2. ✓ Test in simulator first (if using mBlock)
3. ✓ Check battery level (> 30%)
4. ✓ Close other programs using serial port
5. ✓ Backup previous program if important

### During Upload
1. ✓ Don't touch CyberPi buttons
2. ✓ Don't unplug USB cable
3. ✓ Don't close uploader software
4. ✓ Watch for errors in status messages
5. ✓ Wait for "Success" confirmation

### After Upload
1. ✓ Test thoroughly before disconnecting
2. ✓ Check serial monitor for errors
3. ✓ Test all features (buttons, sensors, motors)
4. ✓ Note any issues for debugging
5. ✓ Save a backup of working version

---

## Managing Multiple Programs

### Switching Between Programs

CyberPi can only run **one program at a time**. To switch:

1. Upload the new program (overwrites the old one)
2. OR use program slots (advanced):
   - Some apps support multiple "slots"
   - Switch between them using CyberPi menu
   - See CyberPi manual for details

### Backup Important Programs

**Method 1: Save Project Files**
- Keep .sb3 (mBlock) or .py files on your computer
- Organize in folders by project

**Method 2: Export Firmware**
- In mBlock: "File" > "Export" > Save .mpy file
- Label clearly: `mbot-game-v1.mpy`

**Method 3: Version Control** (Advanced)
- Use Git to track changes
- See RuVector GitHub for examples

---

## Next Steps

Now that you can upload programs:

1. **Try Example Programs** - mBlock has many built-in examples
2. **Modify Examples** - Change values and see what happens
3. **Create Your Own** - Start simple (blink LED, move forward)
4. **Try RuVector** - Follow Guide 03 for AI-powered mBot

---

## Resources

- **mBlock Tutorials:** [mblock.makeblock.com/en/learn](https://mblock.makeblock.com/en/learn)
- **MicroPython Docs:** [docs.micropython.org](https://docs.micropython.org)
- **CyberPi API Reference:** [makeblock.com/pages/cyberpi-support](https://www.makeblock.com/pages/cyberpi-support)
- **RuVector GitHub:** [github.com/Hulupeep/mbot_ruvector](https://github.com/Hulupeep/mbot_ruvector)

---

**Previous:** [01-connecting-laptop-to-mbot.md](./01-connecting-laptop-to-mbot.md)
**Next:** [03-adding-peripherals.md](./03-adding-peripherals.md)
