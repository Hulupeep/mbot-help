# Adding Peripherals to mBot2

**Beginner-Friendly Guide** | **Learn to Connect Extra Devices**

This guide shows you how to add extra sensors, displays, cameras, and other devices to your mBot2.

---

## Understanding Ports and Connections

Your mBot2 has several places to plug things in:

### CyberPi Ports (On the "Brain")
- **Port 1 & 2** - Yellow RJ11 connectors for Makeblock sensors
- **USB-C** - For computer connection and some USB devices
- **Grove Ports** - 4-pin connectors for Grove sensors
- **I2C** - For advanced sensors (shared bus)
- **SPI** - For high-speed devices like displays

### mBot2 Shield Ports (On the Robot Base)
- **M1 & M2** - Motor ports (already used by wheels)
- **Servo Ports** - For servos (pen, gripper, etc.)
- **Additional Sensor Ports** - Varies by shield model

> **💡 What's a Port?** Think of it like a power outlet - different devices need different types of "plugs" to connect.

---

## Device Guide by Type

### 1. Displays

#### **Freenove FNK0104 (LCD Display - Non-Touch)**

**What It Does:** Shows text, numbers, and simple graphics

**Specifications:**
- Size: 1.69" square display
- Resolution: 240x280 pixels
- Colors: 65K (RGB565)
- Interface: SPI
- Voltage: 3.3V

**How to Connect:**

1. **Identify the pins on FNK0104:**
   - VCC (Power)
   - GND (Ground)
   - SCK (Clock)
   - SDA (Data)
   - RS (Register Select)
   - RST (Reset)
   - CS (Chip Select)

2. **Wire to CyberPi Grove Port:**
   ```
   FNK0104        CyberPi Grove (Top Port)
   --------       ------------------
   VCC     ----->  Pin 1 (3.3V Red wire)
   GND     ----->  Pin 2 (GND Black wire)
   SCK     ----->  Pin 3 (SCL Yellow wire)
   SDA     ----->  Pin 4 (SDA White wire)
   ```

   **Additional connections (use spare pins):**
   ```
   RS      ----->  GPIO Pin 1
   RST     ----->  GPIO Pin 2
   CS      ----->  GPIO Pin 3
   ```

3. **Python Code Example:**
   ```python
   from cyberpi import *
   import spi

   # Initialize SPI for display
   spi.init(sck=16, mosi=17, miso=18)

   # FNK0104 initialization sequence
   # (See Freenove documentation for full init code)

   def display_text(text, x=0, y=0):
       """Show text on FNK0104 display"""
       # Send commands to display
       # (Implementation depends on FNK0104 library)
       pass

   # Example usage
   display_text("Hello from mBot2!", 10, 10)
   ```

4. **Common Issues:**
   - **Blank screen:** Check power connections (VCC/GND)
   - **Garbled output:** Verify SPI pins match code
   - **No response:** Ensure 3.3V (NOT 5V - will damage display!)

---

### 2. GPS Modules

#### **NEO-7M GPS Module**

**What It Does:** Tells your robot its exact location (latitude, longitude, altitude)

**Specifications:**
- Chipset: U-Blox NEO-7M
- Channels: 56
- Update Rate: 1-10Hz
- Accuracy: 2.5m
- Voltage: 3.3V - 5V
- Interface: UART (Serial)

**How to Connect:**

1. **Identify GPS module pins:**
   - VCC (3.3V-5V power)
   - GND (Ground)
   - TX (Transmit data)
   - RX (Receive data)
   - PPS (Pulse per second - optional)

2. **Wire to CyberPi:**
   ```
   NEO-7M         CyberPi
   ------         --------
   VCC     ----->  3.3V or 5V (Check module specs!)
   GND     ----->  GND
   TX      ----->  RX (Serial port - Grove pin 4)
   RX      ----->  TX (Serial port - Grove pin 3)
   ```

3. **Python Code Example:**
   ```python
   from cyberpi import *
   import time

   # Initialize UART for GPS
   uart.init(baudrate=9600)

   def parse_gps_data():
       """Read and parse GPS NMEA sentences"""
       data = uart.read()

       if data and b'$GPGGA' in data:
           # Parse GPGGA sentence (position data)
           parts = data.decode('utf-8').split(',')

           if len(parts) > 6:
               lat = parts[2]     # Latitude
               lat_dir = parts[3]  # N/S
               lon = parts[4]     # Longitude
               lon_dir = parts[5]  # E/W

               print(f"Location: {lat}{lat_dir}, {lon}{lon_dir}")
               return lat, lon
       return None, None

   # Main loop
   while True:
       lat, lon = parse_gps_data()
       if lat:
           led.on(0, 255, 0, "all")  # Green = GPS fix
       else:
           led.on(255, 0, 0, "all")  # Red = No fix
       time.sleep(1)
   ```

