# Angel Dimitrov — Software Developer | Automation Engineer | Systems Architect

> *"From zero to a military-grade software ecosystem in 6 months — self-taught, AI-assisted engineering, and iron discipline."*

---

## Contact Information

| | |
|---|---|
| **Name** | Angel Dimitrov |
| **Location** | Sofia, Bulgaria |
| **Phone** | +359 88 888 1703 |
| **Email** | angel.d.dimitrovv@gmail.com |
| **GitHub** | [This profile] |
| **Languages** | Bulgarian (native), English (technical reading/writing — documentation and code) |

---

## Professional Summary

**Self-taught software developer and systems architect**, having built from scratch a complete Full-Stack ecosystem with military-grade security, real-time automation, and an integrated business model. I design, build, and manage end-to-end software systems — from database architecture and network communication, to the visual user interface and monetization.

**Core approach:** AI-assisted engineering using multiple language models. I leverage AI as a tool for accelerated development, validating every decision through rigorous "cross-examination" and architectural analysis of model outputs. The result is a fully functional, production-grade system.

**AI Investment:** Over **8 billion tokens** consumed across multiple AI models during a 6-month development sprint — equivalent to processing and validating well over 50,000 pages of technical documentation and generated code. This represents one of the most intensive AI-assisted solo engineering efforts ever documented.

**Seeking:** A first opportunity in the IT sector — Junior position, internship, contract work, or freelance project. Ready to start at the entry level and prove my value through real work.

---

## Technology Stack

### Programming Languages
`TypeScript` `JavaScript` `Python` `C++` `HTML/CSS`

### Frontend & UI
`React 19` `Zustand` `Redux` `Electron` `Vite` `Tailwind CSS` `Custom Hooks` `Dynamic View Rendering`

### Backend & Server Infrastructure
`Node.js` `Express.js` `WebSockets (ws)` `TypeScript 5.7` `REST API` `JWT Authentication` `better-sqlite3`

### Databases & Storage
`SQLite (WAL mode)` `Google Drive API` `Dropbox API` `Cloud Backups` `Ephemeral FS Recovery` `Redis (ioredis)`

### Cryptography & Security
`XChaCha20-Poly1305` `Ed25519` `Falcon-512` `SHA3-512` `BLAKE2` `HKDF` `scrypt` `PBKDF2` `TPM 2.0` `HWID Binding` `Constant-time Operations` `Memory Encryption (AES-256-GCM)`

### Automation & Computer Vision
`Python` `OpenCV (cv2)` `PyAutoGUI` `Real-time Screen Analysis` `Visual Pattern Matching` `Algorithmic Search (Spiral)` `Multi-threaded Bot Management`

### Payments & Monetization
`Stripe API` `PayPal Checkout SDK` `Coinbase Commerce` `Subscription Management` `Tier-based Access Control`

### DevOps & Tooling
`Docker (multi-stage)` `Git` `GitHub Actions (CI/CD)` `Render Cloud` `Vite` `ESBuild` `N-API (native C++ addons)`

### Concepts
`Zero-Trust Architecture` `Zero-Footprint Execution` `Dual-Path Verification` `In-Memory Execution` `Self-Healing Recovery` `Forensic Logging` `KillSwitch (DoD 7-pass)` `Anti-Replay Protection` `Noise-Wrapped Stealth Protocol`

---

## Core Project: Phantom Shield / Hooligan Commander

> **A complete Full-Stack platform for real-time automation management with an integrated business model and military-grade security.**

### Project Scale

| Metric | Value |
|---|---|
| **Total lines of code** | 50,000+ |
| **TypeScript/JavaScript modules** | 200+ files |
| **Python scripts (bots)** | 6 independent automation bots |
| **C++ native module** | Thousands of lines of N-API code |
| **React components** | 18+ specialized views |
| **Databases** | 3 independent SQLite databases with cloud backup |
| **Development time** | ~6 months (solo) |
| **AI tokens consumed** | 8,000,000,000+ across multiple models |

---

### 1. Server Architecture (Backend)

**PhantomServer** — a central orchestrator with a 25-step initialization sequence:

