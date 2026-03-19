# 🛡️ ShieldMate
### *"When the storm hits, we've got you covered."*

> **Guidewire DEVTrails 2026** — AI-Powered Parametric Insurance for India's Gig Economy  
> **Team:** Innovatrix  
> **Persona:** Food Delivery Partners (Zomato / Swiggy)  
> **Platform:** Web (React) + Mobile (React Native)

---

## 📌 Table of Contents

1. [The Problem](#the-problem)
2. [Our Solution](#our-solution)
3. [Persona & Scenarios](#persona--scenarios)
4. [Application Workflow](#application-workflow)
5. [Weekly Premium Model](#weekly-premium-model)
6. [Parametric Triggers](#parametric-triggers)
7. [Platform Choice: Web + Mobile](#platform-choice-web--mobile)
8. [AI/ML Integration](#aiml-integration)
9. [Tech Stack](#tech-stack)
10. [Development Plan](#development-plan)
11. [API Integrations](#api-integrations)
12. [Architecture Overview](#architecture-overview)
13. [Folder Structure](#folder-structure)

---

## The Problem

India's food delivery partners (Zomato, Swiggy) are the invisible backbone of urban India. A typical delivery partner earns **₹15,000–₹25,000/month**, working 8–12 hour shifts, 6 days a week.

But they are completely exposed to external disruptions:

| Disruption | Frequency (India) | Avg. Income Lost |
|---|---|---|
| Heavy Rain / Floods | 40–60 days/year | ₹500–₹800/day |
| Extreme Heat (>42°C) | 20–30 days/year | ₹300–₹600/day |
| Severe Air Pollution (AQI >300) | 15–25 days/year | ₹400–₹700/day |
| Local Curfews / Bandhs | 5–10 days/year | ₹600–₹900/day |
| Platform Outages (Zomato/Swiggy) | 3–8 incidents/year | ₹300–₹500/day |

**The gap:** No existing insurance product addresses income loss for gig workers caused by parametric (measurable, verifiable) external events. When it rains, they lose money. Nobody pays them back.

**ShieldMate** closes that gap — automatically.

---

## Our Solution

**ShieldMate** is an AI-powered parametric income insurance platform for food delivery partners. It:

- **Monitors** real-time environmental and social disruption data (weather, AQI, curfews, platform status)
- **Triggers** automatic claims when measurable thresholds are breached — **zero paperwork**
- **Pays out** lost income directly to the worker's UPI/bank within minutes
- **Prices** coverage weekly, matching the gig economy's earnings cycle
- **Detects fraud** intelligently using GPS, activity patterns, and anomaly detection

> ⚠️ **Coverage Scope:** ShieldMate covers **INCOME LOSS ONLY**. No health, accident, vehicle repair, or life coverage is included or implied.

---

## Persona & Scenarios

### 👤 Primary Persona: Raju, Food Delivery Partner

> **Raju**, 28, Bengaluru. Delivers for Swiggy 10 hours/day, 6 days/week.  
> Average weekly earnings: **₹4,500**. Monthly: **₹18,000**.  
> No savings buffer. Family of 3 depends entirely on his daily income.

---

### 📖 Scenario 1 — The Monsoon Week

Raju wakes up Monday. IMD has issued a red alert — heavy rain all week in Bengaluru.  
Swiggy reduces order volume by 60%. Raju can only complete 4 deliveries instead of his usual 22.

**Without ShieldMate:** He loses ₹3,200 that week. No recourse.

**With ShieldMate:**
- OpenWeatherMap detects rainfall > 50mm/day in Raju's active zone
- ShieldMate's parametric engine automatically triggers a claim
- Claude AI validates the event against Raju's GPS activity logs
- ₹2,800 (70% of weekly coverage) is credited to his UPI within 2 hours
- He receives a push notification: *"Heavy rain detected in your zone. ₹2,800 credited to your account."*

---

### 📖 Scenario 2 — The Pollution Shutdown

Delhi, November. AQI hits 380 (Severe). The government bans outdoor activity 6am–10am.  
Raju's prime earning window is wiped out.

**With ShieldMate:**
- OpenAQ API detects AQI > 300 sustained for > 4 hours in Raju's pinned zone
- Partial payout (40% of daily rate) auto-triggers for restricted hours
- Fraud engine cross-checks: Raju's GPS shows he was stationary (not spoofing activity)
- ₹320 credited for the lost morning window

---

### 📖 Scenario 3 — Sudden Bandh

A local political bandh is called overnight in Pune. No pickups possible from 8am–2pm.  
Swiggy pauses operations in the affected zones.

**With ShieldMate:**
- Platform API (mock/Swiggy webhook) detects zone suspension
- ShieldMate cross-references with news/social signal API for bandh confirmation
- Curfew/social disruption trigger activates for affected workers in that zone
- Payout proportional to lost hours is processed automatically

---

### 📖 Scenario 4 — Attempted Fraud

A delivery partner tries to claim rain disruption, but GPS data shows they were actively moving between delivery points during the "rain event."

**ShieldMate's Response:**
- Fraud Detection Engine flags: GPS activity contradicts claimed disruption
- Claim auto-rejected with explanation
- Account risk score increases; flagged for manual review on next claim
- No payout processed

---

## Application Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                     SHIELDMATE WORKFLOW                     │
└─────────────────────────────────────────────────────────────┘

[1. ONBOARDING]
  Worker registers → KYC (Aadhaar/PAN mock) → Platform ID linked
  (Zomato/Swiggy partner ID) → Zone pinned (GPS) → Risk profile built

        ↓

[2. WEEKLY POLICY PURCHASE]
  AI calculates dynamic weekly premium → Worker reviews coverage
  → Pays via UPI/Razorpay sandbox → Policy active for 7 days

        ↓

[3. REAL-TIME MONITORING] ← runs continuously in background
  Weather API + AQI API + Platform Status + Social Signals
  → Parametric Engine evaluates thresholds every 15 minutes

        ↓

[4. TRIGGER DETECTION]
  Threshold breached (e.g., rain > 50mm) in worker's active zone
  → Event logged with timestamp, coordinates, severity score

        ↓

[5. CLAIM INITIATION] ← AUTOMATIC (zero-touch)
  Claim auto-created → Claude AI validates event vs. GPS activity
  → Fraud engine runs anomaly check → Risk score computed

        ↓

[6. PAYOUT OR REJECTION]
  ✅ Approved → UPI/Bank payout within 2 hours (Razorpay sandbox)
  ❌ Rejected → Worker notified with reason; appeal option available

        ↓

[7. DASHBOARD UPDATE]
  Worker Dashboard: coverage status, payouts received, risk score
  Admin Dashboard: loss ratios, claim trends, fraud flags, AQI/weather map
```

---

## Weekly Premium Model

### Why Weekly?

Food delivery partners operate on weekly payout cycles (Swiggy/Zomato pay weekly). A monthly or annual premium creates cash flow friction. Weekly pricing = seamless integration into their earnings rhythm.

### Premium Calculation Formula

```
Weekly Premium = Base Rate × Zone Risk Multiplier × Weather Risk Index
                 × Platform Risk Factor × Loyalty Discount

Where:
  Base Rate            = ₹49 (standard coverage, ₹3,500/week max payout)
  Zone Risk Multiplier = 0.8–1.5 (based on historical disruption data for that zone)
  Weather Risk Index   = 0.9–1.4 (based on IMD 7-day forecast at policy purchase)
  Platform Risk Factor = 0.95–1.2 (Swiggy/Zomato zone-level disruption history)
  Loyalty Discount     = 0.95 after 4 consecutive weeks, 0.90 after 8 weeks
```

### Pricing Tiers

| Plan | Weekly Premium | Max Weekly Payout | Coverage Triggers |
|---|---|---|---|
| **Basic Shield** | ₹29 | ₹1,500 | Rain, Extreme Heat |
| **Standard Shield** | ₹49 | ₹3,500 | Rain, Heat, AQI, Platform Outage |
| **Full Shield** | ₹79 | ₹6,000 | All triggers + Social/Curfew events |

### Payout Logic

```
Daily Payout = (Avg. Daily Earnings × Impact Severity %) × Coverage Factor

Impact Severity:
  Partial (2–4 hrs disrupted)  → 30% of daily rate
  Major   (4–7 hrs disrupted)  → 60% of daily rate
  Total   (7+ hrs disrupted)   → 90% of daily rate (capped at plan max)
```

> **Example:** Raju (Full Shield, avg. ₹700/day). Rain disrupts 6 hours → Major impact → Payout = ₹700 × 60% = ₹420 for that day.

---

## Parametric Triggers

All triggers are **objective, measurable, and API-verified** — no manual claim filing required.

| Trigger ID | Event Type | Threshold | Data Source | Coverage Impact |
|---|---|---|---|---|
| T-01 | Heavy Rain | Rainfall > 35mm/hr OR > 50mm/day | OpenWeatherMap | Major/Total |
| T-02 | Extreme Heat | Temperature > 42°C sustained 3+ hrs | OpenWeatherMap | Partial/Major |
| T-03 | Air Quality | AQI > 300 (Severe) for 4+ hrs | OpenAQ API | Partial/Major |
| T-04 | Floods | IMD flood alert Level 2+ in zone | IMD API (mock) | Total |
| T-05 | Platform Outage | Swiggy/Zomato zone suspended 2+ hrs | Platform Webhook (mock) | Partial/Major |
| T-06 | Curfew/Bandh | Verified government/social disruption | News API + manual admin flag | Major/Total |

### Trigger Validation Pipeline

```
Raw API Data → Zone Matching (Worker GPS Pin vs. Event Zone)
             → Duration Check (meets minimum time threshold?)
             → Severity Score (0–100)
             → Cross-reference with Worker Activity Log (GPS)
             → Fraud Score (0–100)
             → Decision: Auto-Approve / Flag for Review / Reject
```

---

## Platform Choice: Web + Mobile

### Why Both?

| Factor | Web (React) | Mobile (React Native) |
|---|---|---|
| **Primary Users** | Admin/Insurer dashboard | Delivery partners (on the go) |
| **Use Case** | Policy management, analytics | Onboarding, claim notifications, payouts |
| **Access** | Desktop/laptop browsers | Android-first (80%+ of delivery partners) |
| **Connectivity** | Stable broadband | 4G/low-bandwidth optimized |

**Web** serves the insurer/admin side — rich analytics, fraud review, policy configuration.  
**Mobile** serves the worker — fast onboarding, push notifications, one-tap claim review, instant payout confirmation.

### Shared Backend
Both platforms consume the same Node.js REST API, ensuring consistent data and business logic across surfaces.

---

## AI/ML Integration

### 1. 🤖 Dynamic Premium Calculation (Claude API)

At the time of weekly policy purchase, we call the Claude API with:
- Worker's zone historical disruption data
- IMD 7-day weather forecast for the zone
- Worker's claim history and activity patterns
- Platform (Zomato/Swiggy) zone-level performance data

Claude returns a **Risk Assessment JSON** with a recommended premium tier, risk score, and reasoning — which our Node.js engine uses to calculate the final weekly premium.

```javascript
// Example Claude API call for premium calculation
const riskPrompt = `
You are an insurance actuary AI for ShieldMate, a parametric income insurance platform for food delivery workers in India.

Worker Profile:
- Zone: ${worker.zone} (${worker.city})
- Avg Weekly Earnings: ₹${worker.avgWeeklyEarnings}
- Active Days/Week: ${worker.activeDaysPerWeek}
- Claim History (last 12 weeks): ${JSON.stringify(worker.claimHistory)}
- Zone Disruption History (last 6 months): ${JSON.stringify(zoneDisruptionData)}
- IMD 7-Day Forecast: ${JSON.stringify(weatherForecast)}

Calculate:
1. Zone Risk Score (0–100)
2. Worker Risk Score (0–100)  
3. Recommended Weekly Premium (₹29 / ₹49 / ₹79)
4. Suggested Coverage Cap for this week
5. Risk Reasoning (2–3 sentences)

Respond ONLY in JSON format.
`;

const response = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 1000,
    messages: [{ role: "user", content: riskPrompt }]
  })
});
```

---

### 2. 🔍 Intelligent Fraud Detection (Claude API + Rule Engine)

Every claim passes through a two-layer fraud detection system:

**Layer 1 — Rule-Based Engine (Node.js)**
- GPS location during event vs. claimed disruption zone
- Activity pattern: was the worker moving (delivering) during the "disruption"?
- Duplicate claim check: same event, same worker, same day
- Velocity check: >3 claims in 7 days → elevated scrutiny

**Layer 2 — Claude AI Fraud Analysis**

```javascript
const fraudPrompt = `
You are a fraud detection AI for ShieldMate insurance platform.

Claim Details:
- Trigger: ${claim.triggerType} at ${claim.timestamp}
- Worker Zone: ${worker.zone}
- Event Zone Coverage: ${eventData.zonesCovered}
- Worker GPS Log (last 4 hrs): ${JSON.stringify(worker.gpsLog)}
- Worker Activity Score: ${worker.activityScore} deliveries in the trigger window
- Historical Fraud Score: ${worker.fraudScore}
- Previous Claims (last 30 days): ${worker.recentClaims}

Assess:
1. Fraud Risk Score (0–100, where 100 = definite fraud)
2. Flags detected (list any suspicious patterns)
3. Recommendation: AUTO_APPROVE / MANUAL_REVIEW / AUTO_REJECT
4. Reasoning (2–3 sentences)

Respond ONLY in JSON format.
`;
```

---

### 3. 📊 Predictive Risk Modeling

- **Zone Risk Heatmap:** Built using 3 years of IMD historical weather data + claim patterns, visualized on the admin dashboard
- **Next-Week Disruption Forecast:** Claude API + OpenWeatherMap 7-day data predicts likely payout exposure for the coming week, helping the insurer manage reserves
- **Worker Churn Prediction:** ML model flags workers likely to lapse their policy (based on usage patterns), triggering proactive retention offers

---

## Tech Stack

### Frontend — Web
```
React 18          — UI framework
Vite              — Build tool
TailwindCSS       — Styling
Recharts          — Analytics dashboard charts
React Query       — API state management
React Router v6   — Navigation
Socket.io-client  — Real-time trigger notifications
```

### Frontend — Mobile
```
React Native 0.74    — Cross-platform mobile (Android-first)
Expo                 — Development & build tooling
NativeWind           — TailwindCSS for React Native
React Navigation     — Screen navigation
Expo Notifications   — Push notifications for claim alerts
Expo Location        — GPS zone pinning
```

### Backend — Node.js
```
Node.js 20 + Express.js   — REST API server
Prisma ORM                — Database abstraction
PostgreSQL                — Primary database
Redis                     — Caching (zone disruption events, session)
Bull Queue                — Background jobs (trigger polling, payout processing)
Socket.io                 — Real-time event broadcasting
JWT                       — Authentication
Zod                       — Request validation
```

### AI/ML
```
Anthropic Claude API (claude-sonnet-4-20250514)
  — Premium calculation
  — Fraud detection
  — Risk reasoning & narratives
  — Predictive disruption forecasting
```

### External APIs (All Free Tiers)
```
OpenWeatherMap API    — Real-time weather + 7-day forecast
OpenAQ API            — Real-time AQI data
Razorpay Sandbox      — Mock payment processing (UPI/bank payouts)
Abstract API          — Phone/email verification for onboarding
NewsData.io API       — Social disruption signal detection (bandhs/curfews)
```

### Infrastructure
```
Render.com      — Node.js backend hosting (free tier)
Supabase        — PostgreSQL + Auth (free tier)
Upstash         — Redis (free tier)
Vercel          — React web frontend hosting (free tier)
Expo EAS        — Mobile build & distribution
```

---

## Development Plan

### Phase 1 — Ideation & Foundation (Weeks 1–2) ✅ Current
- [x] Problem research & persona definition
- [x] Architecture design
- [x] Tech stack finalization
- [x] README documentation
- [ ] Basic project scaffolding (Node.js API + React Web + React Native)
- [ ] OpenWeatherMap + OpenAQ API integration (proof of concept)
- [ ] Claude API integration test (premium calculation prompt)
- [ ] 2-minute pitch video

### Phase 2 — Automation & Protection (Weeks 3–4)
- [ ] Full worker onboarding flow (Web + Mobile)
- [ ] Weekly policy creation with dynamic premium calculation
- [ ] Parametric trigger engine (5 triggers: T-01 to T-05)
- [ ] Automatic claim initiation pipeline
- [ ] Basic fraud detection (rule-based Layer 1)
- [ ] Razorpay sandbox payout integration
- [ ] Claims management dashboard (admin)
- [ ] 2-minute demo video

### Phase 3 — Scale & Optimise (Weeks 5–6)
- [ ] Claude AI fraud detection (Layer 2)
- [ ] Predictive risk heatmap (admin dashboard)
- [ ] Worker dashboard (earnings protected, active coverage)
- [ ] Social disruption trigger (T-06) with NewsData.io
- [ ] GPS spoofing detection
- [ ] Performance optimization (Redis caching, Bull queues)
- [ ] End-to-end disruption simulation demo
- [ ] Final pitch deck (PDF)
- [ ] 5-minute walkthrough video

---

## API Integrations

### OpenWeatherMap
```
Endpoint: api.openweathermap.org/data/2.5/weather
Use: Real-time rainfall (mm/hr), temperature, weather alerts
Polling: Every 15 minutes per active zone
Trigger: T-01 (Rain), T-02 (Heat), T-04 (Floods)
```

### OpenAQ
```
Endpoint: api.openaq.org/v2/latest
Use: Real-time AQI readings by city/coordinates
Polling: Every 30 minutes per active zone
Trigger: T-03 (Air Quality)
```

### Razorpay (Sandbox)
```
Use: Simulated UPI/bank payouts to workers
Flow: Claim approved → Razorpay payout API → Worker UPI credited
Mode: Test/sandbox — no real money moves
```

### Anthropic Claude API
```
Use: Premium calculation, fraud analysis, predictive forecasting
Model: claude-sonnet-4-20250514
Calls: On policy purchase (premium), on claim initiation (fraud)
```

### NewsData.io
```
Endpoint: newsdata.io/api/1/news
Use: Detect bandh/curfew news signals by city keyword
Trigger: T-06 (Social Disruptions)
```

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        SHIELDMATE ARCHITECTURE                  │
└─────────────────────────────────────────────────────────────────┘

  [React Web App]          [React Native App]
       │                          │
       └──────────┬───────────────┘
                  │ HTTPS / REST
                  ▼
        ┌─────────────────┐
        │  Node.js / Express│  ← JWT Auth, Zod Validation
        │     API Server    │
        └────────┬─────────┘
                 │
        ┌────────┴─────────────────────────────────┐
        │                                          │
        ▼                                          ▼
  ┌──────────┐                            ┌──────────────┐
  │PostgreSQL│                            │ Redis Cache  │
  │(Supabase)│                            │ (Upstash)    │
  └──────────┘                            └──────────────┘
        │
        ▼
  ┌─────────────────────┐
  │   Bull Queue (Jobs) │
  └──────┬──────────────┘
         │
    ┌────┴─────────────────────────────────────────┐
    │               Background Workers             │
    │                                              │
    │  [Trigger Poller]    [Payout Processor]      │
    │  OpenWeatherMap API  Razorpay Sandbox API    │
    │  OpenAQ API                                  │
    │  NewsData.io API                             │
    │                                              │
    │  [AI Engine]                                 │
    │  Claude API → Premium Calc + Fraud Score     │
    └──────────────────────────────────────────────┘
```

---

## Folder Structure

```
shieldmate/
├── packages/
│   ├── api/                    # Node.js Express backend
│   │   ├── src/
│   │   │   ├── routes/         # REST API routes
│   │   │   ├── services/       # Business logic
│   │   │   │   ├── premium/    # Premium calculation + Claude AI
│   │   │   │   ├── triggers/   # Parametric trigger engine
│   │   │   │   ├── fraud/      # Fraud detection engine
│   │   │   │   └── payouts/    # Razorpay integration
│   │   │   ├── jobs/           # Bull queue workers
│   │   │   ├── middleware/     # Auth, validation
│   │   │   └── prisma/         # DB schema & migrations
│   │   └── package.json
│   │
│   ├── web/                    # React web (Admin + Worker portal)
│   │   ├── src/
│   │   │   ├── pages/          # Dashboard, Policy, Claims, Analytics
│   │   │   ├── components/     # Shared UI components
│   │   │   ├── hooks/          # React Query hooks
│   │   │   └── lib/            # API client, utils
│   │   └── package.json
│   │
│   └── mobile/                 # React Native (Worker app)
│       ├── app/                # Expo Router screens
│       │   ├── onboarding/     # Registration, KYC, zone setup
│       │   ├── policy/         # Buy/renew weekly plan
│       │   ├── claims/         # Active claims, history
│       │   └── dashboard/      # Worker earnings & coverage
│       └── package.json
│
├── README.md
└── package.json                # Monorepo root (npm workspaces)
```

---

## 🏁 What Makes ShieldMate Different

| Feature | Traditional Insurance | ShieldMate |
|---|---|---|
| Claim Process | Manual, 7–30 days | Automatic, 2 hours |
| Premium Timing | Monthly/Annual | Weekly (gig-aligned) |
| Pricing Logic | Static | AI-Dynamic (zone + weather + behavior) |
| Coverage Trigger | Self-reported | Parametric (API-verified, objective) |
| Fraud Detection | Manual review | AI + GPS + activity analysis |
| Worker Experience | Complex forms | Zero-touch, push notification |

---

## Team Innovatrix

> Building financial safety nets for India's invisible workforce.

---

*ShieldMate — Phase 1 Submission | Guidewire DEVTrails 2026*
