# 🔐 4-Bit XOR-Based Data Encryption & Decryption Unit

> **Repository:** `KLH-CSE-2026-2030-<TeamID>-XOR-EncDec`
> **Course:** Digital Design and Computer Architecture (DDCA)
> **Current phase:** 🟢 Design & simulation complete (see [Project Status](#-project-status))

![Complete circuit](docs/images/full_circuit.png)

---

## 👥 Team

| Name                              | Registration / ID No. | GitHub |
|-----------------------------------|-----------------------|--------|
| Shreyesh Reddy Gudi               | 2620030608            | `@<username>` |
| Kaustubha Srinivas Kaseebhotla    | 2620030601            | `@<username>` |
| Rachuri Harshita                  | 2620030654            | `@<username>` |
| Rudrakashala Harshitha            | 2620030591            | `@<username>` |

**Supervisor:** Kartheek
**Department:** Computer Science and Engineering, KL University, Hyderabad
**Program:** B.Tech CSE, Batch-10 (2026–2030)

---

## 📄 Abstract

Cryptography is essential for securing digital data. The XOR operation is a fundamental building block of many ciphers because it is perfectly reversible. However, most demonstrations of encryption are software-only, and real ciphers such as AES and DES are too complex to design and wire in an undergraduate lab.

This project designs and simulates a **4-bit symmetric-key encryption and decryption unit** in Logisim. It is built entirely from combinational logic. A 4-bit plaintext `P` is XORed with a 4-bit key `K` to produce the ciphertext `C = P ⊕ K`. The same key, applied again, recovers the original message: `D = C ⊕ K = P`. Four bit-wise comparators then verify that the decrypted output matches the plaintext.

The design uses **8 XOR gates and 4 comparators**, with no clock, memory, encoders or decoders. All 16 input combinations tested in simulation decrypted back to the original plaintext.

---

## 🧱 Architecture

```
            ┌──────────────┐        ┌──────────────┐
 P[3:0] ───►│ XOR ENCRYPT  │─ C ───►│ XOR DECRYPT  │─── D[3:0]
    │       │  C = P ⊕ K   │        │  D = C ⊕ K   │      │
    │       └──────▲───────┘        └──────▲───────┘      │
    │              │                       │              ▼
    │              └───────── K[3:0] ──────┘       ┌─────────────┐
    │                    (same key reused)         │ COMPARATOR  │──► MATCH
    └─────────────────────────────────────────────►│   D == P ?  │
                                                   └─────────────┘
```

| Stage        | Equation |
|--------------|----------|
| Encryption   | C<sub>i</sub> = P<sub>i</sub> ⊕ K<sub>i</sub> |
| Decryption   | D<sub>i</sub> = C<sub>i</sub> ⊕ K<sub>i</sub> = P<sub>i</sub> |
| Verification | Match<sub>i</sub> = (D<sub>i</sub> == P<sub>i</sub>) |

| Component          | Count | Purpose |
|--------------------|:-----:|---------|
| Input pins         | 8     | 4 plaintext bits (P0–P3) and 4 key bits (K0–K3) |
| XOR gates          | 8     | 4 for encryption (C0–C3) and 4 for decryption (D0–D3) |
| Comparators        | 4     | One per bit, comparing D<sub>i</sub> with P<sub>i</sub> |
| Flip-flops / clock | 0     | The design is purely combinational |

---

## 📁 Repository Structure

```
.
├── src/                  # Logisim circuit file (.circ)
├── docs/                 # Documentation and circuit screenshots
│   └── images/
├── data/                 # Data-source note (no external dataset; inputs set via pins)
├── results/              # Truth tables, test vectors and verification screenshots
├── reports/              # Project presentation and review reports
└── README.md
```

---

## ⚙️ Setup & Execution

### Prerequisites

- [Logisim](http://www.cburch.com/logisim/) or [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution) (requires Java)

### Run the simulation

1. Clone the repository:
   ```bash
   git clone https://github.com/<org-or-user>/KLH-CSE-2026-2030-<TeamID>-XOR-EncDec.git
   ```
2. Open Logisim and choose **File → Open**. Select the `.circ` file in [`/src`](src/).
3. Pick the **Poke tool** (hand icon) from the toolbar.
4. Click pins **P0–P3** to set the plaintext and **K0–K3** to set the key.
5. Observe the outputs:
   - **C0–C3** show the ciphertext, which updates instantly.
   - **D0–D3** show the decrypted bits, which always equal P.
   - The **comparator outputs** stay lit, confirming each bit matches.

### Example

| Input | Value | Expected output |
|-------|-------|-----------------|
| P     | 1011  | C = 0111        |
| K     | 1100  | D = 1011 → MATCH ✅ |

Full results are in [`/results/results.md`](results/results.md).

---

## 📌 Project Status

| Phase | Deliverable | Status | Git tag |
|-------|-------------|:------:|---------|
| Design | Architecture, objectives, logic equations | ✅ Complete | — |
| Implementation | Logisim circuit with bit-wise verification | ✅ Complete | — |
| Review 1 | _update_ | ⬜ Pending | `review-1` |
| Review 2 | _update_ | ⬜ Pending | `review-2` |
| Final | Final circuit, report and presentation | ⬜ Pending | `final` |

_Last updated: <DD-MM-YYYY>_

---

## ⚠️ Limitations & Future Scope

This is an **educational demonstration** of symmetric-key logic. It is a single-round XOR cipher and is **not production-grade security**. Reusing one key across multiple messages would be vulnerable.

Possible future work:

- **Wider data path.** Scale to 8-bit or 16-bit words.
- **Pseudo-random keys.** Add a key generator or key schedule, moving toward real stream-cipher practice.
- **Reusable module.** Use the unit as a building block in larger digital designs.

---

## 🤝 Contribution Guidelines (Team)

- Every member commits from their **own GitHub account**. Bulk uploads through a single account are not permitted.
- Make **at least one meaningful commit per week** during each phase.
- Tag each major deliverable. For example:
  ```bash
  git tag -a review-1 -m "Review 1 deliverable"
  git push origin review-1
  ```
- Do **not** rename, transfer or move this repository once its URL is recorded without prior written approval from the Course Coordinator.
