

## **digital twin** of Colombo's flood hydraulics - a real engineering tool, not just a web app.

```
┌─────────────────────────────────────────────┐
│  LAYER 1: Geospatial Data Engine            │
│  Colombo elevation grid + drainage network  │
│  + building footprints + canal system       │
├─────────────────────────────────────────────┤
│  LAYER 2: Hydrological Simulation Engine    │
│  Rainfall → Surface runoff → Drainage flow  │
│  → Accumulation → Inundation mapping        │
├─────────────────────────────────────────────┤
│  LAYER 3: Visualization Dashboard           │
│  2D map overlay + 3D building view +        │
│  flood depth heatmap + animation timeline   │
└─────────────────────────────────────────────┘
```

## Layer 1 - Geospatial Data Engine  
This is the **hardest part**  not the coding, but the data.

| Data Needed                   | Source                      | Resolution                 | Availability        |
| ----------------------------- | --------------------------- | -------------------------- | ------------------- |
| Digital Elevation Model (DEM) | SRTM (30m) or ALOS PALSAR   | ~30m per pixel for Colombo | Freely downloadable |
| Building footprints           | OpenStreetMap               | Per-building               | Freely available    |
| Canal/drain network           | OpenStreetMap + Survey Dept | Vector lines               | Partially available |
| Soil absorption rates         | FAO / Sri Lankan soil maps  | District level             | Freely available    |
| Land use / land cover         | OSM classification          | 30m                        | Freely available    |
## **Critical reality check:** 

The SRTM 30m DEM is the minimum viable dataset. At 30m resolution, one grid cell ≈ a small city block. For better simulation, we ideally want 10m or 5m  which costs money or requires fieldwork.  

### **Practical solution for 10 weeks:**  
- Use SRTM 30m as baseline (free, globally consistent)  
- Supplement with OSM building heights (estimated from number of floors if not available)  
- Use OSM canal/river lines as the drainage network  
- Validate against known flood-prone areas (Fort, Maradana, Dematagoda, Wellawatte ,these are documented in Sri Lanka Disaster Management reports)

## Layer 2 - Hydrological Simulation Engine  
This is the **real engineering heart** of the project. Five students can each own a sub-module:  
### Student 1: Rainfall Generator  
- Configurable rainfall intensity slider (mm/hour - e.g., 50mm/hr is a serious monsoon burst)  
- Historical rainfall pattern loader (from Department of Meteorology CSV data)  
- Time-series rainfall generator: starts light → peaks → decreases  
### Student 2: Surface Flow Model  
- Core algorithm: **flow accumulation on a gridded DEM**  
- Each grid cell receives water from rainfall + upstream cells  
- Water flows to the lowest adjacent neighbor (D8 flow direction algorithm)  
- Formula per time step: 
```
water[cell][t+1] = water[cell][t] + rainfall[cell][t] + inflow[neighbors] - outflow - infiltration
```
- Buildings become **barriers** (water cannot pass through)  
- Roads are treated as high-conductivity channels (water flows faster)  
- Green areas (parks, open land) have **higher infiltration** (water absorbed)
## Student 3: Drainage & Canal Model  
- Colombo's canal network carries water OUT of the city toward the sea  
- Model canal capacity: when canals are below capacity, water drains into them; when full, they overflow back  
- Key canals: Fort Canal, Keselwatta Canal, St. Sebastian Canal, Lunawa Lagoon  
- Simple hydraulic model:  (canal capacity) = width × depth × flow_velocity  
- When rainfall exceeds canal drainage capacity → backflow → street flooding  
## Student 4: Flood Inundation Mapping  
- Output: for each grid cell at each time step → water depth in meters  
- Classify inundation severity:  
- 0–0.1m: Slight (pedestrians affected)  
- 0.1–0.3m: Moderate (vehicles stall)  
- 0.3–0.5m: Severe (ground floors flooded)  
- 0.5m: Critical (buildings submerged)  
- Generate flood hazard maps showing maximum inundation depth per location  
## Student 5: Scenario Comparison Engine  
- Save simulation runs with parameters  
- Compare: "What happens if it rains 80mm/hr for 2 hours vs. 120mm/hr?"  
- Show before/after inundation maps  
- Identify: which areas flood first? Which drain fastest?  
- Export flood risk report as PDF
## Layer 3 - Visualization Dashboard  
**Two modes - 2D and 3D:**  

