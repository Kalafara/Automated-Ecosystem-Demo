# PHANTOM SHIELD — GRANDMASTER PREVIEW

### Architectural showcase of a military-grade automated ecosystem built from scratch in 6 months by a self-taught engineer using AI-assisted methodology.

---

> *"This is not a tutorial. This is not a bootcamp project. This is what happens when obsession meets AI-assisted engineering — 561 source files, 195,000 lines of working code, and a system that survives real hostile conditions."*

---

## THE NUMBERS

| Metric | Value |
|---|---|
| **Total source files** | 561 |
| **Total lines of code** | **194,794** (excl. node_modules, libs, build artifacts) |
| **Programming languages** | TypeScript, Python, C++, JavaScript, HTML/CSS |
| **Development time** | 6 months (solo, self-taught) |
| **AI tokens consumed** | 8 billion+ (paid) + estimated 16 billion+ (free models) |
| **Average work session** | 48 hours continuous |
| **Bots** | 6 independent Python automation engines |
| **Frontend views** | 18+ specialized React components |
| **Databases** | 3 independent SQLite databases with cloud backup |
| **Middleware layers** | 8 defensive layers |
| **Cryptographic protocols** | XChaCha20-Poly1305, Ed25519, Falcon-512, SHA-3, BLAKE2 |
| **Payment gateways** | Stripe, PayPal, Coinbase |

---

## ARCHITECTURE OVERVIEW

```
┌─────────────────────────────────────────────────────────────────┐
│                    PHANTOM SHIELD ECOSYSTEM                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────┐    ┌──────────────┐    ┌──────────────────────┐  │
│  │ ELECTRON  │◄──►│  WebSocket   │◄──►│   NODE.JS BACKEND    │  │
│  │  CLIENT   │    │  STEALTH     │    │   PhantomServer      │  │
│  │ (React 19)│    │  PROTOCOL    │    │   25-step init       │  │
│  └──────────┘    │  XChaCha20   │    │   8 middleware       │  │
│                  │  400KB noise │    │   REST API           │  │
│                  └──────────────┘    └──────────┬───────────┘  │
│                                                  │              │
│         ┌────────────────────────────────────────┤              │
│         │                                        │              │
│  ┌──────▼──────┐    ┌──────────────┐    ┌───────▼──────────┐  │
│  │ 6 PYTHON    │    │  NATIVE C++  │    │  SECURITY        │  │
│  │ BOTS        │    │  N-API MODULE│    │  Dual-Path       │  │
│  │ OpenCV      │    │  libsodium   │    │  Verification    │  │
│  │ PyAutoGUI   │    │  TPM 2.0     │    │  KillSwitch      │  │
│  │ YOLOv8      │    │  Anti-Debug  │    │  DoD 7-pass      │  │
│  └─────────────┘    └──────────────┘    └──────────────────┘  │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  INFRASTRUCTURE: Docker • Render Cloud • GitHub Actions   │   │
│  │  BACKUPS: Google Drive • Dropbox • ngrok • Self-Healing   │   │
│  │  PAYMENTS: Stripe • PayPal • Coinbase • 5-Tier System     │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## LEVEL 1: CRYPTOGRAPHY FROM SCRATCH

### Custom ChaCha20 Quarter Round — ZERO External Dependencies

From `server/src/utils/killSwitch.ts` — 1,200+ lines of fully hand-written cryptography:

```typescript
// XChaCha20-Poly1305 Implementation — entirely custom, no libraries
class XChaCha20Poly1305 {
    private static readonly KEY_SIZE = 32;      // 256-bit key
    private static readonly NONCE_SIZE = 24;    // 192-bit nonce for XChaCha
    private static readonly TAG_SIZE = 16;      // 128-bit authentication tag

