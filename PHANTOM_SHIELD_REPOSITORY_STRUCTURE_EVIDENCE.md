# Phantom Shield Repository Structure Evidence

**Author:** Angel Dimitrov  
**Project:** Phantom Shield  
**Repository:** `github.com/Kalafara/Automated-Ecosystem-Demo`  
**Document type:** Repository structure evidence and architectural map  
**Snapshot basis:** Supplied Windows repository tree (`project_structure2(1).txt`)

---

## 1. Purpose

This document provides a structured, evidence-focused view of the Phantom Shield repository. Its purpose is to make the project's real scope, separation of responsibilities, technical layers, and supporting engineering assets easier to inspect.

The document is not a source-code audit and does not claim that every listed component is production-ready. A repository tree can demonstrate that modules, assets, tests, build systems, and architectural boundaries exist, but code quality and runtime correctness must be validated through source review, reproducible builds, automated tests, logs, and live demonstrations.

## 2. Snapshot Summary

The supplied repository snapshot contains **1,561 listed paths**. This number includes source files, image assets, dependency headers, build outputs, logs, database artifacts, backups, generated bundles, and temporary or diagnostic files.

The companion technical portfolio reports **561 source files** and approximately **194,794 source lines**, excluding dependencies, libraries, and build artifacts. These two measurements are not contradictory: the raw tree is broader than the curated source-code count.

### Most represented top-level areas

| Area | Listed paths | Interpretation |
|---|---:|---|
| `protected_modules/` | 594 | Frontend modules, automation engines, native artifacts, and recognition assets |
| `protected/` | 205 | Electron/React core, loaders, services, stores, views, and bundled modules |
| `src/` | 187 | Main Node.js/TypeScript server code and supporting services |
| `public/` | 171 | Public/electron-facing assets, source, scripts, and packaged resources |
| `native/` | 168 | C++/N-API module, dependencies, build system, and native artifacts |
| `test_logs/` | 71 | Recorded outputs from resilience, security, and validation runs |
| `test/` | 38 | Unit, integration, and annihilation-style test organization |

### Dominant file types in the snapshot

| Extension | Count | Main role |
|---|---:|---|
| `.png` | 521 | Computer-vision templates and product assets |
| `.ts` | 276 | Server, services, security, loaders, and infrastructure |
| `.tsx` | 71 | React views and components |
| `.js` | 84 | Scripts, tests, generated or compatibility code |
| `.py` | 36 | Automation engines and repository maintenance utilities |
| `.h` | 81 | Native dependencies and TPM/libsodium interfaces |
| `.log` | 86 | Diagnostics, test evidence, and runtime investigation |
| `.json` | 43 | Configuration, manifests, package metadata, and test fixtures |

## 3. Curated Repository Map

The following map intentionally excludes most dependency internals, generated build files, repetitive image names, logs, and temporary artifacts.

```text
server/
├── src/
│   ├── api/
│   ├── backup/
│   ├── cache/
│   ├── commander/
│   ├── config/
│   ├── core/
│   ├── database/
│   ├── dmz/
│   ├── middleware/
│   ├── mother/
│   ├── network/
│   ├── notifications/
│   ├── python/
│   ├── recovery/
│   ├── security/
│   ├── server/
│   ├── services/
│   └── utils/
├── protected/
│   ├── core/
│   │   ├── components/
│   │   ├── config/
│   │   ├── entries/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── loader/
│   │   ├── main/
│   │   ├── polyfills/
│   │   ├── preload/
│   │   ├── renderer/
│   │   ├── services/
│   │   ├── stores/
│   │   ├── styles/
│   │   ├── types/
│   │   ├── utils/
│   │   ├── views/
│   │   └── vision/
│   └── modules/
├── protected_modules/
│   ├── bot/              # Six Python automation engines
│   ├── botbox/           # Visual recognition assets
│   ├── frontend/
│   ├── native/
│   ├── core/
│   └── assets/
├── native/
│   ├── phantom_shield_native.cpp
│   ├── binding.gyp
│   ├── deps/
│   ├── third_party/
│   ├── build/
│   └── bin/
├── public/
│   ├── src/
│   ├── assets/
│   ├── main/
│   ├── scripts/
│   ├── plans/
│   └── protected/
├── test/
│   ├── unit/
│   ├── integration/
│   └── annihilation/
├── test_logs/
├── backups/
│   ├── drive/
│   ├── dropbox/
│   └── local/
├── config/
├── data/
├── internal/
├── scripts/
├── Dockerfile
├── package.json
├── tsconfig.json
└── startup.sh
```