**2D Mode (more achievable, Week 1-6 target):**  
- Folium map centered on Colombo (latitude 6.9271, longitude 79.8612)  
- Overlay water depth as a color gradient (blue = water, intensity = depth)  
- Time-slider: watch flooding accumulate over simulated time (1 hour compressed into 30 seconds)  
- Click any building/road → popup showing flood depth at that location  
- Toggle layers: buildings on/off, canals on/off, elevation contours on/off  

**3D Mode (ambitious stretch goal, Week 7-10):**  
- WebGL-based 3D Colombo usingDeck.gl or Three.js  
- Extrude building footprints by estimated height (from OSM floor count or default 3 floors = 9m)  
- Animate water level rising within and around buildings  
- This is **very impressive on demo day** - judges have never seen a 3D flood simulation before  

**Dashboard Features:**  
- Rainfall control panel (intensity, duration, start/stop)  
- Real-time water balance display (total rainfall vs. water drained vs. water accumulated)  
- Flood hotspot list: top 10 most severely flooded locations at current time step  
- Download scenario report (CSV of inundation data per location)

## 10-Week Execution Plan


| Week | Focus                                        | Deliverable                                                                  |
| ---- | -------------------------------------------- | ---------------------------------------------------------------------------- |
| 1    | Data collection + environment setup          | SRTM DEM of Colombo downloaded, OSM data extracted, Python/NumPy stack ready |
| 2    | DEM preprocessing + visualization            | Elevation map of Colombo rendered, grid built, building footprints overlaid  |
| 3    | D8 flow direction algorithm                  | Water flow model working on static terrain (no rainfall yet)                 |
| 4    | Rainfall generator + infiltration model      | Rainfall slider working, infiltration rates applied per land type            |
| 5    | Canal/drainage model                         | Drainage network integrated, canal capacity logic working                    |
| 6    | Integration + 2D visualization               | Full simulation pipeline → Folium map overlay working                        |
| 7    | Flood hotspot classifier + scenario engine   | Severity classification, scenario comparison working                         |
| 8    | Dashboard polish + performance optimization  | Real-time simulation runs at acceptable frame rate                           |
| 9    | 3D visualization (stretch goal) + validation | Compare simulation output against known flood-prone area records             |
| 10   | Demo prep + documentation                    | Final demo video, user manual, technical documentation                       |
## Feasibility Check

| Concern                                    | Assessment                                                                                                                                                                                     |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "SRTM 30m is too coarse"                   | Workable for a demo - each cell ≈ a small block. It's what real researchers use at project start.                                                                                              |
| "Can we get canal/drain data?"             | OSM has most major canals traced. Missing data is a known limitation.                                                                                                                          |
| "This needs civil engineering knowledge"   | The D8 flow algorithm is well-documented and implementable by CS students. You don't need hydrology expertise  just implement standard published methods and cite them.                        |
| "Will the simulation be accurate?"         | No; and that's fine. Label it as a **demonstration prototype**, not a production flood model. The value is in demonstrating the _concept_ and the software engineering, not replacing HEC-RAS. |
| "Can 5 students work in parallel on this?" | Yes; each student owns a distinct module (rainfall, flow, drainage, visualization, scenarios) with clear interfaces between them.                                                              |

## All 5 Student Roles  Fully Assigned

# Student 1: Rainfall & Weather Data Engineer  
  
**Owns:** The input side of the simulation the "rain" that drives everything.  
  
**What they build:**  
  
1. **Rainfall Event Simulator**  
	- Configurable intensity slider (mm/hr): light rain (5mm/hr), moderate (25mm/hr), heavy monsoon (80mm/hr), extreme (150mm/hr)  
	- Time-series rainfall profiles: burst patterns, continuous patterns, intermittent patterns  
	- Historical rainfall CSV loader (from Department of Meteorology daily data)  
  
2. **Rainfall Spatial Mapper**  
	- Colombo does not rain uniformly the southwestern monsoon hits Kollupitiya differently than Kolonnawa  
	- Assign different rainfall intensities to different grid zones based on historical patterns  
	- Create a heatmap of Colombo's typical rainfall distribution by area  
  
3. **Infiltration Model per Land Type**  
	- Green areas (parks, paddy fields): high infiltration rate → water absorbed into soil  
	- Roads and paved areas: zero infiltration → all water becomes surface runoff  
	- Built-up areas: minimal infiltration  
	- Use OSM land-use classification to tag each grid cell with infiltration coefficient  
	- Formula: `infiltration[cell] = infiltration_rate[land_type] × water[cell] × dt`  
  