    private static quarterRound(state: Uint32Array, a: number, b: number, c: number, d: number): void {
        // ChaCha20 quarter round operation (constant-time)
        state[a] = state[a] + state[b]; state[d] ^= state[a];
        state[d] = (state[d] << 16) | (state[d] >>> 16);
        state[c] = state[c] + state[d]; state[b] ^= state[c];
        state[b] = (state[b] << 12) | (state[b] >>> 20);
        state[a] = state[a] + state[b]; state[d] ^= state[a];
        state[d] = (state[d] << 8)  | (state[d] >>> 24);
        state[c] = state[c] + state[d]; state[b] ^= state[c];
        state[b] = (state[b] << 7)  | (state[b] >>> 25);
    }
```

> **Why this matters:** Writing ChaCha20 by hand means you understand cryptographic primitives at the bit-manipulation level. This code is constant-time — resistant to timing side-channel attacks. Few senior engineers have ever implemented this themselves.

### Falcon-512 Post-Quantum Signatures

```typescript
interface Falcon512KeyPair {
    publicKey: Uint8Array;  // 897 bytes for Falcon-512 public key
    privateKey: Uint8Array; // 1281 bytes for Falcon-512 private key
}

// Constant-time comparison — timing-attack resistant
class ConstantTime {
    static equals(a: Uint8Array, b: Uint8Array): boolean {
        if (a.length !== b.length) return false;
        let result = 0;
        for (let i = 0; i < a.length; i++) {
            result |= a[i] ^ b[i];
        }
        return result === 0;
    }

    static select(condition: number, a: number, b: number): number {
        const mask = -condition;  // All 1s if true, all 0s if false
        return (a & mask) | (b & ~mask);
    }
}
```

> **Why this matters:** Falcon-512 is a NIST-standardized post-quantum algorithm. Implementing it without libraries demonstrates understanding of lattice-based cryptography. Constant-time operations prevent attackers from measuring how long cryptographic operations take to extract secrets.

---

## LEVEL 2: SERVER ARCHITECTURE

### PhantomServer Entry Point — 25-Step Boot Sequence

From `server/src/main.ts` — the brain of the entire operation:

```typescript
/**
 * PHANTOM SHIELD - BLACK LEVEL SERVER ENTRY POINT
 * INDUSTRIAL-GRADE SERVER ORCHESTRATOR WITH TRIPLE-CHECKPOINT HANDSHAKE,
 * SELF-HEALING RECOVERY, AND REAL-TIME THREAT RESPONSE.
 * 
 * WARNING: This system operates with zero forgiveness. One anomaly triggers
 * complete memory wipe and self-healing injection. No forensic traces remain.
 */

// P0-CRIT-01: Guard DNA_ALLOW_TEST_BYPASS to non-production only
if (process.env.DNA_ALLOW_TEST_BYPASS === 'true' &&
    (process.env.NODE_ENV || 'production') === 'production') {
    console.error('[SECURITY] DNA_ALLOW_TEST_BYPASS is true in production - CRASHING');
    process.exit(1);
}

// === CORE BLACK-LEVEL MODULES ===
import { createEncryptionEngine } from './security/encryption';
import { streamGuard } from './middleware/streamGuard';
import { resourceGuard, jsonComplexityGuard } from './middleware/resourceGuard';
import { timingGuard } from './middleware/timingGuard';
import { HardwareValidator } from './security/hardware';
import { HeartbeatMonitor } from './network/heartbeat';
import { SecurityCore } from './security/securityCore';          // Triple checkpoint
import { SessionManager } from './core/sessionManager';           // 7+3 trial engine
import { SubscriptionOrchestrator } from './core/subscriptionOrchestrator';
import { DonationGateway } from './security/donationGateway';     // Stripe + PayPal
import { RecoverySystem } from './recovery/recovery';             // Self-healing
```

> **Why this matters:** This orchestrator manages 30+ subsystems with zero tolerance for failure. The first 5 lines of executable code are a security check that intentionally crashes the server if misconfigured — this is defense-in-depth thinking.

---

## LEVEL 3: STEALTH WEBSOCKET PROTOCOL

### Military-Grade Noise-Wrapped Communication

From `server/src/network/websocket.ts` — 2,600+ lines:

```typescript
const CONFIG = {
    TOTAL_BUFFER_SIZE: 409600,     // 400KB — data buried in noise
    ENCRYPTED_DATA_MAX_SIZE: 307200, // 300KB max payload
    ENCRYPTION_ALGORITHM: 'XChaCha20-Poly1305',
    HANDSHAKE_TIMEOUT: 10000,      // 10s — aggressive
    MAX_CLOCK_SKEW_MS: 5000,       // Anti-replay window
    SELF_DESTRUCT_ON_TAMPER: true, // Kill-switch armed
};
```

**The protocol works in 4 phases:**
1. **handshake_init** → Client sends HWID (64/128 hex), server responds with challenge
2. **HWID validation** → Hardware fingerprinting, VM detection, TPM presence check
3. **Integrity challenge** → SHA-512 hash with pepper, constant-time verification
4. **Session validation** → JWT or session token, hardware-bound

**Data transmission:**
- Real payload encrypted with XChaCha20-Poly1305
- Encrypted data is "buried" inside a **400KB buffer of random noise**
- The position of key, nonce, tag, and ciphertext within the buffer is determined by **HMAC-SHA512 with a hardware-bound seed**
- Large payloads are **chunked** with dual integrity checks (CRC32 + SHA-256)
- All buffers are **DoD 7-pass wiped** after use

> **Why this matters:** This is not standard WebSocket communication. This is a custom stealth protocol designed to resist traffic analysis, replay attacks, and man-in-the-middle interception. The noise wrapping technique means an observer sees only random data — they cannot determine that a message was even sent.

---

## LEVEL 4: COMPUTER VISION AUTOMATION

### Spiral Search Algorithm — Systematic Target Location

From `server/protected_modules/bot/BOT3.py`:

```python
def move_map_spiral(current_target):
    """Methodical map traversal via expanding square — 4 directions, 10-min timeout"""
    start_search = time.time()
    times_to_move = 1
    