## 4. Architectural Layers and Evidence

### 4.1 Server and orchestration layer - `src/`

The `src/` tree contains separate areas for APIs, middleware, security, data access, recovery, backup, networking, configuration, Python-process coordination, server initialization, notifications, caching, and shared utilities.

This organization supports the portfolio claim that Phantom Shield is not a single automation script. It has a central Node.js/TypeScript orchestration layer that coordinates authentication, sessions, policies, communication, automation processes, persistence, recovery, and operational controls.

Representative directories include:

- `src/api/` - request-facing interfaces and application endpoints;
- `src/middleware/` - policy, validation, rate, and request-processing boundaries;
- `src/security/` and `src/dmz/` - security-oriented controls and separation layers;
- `src/python/` and `src/commander/` - coordination of automation processes;
- `src/database/`, `src/cache/`, and `src/backup/` - state, performance, and recovery;
- `src/network/` and `src/services/` - communication and reusable application services;
- `src/recovery/` - explicit recovery paths rather than silent failure handling.

### 4.2 Electron/React client core - `protected/core/`

The client layer is divided into components, views, stores, services, loaders, Electron main/preload code, renderer code, configuration, types, utilities, styles, and computer-vision-related modules.

Concrete evidence in the tree includes:

- `renderer/App.tsx`, `BotController.tsx`, `TelemetryProvider.tsx`, and `ViewNavigator.tsx`;
- state stores for bots, licensing, missions, security, stealth, and UI;
- services for bots, communication, databases, AI, payments, security, sound, updates, and Python process management;
- API clients, WebSocket communication, bridges, audit logging, and WebRTC components;
- dedicated views for AI chat, browser, community, HUD, licensing, profile, security, stealth, storage, and upgrades;
- loader registries for components, services, and stores;
- Electron main, preload, protocol, and native-bridge files.

This separation is consistent with a modular desktop application rather than a single-page demonstration.

### 4.3 Automation layer - `protected_modules/bot/` and `botbox/`

The tree contains six named Python automation files:

- `BOT1.py`
- `BOT2.py`
- `BOT3.py`
- `BOT4.py`
- `BOT5.py`
- `BOT6.py`

The adjacent `botbox/` area contains a large set of PNG templates used for screen recognition and GUI-driven workflows. In the supplied snapshot, PNG files are the largest extension group, which is consistent with a computer-vision/template-matching automation design.

The tree proves the presence of distinct automation engines and their recognition assets. Runtime reliability still requires demonstration through controlled execution, logs, timeout/retry behavior, and repeatable tests.

### 4.4 Native C++ / N-API layer - `native/`

The native layer contains:

- `phantom_shield_native.cpp`;
- `binding.gyp` and native package metadata;
- build scripts and compiled `.node` artifacts;
- libsodium headers and binaries;
- TPM/TSS-related headers and third-party interfaces;
- native test and integration scripts;
- repository-maintenance scripts used during restructuring and compilation work.

This is direct structural evidence that the project includes a real native build boundary between Node/Electron and C++ code. It does not independently certify the security properties of the implementation; those require code review, reproducible compilation, test vectors, and threat-model validation.

### 4.5 Data, backup, and recovery

The tree includes three SQLite database families with WAL-related files, encrypted hardware-identity storage, and separate backup paths for Google Drive, Dropbox, and local recovery.

These paths support the existence of:

- distinct data stores;
- WAL-oriented SQLite operation;
- backup manifests and multiple recovery destinations;
- explicit recovery and operational-state concerns.

Database files, `.env` files, encrypted stores, and backup metadata must not be published in a public repository snapshot.

### 4.6 Testing and diagnostics

The repository contains:

- `test/unit/`;
- `test/integration/`;
- `test/annihilation/`;
- end-to-end authentication and registration scripts;
- database, module, session, hardware-scan, backup, and loader checks;
- a separate `test_logs/` directory with repeated tier-based run outputs.

