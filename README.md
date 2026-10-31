# TrafficSense 🚦

An AI-assisted traffic management prototype that analyses road videos, tracks vehicles, counts traffic flow, and displays signal recommendations through a dashboard.

## Overview

TrafficSense processes two road inputs—**Front** and **Right**—to monitor traffic at an intersection. Users can calibrate a road region and counting line so vehicles on the opposite carriageway are excluded.

The AI runs on a computer. An Arduino Uno controls the physical traffic-light LED prototype through USB serial communication.

## Features

- **Two-video monitoring:** Analyse Front and Right road videos.
- **Vehicle detection and tracking:** Detect vehicles using YOLO and assign tracking IDs with ByteTrack.
- **Cumulative vehicle counting:** Count each tracked vehicle once when it crosses the counting line.
- **Road calibration:** Define the monitored carriageway and counting direction.
- **Annotated dashboard:** Display vehicle boxes, counts, signal recommendations, and incident records.
- **Emergency-priority simulation:** Demonstrate priority handling using an explicitly labelled simulated ambulance.
- **Incident-analysis support:** Includes calibrated crossing rules, number-plate OCR, and evidence-review components.
- **Arduino integration:** Connect to an LED signal model with clearance timing and a communication watchdog.

## How It Works

1. Upload the two road videos.
2. Capture a reference frame and configure the road geometry.
3. Sample video frames for analysis.
4. Detect vehicles using YOLO.
5. Track vehicles across frames using ByteTrack.
6. Count unique tracks crossing the selected line.
7. Generate signal recommendations.
8. Update the dashboard and, when configured, communicate with the Arduino.

## Tech Stack

| Component | Technology |
|---|---|
| Dashboard | HTML, CSS, JavaScript |
| Backend | Python |
| Computer vision | OpenCV, YOLO |
| Vehicle tracking | ByteTrack |
| Number-plate OCR | EasyOCR |
| Database | SQLite |
| Hardware | Arduino Uno and LEDs |
| Communication | USB serial using pySerial |

## Current Demo Behaviour

The presentation demo includes:

- Alternating **10-second** signal recommendations for Front and Right.
- A randomly selected tracked vehicle in the second video labelled **Simulated ambulance**.
- A **15-second Right-road Green recommendation** during that simulated event.
- An emergency record that remains visible after priority completes.

These are demonstration behaviours. The injected ambulance event is not a real AI emergency-vehicle detection, and the displayed recommendations do not confirm physical signal states.

The saved video calibration and simulation configuration are specific to the local demonstration and may not be included in the source-only archive.

## Project Structure

```text
Code/
├── trafficsense/          # Python backend and AI processing
│   └── static/           # Served HTML dashboard
├── arduino/              # Arduino controller firmware
├── config/               # Example configurations
├── scripts/              # Setup and model utilities
├── tests/                # Automated tests
├── docs/                 # Technical documentation
├── requirements-vision.txt
└── run.py
```

The full submission folder also contains the report, presentation, diagrams, selected videos, and demo recording.

## Installation

Python **3.11** is recommended.

Run these commands from the folder containing `run.py`. If you extracted the source-code ZIP, this is the `Code` folder.

### 1. Create the environment

```bash
python3 scripts/setup_environment.py
```

### 2. Install dependencies

**macOS / Linux:**

```bash
.venv/bin/python -m pip install -r requirements-vision.txt
```

**Windows:**

```powershell
.venv\Scripts\python.exe -m pip install -r requirements-vision.txt
```

### 3. Download the models

**macOS / Linux:**

```bash
.venv/bin/python scripts/download_models.py
```

**Windows:**

```powershell
.venv\Scripts\python.exe scripts\download_models.py
```

Model downloads require internet access. Large model files are excluded from the source-only submission ZIP.

## Run the Dashboard

```bash
python3 run.py --port 8773 --runtime runtime/user-session
```

On Windows, use `python` if `python3` is unavailable.

Open:

```text
http://127.0.0.1:8773/
```

Select **Use live**, upload your videos, and press **Start**.

Uploads made in standalone demo mode remain in the browser and are not processed by the Python backend.

## Calibration

Calibration restricts analysis to the intended road approach.

- Mark the approaching carriageway.
- Define the counting line.
- Select the direction vehicles must cross.
- Recalibrate when replacing a video or changing the camera position.

The current dashboard’s global calibration control opens Front. Right-road calibration is available through the backend API. See `docs/USER_DASHBOARD.md` for details.

## Arduino Setup

Upload:

```text
arduino/TrafficSenseController/TrafficSenseController.ino
```

### LED Connections

| Road | Red | Yellow | Green |
|---|---|---|---|
| Front | D2 | D3 | D4 |
| Right | D5 | D6 | D7 |

- Use an individual **1 kΩ resistor** for each LED.
- Connect the LED returns to **common GND**.
- Connect the Arduino to the computer using USB.
- Serial communication uses **115200 baud**.

Cameras connect to the computer. They do not connect directly to the Arduino Uno.

Physical signal control requires complete calibration and a valid hardware connection. The firmware includes clearance timing, conflict rejection, and a communication watchdog.

## Testing

Run from the code folder:

**macOS / Linux:**

```bash
.venv/bin/python -m unittest discover -s tests -q
```

**Windows:**

```powershell
.venv\Scripts\python.exe -m unittest discover -s tests -q
```

## Limitations

- This is a student prototype, not a road-ready traffic controller.
- Tracking errors, occlusion, and changing vehicle IDs can affect counts.
- Number-plate recognition depends on video resolution, angle, lighting, and plate visibility.
- Emergency and helmet recognition remain experimental.
- The current ambulance demonstration uses an explicitly simulated event.
- Current demo signal phases do not establish real-world traffic optimisation.
- Physical Arduino operation still requires testing with the connected board and LEDs.
- Installation on a different computer has not yet been verified.

## Team

**Quantum Vortex**