- **Express.js HTTP server** with aggressive connection limits and a multi-layered middleware chain
- **8 independent defensive middleware layers** (Rate Limiting, Anomaly Detection, Forensic Logging, CSRF Protection, JSON Complexity Guard, Timing Guard, Resource Guard, BlackLevel Security)
- **WebSocket server with a military-grade stealth protocol:**
  - XChaCha20-Poly1305 encryption on all messages
  - Noise wrapping: real data is "buried" inside a 400KB buffer of random noise
  - Deterministic component locations via HMAC-SHA512 with a hardware-bound seed
  - Chunking with dual integrity checks (CRC32 + SHA-256)
  - Constant-time comparisons to prevent timing attacks
  - Anti-replay protection (nonce + timestamp, 1-minute max age)
  - DoD 7-pass wipe of all buffers after use
- **4-phase handshake:** HWID validation → Hardware fingerprinting → Integrity challenge → Session verification
- **AI Tactical Chat** system for automated tactical responses
- **WebRTC signaling** for P2P communication between clients
- **Module streaming** — secure on-demand module delivery (tier-based filtering)
- **Heartbeat monitoring** with clock skew detection and automatic disconnect on anomalies

**BlackLevelSecurityMiddleware:**
- Token bucket rate limiting per HWID/IP (20 ops / 5 seconds)
- Anomaly detection with a scoring system (threshold: 50 points)
- Stealth response wrapping: random noise field injection, fake headers (nginx, Apache), noise cookies
- Jitter (0-50ms) to prevent timing attacks

---

### 2. Cryptography & Security

**KillSwitch module (1,200+ lines, custom implementation, ZERO external dependencies):**
- **XChaCha20-Poly1305** — complete inline implementation (ChaCha20 quarter round, HChaCha20, Poly1305)
- **Falcon-512** — post-quantum digital signature scheme
- **DoD 7-pass secure wipe** with full verification
- **Forensic stealth exfiltration** via multiple covert channels
- **Zero-disk footprint** — RAM-only operations
- **100% constant-time operations** for all cryptographic comparisons

**PhantomEncryptionEngine (2,700+ lines):**
- XChaCha20-Poly1305 symmetric encryption with hardware acceleration
- X25519 Elliptic Curve Diffie-Hellman with forward secrecy
- Ed25519 digital signatures with deterministic nonces
- Scrypt (N=16384, r=8, p=1) and PBKDF2 (310,000 iterations, OWASP 2023)
- HKDF key derivation with context binding
- SHA-3 (Keccak) and BLAKE2 for quantum resistance
- Automatic hardware crypto acceleration detection
- Entropy collector with 5 independent sources + health monitoring
- Key rotation every 24 hours, ephemeral keys with 5-minute lifespan
- Self-destruct on 10 consecutive failed decryption attempts

**Dual-Path Verification:**
- **Wall 1 — Security Module:** HWID validation (similarity threshold 0.85), anti-spoof, session token
- **Wall 2 — Mother Module:** Deep hardware DNA audit via native C++ module
- Both modules are INDEPENDENT and run in parallel — the system requires a "GREEN" signal from both

**Hardware DNA Binding:**
- Granular tracking: Motherboard, CPU, GPU, drives, MAC addresses, BIOS, TPM
- Individual hashes for each component
- EncryptedMemory\<T\> — all in-memory data encrypted with AES-256-GCM
- Anti-VM detection, anti-debugging techniques
- TPM 2.0 integration (PCR quotes, attestation, hardware-bound keys)

---

### 3. Python Automation — Computer Vision Bots

**6 independent automation bots (BOT1-BOT6), operating in parallel:**

- **Computer Vision stack:** OpenCV (cv2.matchTemplate with TM_CCOEFF_NORMED) + PyAutoGUI
- **150+ visual reference images**, loaded via base64 streaming from the server (RAM-only, zero disk footprint)
- **Visual recognition:** confidence thresholds, grayscale optimization, hold-click mechanics
- **Spiral search algorithm (move_map_spiral):** methodical map traversal via an expanding square (4 directions), with a 10-minute timeout
- **Multi-layered error handling system:**
  - Timeout failsafes on every while loop (300s, 600s, 900s)
  - Retry limits (3 attempts before strategy change)
  - Emergency recovery (F5 restart with 2-minute cooldown)
  - Dynamic conditional routing — the bot makes decisions based on visual feedback
- **Feedback Loops:** pre-action and post-action state checks, automatic strategy switching on failure
- **Built-in telemetry:**
  - Real-time: operation count, active process time, throughput (operations/hour), fastest-operation records
  - Stability: planned restart count, emergency restart count, retry count
  - Detailed final report on exit

**Python Bridge communication:**
- WebSocket connection with JWT authentication
- RAM-only image cache
- Heartbeat system for bot activity tracking
- Threading: each bot in a separate thread with time limit enforcement (checked every 10 seconds)