    while True:
        if time.time() - start_search > 600:
            return "RESTART_REQUIRED"  # Timeout failsafe — never infinite loop
        
        for dir_idx in range(1, 5):
            for _ in range(times_to_move):
                if dir_idx == 1:
                    pyautogui.moveTo(1100, 600)
                    pyautogui.dragTo(400, 600, duration=1.0, button='left')
                elif dir_idx == 2:
                    pyautogui.moveTo(800, 800)
                    pyautogui.dragTo(800, 300, duration=1.0, button='left')
                # ... directions 3 & 4 complete the expanding square
                
                time.sleep(2)
                loc = find_base_fast_spiral(current_target)
                if loc:
                    return loc  # Target found!
                    
            if dir_idx % 2 == 0:
                times_to_move += 1  # Expand the spiral
```

### OpenCV Visual Pattern Matching — RAM-Only Asset Pipeline

```python
def load_assets_from_stdin():
    """Stream 150+ reference images via base64 from server — NEVER touch disk"""
    raw = sys.stdin.read()
    data = json.loads(raw)
    assets = {}
    for asset in data.get('assets', []):
        img_bytes = base64.b64decode(asset['data'])
        nparr = np.frombuffer(img_bytes, np.uint8)
        img = cv2.imdecode(nparr, cv2.IMREAD_COLOR)
        assets[asset['filename']] = img
    return assets

def _locate_on_screen(asset_img, conf=0.90, gray=False):
    """Professional-grade visual pattern matching with confidence thresholding"""
    screen = pyautogui.screenshot()
    screen_np = np.array(screen)
    screen_cv = cv2.cvtColor(screen_np, cv2.COLOR_RGB2BGR)
    
    if gray:
        screen_cv = cv2.cvtColor(screen_cv, cv2.COLOR_BGR2GRAY)
        template = cv2.cvtColor(asset_img, cv2.COLOR_BGR2GRAY)
    else:
        template = asset_img
    
    result = cv2.matchTemplate(screen_cv, template, cv2.TM_CCOEFF_NORMED)
    min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)
    
    if max_val >= conf:
        h, w = template.shape[:2]
        center_x = max_loc[0] + w // 2
        center_y = max_loc[1] + h // 2
        return (center_x, center_y)
    return None
