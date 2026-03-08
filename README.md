# Tata Nexon EV — Live Trip Tracker

A GitHub Pages-ready website showcasing live EV trip tracking with interactive route maps and comprehensive analytics dashboard.

## Quick Start

Simply open `index.html` in any modern web browser. No installation or build process required.

### Live Location Updates

To enable live tracking, update `data/live_location.json` with current vehicle data:

```json
{
  "latitude": 19.1136,
  "longitude": 72.8691,
  "timestamp": "2026-03-07T15:42:00Z",
  "speed": 65,
  "soc": 78,
  "odometer": 2450,
  "status": "driving",
  "address": "Bangalore, Karnataka"
}
```

The website polls this file every 30 seconds and updates the live location marker on the map and status indicator in the header.

## Features

### Route Map Tab
- Interactive D3.js map showing all 11 completed trips
- Live vehicle location with pulsing red marker
- Click any trip to isolate it
- Scroll to zoom, click background to reset
- Total distance and charge session statistics

### Dashboard Tab
- Trip statistics and KPIs
- Multiple analytical charts:
  - Distance traveled over time
  - Energy consumption breakdown
  - Speed distribution analysis
  - Efficiency metrics
  - Usage patterns by time of day

### Live Status Indicator
- Green pulsing dot indicates online vehicle
- Status display: Driving / Charging / Parked
- Current location address
- Time since last update

## Data Files

| File | Purpose | Format |
|------|---------|--------|
| `index.html` | Main website | HTML5 + React + D3.js |
| `data/ev_trips.json` | Trip history | JSON array of trip objects |
| `data/live_location.json` | Current vehicle position | JSON object |

## Deployment to GitHub Pages

1. Copy this entire `ev-tracker/` folder to your GitHub Pages repository
2. Push to your `gh-pages` branch or master branch (depending on your repo settings)
3. Access at `https://yourusername.github.io/ev-tracker/`

## API Integration

To integrate with a live vehicle API:

1. Replace the fetch call in `index.html` that loads `live_location.json`
2. Or set up a backend endpoint that updates `data/live_location.json` regularly

The relevant polling code in `index.html`:
```javascript
fetch('./data/live_location.json?' + Date.now())
  .then(r => r.json())
  .then(data => {
    if (data.latitude && data.longitude) {
      setLiveLocation(data);
      setLastUpdate(new Date());
    }
  })
```

## Technical Stack

- **Frontend:** React 18 (CDN)
- **Mapping:** D3.js v7
- **Charts:** Recharts 2.10
- **Styling:** Inline CSS with Tailwind-inspired utilities
- **Data:** Static JSON files

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Customization

### Update Vehicle Info
Edit the header section in `index.html`:
- Battery capacity (currently "29 kWh")
- Date range (currently "Dec 2025 — Mar 2026")
- Vehicle name/title

### Modify Colors
All colors are CSS hex values in the `<style>` tag:
- Background: `#0a0b0f` (dark)
- Primary: `#3b82f6` (blue)
- Live indicator: `#22c55e` (green)
- Live vehicle: `#ef4444` (red)

### Add New Data
Replace `data/ev_trips.json` with your own trip history data.

## Performance

- **File Size:** ~330 KB total (self-contained)
- **Load Time:** <2 seconds on typical broadband
- **Polling:** 30-second interval for live location
- **No external API calls** (except CDN libraries)

## Troubleshooting

### Live location marker not showing
- Ensure `data/live_location.json` has valid `latitude` and `longitude` values
- Check browser console for fetch errors
- Verify CORS if serving from subdirectory

### Map not rendering
- Clear browser cache and reload
- Check that D3.js loaded from CDN
- Verify JSON data structure in `ev_trips.json`

### Charts not displaying
- Verify Recharts library loaded from CDN
- Check that trip data has required fields
- Open browser dev tools console for error messages

## License

This website was generated from React components. All source data and code are original.

---

Built with React, D3.js, and Recharts for the Tata Nexon EV journey.
