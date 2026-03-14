
<div align="center">
# 📋 Settlement Ratio Gap

### *Why does a 98% CSR become 88% — for the same insurer, same year?*

[![Dataset](https://img.shields.io/badge/Data-IRDAI%20India-terracotta?style=flat-square&color=9C3A28)](https://www.kaggle.com/datasets/bhanageviraj/life-insurance-death-claims)
[![Claims](https://img.shields.io/badge/Claims-7.2M-slate?style=flat-square&color=3A5C70)](https://www.kaggle.com/datasets/bhanageviraj/life-insurance-death-claims)
[![Period](https://img.shields.io/badge/FY-2017%E2%80%932022-olive?style=flat-square&color=4A7050)](https://claude.ai/chat/9a55a615-11d7-4e80-8121-fb70a2bb1377)
[![Visualization](https://img.shields.io/badge/%F0%9F%94%97-Interactive%20Demo-amber?style=flat-square&color=B87006)](https://kristianto.pages.dev/projects/India-insurance-analyst/visualization)

</div>
---

---

## The Problem

Claim Settlement Ratio (CSR) is *the* single number consumers use to pick a life insurer. Most headlines report it by  **claim count** . But for anyone holding a large policy, the number that actually matters is CSR by **claim value** — and the two are rarely the same.

This project asks: *is that gap random noise, or something structural?*

<br>
## 💡 Two Findings That Changed the Frame

**① The gap is not a coincidence**

> Out of 117 insurer-year observations, **115 showed a negative gap** — amount CSR below count CSR.
> `p = 8.31 × 10⁻³²`

This isn't a reporting artifact. It's a mathematical consequence of how claims get investigated.

---

**② The same data, two completely different rankings**

```
                  by Count          by Value        Shift
  HDFC Life       98.52%  (#3)  →   88.52%  (#20)   ↓ 17 ranks
  Aegon           97.68%  (#6)  →   96.24%  (#4)    ↑  2 ranks
  Shriram         89.62%  (#18) →   77.30%  (#24)   ↓  6 ranks
```

> A policyholder choosing HDFC based on its "99% CSR" headline is reading a number built from small-claim experience — not theirs.

<br>
## ⚙️ The Mechanism

The gap has an exact identity — no distribution assumptions required:

$$
\text{Gap} = \frac{\text{Cov}(X,; p(X))}{\mathbb{E}[X]}
$$

As long as larger claims face more scrutiny (`p'(x) < 0`), the covariance is negative, and the gap is  **mathematically unavoidable** .

This project also introduces **Investigation Intensity** — a behavioral metric that captures *how differently* an insurer treats small vs. high-value claims:

$$
\text{Investigation Intensity} = -\text{Gap} \times \mathbb{E}[X]
$$

It re-ranks insurers in ways CSR alone never could.

<br>
## ⚖️ Honest Trade-offs

| ✅ Solid                               | ⚠️ Caveat                                     |
| -------------------------------------- | ----------------------------------------------- |
| Gap identity is mathematically exact   | β̂ estimates assume uniform CV = 1.5          |
| 98.3% sign test is near-certain        | Gap ≠ proof of intentional claim rejection     |
| Investigation Intensity proxy is valid | Individual death claims only — no group/health |

<br>
## 🗺️ What's Next

* [ ] Fit logistic regression on individual claim records to validate β̂ directly
* [ ] Segment by product line — does β differ for term life vs. ULIP?
* [ ] Extend to other regulators
* [ ] Consumer tool: *"Enter your sum assured → find the right insurer for your risk profile"*

<br>
## 📁 Repository

```
├── notebooks/
│   └── claim_decision_model.ipynb          ← Monte Carlo: lognormal · Pareto · Weibull
└── outputs/
    └── working_paper.pdf                   ← full working paper (LaTeX)
```

<br>
---

<div align="center">
*"Settlement Ratio Gap is not just a reporting number —*
*it's a window into how a company's claim decision engine actually works."*

<br>
**Kristianto** · Insurance & Risk Analytics · [kristianto.pages.dev](https://kristianto.pages.dev/) · March 2026

</div>
