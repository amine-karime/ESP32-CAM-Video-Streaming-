
# ESP32-CAM Video Streaming & Face Detection Project

This project uses the **ESP32-CAM** module with the **ESP32-CAM-MB shield** to stream video over Wi-Fi and experiment with face detection. Below is a detailed guide to replicate this project, including troubleshooting tips I learned while building my first IoT application.

---

## Table of Contents
- [Hardware Requirements](#hardware-requirements)
- [Installation & Setup](#installation--setup)
- [How to Use with Arduino IDE](#how-to-use-with-arduino-ide)
- [Problems & Solutions](#problems--solutions)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## Hardware Requirements
- **ESP32-CAM-MB Shield** (for programming).
- **AI-Thinker ESP32-CAM** (with OV2640 camera).
- **5V/2A Power Supply** (mandatory for stability).
- **MicroSD Card** (optional, for saving photos).

---

## Installation & Setup

### 1. **Install CH340 Driver (Windows 10)**  
The ESP32-CAM-MB shield uses the **CH340 USB-to-Serial chip**.  
- **Step 1**: Download the driver: [CH341SER.zip](https://www.wch-ic.com/downloads/ch341ser_zip.html).  
- **Step 2**: Extract the ZIP file, run `SETUP.EXE`, and follow the prompts.  
- **Step 3**: Restart your computer.  

---

### 2. **Set Up Arduino IDE**  
#### Step 1: Install Arduino IDE  
Download and install **Arduino IDE 1.8.18** from [Official Website](https://www.arduino.cc/en/software/OldSoftwareReleases).  

#### Step 2: Add ESP32 Board Support  
1. Open Arduino IDE.  
2. Go to `File → Preferences`.  
3. In **Additional Boards Manager URLs**, paste:  
   ```text
   https://dl.espressif.com/dl/package_esp32_index.json
   ```
   Click OK.

#### Step 3: Install ESP32 Package
Go to `Tools → Board → Boards Manager`.

Search for ESP32 and install the latest version.

#### Step 4: Select Board & Camera Model
Go to `Tools → Board → ESP32 Arduino → AI Thinker ESP32-CAM`.

Set Partition Scheme to Huge APP (3MB No OTA).

---

### 3. **Upload the Code**

I used the CameraWebServer example from the ESP32 library. Here’s how to customize it:

#### Step 1: Open the Example
Go to `File → Examples → ESP32 → Camera → CameraWebServer`.

#### Step 2: Configure Settings
Set Wi-Fi Credentials:
```cpp
const char* ssid = "*********";       // Your Wi-Fi name
const char* password = "**********";    // Your Wi-Fi password
```

Select Camera Model:
Uncomment **#define CAMERA_MODEL_AI_THINKER** (line 33):
```cpp
//#define CAMERA_MODEL_WROVER_KIT
#define CAMERA_MODEL_AI_THINKER
//#define CAMERA_MODEL_ESP_EYE
```

Adjust Resolution (optional):
Change `FRAMESIZE_QVGA` to `FRAMESIZE_SVGA` for higher quality:
```cpp
config.frame_size = FRAMESIZE_SVGA;  // 800x600 resolution
```

#### Step 3: Upload
Connect the ESP32-CAM-MB shield to your PC via USB.

Click the **Upload** button (no need to press any buttons!).

---

## Problems I Faced (and How I Fixed Them)

### 1. **Driver Installation Failed**
**Symptom**: PC didn’t recognize the ESP32-CAM-MB shield.  
**Fix**: Installed the **CH340 driver** and restarted the PC.

### 2. **PSRAM Not Detected**
**Symptom**: `E (656) spiram: SPI RAM enabled but initialization failed.`  
**Fix**:
- Used **Arduino IDE 1.8.18** (newer versions had issues).
- Selected **Huge APP (3MB No OTA)** partition scheme.

### 3. **Wi-Fi Connection Dropped**
**Symptom**: Random disconnections during streaming.  
**Fix**:
- Switched to a **2.4 GHz Wi-Fi** network (ESP32-CAM doesn’t support 5 GHz).
- Used a **5V/2A power supply** instead of USB power.

---

## Quick Modifications

### Adjust Video Resolution
Modify `config.frame_size` in the code:

| Resolution    | Value                 |
| ------------- | --------------------- |
| 320x240 (Default) | `FRAMESIZE_QVGA` |
| 640x480 | `FRAMESIZE_VGA` |
| 800x600 | `FRAMESIZE_SVGA` |

---

## My Journey as a First-Time IoT Developer

This was my **first IoT project**, and while challenging, it taught me:

- **Stable power supplies are crucial** for ESP32-CAM’s reliability. A 5V/2A supply is necessary for smooth operation.
- **Driver issues can block progress**. Installing the CH340 driver correctly was a key step.
- **2.4 GHz Wi-Fi is required for ESP32-CAM**. I initially tried connecting to 5 GHz, which caused issues.
- **PSRAM dependency is critical**. Without it, face detection and other processes won’t work efficiently.
- **Hardware connections must be solid**. Loose cables or improper connections led to failures like "Camera init failed."
- **Video streaming optimization is key**. Lowering resolution and adjusting frame size improved performance.
- **Real-time debugging is essential**. I learned to modify parameters on the fly for better results.
- **Documentation and community were invaluable**. Tutorials and project posts helped me solve problems.
- **Patience and persistence**: I learned to push through obstacles, a crucial mindset for IoT.

### Additional Insights on IoT and Networking:

- **IoT architecture**: Understanding device communication and how they link to networks was key to success.
- **Networking protocols**: Configuring network settings like SSID and static IPs for stability was important for seamless operation.
- **Network security**: Securing Wi-Fi connections became a priority to protect devices and data.
- **Scalability**: I learned how to design IoT systems that can handle increased traffic and devices without compromising performance.
- **Edge computing**: Processing data locally reduced latency and bandwidth use, improving real-time interactions.
- **Data management**: Managing data efficiently, especially for streaming and image capture, is crucial for IoT systems.

This experience has definitely prepared me for future projects. I will certainly be using the knowledge and skills I gained from this project for future IoT applications. The challenges I overcame and the concepts I learned will guide me as I continue to explore the vast possibilities of IoT development.

---

## 📚 References
- [CH340 Driver Installation Guide](https://www.wch-ic.com/downloads/ch341ser_zip.html)
- [ESP32-CAM Pinout Diagram](https://randomnerdtutorials.com/esp32-cam-ai-thinker-pinout/)
- [CameraWebServer Example Code](https://github.com/espressif/arduino-esp32/tree/master/libraries/ESP32/examples/Camera/CameraWebServer)


