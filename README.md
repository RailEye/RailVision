# RailVision AI — SIH1349 Working Prototype

AI-powered CCTV analytics prototype for railway-station surveillance.

## Included
- CCTV video upload (`.mp4`, `.avi`, `.mov`, `.mkv`) and Webcam mode
- Advanced YOLO11 object detection (Defaults to `yolo11m.pt` for high accuracy)
- Precision AI Filtering: Bounding box size filtering and 5-frame temporal smoothing to eliminate false alarms
- Persistent person tracking (BoT-SORT)
- Crowd counting, configurable overcrowding alerts, and ROI density analysis
- Short-term Crowd Trend Forecasting (Linear projection of zone occupancy)
- Approximate crowd heatmap & movement trails
- Privacy mode using OpenCV face detection + blur
- Track Intrusion / Platform-edge crossing detection
- Restricted-zone entry alerts & Staff post monitoring
- Weapon detection & simple abandoned-object heuristic
- Seeded interactive Incident Log for demo readiness, with CSV export
- Dark-mode Operations Dashboard with live analytics
- No raw video is written to disk by the application

## Windows + VS Code

1. Install Python 3.10 or 3.11.
2. Open this folder in VS Code.
3. Open Terminal.
4. Create the environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt:

```cmd
.venv\Scripts\activate
```

5. Install packages:

```cmd
python -m pip install --upgrade pip
pip install -r requirements.txt
```

6. Start:

```cmd
streamlit run app.py
```

7. Open the displayed local address, normally `http://localhost:8501`.

The first run downloads the YOLO models (including the default `yolo11m.pt`) automatically from Ultralytics.

## Demo workflow

1. Open the app to immediately see the **Seeded Demo Events** in the Incident Log (shows the app in an active state).
2. Choose **Upload Recording** and upload a railway/station/crowd video.
3. Ensure **Model** is set to `yolo11m.pt Medium ✓` for maximum accuracy.
4. Set the crowd threshold low enough for the demo.
5. Enable **Face anonymisation** and **Track intrusion**.
6. Click **Start AI Processing**.
7. Show:
   - Live AI Engine filtering out glitches (temporal smoothing)
   - Real-time person count & Crowd trend forecasts on the Analytics tab
   - Tracked IDs & Movement trails
   - Track intrusion & Restricted-zone alerts
   - Live Incident Log
8. Export the incident log as CSV.

## Important prototype limitations

This is a hackathon prototype, not a certified railway safety system.
- Crowd risk is based on configurable thresholds, not official railway capacity standards.
- Face blur is a privacy aid, not a legal compliance guarantee.
- Abandoned-object detection is a heuristic and requires validation before real deployment.
- "Unusual behavior" should be described as AI-assisted event detection, not automatic crime determination.
- Use only CCTV footage that you are authorized to process.

## Suggested final architecture

CCTV/Video -> OpenCV -> YOLO detection/tracking -> Analytics engine -> Privacy layer -> Alert engine -> Dashboard/API
