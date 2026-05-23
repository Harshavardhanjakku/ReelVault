<div align="center">

<img src="https://img.shields.io/badge/ReelVault-v2.0-0095f6?style=for-the-badge&logo=firebase&logoColor=white" alt="ReelVault" />

# 🎬 ReelVault

### *Save, organize, and revisit your favorite reels — instantly.*

<p>
  <img src="https://img.shields.io/badge/Firebase-Firestore-FFCA28?style=flat-square&logo=firebase&logoColor=black" />
  <img src="https://img.shields.io/badge/Vanilla_JS-ES2022-F7DF1E?style=flat-square&logo=javascript&logoColor=black" />
  <img src="https://img.shields.io/badge/HTML5-Single_File-E34F26?style=flat-square&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/CSS3-Dark_Mode-1572B6?style=flat-square&logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" />
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square" />
</p>

<br/>

> A **production-ready**, single-file web app to bookmark Instagram/social reels with categories, notes, real-time search, dark mode, duplicate detection, and CSV/TXT export — all powered by Firebase Firestore.

<br/>

[🚀 Live Demo](#) · [📦 Download](#installation) · [🐛 Report Bug](issues) · [✨ Request Feature](issues)

---

</div>

## 📋 Table of Contents

- [🎬 ReelVault](#-reelvault)
    - [*Save, organize, and revisit your favorite reels — instantly.*](#save-organize-and-revisit-your-favorite-reels--instantly)
  - [📋 Table of Contents](#-table-of-contents)
  - [✨ Features](#-features)
  - [🖼️ Screenshots](#️-screenshots)
  - [🏗️ Architecture](#️-architecture)
  - [⚡ Tech Stack](#-tech-stack)
  - [🚀 Installation](#-installation)
    - [Option A — Direct use (30 seconds)](#option-a--direct-use-30-seconds)
    - [Option B — Clone and serve](#option-b--clone-and-serve)
    - [Option C — Deploy to Firebase Hosting](#option-c--deploy-to-firebase-hosting)
  - [🔥 Firebase Setup](#-firebase-setup)
    - [Firestore Security Rules (recommended)](#firestore-security-rules-recommended)
  - [📁 Project Structure](#-project-structure)
  - [🔄 Data Flow](#-data-flow)
  - [🧩 Component Map](#-component-map)
  - [📊 Firestore Schema](#-firestore-schema)
  - [⌨️ Keyboard Shortcuts](#️-keyboard-shortcuts)
  - [🌙 Dark Mode](#-dark-mode)
  - [📤 Export System](#-export-system)
  - [🛡️ Security Notes](#️-security-notes)
  - [🗺️ Roadmap](#️-roadmap)
  - [🤝 Contributing](#-contributing)
  - [📄 License](#-license)

---

## ✨ Features

<table>
<tr>
<td>

**Core**
- ✅ Save reel links & text notes
- ✅ Auto-detects links vs plain notes
- ✅ Duplicate detection with live warning
- ✅ Delete / unsave instantly

</td>
<td>

**Organization**
- ✅ 8 category tags (Travel, Food, Tech…)
- ✅ Optional per-reel notes
- ✅ Formatted save dates
- ✅ Sort by newest / oldest / A→Z

</td>
</tr>
<tr>
<td>

**Search & Filter**
- ✅ Real-time full-text search
- ✅ Category filter chips
- ✅ Combined search + category filter
- ✅ Live result count

</td>
<td>

**UX & Performance**
- ✅ Dark / Light mode (persisted)
- ✅ LocalStorage cache → instant load
- ✅ Staggered card animations
- ✅ Mobile-first responsive layout

</td>
</tr>
<tr>
<td>

**Productivity**
- ✅ One-click Copy Link
- ✅ Export as TXT or CSV
- ✅ `Ctrl/⌘ + K` to open Add modal
- ✅ `Escape` to close modal

</td>
<td>

**Dashboard**
- ✅ Total saved count
- ✅ Saved today counter
- ✅ Active categories count
- ✅ Links vs notes split

</td>
</tr>
</table>

---

## 🖼️ Screenshots

| Light Mode | Dark Mode |
|:---:|:---:|
| *(Clean white card UI with gradient FAB)* | *(Deep black surface with accent colors)* |

| Add Modal | Category Filter |
|:---:|:---:|
| *(Slide-up modal with dupe detection)* | *(Horizontal scrolling chip row)* |

---

## 🏗️ Architecture

```mermaid
flowchart TB
    subgraph Client["🖥️ Client — Single HTML File"]
        direction TB
        UI["UI Layer\nHTML + CSS3"]
        JS["Logic Layer\nVanilla JS ES2022"]
        LS["LocalStorage\nCache Layer"]
        UI <--> JS
        JS <--> LS
    end

    subgraph Firebase["🔥 Firebase Cloud"]
        direction TB
        FS["Cloud Firestore\nreels collection"]
        AUTH["Firebase Auth\n(optional / future)"]
    end

    JS -- "addDoc / deleteDoc / getDocs" --> FS
    FS -- "snapshot data" --> JS
    LS -- "instant cache read" --> JS

    style Client fill:#0f172a,stroke:#0095f6,color:#f1f5f9
    style Firebase fill:#1c1917,stroke:#FFCA28,color:#fef3c7
```

---

## ⚡ Tech Stack

| Layer | Technology | Why |
|---|---|---|
| **Frontend** | HTML5 + CSS3 + Vanilla JS | Zero build step, instant deploy, no framework bloat |
| **Database** | Firebase Firestore | Real-time, scalable NoSQL, free tier generous |
| **Auth** | Firebase Auth *(roadmap)* | Google Sign-in for multi-user support |
| **Caching** | `localStorage` | Sub-millisecond cache reads before network |
| **Fonts** | DM Sans + DM Serif Display | Premium pairing, loaded from Google Fonts |
| **Hosting** | Any static host (GitHub Pages, Netlify, Firebase Hosting) | Single `.html` file — no server required |

---

## 🚀 Installation

### Option A — Direct use (30 seconds)

```bash
# 1. Download the file
curl -O https://your-host/saved-reels-app.html

# 2. Open in browser
open saved-reels-app.html
```

### Option B — Clone and serve

```bash
git clone https://github.com/yourusername/reelvault.git
cd reelvault

# Serve locally (Python)
python3 -m http.server 8080

# OR with Node
npx serve .
```

Then open `http://localhost:8080/saved-reels-app.html`

### Option C — Deploy to Firebase Hosting

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Set public directory, copy file in
firebase deploy
```

---

## 🔥 Firebase Setup

```mermaid
sequenceDiagram
    autonumber
    actor Dev as 🧑‍💻 Developer
    participant FP as Firebase Console
    participant FS as Firestore
    participant App as ReelVault App

    Dev->>FP: Create new project
    FP-->>Dev: Project created
    Dev->>FP: Enable Firestore (production mode)
    FP-->>FS: Database provisioned
    Dev->>FP: Register Web App
    FP-->>Dev: firebaseConfig object
    Dev->>App: Paste config into <script>
    App->>FS: initializeApp(config)
    FS-->>App: Connection established ✅
    App->>FS: db.collection("reels").get()
    FS-->>App: Documents returned
```

**Step-by-step:**

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. **Create Project** → name it (e.g. `reel-vault`)
3. Firestore Database → **Create database** → Start in **test mode**
4. Project Settings → **Add App** → Web `</>`
5. Copy your `firebaseConfig` and replace in the HTML:

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

### Firestore Security Rules (recommended)

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reels/{reelId} {
      // Public read/write for single-user app
      allow read, write: if true;

      // OR lock to authenticated users (after adding Auth):
      // allow read, write: if request.auth != null;
    }
  }
}
```

---

## 📁 Project Structure

```
reelvault/
│
├── saved-reels-app.html          # ← Entire app (HTML + CSS + JS)
│   ├── <style>                   #   All CSS with CSS custom properties
│   ├── <body>                    #   Topbar, Stats, Controls, Cards, Modal, FAB
│   └── <script>                  #   All JS logic (plain script, no modules)
│
├── README.md                     # This file
└── .firebaserc                   # Firebase project alias (if using CLI)
```

> **Design decision:** Everything in one `.html` file makes deployment trivially simple — copy one file anywhere and it works. No build step, no node_modules, no bundler.

---

## 🔄 Data Flow

```mermaid
flowchart LR
    subgraph Input["📥 User Input"]
        A[/"User types\nreel URL"/]
        B[/"Selects\ncategory"/]
        C[/"Adds\nnote (opt)"/]
    end

    subgraph Validation["🛡️ Validation Layer"]
        D{Empty\ncheck}
        E{Duplicate\ndetection}
    end

    subgraph Write["✍️ Write Path"]
        F["addDoc()\nFirestore"]
        G["Optimistic\nUI update"]
        H["Persist\nlocalStorage"]
    end

    subgraph Display["🖥️ Display"]
        I["renderList()"]
        J["updateStats()"]
        K["Show toast\nconfirmation"]
    end

    A --> D
    B --> D
    C --> D
    D -- "empty" --> L["⚠️ Toast warning"]
    D -- "valid" --> E
    E -- "dupe" --> M["🟡 Banner + disable save"]
    E -- "unique" --> F
    F --> G
    G --> H
    H --> I
    I --> J
    J --> K

    style Input fill:#1e3a5f,stroke:#0095f6,color:#e0f2fe
    style Validation fill:#3b1f1f,stroke:#ff3b30,color:#fee2e2
    style Write fill:#1a3320,stroke:#34c759,color:#dcfce7
    style Display fill:#2d1f3d,stroke:#af52de,color:#f3e8ff
```

---

## 🧩 Component Map

```mermaid
graph TD
    APP["🎬 ReelVault App"]

    APP --> TOPBAR["📌 Topbar\n─────────\nBrand logo\nExport menu\nDark mode toggle"]
    APP --> STATS["📊 Stats Row\n─────────\nTotal · Today\nCategories · Links"]
    APP --> CONTROLS["🔍 Controls\n─────────\nSearch input\nCategory chips"]
    APP --> SORTROW["↕️ Sort Row\n─────────\nResult count\nSort selector"]
    APP --> LIST["🃏 Card List\n─────────\nDynamic card grid\nEmpty state UI\nLoading spinner"]
    APP --> FAB["➕ FAB Button\n─────────\nFloating action\nOpens Add modal"]
    APP --> MODAL["💬 Add Modal\n─────────\nLink input\nCategory select\nNote textarea\nDupe warning"]
    APP --> TOAST["🔔 Toast\n─────────\nGlobal notifications\nAuto-dismiss"]

    LIST --> CARD["📇 Reel Card\n─────────\nThumb / fallback\nTitle + badge\nNote + date\nOpen · Copy · Remove"]

    style APP fill:#0f172a,stroke:#0095f6,color:#38bdf8
    style CARD fill:#1c1917,stroke:#ff9500,color:#fef3c7
```

---

## 📊 Firestore Schema

```mermaid
erDiagram
    REELS_COLLECTION {
        string  id          "Auto-generated document ID"
        string  text        "Reel URL or plain note"
        string  category    "Travel | Food | Fashion | Tech | Fitness | Music | Comedy | Other"
        string  note        "Optional user annotation"
        number  created     "Unix timestamp (ms) — Date.now()"
    }
```

**Example document:**

```json
{
  "id": "xK9mP2qRtAb7vNcL",
  "text": "https://www.instagram.com/reel/C8xYzAbCdEf/",
  "category": "Food",
  "note": "Amazing pasta recipe, try this weekend",
  "created": 1718188800000
}
```

**Firestore path:** `reels/{auto-id}`

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + K` / `⌘ + K` | Open "Add Reel" modal |
| `Escape` | Close modal |
| `Tab` | Navigate form fields |
| `Enter` | Submit form (inside modal) |

---

## 🌙 Dark Mode

```mermaid
stateDiagram-v2
    [*] --> CheckStorage: App loads
    CheckStorage --> LightMode: localStorage = "light"\nor no value
    CheckStorage --> DarkMode: localStorage = "dark"

    LightMode --> DarkMode: User clicks toggle
    DarkMode --> LightMode: User clicks toggle

    DarkMode --> SaveDark: Persist to localStorage
    LightMode --> SaveLight: Persist to localStorage

    SaveDark --> DarkMode
    SaveLight --> LightMode
```

Implementation uses a single `data-theme` attribute on `<html>` and CSS custom properties — no class toggling, no JS style manipulation. Every color adapts automatically via `:root` and `[data-theme=dark]` variable overrides.

---

## 📤 Export System

```mermaid
flowchart TD
    A["User clicks 📤 Export"] --> B["Dropdown opens"]
    B --> C{Format choice}
    C -->|"📄 TXT"| D["Build plain-text\nformatted string\nper reel"]
    C -->|"📊 CSV"| E["Build CSV rows\nwith headers"]
    D --> F["new Blob(content,\n'text/plain')"]
    E --> G["new Blob(content,\n'text/csv')"]
    F --> H["createObjectURL()"]
    G --> H
    H --> I["<a> programmatic\nclick → download"]
    I --> J["revokeObjectURL()"]
    J --> K["✅ Toast: Exported!"]
```

**TXT output example:**
```
[Food] https://instagram.com/reel/abc123
  Note: Amazing pasta recipe
  Date: 15 Jun 2025

[Tech] https://instagram.com/reel/xyz789
  Note: -
  Date: 14 Jun 2025
```

**CSV output example:**
```csv
Link,Category,Note,Date
"https://instagram.com/reel/abc123",Food,"Amazing pasta recipe",15 Jun 2025
"https://instagram.com/reel/xyz789",Tech,"",14 Jun 2025
```

---

## 🛡️ Security Notes

| Concern | Mitigation |
|---|---|
| **XSS via user input** | All user content passes through `escHtml()` before DOM insertion — no `innerHTML` with raw user data |
| **Firestore abuse** | Switch rules from `allow read,write: if true` to `if request.auth != null` once Auth is added |
| **API key exposure** | Firebase Web API keys are designed to be public — security is enforced via Firestore Rules, not key secrecy |
| **Open redirect** | All `window.open()` calls use `noopener noreferrer` to prevent tab-napping |
| **Clipboard** | Uses async Clipboard API with `execCommand` fallback for older browsers |

---

## 🗺️ Roadmap

```mermaid
gantt
    title ReelVault Development Roadmap
    dateFormat  YYYY-MM-DD
    section v1.0 (Shipped)
    Basic save & delete        :done, 2025-01-01, 2025-02-01
    Firebase Firestore          :done, 2025-02-01, 2025-03-01
    section v2.0 (Current)
    Dark mode                   :done, 2025-03-01, 2025-04-01
    Categories + search         :done, 2025-04-01, 2025-05-01
    Export TXT/CSV              :done, 2025-05-01, 2025-06-01
    Duplicate detection         :done, 2025-05-15, 2025-06-15
    LocalStorage cache          :done, 2025-06-01, 2025-06-15
    section v3.0 (Planned)
    Google Auth login           :active, 2025-07-01, 2025-08-01
    Per-user data isolation     :        2025-07-15, 2025-08-15
    Auto thumbnail preview      :        2025-08-01, 2025-09-01
    section v4.0 (Future)
    Collections / folders       :        2025-09-01, 2025-10-01
    Browser extension           :        2025-10-01, 2025-11-01
    PWA / offline mode          :        2025-11-01, 2025-12-01
```

**Upcoming features:**
- [ ] 🔐 Firebase Auth — Google Sign-in
- [ ] 👤 Per-user data isolation
- [ ] 🖼️ Auto-fetch Open Graph thumbnails
- [ ] 📁 Collections / folder system
- [ ] 🧩 Chrome extension — save from any page
- [ ] 📱 PWA with offline support
- [ ] 🏷️ Custom tags beyond preset categories
- [ ] 🔗 Share collections via public link

---

## 🤝 Contributing

Contributions are what make open source amazing. Any contribution you make is **greatly appreciated**.

```mermaid
gitGraph
    commit id: "Initial commit"
    commit id: "Basic Firebase CRUD"
    branch feature/dark-mode
    commit id: "Add CSS variables"
    commit id: "Toggle + localStorage"
    checkout main
    merge feature/dark-mode id: "✅ Merge dark mode"
    branch feature/categories
    commit id: "Add category schema"
    commit id: "Filter chips UI"
    checkout main
    merge feature/categories id: "✅ Merge categories"
    commit id: "v2.0 release 🎉"
```

**How to contribute:**

1. **Fork** the repository
2. Create your feature branch
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. Commit your changes
   ```bash
   git commit -m 'feat: add AmazingFeature'
   ```
4. Push to the branch
   ```bash
   git push origin feature/AmazingFeature
   ```
5. Open a **Pull Request**

**Commit convention:** This project uses [Conventional Commits](https://www.conventionalcommits.org/)

```
feat:     New feature
fix:      Bug fix
style:    CSS/UI changes
refactor: Code restructure
docs:     Documentation
chore:    Build / tooling
```

---

## 📄 License

Distributed under the **MIT License**.

```
MIT License — Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

See [`LICENSE`](LICENSE) for full text.

---

<div align="center">

**Built with ❤️ using Firebase + Vanilla JS**

*If this project helped you, please consider giving it a ⭐*

<br/>

[![GitHub stars](https://img.shields.io/github/stars/yourusername/reelvault?style=social)](https://github.com/yourusername/reelvault)
[![GitHub forks](https://img.shields.io/github/forks/yourusername/reelvault?style=social)](https://github.com/yourusername/reelvault)

</div>
