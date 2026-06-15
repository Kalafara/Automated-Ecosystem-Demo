Phantom Shield — Technical Architecture Overview

Architectural showcase of an automation ecosystem built from scratch in 6 months by a self‑taught developer using AI‑assisted methodology.


PROJECT SCALE

- Total lines of code: 150,000+ (excluding dependencies and build artifacts)
- Source files: 560+
- Programming languages: TypeScript, Python, C++, JavaScript, HTML/CSS
- Development time: 6 months (solo, self‑taught)
- AI tokens consumed: 8 billion+ across multiple models (paid)
- Bots: 6 independent Python automation engines
- Frontend views: 18+ specialized React components
- Databases: 3 independent SQLite databases with cloud backup
- Middleware layers: 8 defensive layers
- Cryptographic protocols: XChaCha20‑Poly1305, Ed25519, Falcon‑512, SHA‑3, BLAKE2
- Payment gateways: Stripe, PayPal, Coinbase


ARCHITECTURE OVERVIEW

The system consists of four main layers connected through a central server.

1. Client Layer – An Electron desktop application built with React 19. It connects to the backend via a custom encrypted WebSocket protocol. The client is a zero-footprint shell: all logic is streamed into RAM after authentication and wiped on session close.

2. Communication Layer – A custom privacy-preserving WebSocket protocol using XChaCha20-Poly1305 encryption. Real payload data is placed inside a 400KB buffer of random noise. The positions of the key, nonce, tag, and ciphertext are determined by HMAC-SHA512 with a hardware-bound seed. Large messages are chunked and protected with dual integrity checks (CRC32 + SHA-256). Anti-replay protection and constant-time operations guard against timing attacks.

3. Server Layer – A Node.js/TypeScript orchestrator with a 25-step initialization sequence. It manages 8 defensive middleware layers (rate limiting, anomaly detection, forensic logging, CSRF protection, JSON complexity guard, timing guard, resource guard, and a final security enforcement layer). The server exposes REST API endpoints, handles session management, and orchestrates the automation bots.

4. Automation and Security Layer – Six independent Python bots using OpenCV and PyAutoGUI for computer vision and GUI automation. A native C++ module provides hardware-bound security via TPM 2.0 attestation, memory protection with guard pages and stack canaries, and anti-debugging mechanisms. Dual-Path Verification requires both the Security module and a separate Mother module to validate a client independently before granting access.

Infrastructure – Docker multi-stage builds, deployment on Render Cloud, CI/CD via GitHub Actions. Cloud backups to Google Drive and Dropbox with self-healing recovery. Payment integration with Stripe, PayPal, and Coinbase for a 5-tier subscription system.


LEVEL 1: CRYPTOGRAPHY FROM SCRATCH (EDUCATIONAL IMPLEMENTATION)

Note: The cryptographic primitives below were implemented from scratch for educational purposes and deep understanding of the underlying mathematics. In a production environment, one would use well‑audited libraries like libsodium. The code demonstrates low‑level knowledge of bit‑wise operations, constant‑time programming, and side‑channel resistance.

Custom ChaCha20 Quarter Round

From server/src/utils/killSwitch.ts — 1,200+ lines of hand‑written cryptography:

// XChaCha20‑Poly1305 Implementation — custom, no external crypto libraries
class XChaCha20Poly1305 {
    private static readonly KEY_SIZE = 32;      // 256‑bit key
    private static readonly NONCE_SIZE = 24;    // 192‑bit nonce for XChaCha
    private static readonly TAG_SIZE = 16;      // 128‑bit authentication tag

    private static quarterRound(state: Uint32Array, a: number, b: number, c: number, d: number): void {
        // ChaCha20 quarter round operation (constant‑time)
        state[a] = state[a] + state[b]; state[d] ^= state[a];
        state[d] = (state[d] << 16) | (state[d] >>> 16);
        state[c] = state[c] + state[d]; state[b] ^= state[c];
        state[b] = (state[b] << 12) | (state[b] >>> 20);
        state[a] = state[a] + state[b]; state[d] ^= state[a];
        state[d] = (state[d] << 8)  | (state[d] >>> 24);
        state[c] = state[c] + state[d]; state[b] ^= state[c];
        state[b] = (state[b] << 7)  | (state[b] >>> 25);
    }
}

Why this matters: Writing ChaCha20 by hand requires understanding cryptographic primitives at the bit‑manipulation level. The code is constant‑time — resistant to timing side‑channel attacks.

Falcon‑512 Post‑Quantum Signatures

interface Falcon512KeyPair {
    publicKey: Uint8Array;  // 897 bytes
    privateKey: Uint8Array; // 1281 bytes
}

// Constant‑time comparison — timing‑attack resistant
class ConstantTime {
    static equals(a: Uint8Array, b: Uint8Array): boolean {
        if (a.length !== b.length) return false;
        let result = 0;
        for (let i = 0; i < a.length; i++) {
            result |= a[i] ^ b[i];
        }
        return result === 0;
    }
}

