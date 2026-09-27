# ⚡ VoltGo — Electric Vehicle Companion App

> Internship Project | Frontend Web Application | EV Charging Management

---

## 📋 Project Overview

VoltGo is a mobile-responsive web application designed to help electric vehicle (EV) owners manage their charging experience. Built as a single-page application (SPA) using plain HTML, CSS, and JavaScript — no frameworks required.

---

## ✅ Features

### 1. 🗺️ Nearest Station Finder
- Interactive simulated map with pin markers
- Live station list with distance, availability status, and connector types
- Color-coded availability (green / yellow / red)
- One-tap "Navigate" button per station
- Location search bar

### 2. 🚨 SOS Emergency Signal
- Large, accessible SOS button with animated pulse ring
- Sends GPS coordinates + vehicle data to emergency contacts (simulated)
- Saved contacts: Roadside Assist, Family, Hospital
- Individual "Call" buttons per contact
- Status alert banner after activation

### 3. 💳 Payment
- Live card display (updates as user types)
- Secure-style form: card number, name, expiry, CVV
- Session cost summary breakdown (session time + fast-charge fee + platform fee)
- Transaction history with date, location, and amount

### 4. 🔌 Charge Type Filter
- Filter chips: All / AC Slow / DC Fast / CCS2 / CHAdeMO / Type 2 / Bharat AC/DC
- Cards for each charger type showing: speed, description, compatible vehicles, price per kWh
- Instant filter — no page reload

---

## 🗂️ Project Structure

```
ev-project/
├── index.html      ← Main application (all features in one file)
└── README.md       ← This file
```

> All CSS and JavaScript are embedded in `index.html` for simplicity. In a production build, split into `styles.css` and `app.js`.

---

## 🚀 How to Run

```bash
# Option 1: Open directly in a browser
open index.html

# Option 2: Run a local server (recommended)
npx serve .
# or
python3 -m http.server 8080
# then visit http://localhost:8080
```

---

## 📱 Mobile Responsiveness

- Fully responsive layout using CSS Grid and Flexbox
- Fixed bottom navigation bar with 5 tabs
- `viewport-fit=cover` for edge-to-edge mobile display
- `env(safe-area-inset-*)` for notch-safe padding
- Tested at 375px (iPhone SE), 390px (iPhone 14), 412px (Android)

---

## 🔌 API Endpoints (Integration Guide)

The following endpoints are ready to be connected. Replace the simulated data in `index.html` with real API calls.

| Feature | Method | Endpoint | Description |
|---|---|---|---|
| Station Finder | `GET` | `/api/stations?lat={lat}&lng={lng}&radius=5000` | Returns nearby stations with availability |
| Station Detail | `GET` | `/api/stations/{id}` | Single station info + charger types |
| SOS Alert | `POST` | `/api/sos/alert` | Send SOS with GPS + vehicle ID |
| Emergency Contacts | `GET` | `/api/user/contacts` | Fetch saved emergency contacts |
| Create Payment | `POST` | `/api/payments/charge` | Initiate payment session |
| Payment History | `GET` | `/api/payments/history` | User's transaction log |
| Charger Types | `GET` | `/api/chargers/types` | All available charger specs |

### Example API Call (Station Finder)

```javascript
async function fetchNearbyStations(lat, lng) {
  const response = await fetch(`/api/stations?lat=${lat}&lng=${lng}&radius=5000`, {
    headers: {
      'Authorization': 'Bearer YOUR_TOKEN',
      'Content-Type': 'application/json'
    }
  });
  const data = await response.json();
  return data.stations;
}
```

### Example API Call (SOS)

```javascript
async function sendSOS(userId, lat, lng, batteryLevel) {
  await fetch('/api/sos/alert', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ userId, lat, lng, batteryLevel, timestamp: Date.now() })
  });
}
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| HTML5 | Structure and semantic markup |
| CSS3 | Styling, animations, responsive layout |
| Vanilla JavaScript | Interactivity, DOM manipulation |
| Google Fonts | Typography (Space Grotesk + Inter) |

---

## 🎨 Design System

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0a0f1e` | Page background |
| `--surface` | `#111827` | Section backgrounds |
| `--card` | `#1a2236` | Card backgrounds |
| `--accent` | `#00e5a0` | Primary green — CTAs, highlights |
| `--accent2` | `#3b82f6` | Blue — map, secondary actions |
| `--danger` | `#ef4444` | SOS, errors |
| `--warn` | `#f59e0b` | Low availability warning |
| Heading font | Space Grotesk (700) | All headings |
| Body font | Inter (400/500) | All body text |

---

## 👩‍💻 Author

Built as an internship project demonstrating:
- Mobile-first responsive design
- Multi-feature single-page application
- API-ready architecture
- Real-world EV use cases

---

## 📄 License

MIT — Free to use for educational and internship purposes.