**Deliverable for Student 1 by Week 4:** A working rainfall event player that feeds water into the simulation grid in real-time, with each grid cell tagged for its infiltration behavior.

## Student 2: Surface Flow & DEM Processing Engineer  
  
**Owns:** The terrain processing Colombo's elevation data and implementing the water flow algorithm.  
  
**What they build:**  
  
1. **DEM Acquisition & Preprocessing**  
	- Download SRTM 30m elevation data for the Colombo bounding box (approximately lat 6.78–6.99, lon 79.80–79.92)  
	- Convert raw SRTM HGT file to a NumPy 2D array of elevation values  
	- Clip to Colombo administrative boundary (use shapefile from Survey Department or OSM boundary)  
	- Resample to working grid resolution (30m or 90m if performance is an issue)  
	- Fill sinks (pixels lower than all neighbours that would cause water to get "stuck") using the Wang & Liu algorithm  
	  
2. **D8 Flow Direction Algorithm**  
	- For each grid cell, determine which neighbour is the steepest downhill direction  
	- Water flows in direction of steepest descent  
	- Cells with no downhill neighbour (local minima / pits) → water accumulates as a pond  
	- Build a flow direction grid (8 values per cell, one per direction)  
  
3. **Flow Accumulation Engine**  
	- For each cell, sum up how many upstream cells drain into it  
	- High flow accumulation = major drainage channel (where streams/rivers would form)  
	- This becomes the base map for where flooding will be worst  
  
4. **Building Barrier Enforcement**  
	- Load OSM building footprints  
	- Treat building cells as elevation raised to a very high value (water cannot flow through)  
	- Merge buildings with the DEM: `elevation[building_cell] = max_elevation + 1`  
	- - Buildings become **barriers** (water cannot pass through)  
	- Roads are treated as high-conductivity channels (water flows faster)  
	- Green areas (parks, open land) have **higher infiltration** (water absorbed)
	
5. **Time-Step Water Routing**  

	- Per simulation step:  
```  
outflow[cell] = water[cell] × flow_fraction[direction] × dt  
water[cell] += rainfall_input[cell] + sum(inflow from neighbours) - sum(outflow to neighbours) - infiltration  
```  
  
**Deliverable for Student 2 by Week 5:** A working D8 flow model showing where water drains across Colombo's terrain, with buildings enforced as barriers, running in real-time as a NumPy simulation.


## Student 3: Drainage & Canal Network Engineer  
  
**Owns:** The "out" side of the simulation how water leaves the city through Colombo's canal system.  
  
**What they build:**  
  
1. **Canal Network Extraction from OSM**  
	- Extract all canal, stream, and river lines from OSM for Colombo  
	- Key canals: Fort Canal, Keselwatta Canal, St. Sebastian Canal (Dematagoda area), Lunawa Canal, Diyawanna Channel  
	- Convert canal polylines into grid cells — each canal cell has a capacity (m³/s)
	- Save scenarios to SQLite: `scenarios(id, name, rainfall_config, canal_state, tide, created_at)`  
	- Load and run any saved scenario  
2. **Scenario Comparison Engine**  
	- Run two scenarios side-by-side  
	- Output: difference map  "areas that flood in **Scenario A** but not in **Scenario B**"  
	- Key question the tool answers: "What happens if it rains **80mm/hr** vs **120mm/hr** for 2 hours?"  
	- Show: max flood depth per location in each scenario, time to peak flooding, total water accumulated  
3. **Flood Risk Report Generator**  
	- After each simulation run, generate a structured report:  
	- Executive summary: total area flooded, worst-hit areas, time to peak  
	- Per-Division breakdown (Colombo MC, Dehiwala, etc.) of flood impact  
	- Comparison to baseline (if scenario was run)  
	- Export as PDF using ReportLab or as HTML  
	- Report saved to disk and downloadable from dashboard  
4. **Real-Time Statistics Panel**  
	During simulation:  
	- Total rainfall volume (mm³)  
	- Total water on surface (mm³)  
	- Total water drained via canals (mm³)  
	- Total infiltration (mm³)  
	- Flood coverage % (what % of Colombo is flooded right now)  
	- Live updating graph (matplotlib or Plotly) showing these curves over time  
	- This gives judges and users immediate quantitative understanding  
5. **Data Persistence & Export**  
	- Save full simulation results per grid cell per time step to SQLite  
	- Export as CSV: `location_id, lat, lon, max_depth, time_to_flood, time_to_drain`  
	- This CSV can be opened in QGIS by urban planners for further analysis  
	- Geospatial export as GeoJSON for use in external GIS tools  
