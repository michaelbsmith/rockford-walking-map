# Rockford Walking Reach

An interactive map showing how far you can walk from any point in Rockford, Illinois, in a given time, and how that changes with walking speed and with avoiding stairs.

Click the map to set a starting point, then adjust:

- **Time budget** (5 to 30 minutes)
- **Walking speed** (0.8 to 1.8 m/s)
- **Avoid stairs** (step-free)

Streets you can reach are coloured by walking time. Streets reachable at 1.4 m/s with stairs allowed, but not with your settings, are shown in grey. The panel counts amenities (groceries, health, education, parks and playgrounds, cafés and restaurants) and benches within reach.

## How it works

Everything runs in the browser. `export_city.py` downloaded the walking network and points of interest from OpenStreetMap once and wrote them to `data/rockford/`. The page loads those files and runs the shortest-path search itself, so there is no server or routing service.

To regenerate the data:

```
pip install osmnx
python3 export_city.py "Rockford, Illinois, USA" rockford --name "Rockford, IL" --center 42.2711,-89.0940 --radius 8000
```

To run it locally, start a web server in this folder (opening `index.html` directly does not work):

```
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Limits

This is a prototype.

- Public transport, slope and street lighting are not included.
- Street and amenity data come from OpenStreetMap and are incomplete in places, particularly sidewalks.
- Amenities are matched to the nearest street intersection, and parks and larger buildings count as single points, so counts near the edge of the reach are approximate.
- Rockford has few mapped flights of steps, so the stair-avoidance option changes the result little.
- The map covers a 16 km square around downtown Rockford. Reach stops at its edge.

## Data and credits

Street and amenity data: © OpenStreetMap contributors, available under the Open Database Licence (<https://www.openstreetmap.org/copyright>). The files in `data/` are derived from that data and remain under the ODbL.

Basemap: © OpenFreeMap, © OpenMapTiles, data from OpenStreetMap.

Based on the open-source project "15 minutes. For whom?" by Martin Bangratz (MIT licence, see `LICENSE`). The `vendor/` folder holds unmodified copies of MapLibre GL JS (BSD-3-Clause) and the leaflet-maplibre-gl bridge (ISC), each with its own licence file. Leaflet is loaded from cdnjs.
 