---

### 4. Frontend — React Application with 18+ Views

**User Interface Architecture:**

- **Dynamic View Navigator (useViewNavigator):** React hook for dynamic view rendering without page reload
- **18+ specialized modules:**
  - `HUDView` — main dashboard with live telemetry
  - `AIChatView` — AI tactical chat
  - `BotController` — 6-bot management with single-bot enforcement
  - `SecurityView` — security monitoring
  - `StealthView` — stealth configuration
  - `ThreatView` — threat analysis
  - `HardwareView` — hardware diagnostics
  - `LicenseView` — license management
  - `UpgradeDashboard` — tier plan visualization
  - `StorageView`, `BrowserView`, `CommsView`, `CommunityView`, `IntelView`, `LogisticsView`, `NewsView`, `ProfileView`, `GuideView`, `InstructionsView`
- **GamesHub** — 5 specialized game panels (Social, Stats, Utility, Novelty)
- **State Management:** 7 Zustand stores (botStore, chatStore, licenseStore, missionStore, securityStore, stealthStore, uiStore)
- **Styling:** Cyberpunk/Dark Mode theme, responsive design, consistent visual identity

**Zero-Footprint Client:**
- Electron "empty shell" client — zero business logic on disk
- All modules are streamed from the server directly into RAM after successful authentication
- DMZ decryption protocol with AES-256-GCM and scrypt key derivation
- Volatile execution: at session end, the client returns to its "empty" state

---

### 5. Native C++ Module (N-API)

**Large-scale C++ module (thousands of lines) with N-API integration for Node.js:**

- **CryptographyEngine:** XChaCha20-Poly1305, Ed25519 via libsodium (NaCl)
- **TPMAttestation:** TPM 2.0 integration via TSS2 (Trusted Software Stack) — PCR quotes, attestation
- **LicenseManager:** LicenseTicket structure (280 bytes) with Ed25519 signature and hardware binding
- **MemoryGuard:** SecureAllocation with SHA3-512 hashes, guard pages (max 256), stack canaries, heap magic (0xDEADC0DE)
- **IntegrityMonitor:** Code hash, memory hash, stack hash, and heap hash verification every 5 seconds
- **AuditLogger:** AuditEntry with Ed25519-signed audit logs
- **AntiDebug:** Debugger, VM, and sandbox environment detection
- **SelfDestruct:** 7-pass secure wipe on anomaly detection
- **RuntimeProtection:** JIT protection, timing anomaly detection

---

### 6. Business Model & Monetization

**5-Tier Access system with precise time-based billing:**

| Tier | Daily Limit | Type |
|---|---|---|
| **TRIAL** | 6 hours | 7 days + 3 bonus days |
| **FREE** | 2 hours | Unlimited duration |
| **HOOLIGAN** | 8 hours | Paid ($19-179) |
| **VIP** | 16 hours | Paid ($29-249) |
| **BLACK LEVEL** | Unlimited | Paid ($39-299) |

**Billing system principles:**
- **Self-hosted business model** — the server is the sole authority ("Police Officer")
- **Active-only metering:** the "meter" runs ONLY when a bot is actively engaged — not when the user is merely logged in
- **Midnight reset:** all limits reset strictly at 00:00
- **Single-bot enforcement:** only 1 bot can run at a time
- **Global 30-minute grace period** across all tiers
- **ONLY bots are paid** — everything else (Community, Arcade, AI Chat, Browser) is 100% free

**Payment integrations:**
- **Stripe API** — full integration with checkout sessions, subscription management, webhooks
- **PayPal Checkout SDK** — Orders API v2
- **Coinbase Commerce** — cryptocurrency payments
- **Forensic audit trail** — every transaction recorded in an immutable hash-chain journal
- **Hardware-bound activation** — payments are tied to specific hardware

---

### 7. Infrastructure & DevOps

**Automated Recovery (Self-Healing):**
- Automatic emergency database restore from Google Drive / Dropbox when a file is missing
- Designed for Render Free Tier (ephemeral filesystem)
- Multi-platform cloud backups with encryption

**Docker multi-stage build:**
- Stage 1: Node 20-slim with Python 3.11, OpenCV, numpy, libsodium
- Stage 2: Minimal production image with non-root user
- HEALTHCHECK every 30 seconds
- Xvfb virtual display for headless GUI operations

**CI/CD:**
- GitHub Actions for Python syntax validation (py_compile, mypy, flake8)
- Auto-deploy to Render.com