Why this matters: Falcon‑512 is a NIST‑standardized post‑quantum algorithm. The constant‑time implementation prevents attackers from extracting secrets via timing measurements.


LEVEL 2: SERVER ARCHITECTURE

PhantomServer Entry Point — 25‑Step Boot Sequence

From server/src/main.ts:

/**
 * PHANTOM SHIELD — PRODUCTION SERVER ORCHESTRATOR
 * 25‑step initialization, triple‑checkpoint handshake,
 * self‑healing recovery, real‑time threat response.
 */

// Security guard: ensure test bypass is disabled in production
if (process.env.DNA_ALLOW_TEST_BYPASS === 'true' &&
    (process.env.NODE_ENV || 'production') === 'production') {
    console.error('[SECURITY] DNA_ALLOW_TEST_BYPASS enabled in production — exiting');
    process.exit(1);
}

// Core modules
import { createEncryptionEngine } from './security/encryption';
import { streamGuard } from './middleware/streamGuard';
import { resourceGuard, jsonComplexityGuard } from './middleware/resourceGuard';
import { timingGuard } from './middleware/timingGuard';
import { HardwareValidator } from './security/hardware';
import { HeartbeatMonitor } from './network/heartbeat';
import { SecurityCore } from './security/securityCore';
import { SessionManager } from './core/sessionManager';
import { SubscriptionOrchestrator } from './core/subscriptionOrchestrator';
import { RecoverySystem } from './recovery/recovery';

Why this matters: The orchestrator manages 30+ subsystems. The first lines of executable code are a security check that intentionally prevents the server from running if misconfigured — defense in depth.


LEVEL 3: ENCRYPTED WEBSOCKET PROTOCOL

Privacy‑Preserving Communication with Obfuscation

From server/src/network/websocket.ts — 2,600+ lines:

const CONFIG = {
    TOTAL_BUFFER_SIZE: 409600,     // 400KB — data obfuscated in noise
    ENCRYPTED_DATA_MAX_SIZE: 307200, // 300KB max payload
    ENCRYPTION_ALGORITHM: 'XChaCha20‑Poly1305',
    HANDSHAKE_TIMEOUT: 10000,      // 10s
    MAX_CLOCK_SKEW_MS: 5000,       // Anti‑replay window
};

4‑phase handshake:

1. Client sends HWID (64/128 hex), server responds with challenge
2. HWID validation — hardware fingerprinting, VM detection, TPM presence check
3. Integrity challenge — SHA‑512 hash with pepper, constant‑time verification
4. Session validation — JWT or session token, hardware‑bound

Data transmission:

- Real payload encrypted with XChaCha20‑Poly1305
- Encrypted data is placed inside a 400KB buffer of random noise
- The positions of key, nonce, tag, and ciphertext within the buffer are determined by HMAC‑SHA512 with a hardware‑bound seed
- Large payloads are chunked with dual integrity checks (CRC32 + SHA‑256)
- All buffers are securely wiped after use

Why this matters: The protocol resists traffic analysis, replay attacks, and man‑in‑the‑middle interception. An observer sees only random data.


LEVEL 4: COMPUTER VISION AUTOMATION

Spiral Search Algorithm — Systematic Target Location

From server/protected_modules/bot/BOT3.py:

def move_map_spiral(current_target):
    """Methodical traversal via expanding square — 4 directions, 10‑min timeout"""
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
                    return loc
                    
            if dir_idx % 2 == 0:
                times_to_move += 1

OpenCV Visual Pattern Matching — RAM‑Only Asset Pipeline