6. **User Interface Polish**  
	- Build the main Flask/Streamlit dashboard layout  
	- Navigation: Simulation | Map | Scenarios | Reports  
	- Ensure the app is responsive and deployable on a local machine  
	- Write the `README.md` and installation guide
- 7.**Canal Capacity Model**  
	Each canal cell has:  
	- Width (metres) - from OSM width tag or estimated from canal type  
	- Depth (metres) - assumed from canal classification or estimated  
	- Slope - from DEM elevation difference between canal endpoints  
	- Flow velocity via Manning's equation: `V = (1/n) × R^(2/3) × S^(1/2)`  
	- Discharge capacity: `Q = V × A` (velocity × cross-sectional area)  
	- If canal is below capacity → water drains from street into canal  
	- If canal exceeds capacity → backflow (water flows from canal back onto streets)  
8.**Outfall / Sea Discharge**  
	- Colombo's canals drain to the Indian Ocean and Negombo Lagoon  
	- Cells at the city boundary (coastal/outfall points) discharge water OUT of the simulation domain  
	- Model tidal backstop: at high tide, outfall is restricted (sea level blocks discharge)  
9.**Canal Overflow & Backflow**  
	- When canal `current_flow > max_capacity`: canal cells become water sources (flooding)  
	- Backflow water spreads to adjacent non-canal cells using overflow rules  
- 
**Deliverable for Student 3 by Week 6:** A fully integrated drainage model showing canal drainage reducing street flooding and demonstrating overflow when canals are overwhelmed.  
## **Student 4: Flood Mapping & Inundation Visualizer

**Owns:** The visual output - turning numbers into something the user can understand and interact with.  
**What they build:**  
1.**Flood Depth Classification**  
	- For each grid cell at each time step, compute water depth  
	- Classify severity:  
```
Class 0: No flooding     (depth = 0)
Class 1: Slight          (0 < depth ≤ 0.1m)  — pedestrians inconvenienced
Class 2: Moderate        (0.1 < depth ≤ 0.3m) — vehicles stall
Class 3: Severe          (0.3 < depth ≤ 0.5m) — ground floors flood
Class 4: Critical        (depth > 0.5m)        — buildings inundated
```
2.**2D Interactive Map (Folium)**  
	- Base layer: OpenStreetMap tiles centered on Colombo  
	- Overlay: for each grid cell, a semi-transparent polygon colored by flood class  
	- Time slider: 0 → 60 minutes (or whatever the simulation duration is)  
	- On click: popup showing elevation, current water depth, flood class, and distance to nearest canal  
	- Toggle layers: buildings on/off, canals on/off, flood overlay on/off, elevation contours on/off  
3.**2D Animation Player**  
	- Animate the flood spreading over the 2D map as the simulation runs  
	- Play / Pause / Reset controls  
	- Speed control: 1x, 2x, 5x simulation speed  
	- Cumulative rainfall indicator and total water accumulated counter  
4.**Flood Hotspot Dashboard**  
	- Real-time list: "Top 10 locations with highest flood depth right now"  
	- Each entry: location name (nearest landmark), depth in metres, flood class, time since flooding started  
	- Auto-updates as simulation progresses  
5.**3D Visualization (Stretch Goal — Week 8-10)**  
	- WebGL 3D model of Colombo using Deck.gl  
	- Building footprints extruded by estimated height (3 floors = 9m default)  
	- Flood water rendered as a semi-transparent blue layer with depth-based opacity  
	- Camera controls: orbit, zoom, pan  
	- This is the showstopper on demo day  
	
**Deliverable for Student 4 by Week 7:** A working Folium 2D map with flood overlay, time slider, and hotspot panel — plus a plan in place for the 3D visualization.  

# Student 5: Scenario Engine & Reporting Officer  
**Owns:** The comparison and decision-support layer  what makes this tool useful beyond a simulation.  
**What they build:**  
1.**Scenario Definition System**  
	- A scenario = one complete simulation run with:  
	- Rainfall profile (intensity, duration, pattern)  
	- Initial canal state (full/empty - can simulate post-monsoon already-saturated canals)  
	- Tide condition (high/low)  
	- Save scenarios to SQLite: `scenarios(id, name, rainfall_config, canal_state, tide, created_at)`  
	- Load and run any saved scenario  