```

### Multi-Layered Error Handling — Professional Grade Resilience

```python
# Three independent fail-safe mechanisms working together:
in_battle = False
attack_start_time = time.time()
attack_retry_limit = 0
total_attempts = 0

while not in_battle:
    if time.time() - attack_start_time > 300:
        break                      # LAYER 1: Timeout failsafe — never hang
    
    if attack_retry_limit >= 3:
        break                      # LAYER 2: Retry limit — don't beat dead horse
    
    pyautogui.click(target_coords)
    time.sleep(10)
    
    if find_and_click('Attack1.2', move_away=True, conf=0.70):
        time.sleep(4)
        if find_and_click('Attack2', move_away=True):
            time.sleep(2)
            find_and_click('Attack3', move_away=True)  # Optional bonus
            in_battle = True
            break
        else:
            total_attempts += 1
            if total_attempts >= 6:
                break              # LAYER 3: Smart abort — strategy switch
    else:
        attack_retry_limit += 1
```

> **Why this matters:** This is not a simple "click-when-found" script. This is a professional automation framework with three independent fail-safe layers working simultaneously: timeout guards, retry limits with strategy switching, and smart abort conditions. This is exactly how production test automation frameworks are designed at companies like Google and Microsoft.

---

## LEVEL 5: NATIVE C++ SECURITY MODULE

### Hardware-Level Memory Protection

From `server/native/phantom_shield_native.cpp`:

```cpp
// Military-grade security module for automation systems
// BLACK security level — Production ready

#define NAPI_VERSION 8
#define SODIUM_STATIC
#define WIN32_LEAN_AND_MEAN

#include <node_api.h>
#include <windows.h>
#include <winternl.h>     // NT kernel internals
#include <winhttp.h>       // Secure HTTP
#include <wincrypt.h>      // Windows Crypto API
#include <bcrypt.h>        // CNG — Next Gen Crypto
#include <ncrypt.h>        // TPM key storage
#include <tbs.h>           // TPM Base Services
#include <tss2/tss2_sys.h> // TPM 2.0 System API
#include <tss2/tss2_esys.h>// TPM 2.0 Enhanced System API
#include <intrin.h>        // CPU intrinsics

extern "C" {
#include "sodium.h"        // libsodium (NaCl) — XChaCha20, Ed25519
}

// Security constants
#define SECURITY_LEVEL_BLACK 0x0000000B
#define XCHACHA20_KEY_SIZE 32
#define ED25519_SIGNATURE_SIZE 64
#define SHA3_512_SIZE 64
#define GUARD_PAGE_SIZE 4096
#define MAX_GUARD_PAGES 256         // Up to 256 memory guard pages
#define INTEGRITY_CHECK_INTERVAL 5000  // Verify every 5 seconds
#define TPM_ATTESTATION_INTERVAL 60000 // TPM re-attest every 60 seconds
```

**Subsystems in the native module:**
- **CryptographyEngine** — XChaCha20-Poly1305 + Ed25519 via libsodium
- **TPMAttestation** — TPM 2.0 integration via TSS2 (PCR quotes, attestation, hardware-bound keys)
- **MemoryGuard** — SecureAllocation with SHA3-512 hashes, 256 guard pages, stack canaries, heap magic (0xDEADC0DE)
- **IntegrityMonitor** — Code hash, memory hash, stack hash, and heap hash verification every 5 seconds
- **AntiDebug** — Debugger detection, VM detection, sandbox environment detection
- **AuditLogger** — Ed25519-signed audit entries with encrypted data
- **SelfDestruct** — 7-pass secure wipe on anomaly detection
- **RuntimeProtection** — JIT protection, timing anomaly detection

> **Why this matters:** This is kernel-adjacent programming. The module directly interfaces with Windows NT internals (winternl.h), the TPM 2.0 hardware stack (TSS2), and the Windows Cryptography Next Generation API. This is the same level of systems programming used by anti-cheat engines and endpoint security products.

---

## LEVEL 6: FULL-STACK GROWTH TREE

### From One Script to an Ecosystem — 6 Months

```
Month 1:  "Can I automate this click?"
          └─► BOT1.py — single bot, pyautogui.click(), hardcoded coordinates

