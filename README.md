
# 🎯 Auto-Turret: Open-Source Autonomous Object Tracking System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-4-red.svg)](https://www.raspberrypi.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.8-green.svg)](https://opencv.org/)

A fully open-source, high-tech autonomous turret system that detects and tracks moving objects in real-time using computer vision, machine learning, and precise servo control. Perfect for robotics enthusiasts, makers, students, and security applications.

## 📸 Project Preview

```

┌─────────────────────────────────────────────────────────┐
│                    AUTO-TURRET SYSTEM                    │
│                                                         │
│         ┌─────────────────────────────┐                 │
│         │    Camera Module            │                 │
│         │  (Object Detection)         │                 │
│         └──────────────┬──────────────┘                 │
│                        │                                │
│         ┌──────────────┴──────────────┐                 │
│         │    Pan-Tilt Mechanism       │                 │
│         │    (2x Servo Motors)        │                 │
│         └──────────────┬──────────────┘                 │
│                        │                                │
│         ┌──────────────┴──────────────┐                 │
│         │    Raspberry Pi 4           │                 │
│         │    (Brain & Control)        │                 │
│         └──────────────┬──────────────┘                 │
│                        │                                │
│         ┌──────────────┴──────────────┐                 │
│         │    Power Supply             │                 │
│         │    (5V/3A + 6V/3A)         │                 │
│         └─────────────────────────────┘                 │
└─────────────────────────────────────────────────────────┘

```

## ✨ Features

- **🎯 Real-time Object Detection**: Uses YOLOv8 for accurate person/object detection
- **🔍 Motion Detection**: Background subtraction for movement-based tracking
- **🤖 Autonomous Tracking**: PID-controlled smooth servo movements
- **📊 Multi-object Tracking**: Tracks multiple objects simultaneously with unique IDs
- **🎮 Dual Mode Operation**: Autonomous and manual control modes
- **📱 Remote Monitoring**: Web-based dashboard for live viewing
- **🔔 Alert System**: Telegram bot integration for notifications
- **📹 Video Recording**: Automatic recording of detection events
- **🔧 Highly Configurable**: YAML-based configuration with hot-reload
- **🖥️ Cross-platform**: Works on Raspberry Pi, Linux, Windows, and macOS

## 📋 Table of Contents