This structure supports the claim that testing and failure investigation were treated as separate engineering activities. The strongest public proof would be a curated test inventory, documented commands, CI results, and selected sanitized logs.

### 4.7 Build, packaging, and delivery

The snapshot includes:

- `Dockerfile`;
- `package.json` and lock files;
- TypeScript configurations;
- PowerShell and shell startup/build scripts;
- Electron and native build artifacts;
- generated protected bundles;
- native `.node` binaries.

These entries support a multi-runtime delivery model involving Node.js/TypeScript, Electron, Python, and native C++.

## 5. Evidence Matrix

| Repository evidence | Capability supported | Boundary |
|---|---|---|
| Six `BOT*.py` files and extensive PNG templates | Multiple GUI/computer-vision automation workflows | Does not prove runtime accuracy without demonstrations |
| React views, stores, services, loader registries | Modular desktop client with shared state and dynamic modules | Does not prove every view is currently functional |
| Node/TypeScript `src/` domains | Central server/orchestration architecture | Does not prove clean dependency direction without code review |
| Native C++ source, `binding.gyp`, compiled `.node` files | Real N-API/native integration and build work | Does not independently validate security claims |
| SQLite/WAL files and backup destinations | Persistence, concurrency-oriented configuration, recovery work | Database contents and secrets must remain private |
| Unit/integration/annihilation directories and logs | Layered testing intent and repeated validation runs | Public proof requires commands, results, and reproducibility |
| Docker/startup/build configuration | Packaging and deployment preparation | Does not prove production availability by itself |
| Diagnostic scripts and logs | Active debugging and observability work | Raw logs may expose sensitive operational information |

## 6. AI-Assisted Development and Human Ownership

Phantom Shield was developed through an intensive AI-assisted workflow. AI models were used to generate implementation proposals, compare alternatives, review changes, diagnose failures, and accelerate development across multiple languages and frameworks.

Human ownership remained in:

1. defining the product goals and requested capabilities;
2. deciding which features belonged in the system;
3. selecting between competing model recommendations;
4. integrating generated changes into the existing repository;
5. running the application and validating observable behavior;
6. reviewing logs, failures, and regressions;
7. accepting, rejecting, or revising each result.

This document does not claim that the author manually wrote or can independently reproduce every source line. It documents the scale and organization of a human-directed, AI-assisted engineering project and the practical integration work required to keep its layers operating together.

## 7. Publication and Security Rules

**Do not upload the raw supplied tree unchanged.** It exposes local drive paths and names of sensitive artifacts, including `.env` files, backups, databases, encrypted stores, logs, build outputs, and security-related modules.

For a public GitHub repository:

- publish this curated document instead of the raw tree;
- never commit `.env`, `.env.backup`, private keys, secrets, databases, WAL files, user data, or backup manifests;
- exclude `node_modules/`, native dependency bundles, `build/`, `dist/`, generated binaries, caches, and temporary files;
- sanitize logs before publication;
- keep only representative test outputs;
- use `.gitignore` and secret scanning;
- consider publishing a generated tree produced from the already-sanitized public repository.

## 8. Professional Interpretation

The repository structure provides credible evidence of a broad, multi-layer engineering effort. It shows deliberate separation between server orchestration, desktop UI, automation engines, native integration, data, recovery, testing, and delivery concerns.

The strongest conclusion supported by the tree is not that every component is production-ready. It is that Phantom Shield is a substantial, organized, AI-assisted systems-integration project built around a real automation objective, with visible evidence of iterative debugging, modular expansion, native experimentation, testing, and operational thinking.

## 9. Recommended Public Evidence Package

For GitHub or job applications, use the following package:

1. Main `README.md` with a concise product overview and safe setup instructions;
2. Visual Project Portfolio;
3. Technical Architecture & Engineering Portfolio;
4. This Repository Structure Evidence document;
5. A short, reproducible demonstration;
6. A curated test inventory and selected CI results;
7. A sanitized source tree generated from the public repository.

---

**Evidence boundary:** Repository structure demonstrates presence and organization. Source review, reproducible tests, runtime demonstrations, and independent assessment determine correctness, maintainability, security, and production readiness.
