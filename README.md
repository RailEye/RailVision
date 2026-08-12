# RailVision AI — SIH1349 Working Prototype

AI-powered CCTV analytics prototype for railway-station surveillance.

## Included
- CCTV video upload (`.mp4`, `.avi`, `.mov`, `.mkv`)
- Webcam mode
- YOLO person detection
- Persistent person tracking (BoT-SORT through Ultralytics)
- Crowd counting and configurable overcrowding alerts
- Region-of-interest (ROI) crowd density analysis
- Approximate crowd heatmap
- Privacy mode using OpenCV face detection + blur
- Restricted-zone entry alerts
- Simple abandoned-object heuristic using tracked non-person objects
- Incident/event log
- CSV export
- Dashboard with live analytics
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

The first run downloads the YOLO model (`yolo11n.pt`) automatically from Ultralytics.

## Demo workflow

1. Choose **Upload CCTV video**.
2. Upload a railway/station/crowd video.
3. Set the crowd threshold low enough for the demo.
4. Enable **Privacy Mode**.
5. Start processing.
6. Show:
   - person count
   - tracked IDs
   - crowd risk
   - ROI
   - heatmap
   - restricted-zone alert
   - incident log
7. Export the incident log as CSV.

## Important prototype limitations

This is a hackathon prototype, not a certified railway safety system.
- Crowd risk is based on configurable thresholds, not official railway capacity standards.
- Face blur is a privacy aid, not a legal compliance guarantee.
- Abandoned-object detection is a heuristic and requires validation before real deployment.
- "Unusual behavior" should be described as AI-assisted event detection, not automatic crime determination.
- Use only CCTV footage that you are authorized to process.

## Suggested final architecture

CCTV/Video -> OpenCV -> YOLO detection/tracking -> Analytics engine -> Privacy layer -> Alert engine -> Dashboard/API
