# Genspire — Build & Connect 🚀

> **Where startup builders meet, collaborate, and ship.**

Genspire is a professional network built specifically for builders — founders, developers, and designers who are actively creating something. Unlike formal professional networks, Genspire combines a social portfolio, AI-powered discovery, and live voice collaboration into one platform.

**Your next co-founder is one conversation away.**

[<img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" height="50">](https://play.google.com/store/apps/details?id=app.genspire)

---

## ✨ Core Features

### 🧠 AI-Powered Semantic Search & Personalized Feed
The most technically sophisticated feature of Genspire. Rather than keyword matching, search and discovery use vector embeddings:

- Builder profiles and project documents are automatically vectorized using **Google Gemini AI (embedding-001)** via Cloud Function triggers
- Search computes **cosine similarity** across the full index, returning the top 30 ranked results (projects + builders) with a similarity threshold filter
- A personalized **"For You" feed** matches your intent vector — captured during onboarding — against other builders' project vectors, with human-readable match explanations (e.g. "Looking for a co-founder", "Wants feedback")

### 🎙️ Multi-Room Live Voice Lounges
Real-time audio rooms organized by topic — App Dev, AI & ML, Startups, Game Dev:

- Powered by **Agora RTC** with automatic audio routing and hardware speaker/earpiece toggling
- Real-time network quality badges (Excellent, Good, Fair, Poor) based on live uplink/downlink metrics
- Rooms capped at 10 participants with **Firestore-managed waitlists** — Cloud Functions automatically notify the next user via FCM when a spot opens
- Schedule voice sessions up to 7 days ahead. Interested users receive automated FCM reminders 10 minutes before start
- Floating mini-player keeps voice channels alive when the app is backgrounded
- Automated background worker cleans up empty inactive rooms every 5 minutes

### 📦 Offline-First Architecture
Genspire loads instantly regardless of connectivity:

- **Cache-then-network** strategy: feeds load from local SQLite in milliseconds, then silently refresh from Firestore in the background
- Silent FCM push notifications trigger a background isolate to sync fresh data to SQLite without interrupting the UI
- Write operations blocked client-side during offline state to prevent failed sync attempts

### 💬 Rich Messaging
- **1:1 Direct Chat** with voice messages, compressed image attachments, file sharing, atomic message reactions, and reply threading
- **Builders Hub** — a global real-time chat room with server-side rate limiting via Cloud Functions
- In-memory display name cache eliminates redundant Firestore reads during chat rendering

### 🤝 Connections & Trust Vouches
- Connection requests include project context, role sought, and custom message
- Vouch counts managed exclusively server-side to prevent client manipulation
- Disconnecting a user cleans up connection documents, chat rooms, and all associated media via Cloud Functions

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | Riverpod |
| Navigation | GoRouter |
| AI / ML | Google Gemini AI (embedding-001) — Vector Embeddings, Semantic Search |
| Real-Time Audio | Agora RTC |
| Database | Firebase Firestore + Firebase Realtime Database |
| Local Storage | SQLite (offline-first cache) |
| Authentication | Firebase Auth |
| Media Storage | Firebase Storage |
| Push Notifications | Firebase Cloud Messaging (FCM) |
| Backend Logic | Firebase Cloud Functions (TypeScript) |

---

## 🏗️ Architecture Highlights

```
Offline-First Flow:
SQLite Cache (instant) → UI renders → Firestore fetch → Cache update

AI Search Flow:
User query → Gemini embedding → Cosine similarity → Ranked results

Voice Room Flow:
Agora RTC session → Firestore participant list → Realtime DB presence → FCM notifications
```

---

## 📂 Project Structure

```
lib/
├── main.dart                  # Parallelized startup, global error handling
├── app_router.dart            # GoRouter with onboarding and auth guards
├── app_theme.dart             # HSL brand palette, semantic theme extensions
├── controllers/               # Page controllers and state notifier classes
├── data/                      # Static schemas (roles, skills)
├── models/                    # Immutable data models (User, Build, Chat, VoiceRoom)
├── providers/                 # Riverpod providers for auth, theme, caching
├── repositories/              # Cache-then-network sync layer
├── services/                  # Background services (FCM, Agora, SQLite, Errors)
├── screens/                   # Lounges, feeds, profiles, discovery
└── widgets/                   # Waveforms, autocomplete, skeleton loaders

functions/                     # Firebase Cloud Functions (TypeScript)
├── src/
│   ├── index.ts               # Entry point and exports
│   ├── search.ts              # Gemini vectorization and semantic search
│   ├── voiceLounge.ts         # Room management, waitlists, reminders
│   ├── messaging.ts           # Hub rate limiting, disconnect cleanup
│   └── vouches.ts             # Server-side vouch count management
```

---

## 🎨 Visual Identity

Genspire uses a tech-forward HSL color palette with full light and dark mode support:

| Role | Light Mode | Dark Mode |
|---|---|---|
| Primary (Teal) | `#0D9488` | `#2DD4BF` |
| Secondary | `#5EEAD4` | `#99F6E4` |
| Accent (Amber) | `#F59E0B` | `#FBBF24` |
| Background | `#FAFAFA` | `#0F1419` |
| Surface | `#FFFFFF` | `#1C1F24` |

Stage colors — Idea (Teal), Building (Amber), Launched (Emerald), Scaling (Violet) — reflect a builder's journey from concept to growth.

---

## 📱 Platform
- **Android** — Live on Google Play Store
- Firebase project hosted in `asia-southeast1` for optimal latency in South/Southeast Asia

---

## 📲 Download

Available on Google Play Store:
**[play.google.com/store/apps/details?id=app.genspire](https://play.google.com/store/apps/details?id=app.genspire)**

---

## 👨‍💻 Developer

Built solo by **Abubakar Qazi** — Flutter developer based in Islamabad, Pakistan.

[GitHub](https://github.com/abubakar-qazi) · [LinkedIn](https://linkedin.com/in/abubakar-qazi-6b9934311)
