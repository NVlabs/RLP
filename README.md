# RLP: Reinforcement Learning **Pre‑training** 
_A verifier‑free, information‑gain objective that teaches models to “think before predicting” during pre‑training._

[![Paper](https://img.shields.io/badge/Paper-arXiv-TBD)](#paper)

**Teach models to think *during* pretraining, not just after.**


> We introduce **RLP (Reinforcement Learning Pre‑training)**: treat chain‑of‑thought (CoT) as an *action* taken before next‑token prediction, and reward it by the **information gain** it provides on the observed next token. This yields a **verifier‑free, dense** reward that can be applied to ordinary pre‑training text. On **Qwen3‑1.7B‑Base**, RLP improves the overall math+science average by **≈ +19%** over the base model and **≈ +17%** over compute‑matched continuous pre‑training; after identical post‑training the gains **compound**. On a **12B hybrid Mamba‑Transformer (NeMo‑12B)**, the overall average rises from **42.81 → 61.32** (+18.51 points), with large science reasoning gains.

## RLP at a glance

**Idea.** Before predicting token $x_t$, sample a short **thought** $c_t$ (CoT) from the model. Then score the true next token twice:

* **Reasoned scorer:** $\log p_\theta\!\big(x_t \,\big|\, x_{<t}, c_t\big)$
* **No-think baseline (EMA teacher):** $\log \bar p_\phi\!\big(x_t \,\big|\, x_{<t}\big)$

**Reward (information gain):**

$$
r(c_t) \;=\; \log p_\theta(x_t \mid x_{<t}, c_t)\;-\;\log \bar p_\phi(x_t \mid x_{<t})
$$

This is **dense** (per token), **verifier-free**, and aligned with pre-training data.

**Optimization.**

* Sample **$G$** thoughts per position (group-relative advantages reduce variance).
* Update **only the thought tokens** via a clipped surrogate (behavior snapshot; per-token importance ratios).
* Maintain a **slowly updated EMA** teacher as the no-think counterfactual.

**Why it helps.**

* Rewards thoughts **in proportion to predictive utility** (not verbosity).
* Provides **position-wise credit** at every token—no external verifiers or entropy filters.
* Interleaves naturally with standard pre-training data.

---

## Next token prediction Comparison 

## Key results

### 🔹 Qwen3 1.7B Base

* **Setup:**

  * We compare **RLP** against both the base model (**BASE**) and a compute matched **Continuous Pretraining (CPT)** baseline.
  * All models use the same **SFT + RLVR post training** pipeline for a fair comparison.

* **Pretraining Gains:**

  * **RLP outperforms BASE by +19%** and **CPT by +17%** on average across math and science benchmarks.
  * These improvements come **without extra compute**, showing the gains are from methodology rather than raw FLOPs.

* **Post Training Synergy:**

  * After identical SFT + RLVR, **RLP compounds its advantage**, achieving:

    * **+8% relative over BASE+Post**
    * **+7% relative over CPT+Post**
  * This shows that **RLP builds durable reasoning foundations** that are strengthened, not erased, by downstream alignment.

* **Takeaway:**

  * Unlike next token prediction or continuous pretraining, **RLP instills reasoning during pretraining itself**.
  * These early advantages persist through post training, giving models **stronger and more robust reasoning capabilities**.


### 🔹 Nemotron Nano 12B v2 Base

* **Setup:**

  * We compare an intermediate checkpoint of **Nemotron-Nano-12B-v2-Base** trained on **19.8T tokens** with **RLP applied for only 250M tokens**.
  * The **BASE** model, in contrast, is trained fully on **20T tokens**.

* **Pretraining Gains:**

  * **RLP substantially outperforms BASE across all domains** despite using **~200B fewer tokens**.
  * On average, **RLP is +35% better than BASE**, highlighting both efficiency and scalability.

* **Domain Specific Improvements:**

  * **Math performance** improves moderately.
  * The largest gains are in **science reasoning**, where **Science Avg improves by +23 absolute points**.

* **Takeaway:**

  * The benefits of **RLP not only persist but amplify** at larger model scales.
  * RLP generalizes effectively across architectures, yielding robust reasoning improvements even in hybrid models like Nemotron.