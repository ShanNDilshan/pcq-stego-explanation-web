# PQ-Stego — Website Content & Marketing Document

## 🎯 Product Identity

**Name:** PQ-Stego  
**Tagline:** *Hide Smarter. Stay Quantum-Safe.*  
**Sub-tagline:** The first ML-guided steganography system secured by post-quantum cryptography.

**One-liner Value Proposition:**  
PQ-Stego protects your most sensitive data not just by encrypting it — but by making it **completely invisible**, and ensuring the encryption itself is **unbreakable by future quantum computers**.

---

## 🧠 Marketer's Content Strategy

### 1. The Hook — What Problem Are We Solving?

Most people think encryption is enough. It isn't.

When you encrypt a file, you protect what's inside — but you broadcast that *something secret is being sent*. In surveillance-heavy environments, intelligence interception, or high-stakes communications, just **showing encrypted traffic is enough to flag you**.

Steganography solves that. It hides your data *inside* ordinary images or audio files — no padlocks, no suspicion.

But traditional steganography has two critical flaws:
1. **It's blind** — it embeds data in random regions, making it statistically detectable by AI-based steganalysis tools.
2. **It's classically encrypted** — RSA and ECC, the most widely used encryption standards, will be cracked by quantum computers within the decade (per NIST projections).

**PQ-Stego fixes both.**

---

### 2. The Solution — What Is PQ-Stego?

PQ-Stego is a hybrid security system that combines:

- **AI-guided steganography** — Uses a CNN-based machine learning model trained to identify *perceptually safe* regions in images and audio before embedding. It knows *where* to hide so no one can find it.
- **Capacity prediction** — A regression ML model accurately predicts the *maximum safe payload* the media can hold without triggering statistical detection.
- **Heatmap visualization** — The system generates a visual heatmap showing exactly which regions are being used, giving engineers full transparency.
- **Post-Quantum Cryptography (PQC)** — Payloads are encrypted with AES-256, key-encapsulated via **CRYSTALS-Kyber** (NIST PQC standard), and digitally signed with **CRYSTALS-Dilithium** — both immune to quantum attacks.
- **Multi-layer defense** — The data is encrypted *before* it's hidden. Even if someone finds the steganographic data, they still cannot read it without quantum-resistant keys.

---

### 3. How It Works — The Workflow

**Step 1 — Encrypt Payload**  
Your message or file is encrypted with AES-256. The symmetric key is then encrypted with Kyber (lattice-based key encapsulation). Dilithium creates a signature ensuring message authenticity and integrity.

**Step 2 — Analyze Media**  
The carrier file (a `.pgm` image or `.wav` audio) is passed through CNN models. The image model performs spatial analysis to identify low-perceptual-sensitivity zones. The audio model analyzes spectral frequency characteristics.

**Step 3 — Predict Safe Capacity**  
A regression model predicts the exact maximum number of bits that can be safely embedded without statistical detection or perceptual distortion.

**Step 4 — Generate Heatmap**  
A heatmap is generated that marks exactly which regions of the carrier are being used — green zones (safe to embed), red zones (avoid). This is a key differentiator — no other steganography tool offers ML-guided spatial awareness.

**Step 5 — Embed Payload**  
For images: DCT-QIM (Discrete Cosine Transform with Quantization Index Modulation) — used in JPEG frequency domain, highly robust.  
For audio: LSB (Least Significant Bit) substitution balanced with SNR-safe thresholds.

**Step 6 — Retrieve & Verify**  
Receiver uses Kyber private key to decapsulate AES key, Dilithium public key to verify signature, and the system automatically extracts the payload with checksum verification.

---

### 4. Competitive Advantage — Why PQ-Stego Wins

| Feature | Traditional Steganography | PQ-Stego |
|---|---|---|
| Encryption | RSA / ECC (quantum-vulnerable) | Kyber + Dilithium (NIST PQC Standard) |
| Embedding Strategy | Random / uniform | ML-guided, perception-aware |
| Detectability Risk | High (statistical anomalies) | Low (tested under steganalysis) |
| Capacity Awareness | None | ML regression prediction |
| Media Support | Usually image only | Image (.pgm) + Audio (.wav) |
| Payload Verification | None | Checksum + Dilithium signature |
| Future-Proofing | Breaks with quantum computers | Designed for the post-quantum era |

---

### 5. Results — What the Numbers Say

**Image Quality (PSNR):** 44+ dB — Well above the 30 dB threshold considered imperceptible to the human eye. The embedded carrier is visually identical to the original.

**Structural Similarity (SSIM):** 0.99 — Near-perfect structural preservation. The image structure, texture, and luminance are nearly unchanged.

**Audio Quality (SNR):** 110 dB — Exceptionally high signal clarity. The audio embedding introduces no audible distortion.

**Audio Perceptual Quality (MOS):** High Quality — Listeners could not distinguish original from embedded audio clips.

**Capacity Correlation:** R = 0.9991 — The ML model's predicted safe capacity matches actual safe capacity with 99.91% correlation. This is production-grade accuracy.

**Robustness:** The system successfully recovers embedded payloads even under JPEG compression and Gaussian noise attacks — as validated in the noise/compression robustness analysis chart.

---

### 6. Key Figures / Images

| Image | Location | Usage |
|---|---|---|
| System Architecture Diagram | `images/system-architecture.jpeg` | Architecture section — shows full pipeline |
| Embedded Image Result | `images/embedded-image.png` | Results section — before/after image |
| Embedded Audio Result | `images/embedded-audio.png` | Results section — audio waveform comparison |
| Predicted vs Actual Capacity | `images/predicted-vs-actual.jpg` | Results section — scatter plot proving ML accuracy |
| Noise/Compression Robustness | `images/noise-compression.jpg` | Results section — bar/line chart proving robustness |
| Hero Background | `images/hero-bg.jpg` | Hero section background texture |
| Python Logo | `images/Python.png` | Tech stack section |
| PyTorch Logo | `images/pytorch.png` | Tech stack section |
| FastAPI Logo | `images/fastapi.png` | Tech stack section |
| OpenCV Logo | `images/opencv.png` | Tech stack section |
| NumPy Logo | `images/numpy.png` | Tech stack section |
| Matplotlib Logo | `images/matplotlib.jpg` | Tech stack section |

---

### 7. Website Section Map (Marketing Flow)

1. **Hero** — Bold hook: "Hide Smarter. Stay Quantum-Safe." + Product one-liner + CTAs
2. **The Problem** — 3 pain cards: Blind Embedding / Quantum Threat / Detection Risk
3. **The Solution** — What PQ-Stego is in one product pitch
4. **How It Works** — 6-step animated workflow (numbered cards)
5. **Architecture** — Full system diagram with concise explanation
6. **Technology** — Tech stack logos (Python, PyTorch, FastAPI, OpenCV, NumPy)
7. **Results & Performance** — Key metric numbers first (PSNR, SSIM, SNR, Correlation) then result images
8. **Competitive Advantage** — Comparison table vs. traditional approaches
9. **Research Team** — Team photos, names, supervisors
10. **Footer** — University, department, year

---

### 8. Tone & Voice Guidelines

- **Confident, not academic.** Avoid "this research proposes..." — say "PQ-Stego solves..."
- **Outcome-first.** Lead with results and benefits, then explain the method.
- **Security-specialist audience.** Readers understand crypto terms but want clear product framing.
- **No padding.** Every sentence must deliver value. Cut filler phrases.
- **Credibility signals.** Use exact numbers (0.9991 correlation, 44+ dB PSNR, NIST PQC standard) to build trust.
