# Cipher-AI-Analysis

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Last Commit](https://img.shields.io/github/last-commit/JamieGrunewald/cipher-ai-analysis)
![Status](https://img.shields.io/badge/ai__fingerprinting-in%20development-orange)

Statistical analysis tools for classical cipher breaking and AI-generated text fingerprinting.

**Jamie Grunewald** | [LinkedIn](https://www.linkedin.com/in/jamielg) | [github.com/JamieGrunewald](https://github.com/JamieGrunewald)

---

## Overview

This repository applies statistical text analysis techniques across two domains:

1. **Classical Cipher Breaking** — frequency analysis, Index of Coincidence, and chi-square scoring to break polyalphabetic ciphers without prior knowledge of the key.
2. **AI Text Fingerprinting** *(in development)* — extending the same statistical foundations to detect authorship signatures in AI-generated text.

The cipher analysis module originated as a live demo for the CypherCon 9 talk **"Breaking Ciphers & Fingerprinting AI"** (Milwaukee, April 2026), based on graduate cryptography research at the University of Delaware (CPEG 472).

---

## Repository Structure

```
cipher-ai-analysis/
├── cipher_analysis/
│   ├── cyphercon_demo.py               # Live demo: break a Vigenère-encrypted WarGames quote
│   ├── words.txt                       # English word list for plaintext scoring
│   ├── sample_output.txt               # Reference output from a clean run
│   └── BreakingCiphers_Cyphercon9.pdf  # CypherCon 9 slide deck
├── ai_fingerprinting/                  # Coming soon
└── README.md
```

---

## Cipher Analysis

### The Attack Pipeline

A complete Vigenère cipher break executed in seven steps:

| Step | Technique | Purpose |
|------|-----------|---------|
| 1 | Ciphertext display | Establish the problem |
| 2 | IOC + Chi-Square | Statistical recon — identify cipher type |
| 3 | IOC column sweep | Determine key length |
| 4 | Per-column frequency attack | Recover alphabetic key characters |
| 5 | Word-list disambiguation | Resolve chi-square near-ties |
| 6 | Key reconstruction | Reveal the full key |
| 7 | Plaintext recovery | Decrypt the ciphertext |

### Running the Demo

**Requirements:** Python 3.8+, no external dependencies.

```bash
# Interactive mode (press ENTER to advance each step)
python3 cipher_analysis/cyphercon_demo.py

# Auto mode (timed pauses — useful for recording)
python3 cipher_analysis/cyphercon_demo.py --auto
```

`words.txt` must be in the same directory as the script.

---

## AI Fingerprinting *(coming soon)*

The same statistical patterns that expose a repeating cipher key also expose authorship signatures in text. The planned module will apply IOC, character frequency distributions, and stylometric scoring to compare text samples and identify AI-generated content.

### Why This Is Hard (And Interesting)

A fair question: if both humans and LLMs write in English, aren't their statistical profiles nearly identical?

Yes.  That is exactly what makes it interesting.

Gross statistics like letter frequency and Index of Coincidence will look nearly identical between human and LLM output. You won't separate them with the same tools that crack a Vigenère cipher. The signal is finer than that.

But LLMs don't sample from natural English — they sample from a learned approximation of it, and that approximation has detectable artifacts:

- **Entropy consistency** — human writing has high local entropy variance (some sentences are predictable, some aren't). LLM output tends to hover in a narrower band.
- **Token-level patterns** — characteristic preferences at the subword level that don't match human writing distributions, particularly around punctuation, transition phrases, and hedge language.
- **Perturbation response** — the most promising signal. Slightly perturb a passage and re-score it; LLM output shows a characteristic pull back toward high-probability tokens that human writing doesn't. This is the core idea behind DetectGPT.

The bridge from cipher analysis isn't the specific metrics — it's the mindset: measure structure, probe the system, follow the gradient signal. The tools change. The approach doesn't.

---

## Background

The cipher analysis pipeline mirrors the full implementation in the [Crypto](https://github.com/JamieGrunewald/Crypto) repository (CPEG 472 coursework). The demo script is self-contained for portability.

---

## License

MIT License — see [LICENSE](LICENSE)
