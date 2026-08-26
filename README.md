# reymissioncontroller — High-Fidelity GCS for ArduPilot

A high-density desktop Ground Control Station (GCS) built on top of the official **ArduPilot Mission Planner** core libraries, redesigned with a modern dark slate-gray aerospace visual theme.

## Architecture

This application consists of two integrated components:
1. **Frontend (Electron/React/TypeScript)**: The visual user interface layer matching high-fidelity aerospace flight software layouts. It integrates a real Leaflet interactive satellite map, canvas PFD instrument dial, and vital gauge tiles.
2. **Backend Adapter (GCSBridge - C# .NET 10)**: A real-time UDP-to-WebSocket bridge. It references and links directly against the official, compiled `MAVLink` classes inside Michael Oborne's **Mission Planner (GPL-3.0)** code. It parses incoming telemetry and relays flight instructions with complete framing verification.

```
Vehicle (SITL or hardware UDP) <-> GCSBridge.exe (C# / MAVLink) <-> WebSocket JSON <-> Electron/React UI
```

---

## Workspace Structure

- `backend/GCSBridge/`: C# program hosting the WebSocket JSON API. Uses the official ArduPilot `MAVLink.MavlinkParse` state parser.
- `backend/MissionPlanner/`: Cloned copy of the official Mission Planner library repositories.
- `frontend/src/`: React source views, instruments (PFD), and components.
- `frontend/dist_electron/win-unpacked/`: Packaged Windows binaries.

---

## How to Build & Run

### 1. Launch the Desktop Executable
Run the pre-compiled production package directly from the target folder:
- **Location**: `c:\Users\notme\Downloads\mission palner\Launch GCS.bat`
- This script starts the backend WebSocket server and opens the GCS presentation window.

### 2. Run in Development Mode
To make changes with hot reloading active:

```powershell
# Term 1: Start the backend MAVLink bridge
cd backend/GCSBridge
dotnet run

# Term 2: Start the Vite dev server
cd frontend
npm run dev
```

---

## Licensing
This project links dynamically to code inside the official **Mission Planner** repository, which is licensed under the **GNU General Public License v3.0 (GPL-3.0)**. The complete source code of both the frontend UI and C# adapter layers is provided in compliance with GPL-3.0 copyleft requirements.