def load_assets_from_stdin():
    """Stream 150+ reference images via base64 from server — never touches disk"""
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
    """Pattern matching with confidence thresholding"""
    screen = pyautogui.screenshot()
    screen_np = np.array(screen)
    screen_cv = cv2.cvtColor(screen_np, cv2.COLOR_RGB2BGR)
    
    if gray:
        screen_cv = cv2.cvtColor(screen_cv, cv2.COLOR_BGR2GRAY)
        template = cv2.cvtColor(asset_img, cv2.COLOR_BGR2GRAY)
    else:
        template = asset_img
    
    result = cv2.matchTemplate(screen_cv, template, cv2.TM_CCOEFF_NORMED)
    _, max_val, _, max_loc = cv2.minMaxLoc(result)
    
    if max_val >= conf:
        h, w = template.shape[:2]
        return (max_loc[0] + w // 2, max_loc[1] + h // 2)
    return None

Multi‑Layered Error Handling

Three independent fail‑safe mechanisms working together:

timeout_guard = 300      # LAYER 1: Timeout failsafe
retry_limit = 3          # LAYER 2: Retry limit with strategy switch
attempt_limit = 6        # LAYER 3: Smart abort condition

while not task_complete:
    if time.time() - start_time > timeout_guard:
        break
    if retries >= retry_limit:
        break
    perform_action()
    if check_success():
        task_complete = True
    else:
        retries += 1
        total_attempts += 1
        if total_attempts >= attempt_limit:
            break

Why this matters: Professional automation framework with three independent fail‑safe layers: timeouts, retry limits with strategy switching, and smart abort conditions. This follows patterns used in production test automation.


LEVEL 5: NATIVE C++ SECURITY MODULE

Hardware‑Level Memory Protection

From server/native/phantom_shield_native.cpp:

// Security module for automation systems
#define NAPI_VERSION 8
#define SODIUM_STATIC

#include <node_api.h>
#include <windows.h>
#include <winternl.h>      // NT kernel internals
#include <wincrypt.h>      // Windows Crypto API
#include <bcrypt.h>        // CNG — Next Gen Crypto
#include <ncrypt.h>        // TPM key storage
#include <tbs.h>           // TPM Base Services
#include <tss2/tss2_esys.h>// TPM 2.0 Enhanced System API
#include <intrin.h>        // CPU intrinsics

extern "C" {
#include "sodium.h"        // libsodium
}

// Constants
#define XCHACHA20_KEY_SIZE 32
#define SHA3_512_SIZE 64
#define GUARD_PAGE_SIZE 4096
#define MAX_GUARD_PAGES 256
#define INTEGRITY_CHECK_INTERVAL 5000
#define TPM_ATTESTATION_INTERVAL 60000

Subsystems:

- CryptographyEngine — XChaCha20‑Poly1305 + Ed25519 via libsodium
- TPMAttestation — TPM 2.0 integration via TSS2 (PCR quotes, attestation, hardware‑bound keys)
- MemoryGuard — SecureAllocation with SHA3‑512 hashes, guard pages, stack canaries
- IntegrityMonitor — Code, memory, stack, and heap hash verification every 5 seconds
- AntiDebug — Debugger, VM, and sandbox detection
- AuditLogger — Ed25519‑signed audit entries
- SecureWipe — Multi‑pass secure memory wiping on anomaly detection
- RuntimeProtection — JIT protection, timing anomaly detection

Why this matters: The module directly interfaces with Windows NT internals, TPM 2.0 hardware, and the Windows Cryptography API. This is systems programming comparable to endpoint security products.


LEVEL 6: FULL‑STACK GROWTH TREE

From One Script to an Ecosystem — 6 Months

Month 1: A single Python script using pyautogui.click() with hardcoded coordinates to automate a repetitive task.

Month 2: Added OpenCV for visual recognition with confidence thresholds and grayscale optimization. Created two more specialized bots.

Month 3: Started research on native C++ modules for hardware fingerprinting and basic encryption. Built the first Node.js server prototype.

Month 4: Developed the PhantomServer orchestrator with 25-step initialization and 8 middleware layers. Built the custom WebSocket protocol with XChaCha20 encryption and noise obfuscation. Created the Electron client with React 19. Added 4 more bots with multi-threading.

Month 5: Implemented a 5-tier subscription system with Stripe, PayPal, and Coinbase. Added active-only metering, midnight reset, and hardware-bound licenses. Trained YOLOv8 on 160,000 images over 370 epochs. Created Docker container and deployed on Render Cloud.

Month 6: Wrote the KillSwitch module — 1,200 lines of custom cryptography with Falcon-512 post-quantum signatures. Added Dual-Path Verification. Built self-healing cloud database recovery. Ran 23-tier stress tests. Completed 18+ React views, community chat, browser, and arcade games. Finalized all portfolio documents.


MULTI‑MODEL AI VALIDATION PIPELINE

This entire system was built using a proprietary methodology developed over 8 billion+ tokens of interaction with multiple AI models.

The workflow:

- Chief Architect (Human): Defines the architecture, assigns tasks, cross-validates all outputs, makes final integration decisions, and performs live testing.
- Model 1 (Code Generator): Writes the initial implementation.
- Model 2 (Security Auditor): Hunts for vulnerabilities and weaknesses.
- Model 3 (Optimizer): Proposes faster, cleaner, and more efficient alternatives.
- Model 4 (Validator): Verifies correctness against the specification.
- Model 5 (Cross-Examiner): Challenges every assumption to find logical gaps.

The process continues until all five AI models independently agree that the solution is correct. AI generates code in minutes. The real work is the hours spent cross‑examining, validating, and iterating.


PROJECT STATISTICS

- Total lines of code: 150,000+
- Source files: 561
- Languages: TypeScript, Python, C++, JavaScript, HTML/CSS
- AI tokens consumed: 8 billion+ (paid) + estimated 16 billion+ (free models)
- Bots: 6 independent Python engines
- Frontend views: 18+ React components
- Databases: 3 SQLite databases with cloud backup
- Payment gateways: Stripe, PayPal, Coinbase


"561 files. 150,000 lines. 4 languages. 6 months. Self‑taught. One methodology: command AI models like a team of specialists, validate everything, never give up.

This is not a claim. This is a repository. Read the code."

Angel Dimitrov — Self‑taught Software Developer & Systems Architect

+359 88 888 1703 | angel.d.dimitrovv@gmail.com | github.com/Kalafara/Automated-Ecosystem-Demo
