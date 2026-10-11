# 🌐 God's Eye View — Installation & Feature Launch Guide

This guide documents the complete installation procedure and how to launch and control every feature in **God's Eye View** (`gods-eye-view`).

---

## ⚡ 1. Prerequisites & Installation

### Requirements
- **Node.js**: `24.x` (version `24.14.0` or later) or `26.x`.
  > ⚠️ *Note:* Node 25 is End-Of-Life and will trigger a warning in the setup doctor. Node 22 or older is unsupported by the project's dependencies and engine checks.
- **Git**
- **npm** (v10 / v11)
- **Modern Browser**: Chrome, Edge, Brave, or Safari with WebGL enabled.

---

### Step-by-Step Installation (Terminal)

#### Step 1: Set Node.js to Version 24
Using `nvm` (Node Version Manager):
```bash
# Install Node.js 24 (LTS)
nvm install 24

# Switch to Node 24
nvm use 24

# Verify version (must be >= 24.14.0)
node -v
```

#### Step 2: Clone the Repository
```bash
git clone https://github.com/bilawalsidhu/gods-eye-view.git
cd gods-eye-view
```

#### Step 3: Install Locked Dependencies
Use `npm ci` to install exact locked package versions:
```bash
npm ci
```

#### Step 4: Run the Setup Doctor
Verify system readiness and provider status:
```bash
npm run doctor
```
You should see:
```text
[OK] Node 24.x.x: supported LTS and calibrated for release gates
[OK] npm xx.xx.x
[OK] dependencies installed
```

#### Step 5: Start the Development Server
You have two launch options:

**Standard Launch:**
```bash
npm run dev
```

**macOS Shortcut (Vite cache clear + Keychain integration):**
```bash
./scripts/dev-fresh.sh
```