4. **Important GPS Tips:**
   - **Needs clear sky view** - Won't work indoors!
   - **Cold start = slow** - First fix can take 5-30 minutes
   - **Hot start = fast** - Subsequent fixes take <1 minute
   - **Check antenna connection** - Some modules have external antenna
   - **3.3V vs 5V** - Most NEO-7M modules work with both, but check your specific model

---

### 3. Cameras

#### **ESP32-CAM Module**

**What It Does:** Takes photos and streams video

**Specifications:**
- Resolution: Up to 2MP (1600x1200)
- Camera: OV2640
- WiFi: 802.11 b/g/n
- Interface: Serial or WiFi
- Voltage: 5V (Important!)
- Current: 160-260mA

**How to Connect:**

**Method 1: Direct Serial Connection (Simplest)**

1. **ESP32-CAM pins:**
   ```
   ESP32-CAM      CyberPi/Power
   ---------      --------------
   5V      ----->  5V source (NOT 3.3V!)
   GND     ----->  GND
   U0R (RX) ---->  TX (CyberPi serial)
   U0T (TX) ---->  RX (CyberPi serial)
   ```

2. **Power Requirements:**
   - ESP32-CAM needs **stable 5V at 500mA**
   - CyberPi can't provide enough power!
   - Solution: Use external 5V power bank or battery pack

3. **Basic Connection Diagram:**
   ```
   [5V USB Power Bank]
       |
       +---> ESP32-CAM (5V, GND)
       |
       +---> CyberPi (share GND only!)

   ESP32-CAM TX ---> CyberPi RX (data only)
   ESP32-CAM RX <--- CyberPi TX (data only)
   ```

**Method 2: WiFi Connection (More Flexible)**

1. **Program ESP32-CAM** for camera server:
   ```cpp
   // Arduino code for ESP32-CAM
   #include <WiFi.h>
   #include <esp_camera.h>

   const char* ssid = "mBot_Network";
   const char* password = "your_password";

   void setup() {
       // Configure camera
       camera_config_t config;
       config.pin_d0 = Y2_GPIO_NUM;
       config.pin_d1 = Y3_GPIO_NUM;
       // ... (see ESP32-CAM examples)

       esp_camera_init(&config);

       // Connect to WiFi
       WiFi.begin(ssid, password);

       // Start camera server on port 80
       startCameraServer();
   }
   ```

2. **Access from CyberPi:**
   ```python
   from cyberpi import *
   import urequests  # MicroPython requests library

   # ESP32-CAM's IP address on network
   cam_url = "http://192.168.4.1/capture"

   def capture_image():
       """Get image from ESP32-CAM"""
       response = urequests.get(cam_url)
       if response.status_code == 200:
           image_data = response.content
           # Process image data
           return image_data
       return None
   ```

**Common ESP32-CAM Issues:**
- **Brown-out reset:** Not enough power - use beefier 5V supply
- **No WiFi connection:** Check antenna is connected
- **Image quality poor:** Adjust camera settings (brightness, contrast)
- **Can't upload code:** Pull GPIO0 to GND during programming
- **Camera not detected:** Check ribbon cable is fully inserted

---

### 4. Audio

#### **Speaker Module**

**Types of Speakers:**
1. **Simple Buzzer** - Just tones, plugs into any GPIO
2. **PAM8403 Amplifier + Speaker** - Real audio playback
3. **DFPlayer Mini** - MP3 player with SD card

**PAM8403 + Speaker Setup (Best Quality):**

1. **Components needed:**
   - PAM8403 amplifier module (3W per channel)
   - 4Ω or 8Ω speaker
   - 5V power supply

2. **Connections:**
   ```
   CyberPi         PAM8403          Speaker
   -------         --------         -------
   Audio Out ----> L_IN/R_IN
   5V       -----> VCC
   GND      -----> GND
                   L_OUT ---------> Speaker +
                   GND   ---------> Speaker -
   ```

3. **Python Code:**
   ```python
   from cyberpi import *

   # Play tone through amplifier
   audio.play_tone(440, 1)  # A note, 1 second

   # Play melody
   audio.play_melody("c4:1 e4:1 g4:1 c5:2")

   # Play WAV file (if supported)
   audio.play_file("hello.wav")
   ```

**DFPlayer Mini Setup (MP3 Playback):**

1. **Connections:**
   ```
   DFPlayer       CyberPi
   --------       --------
   VCC     ----->  5V
   GND     ----->  GND
   TX      ----->  RX (Serial)
   RX      ----->  TX (Serial)
   SPK+    ----->  Speaker +
   SPK-    ----->  Speaker -
   ```

2. **Python Code:**
   ```python
   from cyberpi import *

   # Initialize serial for DFPlayer
   uart.init(baudrate=9600)

   def dfplayer_play(track_number):
       """Play MP3 file by number (001.mp3, 002.mp3, etc.)"""
       cmd = bytes([0x7E, 0xFF, 0x06, 0x03, 0x00, 0x00, track_number, 0xEF])
       uart.write(cmd)

   # Play first track
   dfplayer_play(1)
   ```

