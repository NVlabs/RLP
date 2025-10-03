# RLP: Reinforcement as a Pretraining Objective 

[![Star on GitHub](https://img.shields.io/github/stars/NVlabs/RLP.svg?style=social)](https://github.com/NVlabs/RLP/stargazers)

Official repository of [**RLP: Reinforcement as a Pretraining Objective**](https://arxiv.org/abs/2510.01265). 


_A verifier‑free, information‑gain objective that teaches models to “think before predicting” during pre‑training._

[![Paper](https://img.shields.io/badge/Paper-arXiv-TBD)](https://arxiv.org/abs/2510.01265)

[Ali Hatamizadeh[^1]](https://research.nvidia.com/person/ali-hatamizadeh),
[Syeda Nahida Akter[^1]](https://snat1505027.github.io/),
[Shrimai Prabhumoye[^1]](https://shrimai.github.io/),
[Jan Kautz](https://jankautz.com/),
[Mostofa Patwary](https://sites.google.com/view/mostofa-patwary),
[Mohammad Shoeybi](https://developer.nvidia.com/blog/author/mshoeybi/),
[Bryan Catanzaro](https://developer.nvidia.com/blog/author/bcatanzaro/),
[Yejin Choi](https://yejinc.github.io/).

[^1]: Equal Contribution

**Teach models to think *during* pretraining, not just after.**

<img width="1829" height="433" alt="framework" src="https://github.com/user-attachments/assets/db9bec5f-0912-464f-accb-f27e4967983e" />

> We introduce **RLP (Reinforcement Learning Pre‑training)**: treat chain‑of‑thought (CoT) as an *action* taken before next‑token prediction, and reward it by the **information gain** it provides on the observed next token. This yields a **verifier‑free, dense** reward that can be applied to ordinary pre‑training text. On **Qwen3‑1.7B‑Base**, RLP improves the overall math+science average by **≈ +19%** over the base model and **≈ +17%** over compute‑matched continuous pre‑training; after identical post‑training the gains **compound**. On a **12B hybrid Mamba‑Transformer (NeMo‑12B)**, the overall average rises from **42.81 → 61.32** (+18.51 points), with large science reasoning gains.

---

## Next token prediction comparison 

<p align="center">
<img src="https://github.com/user-attachments/assets/a57a0b88-6687-4f0d-9cf0-bd83dd56eb49" width=62% height=62% 
class="center">
</p>


## Key results

### 🔹 Qwen3 1.7B Base

<p align="center">
<img src="https://github.com/user-attachments/assets/77a75776-8cfc-4e45-ad53-1900e4ea8fa9" width=62% height=62% 
class="center">
</p>


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

<p align="center">
<img src="https://github.com/user-attachments/assets/8f343919-0e9a-4a11-9250-a8cdb99321d8" width=62% height=62% 
class="center">
</p>

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


## Citation

If you find RLP to be useful for your work, please consider citing our paper: 

```
@article{hatamizadeh2025rlp,
  title={RLP: Reinforcement Learning Pre‑training},
  author={Hatamizadeh, Ali and Akter,  Syeda Nahida and Prabhumoye, Shrimai and Kautz, Jan and Patwary, Mostofa and Shoeybi,  Mohammad and Catanzaro, Bryan and Choi, Yejin},
  journal={arXiv preprint arXiv:2510.01265},
  year={2025}
}
```

## Star History

[![Stargazers repo roster for @NVlabs/RLP](https://bytecrank.com/nastyox/reporoster/php/stargazersSVG.php?user=NVlabs&repo=RLP)](https://github.com/NVlabs/RLP/stargazers)

[![Star History Chart](https://api.star-history.com/svg?repos=NVlabs/RLP&type=Date)](https://star-history.com/#NVlabs/RLP&Date)


## Licenses

Copyright © 2025, NVIDIA Corporation. All rights reserved.
 
