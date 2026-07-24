# RoamCraft — Simple AI-Powered Travel Itinerary Generator

> **Live Web Application**: [https://roamcraft.onrender.com](https://roamcraft.onrender.com)  
> **GitHub Repository**: [https://github.com/sagun-glitch/RoamCraft](https://github.com/sagun-glitch/RoamCraft)

---

## 1. Executive Summary

**RoamCraft** is a lightweight, AI-driven vacation planning platform built with **Node.js, Express, and Google Gemini 2.5 Flash**. It generates comprehensive, day-by-day travel itineraries delivered via **Server-Sent Events (SSE)** real-time streaming based on user destination, duration, budget tier, and custom activity preferences.

---

## 2. Key Highlights & Features

* **⚡ Real-Time Streaming Output**: Delivers instant markdown-formatted itinerary updates chunk-by-chunk using Server-Sent Events (SSE), eliminating long loading delays.
* **🎯 Precision Personalization**: Tailors daily itineraries based on budget tier (*Budget-friendly*, *Moderate*, *Luxury*) and custom interest preferences (e.g. food tours, historical places, beaches, hiking).
* **📅 Interactive Timeline & Checklist**: Renders structured day blocks with morning/afternoon/evening schedules, interactive packing checkboxes, and local travel tips.
* **📄 One-Click Export & Printing**: Integrated print/PDF engine formats custom itineraries into clean, styled documents.
* **🎨 Modern Dashboard Design**: Engineered with a Scandinavian Terracotta Sand & Slate minimalist aesthetic—strictly NO gradients and NO glassmorphism for maximum legibility and contrast.

---

## 3. Technical Stack & Deployment

| Layer | Technology | Details |
|---|---|---|
| **Live Hosting** | Render Cloud Platform | Deployed live at `https://roamcraft.onrender.com` |
| **Backend Engine** | Node.js (v18+) / Express.js | Manages REST endpoints, static file serving, and SSE streaming pipeline |
| **Generative AI** | Google Gemini 2.5 Flash (`@google/generative-ai`) | High-speed LLM configured with structured system prompts and streaming API |
| **Frontend UI** | HTML5, Vanilla CSS, Vanilla JavaScript (ES6+) | Modern dashboard UI built with Space Grotesk & IBM Plex fonts, and Lucide Icons |
| **Streaming Protocol** | Server-Sent Events (SSE) | HTTP streaming for progressive chunk rendering in client UI |

---

## 4. System Architecture

```
┌─────────────────────────┐
│   User Browser (UI)     │
└────────────┬────────────┘
             │ 1. POST /api/generate-itinerary (JSON Payload)
             ▼
┌─────────────────────────┐
│ Express Server (Render) │
└────────────┬────────────┘
             │ 2. generateContentStream(prompt)
             ▼
┌─────────────────────────┐
│  Google Gemini API      │ (gemini-2.5-flash)
└────────────┬────────────┘
             │ 3. Chunked SSE Stream Data
             ▼
┌─────────────────────────┐
│   User Browser (UI)     │ ──► Progressive Markdown Rendering & Timeline Node View
└─────────────────────────┘
```

---

## 5. API Endpoint Reference

### `POST /api/generate-itinerary`

#### Request Payload (`application/json`)
```json
{
  "destination": "Rome, Italy",
  "days": 3,
  "budget": "Moderate",
  "interests": "historic ruins, authentic pasta, neighborhood walks"
}
```

#### Response Stream (`text/event-stream`)
```http
HTTP/1.1 200 OK
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive

data: {"text":"### Day 01: Ancient Colosseum & Forum\n* 09:00 - Colosseum: Morning guided historical tour.\n"}

data: [DONE]
```

---

## 6. Local Development & Deployment

### Environment Setup
Create a `.env` file in the project root:
```env
PORT=3000
GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
```

### Installation Commands
```bash
# 1. Clone repository
git clone https://github.com/sagun-glitch/RoamCraft.git

# 2. Install dependencies
cd RoamCraft
npm install

# 3. Start application
npm start
```
Access the application at `http://localhost:3000` or visit the live cloud deployment at `https://roamcraft.onrender.com`.

---

## 7. Metadata & Credits

* **Project Name**: RoamCraft
* **Author / Owner**: Sagun Mardi (`sagun-glitch`)
* **Live Application**: [https://roamcraft.onrender.com](https://roamcraft.onrender.com)
* **Source Repository**: [https://github.com/sagun-glitch/RoamCraft](https://github.com/sagun-glitch/RoamCraft)
* **License**: MIT