#### Step 6: Open the Application
Navigate in your browser to:
👉 **[http://localhost:4173](http://localhost:4173)**

---

### 🧹 How to Clear Temporary Data & Start Fresh

God's Eye View **does not save videos, 3D tiles, or imagery to your hard drive** (they stream straight to browser memory). However, it does write tiny JSON metadata caches and Vite build artifacts.

To completely wipe temporary caches and start 100% clean:

```bash
# 1. Delete local JSON caches, logs, and Vite bundle cache
rm -rf .gev-cache node_modules/.vite .gev-logs

# 2. Launch fresh
nvm use && ./scripts/dev-fresh.sh
```
In your browser, press **`Cmd + Shift + R`** (or open an Incognito window) to discard any browser-cached map tiles.

---

## 🚀 2. First-Run Mission Launcher

When you first open `http://localhost:4173`, the setup launcher modal presents four onboarding paths:

| Mission | What it Loads |
| :--- | :--- |
| **✈️ Live Contacts** | Automatically turns on live aircraft, activates detection mesh, and selects an active airborne flight. |
| **🚀 Space Missions** | Replays real orbital rocket launches from the last 30 days with scrubbable ascent trajectory. |
| **🌦️ Environmental** | Activates live weather radar, wind forecasts, seismic feeds, and satellite cloud imagery. |
| **🌐 Explore Manually** | Keyless Earth exploration with Esri/OSM satellite basemap, ready for manual layer toggles. |

---

## 🎛️ 3. Feature Launching Procedures

All features are accessible via **DATA LAYERS**, hotkeys, the **POWER UP** panel, or hands-free **Voice Control**.

---

### 🛩️ Live Flights & Cockpit Mode
*Track 11,000+ real aircraft in real time via OpenSky & adsb.lol (Keyless).*

1. **Launch:**
   - In the left sidebar, expand **DATA LAYERS** ▸ **Movement** ▸ Toggle **Live Flights** (or press `F`).
2. **Track a Target:**
   - Click any aircraft glyph on the 3D globe.
   - The camera locks on, traces a fading flight trail, and opens the aircraft's telemetry card (altitude, ground speed, callsign, origin, heading).
3. **Enter Cockpit View:**
   - Press **`C`** on your keyboard or click the **COCKPIT** button on the target card.
   - The camera rides inside the cockpit while holding high-resolution ground terrain underneath.
4. **Browse Contacts (250 km radius):**
   - Click the **CONTACTS** drawer while in cockpit mode to jump directly into nearby aircraft.
5. **Exit Cockpit:**
   - Press **`Esc`** or click **EXIT COCKPIT**.

---

### 🎖️ Military Traffic
*Real-time military aircraft tracking via ADS-B (Keyless).*

1. **Launch:**
   - Open **DATA LAYERS** ▸ **Movement** ▸ Toggle **Military Flights**.
2. **Visuals:** Military airframes display in distinctive amber markers.
3. **Trace 24h Loop History:**
   - Click any military helicopter or jet to backfill up to 24 hours of flight history, rendered as stacked 3D loops over terrain.

---

### 📹 Live CCTV Mesh & Viewsheds
*~3,900 public road cameras projected directly into the 3D globe (Austin, London, California, Ontario, Finland, Delaware).*

1. **Launch:**
   - Open **DATA LAYERS** ▸ **Cameras** ▸ Toggle **CCTV Mesh**.
2. **View Video / Still:**
   - Zoom into Austin, London, or Delaware. Camera icons will populate intersections.
   - Click any camera to view the live feed (Delaware features live HLS video streams).
3. **Viewshed Projection:**
   - In the CCTV panel header, cycle mode to **VIEWSHED**.
   - The globe projects a 3D frustum cone showing the camera's field of view and blind spots.
   - Drag the on-screen gizmo to calibrate camera angle and rotation.

---

### 🛰️ Satellites & Space Stations
*838-object SGP4 orbital catalog + ISS tracking (Keyless via CelesTrak).*

1. **Launch:**
   - Open **DATA LAYERS** ▸ **Infrastructure** ▸ Toggle **Satellites**.
2. **Track the ISS:**
   - Search `ISS` or click the International Space Station icon.
   - Camera tracks orbital velocity, displaying true orbital plane rings aligned via GMST.
3. **Dense Mode (Starlink constellation):**
   - Click the **DENSE** pill in the Satellites panel to display thousands of active Starlink satellites in orbit.

---

### 🚀 Space Missions (Rocket Launches)
*30-day historical and upcoming space missions (Keyless via Launch Library 2).*

1. **Launch:**
   - Open **DATA LAYERS** ▸ **Events** ▸ Toggle **Space Missions**.
2. **Replay Launch Ascent:**
   - Select an orbital mission (e.g., Falcon 9, Electron, Ariane 6).
   - Use the playback scrubber (`0.25x` to `4x` speed) to replay launch trajectory, stage separation, and orbit insertion.

---

### 🌦️ Weather, Wind & Storm Tracking
*Global forecast flow and real-time observed weather radar (Keyless).*

1. **Wind Flow Simulation:**
   - Open **DATA LAYERS** ▸ **Weather** ▸ Toggle **Wind**.
   - Real-time animated GFS / ECMWF particles visualize 10m forecast winds with colorized velocity.
2. **Observed Rain Radar & Clouds:**
   - Toggle **Observed Weather** in the Weather panel.
   - Use the time slider to scrub through recent rain radar, GOES regional clouds, and lightning strikes.
3. **Cyclone Advisories:**
   - Toggle **Cyclones** to display live NHC/CPHC hurricane/cyclone forecast cones and storm paths.

---

### 🎨 GLSL Optics / Sensor Simulation Modes
*Re-render the entire globe through tactical optical sensor filters.*

Press the number keys **`1` through `7`** on your keyboard:
- **`1`** — Normal True-Color Basemap
- **`2`** — CRT Phosphor Monitor
- **`3`** — NVG (Night Vision Goggles - Green Phosphor)
- **`4`** — FLIR Ironbow (Thermal Sensor)
- **`5`** — FLIR White-Hot (Thermal Infrared)
- **`6`** — Noir (High-contrast monochrome)
- **`7`** — Snow (Arctics / High-glare)

---

### 🎖️ Tactical HUD & Detection Overlay
- **Press `H`**: Toggles the tactical military heads-up display (HUD) with pitch ladder, compass azimuth, and telemetry.
- **Press `D`**: Toggles the AI detection mesh, drawing real-time bounding boxes and tracking IDs on all objects in the camera frustum.
- **Press `` ` `` (backtick)**: Toggles live FPS, draw call metrics, and performance telemetry.

---

### 🖊️ Map Whiteboard & Vector Drawing
*Draw real-world annotations, boundary lines, and measuring markers.*

1. **Manual Drawing:**
   - Click **DISPLAY** ▸ **Draw** in the navigation bar.
   - Choose **Area**, **Line**, or **Pin**.
   - Click points directly onto the 3D terrain; double-click to finish.
   - Annotations stick persistently to the geographic coordinates.
2. **Measuring Distances:**
   - Choose **Line** or ask via voice (*"How far is LAX from DFW?"*). The system draws an arched geodesics line with exact km/miles.

---

### 🧭 Directions & Camera Flythrough
*Turn-by-turn route generation draped over 3D terrain (Keyless via OSRM).*

1. Open **DATA LAYERS** ▸ **Utilities** ▸ Toggle **Directions**.
2. Click Point A (Origin) and Point B (Destination) on the globe.
3. The road network route renders onto terrain.
4. Click **FLY ROUTE** to make the camera follow the calculated route like a low-altitude drone with banked turns.

---

### 📻 World Radio Tuner
*Listen to live geolocated radio stations around the world (Keyless).*

1. Open **DATA LAYERS** ▸ **Utilities** ▸ Toggle **Radio**.
2. An analog radio dial appears at the bottom of the screen.
3. Drag the frequency needle: the globe flies directly to the broadcasting station city and streams the live audio.

---

### 📷 Street Level Imagery (Mapillary)
*Ground-level photography projected onto 3D street networks.*

1. Requires a free Mapillary Client Token (see Power-Up section).
2. Open **DATA LAYERS** ▸ **Cameras** ▸ Toggle **Street Level**.
3. Green coverage lines appear over streets. Click any line to inspect image cones, open the viewer, and click **FOLLOW** to match the 3D globe camera angle to the photograph.

---

### 🎙️ Hands-Free Voice AI Agent
*Talk to the globe in natural language using OpenAI Realtime.*

1. **Requirement:** Add an `OPENAI_API_KEY` or connect ChatGPT OAuth in **POWER UP**.
2. **Activation:**
   - Click the **GEV MIC** button in the lower toolbar and grant browser microphone permission.
3. **Example Voice Commands:**
   - *Directing:* `"Take me to Tokyo."` · `"Orbit around this stadium slowly."` · `"Zoom out to full Earth view."`
   - *Targeting:* `"Track the nearest commercial flight."` · `"Enter cockpit mode."`
   - *Analyst Queries:* `"How many flights are over Texas right now?"` · `"When does the ISS pass over my location?"` · `"What is the largest fire near Los Angeles?"`
   - *Sensors:* `"Switch to night vision."` · `"Turn on active fires and rain radar."`
   - *Annotations:* `"Outline the state of Texas."` · `"Draw the walking route from Central Park to Times Square and fly it."`

---

### 💬 MCP (Model Context Protocol) Integration
*Control God's Eye View directly from Claude Desktop or OpenAI Codex.*

To connect your desktop AI assistants:
1. Refer to [`docs/MCP_SETUP.md`](file:///Users/rajatsharma/Documents/gods%20eye/docs/MCP_SETUP.md).
2. Add the MCP server configuration to your Claude Desktop config:
   ```json
   {
     "mcpServers": {
       "gods-eye-view": {
         "command": "node",
         "args": ["/Users/rajatsharma/Documents/gods eye/server/mcp/stdio.js"]
       }
     }
   }
   ```
3. Restart Claude Desktop. You can now prompt Claude: *"Show me the flight traffic over London in God's Eye View."*

---

## 🔑 4. Adding API Keys (Power-Up Panel)

God's Eye View works out of the box with **zero keys** on Esri Satellite + keyless OSM.

To unlock premium photorealistic 3D, live ship tracking, or voice control:
1. In the bottom-right corner of the web UI, click the **POWER UP** chip (or open `http://localhost:4173/?setup=1`).
2. Paste any of the optional keys:
   - **Cesium ion Token** *(Free Community Tier)*: Enables **Google Photorealistic 3D Tiles** & worldwide 3D terrain.
   - **Google Maps API Key** *(Metered)*: Direct Google 3D Tiles and Google Place Search.
   - **OpenAI API Key** *(Metered)*: Enables Voice Control and AI HUD summaries.
   - **AISStream Key** *(Free)*: Enables global live ship & maritime vessel tracking.
   - **NASA FIRMS Key** *(Free)*: Enables live 24h satellite fire detection.
   - **TomTom API Key** *(Free)*: Adds live traffic flow speeds and congestion colors.
   - **Mapillary Token** *(Free)*: Enables street-level photography.
3. Click **SAVE KEYS**. Keys are securely written to your local `.env` file (never exposed to external clients).

---

## ⌨️ 5. Keyboard Shortcuts Cheat-Sheet

| Key | Action |
| :--- | :--- |
| **`1` – `7`** | Cycle visual sensor modes (Normal, CRT, NVG, FLIR Thermal, Noir, Snow) |
| **`C`** | Toggle Cockpit mode for selected flight |
| **`H`** | Toggle Tactical Military HUD |
| **`D`** | Toggle Screen-Space Detection Boxes |
| **`` ` ``** | Toggle Performance / FPS stats |
| **`Esc`** | Deselect active entity / Exit Cockpit |
| **Trackpad / Wheel** | Zoom in / Zoom out |
| **Left Click + Drag** | Pan globe |
| **Right Click + Drag** | Tilt / Pitch / Orbit camera |

---

## 🛠️ Summary of Scripts

| Command | Purpose |
| :--- | :--- |
| `npm run dev` | Starts Vite dev server at `http://localhost:4173` |
| `npm run doctor` | Verifies Node version, dependencies, and configured keys |
| `./scripts/dev-fresh.sh` | Clears Vite cache and starts server with macOS Keychain keys |
| `npm run build` | Builds production bundle |
| `npm run preview` | Previews production build |
| `npm test` | Runs unit tests |