**Deployment security:**
- All assets encrypted at rest
- Public access only to auth shell — everything else returns 404 (without revealing existence)
- Native module moved out of public directory — accessible only via authenticated endpoint

---

### 8. Testing & Quality Assurance

**Structured test pyramid:**

- **Unit tests** for individual modules
- **Integration tests** for cross-component interactions
- **Annihilation tests (Tier 1-23)** — stress tests for edge cases and boundary conditions
- **Smoke tests** for rapid deployment validation
- **Local QA of Python bots** — stability testing during hours-long autonomous operation
- **Log-based diagnostics** with timestamps and severity levels

---

## Additional Technical Highlights

### Forensic Resilience
- Full event logging with forensically-secure hash-chain verification
- Ed25519-signed audit entries
- Encrypted forensic exfiltration prior to system shutdown
- Stealth headers mimicking normal browser traffic
- Exponential backoff on failure (3 attempts)

### Anti-Tamper Protections
- In-memory CAPTCHA (200x80 pixels, anti-OCR distortion)
- Bruteforce protection with adaptive exponential backoff
- Circuit breaker for payment providers (5 failures → 30s reset)
- Redlock for multi-node distributed mutex

### Network Security
- IP blacklist system
- DDoS protection
- Strict CORS in production
- Helmet.js security headers
- Trust proxy for reverse proxy environments

---

## Previous Professional Experience

### B2B Sales Representative
*Nationwide*
- Direct sales to corporate clients and manufacturing enterprises
- End-to-end management of the sales cycle — negotiations, logistics, financial settlements
- Work with C-level executives, building long-term business relationships

### Real Estate Broker (10 years)
- Market analysis and client consulting
- Property portfolio management
- Closing complex transactions

### Transport & Logistics (10 years)
- Long-term experience requiring maximum concentration
- Working with a diverse range of people
- Supply chain management

---

## Soft Skills

- **Discipline & Accountability:** 20+ years of experience taking full ownership of complex end-to-end processes
- **Stress Resilience:** Adaptability and the ability to make rapid, logical decisions in highly dynamic environments
- **Communication:** Excellent negotiation and corporate client relationship skills from B2B sales
- **Self-Organization:** Proven ability to independently manage time and complex projects without external oversight
- **Analytical Thinking:** A systematic approach to problem-solving and identifying logical gaps
- **Intrinsic Motivation:** Self-ignited passion for programming, capable of long and intense work sprints

---

## How I Work

My development approach is **AI-assisted engineering** — I use multiple AI models as tools for:

1. **Architectural planning** — "cross-examination" of different AI models to find the optimal solution
2. **Accelerated implementation** — AI generates code, I validate, test, and integrate
3. **Code Review** — rigorous verification of every AI-generated solution before integration
4. **QA & edge-case discovery** — systematic search for logical gaps from the end-user's perspective

This approach enables me to achieve a development velocity comparable to a small team while maintaining a high quality standard through strict personal validation.

---

## What I'm Looking For

**A first opportunity in the IT sector.** Open to:

- **Junior Developer** (Frontend, Backend, Full-Stack)
- **Junior QA / Automation Engineer**
- **Internship program**
- **Contract work / Freelance project**
- **Technical Support / IT Support** (with a path to development)

Ready to start at the very bottom, at minimum wage or even unpaid initially, to prove my skills through real work. My only requirement is the ability to **work from home** (remote) and an environment where I can grow.

---

## Honest About the Challenges

- **No formal IT education** — everything I know was learned independently through hands-on practice and AI-assisted learning
- **No conversational English** — but I read and write technical documentation and code in English at a high level
- **No commercial IT experience** — this project is my only, yet deeply comprehensive, portfolio

These "shortcomings" are offset by a **proven ability to build complex, functional software systems from scratch** — something many people with formal degrees and years of experience have not achieved.

---

> *"This project is not just code. It is proof that with enough motivation, discipline, and the right tools, a person can achieve something extraordinary in a surprisingly short time. I'm looking for someone to give me a chance to prove it in a real work environment as well."*
>
> — Angel Dimitrov

---

## License

This project is a demonstration and represents a personal portfolio. All rights reserved.
Automated-Ecosystem-Demo
​A full-stack automated ecosystem with a zero-footprint architecture. Features a secure backend (TypeScript/C++), parallel Python bots with Computer Vision (OpenCV), and a React 19 dashboard. Demonstrates resilient design, complex process management, and secure module streaming.