---

## Advanced: Multi-Device Integration

### Example Setup: Voice-Controlled Robot with GPS & Camera

**Hardware:**
- Raspberry Pi 4 (Ubuntu) - Main server
- iPhone - Mobile hotspot
- mBot2 with CyberPi
- ESP32-CAM
- NEO-7M GPS
- Freenove FNK0104 Display
- USB Microphone + Speaker

**Network Topology:**
```
[iPhone Hotspot]
    |
    +---> [Raspberry Pi] (192.168.4.2)
    |         |
    |         +---> Voice Server (Wyoming STT/TTS)
    |         +---> Claude Code Instance
    |
    +---> [ESP32-CAM] (192.168.4.10)
    |
    +---> [Freenove Display] (192.168.4.11)
    |
    +---> [mBot2/CyberPi] (Bluetooth to Pi)
```

**How It Works:**

1. **Raspberry Pi Setup:**
   ```bash
   # Install Wyoming for voice
   pip3 install wyoming

   # Install Claude Code
   npm install -g @anthropic-ai/claude-code

   # Start voice server
   python3 -m wyoming-faster-whisper \
     --model tiny-en \
     --port 10300

   # Start TTS
   python3 -m wyoming-piper \
     --voice en-us-lessac-medium \
     --port 10200
   ```

2. **iPhone as Hotspot:**
   - Settings > Personal Hotspot > Enable
   - Set strong password
   - Note WiFi name and password
   - Connect Pi, ESP32-CAM, Freenove to this network

3. **Button Press Workflow:**
   ```python
   # On CyberPi
   from cyberpi import *
   import urequests

   def on_button_a():
       """Record voice when button A pressed"""
       # Signal display
       display.show_text("Listening...")

       # Trigger voice recording on Pi
       response = urequests.post(
           "http://192.168.4.2:5000/voice",
           json={"action": "record"}
       )

       # Get GPS location
       lat, lon = get_gps_position()

       # Get camera image
       image = get_camera_image()

       # Send everything to Claude
       response = urequests.post(
           "http://192.168.4.2:5000/claude",
           json={
               "voice": response.json()["transcription"],
               "location": {"lat": lat, "lon": lon},
               "image": image
           }
       )

       # Play Claude's response
       tts_text = response.json()["response"]
       play_tts(tts_text)

   # Register button handler
   controller.register_button_callback(on_button_a, "a", "pressed")
   ```

4. **Claude Integration:**
   ```javascript
   // On Raspberry Pi
   const { exec } = require('child_process');
   const express = require('express');
   const app = express();

   app.post('/claude', async (req, res) => {
       const { voice, location, image } = req.body;

       // Prepare prompt with context
       const prompt = `
       User said: "${voice}"
       Current location: ${location.lat}, ${location.lon}
       [Image from camera attached]

       Please respond naturally to help the user.
       `;

       // Run Claude Code with prompt
       exec(`echo "${prompt}" | claude`, (error, stdout) => {
           res.json({ response: stdout });
       });
   });

   app.listen(5000);
   ```

**This setup enables:**
- ✓ Voice commands processed by local AI
- ✓ GPS location context for Claude
- ✓ Camera vision for Claude to "see"
- ✓ Text-to-speech responses
- ✓ All running locally (private!)

---

## Safety and Best Practices

### Power Safety
- ⚡ **Never exceed voltage ratings** - 5V devices get 5V, 3.3V get 3.3V
- ⚡ **Use proper power supply** - USB power banks are safest
- ⚡ **Check polarity** - Red=+, Black=-, swap = 💥
- ⚡ **Add fuses** for expensive modules

### Wiring Safety
- 🔌 **Use color-coded wires** - Red=power, Black=ground, other=signals
- 🔌 **Secure connections** - Use heat shrink or electrical tape
- 🔌 **Test with multimeter** - Verify voltage before connecting
- 🔌 **Unplug when wiring** - Always power off first!

### Module Safety
- 📦 **Read datasheets** - Know your module's specs
- 📦 **Start simple** - Test one module at a time
- 📦 **Use breadboards** - Prototype before soldering
- 📦 **Keep backups** - One wrong wire can fry a module

---

## Troubleshooting

### Device Not Responding
1. Check power (use multimeter)
2. Verify wiring matches diagram
3. Test with known-good code
4. Check for shorts (wires touching)

### Interference Issues
- Keep high-power wires away from signal wires
- Use shielded cables for long runs
- Add capacitors near power pins
- Use separate power supplies for noisy devices

### Communication Errors
- Verify baud rates match
- Check TX connects to RX (and vice versa)
- Add pull-up resistors for I2C
- Use logic level shifters if voltage mismatch

---

**Previous:** [02-downloading-apps-to-cyberpi.md](./02-downloading-apps-to-cyberpi.md)
**Next:** [04-troubleshooting-guide.md](./04-troubleshooting-guide.md)