2.**Scenario Comparison Engine**  
	- Run two scenarios side-by-side  
	- Output: difference map - "areas that flood in Scenario A but not in Scenario B"  
	- Key question the tool answers: "What happens if it rains 80mm/hr vs 120mm/hr for 2 hours?"  
	- Show: max flood depth per location in each scenario, time to peak flooding, total water accumulated  
3.**Flood Risk Report Generator**  
	- After each simulation run, generate a structured report:  
	- Executive summary: total area flooded, worst-hit areas, time to peak  
	- Per-Division breakdown (Colombo MC, Dehiwala, etc.) of flood impact  
	- Comparison to baseline (if scenario was run)  
	- Export as PDF using ReportLab or as HTML  
	- Report saved to disk and downloadable from dashboard  
4.**Real-Time Statistics Panel**  
	- During simulation:  
	- Total rainfall volume (mm³)  
	- Total water on surface (mm³)  
	- Total water drained via canals (mm³)  
	- Total infiltration (mm³)  
	- Flood coverage % (what % of Colombo is flooded right now)  
	- Live updating graph (matplotlib or Plotly) showing these curves over time  
	- This gives judges and users immediate quantitative understanding  
5.**Data Persistence & Export**  
	- Save full simulation results per grid cell per time step to SQLite  
	- Export as CSV: `location_id, lat, lon, max_depth, time_to_flood, time_to_drain`  
	- This CSV can be opened in QGIS by urban planners for further analysis  
	- Geospatial export as GeoJSON for use in external GIS tools  
6.**User Interface Polish**  
	- Build the main Flask/Streamlit dashboard layout  
	- Navigation: Simulation | Map | Scenarios | Reports  
	- Ensure the app is responsive and deployable on a local machine  
	- Write the `README.md` and installation guide  

**Deliverable for Student 5 by Week 8:** A working scenario comparison engine with PDF report generation and a polished full dashboard integrating all components.
## Consolidated Task Assignment Table

| Student | Module                        | Owns             | Key Output                                                       |
| ------- | ----------------------------- | ---------------- | ---------------------------------------------------------------- |
| 1       | Rainfall & Weather Engine     | Inputs           | Rainfall generator + infiltration mapper running in real-time    |
| 2       | DEM & Flow Model              | Terrain          | D8 flow algorithm + flow accumulation grid for all of Colombo    |
| 3       | Drainage & Canal Model        | Outputs          | Canal capacity model + backflow logic integrated into simulation |
| 4       | Flood Mapping & Visualization | Presentation     | Interactive Folium map + 3D WebGL visualization                  |
| 5       | Scenario Engine & Dashboard   | Decision-Support | Scenario comparison + PDF reports + statistics panel             |
## Parallel Integration Points

| Week | Integration Milestone                                                        |
| ---- | ---------------------------------------------------------------------------- |
| 4    | Student 1's rainfall feeds Student 2's flow model                            |
| 5    | Student 3's drainage model connects to Student 2's flow accumulation         |
| 6    | **Full pipeline integration**: Rainfall → Flow → Drainage → Inundation depth |
| 7    | Student 4's visualization renders Student 2+3's output in real-time          |
| 8    | Student 5's dashboard wraps all modules into one deployable app              |
| 9    | Full simulation runs end-to-end; Student 4 works on 3D visualization         |
| 10   | Demo, documentation, performance optimisation                                |
## Technical Stack Summary (All 5 Students)

| Layer                           | Technology                                                   |
| ------------------------------- | ------------------------------------------------------------ |
| DEM processing + flow algorithm | Python, NumPy, GDAL                                          |
| Canal/drainage model            | Python, NumPy, Manning's equation                            |
| Rainfall + infiltration         | Python, NumPy                                                |
| Visualization 2D                | Folium, GeoPandas                                            |
| Visualization 3D                | Deck.gl (WebGL)                                              |
| Dashboard / Web UI              | Flask or Streamlit                                           |
| Database                        | SQLite                                                       |
| Report generation               | ReportLab or Plotly                                          |
| Data sources                    | SRTM DEM (free), OSM (free), Dept. of Meteorology CSV (free) |
## What the Demo Looks Like  

On project exhibition day, we show:  

- **The rainfall slider** — drag to 150mm/hr  
- **Watch water accumulate** on the 2D map in real-time as the simulation runs  
- **Click Dematagoda** — see popup: "Floods to 0.45m depth at minute 38"  
- **Click "Scenario B"** — run a different rainfall pattern, compare results  
- **Download PDF report** for the Colombo MC showing flood hotspots  
- **(Stretch)** — 3D Colombo with water rising between buildings