Month 2:  "What if I use image recognition?"
          └─► OpenCV integration, confidence thresholds, grayscale optimization
          └─► BOT2.py, BOT3.py — specialized for different game scenarios

Month 3:  "I need to protect this from detection."
          └─► Native C++ module research begins
          └─► HWID fingerprinting, basic encryption
          └─► Server concept: Node.js + Express

Month 4:  "This is becoming a real platform."
          └─► PhantomServer — 25-step init, 8 middleware layers
          └─► WebSocket stealth protocol (XChaCha20 + noise wrapping)
          └─► Electron client with React 19 frontend
          └─► 4 more bots (BOT4-BOT6), multi-threading

Month 5:  "People could actually pay for this."
          └─► 5-tier subscription system (Trial → Free → Hooligan → VIP → Black Level)
          └─► Stripe + PayPal + Coinbase integration
          └─► Active-only metering, midnight reset, hardware-bound licenses
          └─► YOLOv8 training: 160,000 images, 370 epochs
          └─► Docker container, Render Cloud deployment

Month 6:  "Make it unbreakable."
          └─► KillSwitch module — 1,200 lines of custom cryptography
          └─► Falcon-512 post-quantum signatures
          └─► Dual-Path Verification (Security + Mother modules)
          └─► DoD 7-pass secure wipe
          └─► Self-healing cloud database recovery
          └─► 23-tier annihilation stress tests
          └─► 18+ React views, community chat, browser, arcade games
          └─► CV, README, cover letter — ready for the world
```

---

## THE SECRET SAUCE: AI-COMMANDER METHODOLOGY

This entire system was built using a proprietary methodology developed over 8 billion+ tokens of interaction with multiple AI models:

```
┌─────────────────────────────────────────────────────────┐
│              THE DEPARTMENT OF SUPER-SPECIALISTS         │
├─────────────────────────────────────────────────────────┤
│                                                          │
│   CHIEF ARCHITECT (Human)                                │
│   ┌──────────────────────────────────────────┐          │
│   │ Defines the architecture                 │          │
│   │ Assigns tasks to AI models               │          │
│   │ Cross-validates all outputs              │          │
│   │ Makes final integration decisions        │          │
│   │ Performs live testing                    │          │
│   └──────────┬───────────────────────────────┘          │
│              │                                           │
│   ┌──────────▼──────────────────────────────┐           │
│   │         AI SPECIALIST TEAM               │           │
│   ├──────────────────────────────────────────┤           │
│   │ Model #1: Code Generator                 │           │
│   │   "Write the implementation"             │           │
│   │                                          │           │
│   │ Model #2: Security Auditor               │           │
│   │   "Find every vulnerability"             │           │
│   │                                          │           │
│   │ Model #3: Optimizer                      │           │
│   │   "Make it faster, cleaner, better"      │           │
│   │                                          │           │
│   │ Model #4: Validator                      │           │
│   │   "Verify everything is correct"         │           │
│   │                                          │           │
│   │ Model #5: Cross-Examiner                 │           │
│   │   "Challenge every assumption"           │           │
│   └──────────────────────────────────────────┘           │
│                                                          │
│   RESULT: Output validated by 5 independent              │
│   AI "experts" before a single line is integrated        │
└─────────────────────────────────────────────────────────┘
```

**Key principle:** AI generates code in 5 minutes. The real work is the hours (sometimes days) spent cross-examining, validating, and iterating until every model agrees: "This is correct."

---

## FINAL WORD

> *"561 files. 195,000 lines. 4 languages. 6 months. Zero prior programming experience. One methodology: command AI models like a team of specialists, validate everything, never give up.*
>
> *This is not a claim. This is a repository. Read the code."*

---

**Angel Dimitrov** — Self-taught Software Developer & Systems Architect

*+359 88 888 1703 | angel.d.dimitrovv@gmail.com | github.com/Kalafara/Automated-Ecosystem-Demo*
