# econ5200-assignment2
# Audit 02: Deconstructing Statistical Lies

> "There are three kinds of lies: lies, damned lies, and statistics." — Mark Twain

This audit examines three common statistical deceptions that distort decision-making in data-driven systems. Through visualization and analysis, we expose how summary metrics can mask reality.

---

## 1. Latency Skew: When Averages Lie

### The Problem

A system reports **"average latency: 50ms"** — sounds great, right?

<img width="870" height="556" alt="image" src="https://github.com/user-attachments/assets/85297d33-004f-4ea0-84d3-2cd7a7b5b5f6" />


**What the histogram reveals:** Nearly all requests (~980) complete in under 100ms, but the distribution has a **heavy tail** extending to 5,000ms. Those rare slow requests? They're the ones your users remember.

### Key Findings

| Metric | Value | What It Hides |
|--------|-------|---------------|
| Mean | ~50ms | Pulled up by outliers |
| Median | ~20ms | Ignores the tail entirely |
| P99 | ~2,500ms | **This is your real problem** |

### The Lesson

**Always report percentiles (P50, P95, P99), not just averages.** A 1% failure rate at scale means thousands of frustrated users. The mean is a comfortable lie; the P99 is the uncomfortable truth.

---

## 2. Survivorship Bias: The Graveyard You Don't See

### The Problem

A crypto analyst claims: **"Tokens that survive show healthy market cap distributions!"**

![Survivorship Bias](survivorship_comparison.png)

**Left panel — "The Graveyard":** Over 4,400 tokens peaked below 1 (normalized market cap). The vast majority failed catastrophically.

**Right panel — "The Survivors":** Only the top 1% remain. Their distribution looks almost reasonable — peak caps ranging from 5 to 25.

### Key Findings

| Population | Sample Size | Peak Market Cap Range | Survival Rate |
|------------|-------------|----------------------|---------------|
| All Tokens | ~10,000+ | 0 – 25 | 100% |
| Survivors | ~50-100 | 5 – 25 | **~1%** |

### The Lesson

**Success stories are selected, not representative.** When someone shows you "what winners look like," ask: *"Where are the 99% that failed?"* Survivorship bias is how we convince ourselves that success is more achievable — and more replicable — than it actually is.

---

## 3. False Positives: The Base Rate Trap

### The Problem

A fraud detection system boasts **"99% accuracy!"** But in a population where only 0.1% are actually fraudulent:

| | Predicted Fraud | Predicted Legitimate |
|---|---|---|
| **Actual Fraud** | 99 (TP) | 1 (FN) |
| **Actual Legitimate** | 999 (FP) | 98,901 (TN) |

### Key Findings

- **Precision:** 99 / (99 + 999) = **9%**
- **Of every 11 "fraud" alerts, 10 are innocent people.**

A 99% accurate test can still be **91% wrong** when it flags someone.

### The Lesson

**Accuracy without base rates is meaningless.** In rare-event detection (fraud, disease, security threats), false positives dominate. Always ask: *"What's the positive predictive value?"*

---

## Summary: Questions to Always Ask

| Deception | The Lie | The Question |
|-----------|---------|--------------|
| Latency Skew | "Average is 50ms" | What's the P99? |
| Survivorship Bias | "Winners look like X" | Where are the failures? |
| False Positives | "99% accurate" | What's the precision at this base rate? |

---

## Tools & Methodology

- **Visualization:** Histograms with appropriate binning to reveal distribution shapes
- **Metrics:** Percentile analysis, confusion matrices, population segmentation
- **Principle:** Always compare summary statistics against full distributions

---

*Part of the Statistical Literacy Audit Series*  
*Author: [Your Name]*  
*Date: February 2026*
