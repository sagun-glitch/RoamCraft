# RoamCraft — AI-Powered Travel Itinerary Generator

## Executive Summary
**RoamCraft** is an intelligent web application designed to simplify vacation planning. Powered by **Google Gemini 2.5 Flash** and built on a high-performance **Node.js & Express** backend, RoamCraft allows users to generate comprehensive, day-by-day travel itineraries in real-time streaming mode.

* **Live Web Application**: [https://roamcraft.onrender.com](https://roamcraft.onrender.com)
* **GitHub Repository**: [https://github.com/sagun-glitch/RoamCraft](https://github.com/sagun-glitch/RoamCraft)

---

## Key Features

1. **Real-Time AI Streaming (Server-Sent Events)**
   - Delivers instant markdown-formatted itinerary updates chunk-by-chunk without long loading waits.

2. **Customizable Trip Parameters**
   - **Destination Input**: Specify any city, country, or landmark worldwide.
   - **Duration Control**: Plan trips from 1 to 14 days.
   - **Budget Tiering**: Tailor recommendations to *Budget-friendly*, *Moderate*, or *Luxury*.
   - **Personalized Interests**: Tailor activities around local food, historical landmarks, nature, shopping, or nightlife.

3. **Interactive Day-by-Day Dashboard**
   - Expandable and collapsible daily timeline blocks.
   - Morning, Afternoon, and Evening schedule nodes.
   - Interactive packing checklist and local tips widgets.

4. **One-Click Export & Print**
   - Clean, formatted PDF/Print view with customized typography and layout.
   - One-click copy formatted text to clipboard.

5. **Clean & Responsive UI**
   - Built with Scandinavian Terracotta Sand & Slate aesthetic.
   - High-contrast, accessibility-focused interface without gradients or heavy glassmorphism.

---

## Technical Stack & Deployment

| Component | Technology | Description |
|---|---|---|
| **Live Deployment** | Render Cloud Hosting | Deployed live at `https://roamcraft.onrender.com` |
| **Backend Framework** | Node.js / Express.js | Handles REST API endpoints, static asset serving, and SSE streaming. |
| **AI Model** | Google Gemini 2.5 Flash (`@google/generative-ai`) | High-speed generative AI for crafting structured travel itineraries. |
| **Frontend UI** | HTML5, Vanilla CSS, JavaScript (ES6+) | Lightweight, fast client-side application with Lucide Icons & Google Fonts. |
| **Data Protocol** | Server-Sent Events (SSE) | Enables chunked real-time streaming output to the browser. |

---

## System Architecture Flow

```
[ User Input Form ] 
       │
       ▼ (POST /api/generate-itinerary)
[ Express Server (Render Cloud) ] ─── (Gemini API Request) ───► [ Google Gemini 2.5 Flash ]
       │                                                                   │
       ◄──────────────── (Chunked Stream Response / SSE) ──────────────────┘
       │
       ▼
[ Client UI Renderer ] (Interactive Markdown & Timeline View)
```

---

## API Endpoint Specification

### `POST /api/generate-itinerary`

#### Request Body (JSON)
```json
{
  "destination": "Paris, France",
  "days": 3,
  "budget": "Moderate",
  "interests": "museums, bakeries, evening walks"
}
```

#### Response Stream (`text/event-stream`)
```http
HTTP/1.1 200 OK
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive

data: {"text":"### Day 01: Arrival & Historic Heart\n* 09:00 - Notre Dame..."}

data: [DONE]
```

---

## Setup & Local Installation

### Prerequisites
- Node.js (v18.0.0 or higher)
- npm (v9.0.0 or higher)
- Google Gemini API Key ([Get a key from Google AI Studio](https://aistudio.google.com/))

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/sagun-glitch/RoamCraft.git
   cd RoamCraft
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure Environment Variables**
   Create a `.env` file in the project root:
   ```env
   PORT=3000
   GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
   ```

4. **Start the application**
   ```bash
   npm start
   ```
   Open `http://localhost:3000` in your web browser or access the live app at [https://roamcraft.onrender.com](https://roamcraft.onrender.com).

---

## Environment Variables & Security
- Never commit the `.env` file containing your actual API key to version control.
- Ensure `.env` is listed inside `.gitignore`.

---

## License & Credits
- **Author**: Sagun Mardi (`sagun-glitch`)
- **Live App**: [https://roamcraft.onrender.com](https://roamcraft.onrender.com)
- **License**: MIT