- [Hardware Requirements](#hardware-requirements)
- [Shopping List](#shopping-list)
- [Hardware Assembly Guide](#hardware-assembly-guide)
- [Wiring Diagram](#wiring-diagram)
- [Software Installation](#software-installation)
- [Configuration Guide](#configuration-guide)
- [Running the System](#running-the-system)
- [Calibration Guide](#calibration-guide)
- [Troubleshooting](#troubleshooting)
- [Advanced Features](#advanced-features)
- [Contributing](#contributing)

## 🔧 Hardware Requirements

### Essential Components

#### 1. **Main Controller: Raspberry Pi 4 Model B**
- **Specifications**: 4GB or 8GB RAM recommended
- **Purpose**: Main processing unit for computer vision and control
- **Alternative**: Any Linux-based single-board computer or PC with USB ports
- **Required Accessories**:
  - MicroSD Card (32GB+, Class 10, A2 rated)
  - 5V/3A USB-C Power Supply (Official Raspberry Pi power supply recommended)
  - Heatsink and cooling fan (essential for continuous operation)
  - Micro HDMI to HDMI cable (for initial setup)

#### 2. **Camera Module**
- **Primary Option**: Raspberry Pi Camera Module 3 (12MP, Autofocus)
  - Better integration, uses CSI ribbon cable
  - Field of View: 75° (standard) or 120° (wide-angle version)
- **Alternative**: USB Webcam (Logitech C270/C920/C922)
  - Easier setup, plug-and-play
  - Minimum 720p resolution, 30fps recommended
- **Features needed**: 
  - Auto-focus capability
  - Good low-light performance
  - Wide field of view preferred

#### 3. **Servo Motors (2x)**
- **Recommended**: MG996R Metal Gear Servo
  - Torque: 10 kg·cm at 4.8V, 11 kg·cm at 6V
  - Speed: 0.20 sec/60° at 4.8V, 0.17 sec/60° at 6V
  - Rotation: 180° (modified for continuous rotation if needed)
  - Metal gears for durability
- **Alternative**: MG995, DS3225, or any standard-sized servo
- **Requirements**:
  - Metal gears (plastic gears wear out quickly)
  - Minimum 180° rotation range
  - Torque > 5 kg·cm for stable camera mounting

#### 4. **Pan-Tilt Bracket Assembly**
- **Option A: Ready-made Kit**
  - Pan-Tilt servo bracket kit (available on Amazon/eBay)
  - Usually includes mounting hardware
  - Price: $10-15
- **Option B: 3D Printed** (STL files provided in `/hardware/3d_models/`)
  - Pan bracket base
  - Tilt camera mount
  - Servo horn adapters
  - Camera mounting plate

#### 5. **Power Supply**
- **For Raspberry Pi**: 5V/3A USB-C power adapter
- **For Servos**: 5-6V/3A+ DC power supply
  - Option 1: Separate 6V/3A wall adapter
  - Option 2: 7.4V LiPo battery with UBEC (for portable use)
  - Option 3: 12V battery with step-down converter
- **IMPORTANT**: Never power servos directly from Raspberry Pi 5V pin

#### 6. **Electronic Components**
- **Wiring & Connectors**:
  - Male-to-Female jumper wires (20 pieces)
  - Male-to-Male jumper wires (10 pieces)
  - Female-to-Female jumper wires (10 pieces)
  - Breadboard (830 points) or prototyping board
  
- **Voltage Regulation**:
  - LM2596 DC-DC Step Down Converter (if using >6V power)
  - Capacitors: 1000µF/16V (2x, for servo power stabilization)
  - Diode: 1N4007 (for reverse polarity protection)

- **Optional Components**:
  - I2C PWM Driver: PCA9685 16-Channel Servo Driver
    - Allows precise control of up to 16 servos
    - Reduces GPIO pin usage
    - Better PWM signal quality
  - LED indicators (3x: Power, Tracking, Alert)
  - Buzzer for audio alerts
  - OLED Display (128x64) for status display

## 🛒 Shopping List

| Item | Quantity | Estimated Cost | Where to Buy |
|------|----------|----------------|--------------|
| Raspberry Pi 4 (4GB) | 1 | $55-75 | Amazon, Adafruit, PiShop |
| MicroSD Card (32GB) | 1 | $8-12 | Amazon, Best Buy |
| Pi Camera Module 3 | 1 | $25 | Amazon, Adafruit |
| MG996R Servo Motors | 2 | $10-15 each | Amazon, eBay |
| Pan-Tilt Bracket Kit | 1 | $10-15 | Amazon, AliExpress |
| 5V/3A USB-C Power Supply | 1 | $10 | Amazon |
| 6V/3A DC Power Adapter | 1 | $8-12 | Amazon |
| Jumper Wire Kit | 1 | $5-8 | Amazon |
| Breadboard | 1 | $5 | Amazon |
| Capacitor Kit | 1 | $5 | Amazon |
| PCA9685 Servo Driver | 1 | $8-12 | Amazon, Adafruit |
| Heatsink Set | 1 | $5 | Amazon |
| **Total Estimated Cost** | | **$150-200** | |

## 🔨 Hardware Assembly Guide

### Step 1: Raspberry Pi Setup

1. **Install Operating System**
   ```bash
   # Download Raspberry Pi Imager from raspberrypi.org
   # Insert microSD card into computer
   # Open Raspberry Pi Imager
   
   # Select:
   # - Operating System: Raspberry Pi OS (64-bit) with desktop
   # - Storage: Your microSD card
   
   # Click gear icon (Advanced options):
   # - Enable SSH
   # - Set username and password
   # - Configure WiFi (if using wireless)
   # - Set locale settings
   
   # Click Write and wait for completion
```

2. Initial Pi Configuration
   ```bash
   # Insert microSD into Pi, connect keyboard/mouse/display
   # Or connect via SSH (if configured)
   
   # Update system
   sudo apt update && sudo apt upgrade -y
   
   # Enable camera interface
   sudo raspi-config
   # Navigate to: Interface Options → Camera → Enable
   # Also enable: Interface Options → I2C (for PCA9685)
   # Finish and reboot
   
   # Install essential packages
   sudo apt install -y python3-pip python3-venv git cmake
   sudo apt install -y libopencv-dev python3-opencv
   sudo apt install -y libatlas-base-dev libhdf5-dev libhdf5-serial-dev
   sudo apt install -y libjasper-dev libqtgui4 libqt4-test
   ```
3. Attach Camera
   For Raspberry Pi Camera Module:
   ```
   1. Power OFF the Raspberry Pi completely
   2. Locate the CSI connector (near Ethernet port on Pi 4)
   3. Gently pull up the black tabs on the connector
   4. Insert the ribbon cable with blue side facing Ethernet port
   5. Push the black tabs down to secure the cable
   6. Test camera: raspistill -o test.jpg
   ```
   For USB Webcam:
   ```
   1. Simply plug into any USB port
   2. Test: ls /dev/video* (should show /dev/video0)
   3. Verify: fswebcam test.jpg
   ```

Step 2: Pan-Tilt Assembly

A. 3D Printed Version (Recommended)

1. Download and Print Parts
   ```bash
   # Clone repository and find STL files
   git clone https://github.com/yourusername/auto-turret.git
   cd auto-turret/hardware/3d_models/
   
   # Files to print:
   # - base_plate.stl (turret base)
   # - pan_arm.stl (horizontal rotation arm)
   # - tilt_bracket.stl (vertical tilt mount)
   # - camera_holder.stl (camera mounting plate)
   # - servo_adapters.stl (servo horn adapters)
   ```
2. Print Settings
   ```
   Material: PLA or PETG
   Layer Height: 0.2mm
   Infill: 20-30%
   Supports: Yes (for overhangs)
   Brim: Yes (for bed adhesion)
   Print Time: ~4-6 hours for all parts
   ```
3. Assembly Steps
   Pan Servo Installation:
   ```
   1. Attach servo horn to pan servo using provided screw
   2. Insert pan servo into base_plate from bottom
   3. Secure with M3 screws (4x)
   4. Attach pan_arm to servo horn
   5. Ensure smooth rotation without binding
   ```
   Tilt Servo Installation:
   ```
   1. Mount tilt servo to pan_arm using M3 screws
   2. Attach tilt_bracket to servo horn
   3. Mount camera_holder tttiltbracket
   4. Adjust tension screw for smooth movement
   ```
   Camera Mounting:
   ```
   1. Attach camera module to camera_holder
   2. Use hot glue or double-sided tape for security
   3. Route ribbon cable carefully (for Pi Camera)
   4. Ensure cable doesn't restrict movement
   ```

B. Commercial Pan-Tilt Kit Assembly

```
1. Unpack kit and identify all parts
2. Mount pan servo to bottom bracket
3. Attach L-bracket to pan servo horn
4. Mount tilt servo to L-bracket
5. Attach camera mount to tilt servo
6. Secure all screws tightly
```

Step 3: Electronic Connections

Wiring Diagram

```
                    ┌─────────────────────────────────┐
                    │       RASPBERRY PI 4            │
                    │                                 │
       ┌───────────┤ Pin 2 (5V)              GND ├───────────┐
       │           │ Pin 6 (GND)             3.3V │           │
       │           │                                 │           │
       │           │ GPIO12 (PWM0)   ────────────────┼────┐      │
       │           │ GPIO13 (PWM1)   ────────────────┼──┐ │      │
       │           │ SDA (GPIO2)    ───────────────┐ │  │ │      │
       │           │ SCL (GPIO3)    ─────────────┐ │ │  │ │      │
       │           └─────────────────────────────────┘ │ │  │ │      │
       │                                              │ │  │ │      │
       │    ┌───────────────────────┐                  │ │  │ │      │
       │    │   PCA9685 SERVO DRIVER│◄─────────────────┘ │  │ │      │
       │    │                       │                    │  │ │      │
       │    │  V+ (6V)    GND       │                    │  │ │      │
       │    │  PWM0  PWM1           │                    │  │ │      │
       │    │   │      │            │                    │  │ │      │
       │    └───┼──────┼────────────┘                    │  │ │      │
       │        │      │                                 │  │ │      │
       │        │      └──────────────────┐              │  │ │      │
       │        │                         │              │  │ │      │
       │        └─────────────┐           │              │  │ │      │
       │                      │           │              │  │ │      │
       │    ┌─────────────────┼───────────┼──────────────┼──┼─┘      │
       │    │  PAN SERVO      │  TILT SERVO             │  │        │
       │    │  Orange (PWM)◄──┘  Orange (PWM)◄──────────┘  │        │
       │    │  Red (V+)────────────Red (V+)───────────────┐│        │
       │    │  Brown (GND)─────────Brown (GND)────────────┤│        │
       │    └─────────────────────────────────────────────┘│        │
       │                                                  │        │
       │    ┌─────────────────────────────────────────────┘        │
       │    │                                                      │
       │    │    ┌──────────────────────────┐                      │
       │    │    │  6V POWER SUPPLY        │                      │
       │    └────┤  + (Red)    - (Black)  │                      │
       │         │  To Servo Power Bus    │                      │
       │         └──────────────────────────┘                      │
       │                                                           │
       │         ┌──────────────────────────┐                      │
       │         │  5V POWER SUPPLY        │                      │
       └─────────┤  USB-C to Raspberry Pi  │                      │
                 └──────────────────────────┘                      │
```

Method A: Direct GPIO Connection (Simple Setup)

```python
# Connections:
# Pan Servo:
#   - Signal (Orange/Yellow) → GPIO18 (Pin 12)
#   - Power (Red) → External 6V supply
#   - Ground (Brown/Black) → Common Ground

# Tilt Servo:
#   - Signal (Orange/Yellow) → GPIO19 (Pin 35)
#   - Power (Red) → External 6V supply
#   - Ground (Brown/Black) → Common Ground

# Important: Connect all grounds together!
# Raspberry Pi GND ↔ Servo Power Supply GND
```

Connection Steps:

```
1. Set up breadboard with power rails
2. Connect 6V power supply to breadboard power rails
3. Add 1000µF capacitor across power rails (observe polarity!)
4. Connect pan servo signal to GPIO18 (Pin 12)
5. Connect tilt servo signal to GPIO19 (Pin 35)
6. Connect both servo power (red) to 6V rail
7. Connect both servo ground (brown) to GND rail
8. Connect Raspberry Pi GND to breadboard GND rail
9. Double-check all connections before powering on
```

Method B: PCA9685 Servo Driver (Professional Setup)

```python
# I2C Connections:
# PCA9685 VCC → Raspberry Pi 3.3V (Pin 1)
# PCA9685 GND → Raspberry Pi GND (Pin 6)
# PCA9685 SDA → Raspberry Pi SDA (GPIO2, Pin 3)
# PCA9685 SCL → Raspberry Pi SCL (GPIO3, Pin 5)

# Servo Connections to PCA9685:
# Pan Servo → Channel 0
# Tilt Servo → Channel 1

# Power:
# PCA9685 V+ → 6V Power Supply (+)
# PCA9685 GND → 6V Power Supply (-)
# Servo Power → 6V terminal block on PCA9685
```

Connection Steps:

```
1. Enable I2C on Raspberry Pi (sudo raspi-config)
2. Connect PCA9685 to Pi using I2C pins
3. Test I2C connection: sudo i2cdetect -y 1
   (Should see device at address 0x40)
4. Connect 6V power to PCA9685 terminal block
5. Connect servos to PCA9685 channels 0 and 1
6. Install library: pip3 install adafruit-circuitpython-servokit
```

Step 4: Final Assembly

1. Mount Everything on Base
   ```
   ┌─────────────────────────────────────┐
   │                                     │
   │   [Camera]                          │
   │      \                              │
   │       \ (Tilt Servo)                │
   │        \                            │
   │    [Pan Servo]                      │
   │         \                           │
   │          \                          │
   │    [Raspberry Pi]                   │
   │    [Breadboard]                     │
   │    [Power Supply]                   │
   │                                     │
   └─────────────────────────────────────┘
   ```
2. Cable Management
   · Use zip ties to bundle wires
   · Leave slack for pan-tilt movement
   · Label all connections
   · Route power cables away from signal wires
   · Apply hot glue to secure connectors
3. Testing Each Component
   ```bash
   # Test camera
   raspistill -o /tmp/test.jpg
   # or for USB camera
   fswebcam /tmp/test.jpg
   
   # Test servos (create test script)
   python3 test_servos.py
   
   # Test I2C communication (if using PCA9685)
   sudo i2cdetect -y 1
   ```

💻 Software Installation

Method 1: Automatic Installation (Recommended)

```bash
# Clone the repository
git clone https://github.com/yourusername/auto-turret.git
cd auto-turret

# Run the setup script
chmod +x install.sh
sudo ./install.sh

# The script will:
# 1. Create Python virtual environment
# 2. Install all dependencies
# 3. Set up systemd service (optional)
# 4. Configure autostart (optional)
```

Method 2: Manual Installation

```bash
# 1. Clone repository
git clone https://github.com/yourusername/auto-turret.git
cd auto-turret

# 2. Create virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install --upgrade pip setuptools wheel
pip install -r requirements.txt

# 4. Install OpenCV with optimization (Raspberry Pi)
# This takes 1-2 hours but provides better performance
pip install opencv-python-headless==4.8.1.78

# Or use pre-compiled version (faster)
sudo apt install python3-opencv

# 5. Install YOLO dependencies
pip install ultralytics==8.0.200

# 6. Verify installation
python3 -c "import cv2; print('OpenCV version:', cv2.__version__)"
python3 -c "from ultralytics import YOLO; print('YOLO ready')"

# 7. Download initial YOLO model
python3 -c "from ultralytics import YOLO; YOLO('yolov8n.pt')"
```

Docker Installation (Alternative)

```bash
# Build Docker image
docker build -t auto-turret .

# Run with camera access
docker run -it --rm \
  --device=/dev/video0:/dev/video0 \
  --privileged \
  -v $(pwd)/config:/app/config \
  auto-turret
```

⚙️ Configuration Guide

Basic Configuration

Edit config/settings.yaml to customize your setup:

```yaml
# Camera Configuration
camera:
  # For USB webcam
  index: 0
  
  # For Raspberry Pi camera (using libcamera)
  # index: 0
  # backend: libcamera
  
  resolution: [640, 480]  # Lower for better performance
  fps: 30                 # Target FPS
  
# Detection Settings
detection:
  model: yolov8n          # Options: yolov8n, yolov8s, yolov8m
  confidence: 0.5         # Higher = less false positives
  target_classes: [0]     # 0=person, See COCO classes list
  
# Servo Configuration
servos:
  pan_pin: 18            # GPIO pin for pan servo
  tilt_pin: 19           # GPIO pin for tilt servo
  pan_min: 0             # Physical minimum angle
  pan_max: 180           # Physical maximum angle
  pan_center: 90         # Home position
  tilt_min: 45           # Prevent camera hitting base
  tilt_max: 135          # Prevent camera flipping
  tilt_center: 90
  max_step: 5            # Limit movement per frame
  smoothing: 0.7         # Movement smoothing (0-1)
```

Advanced Configuration

```yaml
# PID Tuning Parameters
pid:
  pan:
    kp: 0.15             # Proportional gain
    ki: 0.02             # Integral gain
    kd: 0.08             # Derivative gain
  tilt:
    kp: 0.12
    ki: 0.015
    kd: 0.06

# Multi-camera Setup
cameras:
  - id: 0
    type: usb
    resolution: [640, 480]
    fps: 30
  - id: 1
    type: pi_camera
    resolution: [1280, 720]
    fps: 15

# Alert Configuration
alerts:
  telegram:
    enabled: false
    bot_token: "YOUR_BOT_TOKEN"
    chat_id: "YOUR_CHAT_ID"
  email:
    enabled: false
    smtp_server: "smtp.gmail.com"
    smtp_port: 587
    from_email: "your.email@gmail.com"
    to_email: "alert.email@gmail.com"
    
# Recording Settings
recording:
  enabled: true
  format: mp4
  codec: h264
  fps: 15
  max_duration: 300  # seconds
  
# Network Streaming
streaming:
  enabled: false
  port: 8080
  quality: 75
```

Performance Optimization

For Raspberry Pi 4:

```yaml
# Optimize for Raspberry Pi
camera:
  resolution: [320, 240]  # Reduce resolution
  fps: 15                 # Lower FPS
  
detection:
  model: yolov8n          # Use smallest model
  confidence: 0.6         # Higher threshold
  skip_frames: 2          # Process every 3rd frame
  
# Enable hardware acceleration
hardware:
  use_tensorflow_lite: true  # Use TFLite for inference
  use_opencv_dnn: true       # Use OpenCV DNN backend
```

🚀 Running the System

First Run

```bash
# Navigate to project directory
cd auto-turret

# Activate virtual environment (if using)
source venv/bin/activate

# Run in test mode (no servo movement)
python3 src/main.py --test-mode

# Run normally
python3 src/main.py

# Run headless (no display output)
python3 src/main.py --headless

# Run with custom config
python3 src/main.py --config /path/to/custom_config.yaml
```

Operation Modes

```bash
# Autonomous tracking mode
python3 src/main.py --mode auto

# Manual control mode
python3 src/main.py --mode manual
# Controls: Arrow keys for pan/tilt, Space for center, Q to quit

# Hybrid mode (manual override available)
python3 src/main.py --mode hybrid

# Demo mode (simulated detection)
python3 src/main.py --demo
```

Keyboard Controls

```
During operation:
  'q' or ESC  - Quit program
  'c'         - Center turret
  'm'         - Toggle auto/manual mode
  't'         - Toggle tracking mode
  's'         - Take screenshot
  'r'         - Start/stop recording
  'p'         - Pause/resume detection
  '+'/'-'     - Increase/decrease confidence threshold
  '1' - '5'   - Switch tracking target priority
```

Startup on Boot (Raspberry Pi)

```bash
# Create systemd service
sudo nano /etc/systemd/system/auto-turret.service

# Add the following content:
```

```ini
[Unit]
Description=Auto-Turret Service
After=network.target

[Service]
Type=simple
User=pi
WorkingDirectory=/home/pi/auto-turret
Environment="DISPLAY=:0"
Environment="XAUTHORITY=/home/pi/.Xauthority"
ExecStart=/home/pi/auto-turret/venv/bin/python3 /home/pi/auto-turret/src/main.py
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
# Enable and start service
sudo systemctl enable auto-turret.service
sudo systemctl start auto-turret.service

# Check status
sudo systemctl status auto-turret.service

# View logs
journalctl -u auto-turret.service -f
```

🎯 Calibration Guide

1. Camera Calibration

```bash
# Run camera calibration tool
python3 tools/calibrate_camera.py

# This will:
# 1. Open camera preview
# 2. Show servo test patterns
# 3. Map camera FOV to servo angles
# 4. Save calibration data to config
```

2. Servo Range Calibration

```bash
# Test servo range
python3 tools/servo_calibrator.py

# Follow on-screen instructions:
# 1. Find minimum safe angle
# 2. Find maximum safe angle
# 3. Set center position
# 4. Test movement range
# 5. Save servo limits
```

3. PID Tuning

```bash
# Run PID tuner
python3 tools/pid_tuner.py

# This tool helps you find optimal PID values
# by showing real-time response graphs
```

Manual PID Tuning Steps:

```
1. Start with Kp=0.1, Ki=0, Kd=0
2. Increase Kp until slight oscillation
3. Add Ki to eliminate steady-state error
4. Add Kd to reduce overshoot
5. Fine-tune all values

Signs to look for:
- Overshooting: Decrease Kp or increase Kd
- Slow response: Increase Kp
- Oscillation: Decrease Kp, increase Kd
- Drift: Increase Ki
```

4. Object Detection Threshold Calibration

```bash
# Test different confidence thresholds
python3 tools/detection_tuner.py

# Shows live preview with adjustable threshold
# Helps find optimal balance between:
# - False positives (too low threshold)
# - Missed detections (too high threshold)
```

🔧 Troubleshooting

Common Issues and Solutions

Camera Issues

```bash
# Problem: "No camera found"
# Solution 1: Check camera connection
ls /dev/video*

# Solution 2: Add user to video group
sudo usermod -a -G video $USER

# Solution 3: Test with different backend
python3 -c "import cv2; cap = cv2.VideoCapture(0, cv2.CAP_V4L2); print(cap.isOpened())"

# Solution 4: For Pi Camera, enable legacy camera
sudo raspi-config
# Interface Options → Legacy Camera → Enable

# Problem: Low FPS
# Solution: Reduce resolution and frame rate
# Edit config: resolution: [320, 240], fps: 15
```

Servo Issues

```bash
# Problem: Servo not moving
# Solution 1: Test with simple script
python3 tools/test_servo.py

# Solution 2: Check power supply
# Measure voltage at servo (should be 5-6V)
# Add capacitor across power lines (1000µF)

# Solution 3: Check GPIO permissions
sudo chmod 666 /dev/gpiomem

# Problem: Servo jittering
# Solution 1: Use PCA9685 for better PWM
# Solution 2: Add capacitor (100µF) to servo power
# Solution 3: Reduce PWM frequency

# Problem: Servo overheating
# Solution: Check voltage (should be 6V max for MG996R)
# Solution: Reduce holding torque with servo.detach()
```

Detection Issues

```bash
# Problem: No objects detected
# Solution 1: Lower confidence threshold
# Edit config: confidence: 0.3

# Solution 2: Check lighting conditions
# Ensure adequate lighting (100+ lux)

# Solution 3: Try different model
# Edit config: model: yolov8m (more accurate)

# Problem: Too many false detections
# Solution 1: Increase confidence threshold
# Edit config: confidence: 0.7

# Solution 2: Add motion filtering
# Edit config: motion_filter: true

# Problem: Slow detection speed
# Solution 1: Use smaller model (yolov8n)
# Solution 2: Reduce input resolution
# Solution 3: Use TFLite model
```

Network Issues

```bash
# Problem: Can't access web interface
# Solution 1: Check if streaming is enabled
# Edit config: streaming.enabled: true

# Solution 2: Check firewall
sudo ufw allow 8080

# Solution 3: Find Pi's IP address
hostname -I

# Problem: Stream lagging
# Solution 1: Reduce stream quality
# Edit config: streaming.quality: 50

# Solution 2: Use wired connection
# WiFi can cause latency
```

Diagnostic Commands

```bash
# Run full system diagnostic
python3 tools/diagnostic.py

# Check component status
python3 tools/system_check.py

# Monitor system resources
htop  # CPU and RAM usage
vcgencmd measure_temp  # Pi temperature
sudo i2cdetect -y 1    # I2C devices

# Test all hardware
python3 tests/hardware_test.py

# Generate debug report
python3 tools/debug_report.py --output debug_report.zip
```

🚀 Advanced Features

1. Remote Web Dashboard

```bash
# Start web server
python3 web/server.py

# Access dashboard:
# http://raspberrypi.local:5000
# or http://[IP_ADDRESS]:5000

# Features:
# - Live camera feed
# - Detection overlay
# - Manual control interface
# - Settings adjustment
# - Recording management
```

2. Telegram Bot Integration

```yaml
# Add to config/settings.yaml
telegram:
  enabled: true
  bot_token: "123456789:ABCdefGHIjklMNOpqrsTUVwxyz"
  admin_ids: [123456789]  # Your Telegram user ID
  alerts:
    on_detection: true
    on_motion: true
    snapshot: true
  commands:
    enabled: true
    start: true
    stop: true
    status: true
    photo: true
```

Available Bot Commands:

```
/start    - Start tracking
/stop     - Stop tracking
/status   - Get system status
/photo    - Take snapshot
/position - Get current position
/mode     - Change operation mode
/config   - View/change settings
/help     - Show all commands
```

3. Multi-Camera Setup

```yaml
# Configure multiple cameras
cameras:
  primary:
    type: pi_camera
    resolution: [640, 480]
    fps: 30
    purpose: detection
  
  secondary:
    type: usb
    device: /dev/video2
    resolution: [1280, 720]
    fps: 15
    purpose: recording
```

4. Custom Object Detection Training

```bash
# Train custom model on your objects
python3 tools/train_custom_model.py \
  --dataset ./datasets/custom/ \
  --model yolov8n \
  --epochs 100 \
  --batch 16 \
  --imgsz 640

# Use custom model
# Edit config: model: ./models/custom_yolo.pt
```

📚 API Documentation

Python API Usage

```python
from auto_turret import TurretSystem

# Initialize system
turret = TurretSystem(config_path='config/settings.yaml')

# Start tracking
turret.start()

# Get current status
status = turret.get_status()
print(f"Tracking: {status['tracking']}")
print(f"Targets: {status['num_targets']}")

# Manual control
turret.move_to(pan=90, tilt=45)

# Take snapshot
turret.capture_snapshot('detection.jpg')

# Stop system
turret.stop()
```

REST API Endpoints

```python
# Available when web server is running
GET  /api/status          # System status
GET  /api/position        # Current position
POST /api/move            # Move to position
POST /api/mode            # Change mode
GET  /api/snapshot        # Take snapshot
GET  /api/stream          # Video stream (MJPEG)
GET  /api/detections      # Current detections
POST /api/calibrate       # Start calibration
```

🤝 Contributing

We welcome contributions! See CONTRIBUTING.md for guidelines.

Development Setup

```bash
# Fork and clone repository
git clone https://github.com/YOUR_USERNAME/auto-turret.git
cd auto-turret

# Create development environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements-dev.txt

# Run tests
pytest tests/

# Check code style
flake8 src/
black src/
```

Project Structure

```
auto-turret/
├── src/                    # Source code
│   ├── camera/            # Camera handling
│   ├── detection/         # Object detection
│   ├── tracking/          # Object tracking
│   ├── control/           # Servo control
│   └── utils/             # Utilities
├── hardware/              # Hardware designs
│   ├── 3d_models/         # 3D printable parts
│   ├── schematics/        # Circuit diagrams
│   └── datasheets/        # Component datasheets
├── docs/                  # Documentation
├── tests/                 # Test suite
├── tools/                 # Utility scripts
└── web/                   # Web interface
```
