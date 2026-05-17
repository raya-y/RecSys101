# RecVAE with Weighted Similarity Ensemble for Book Recommendation

Course project for **CCAI 422 Recommender Systems**, University of Jeddah, Second Semester 2025/2026.

This repository contains our reproduction and extension of a RecVAE-based recommendation approach that combines user-item and item-item similarity signals. The original paper introduced a fixed weighted-sum ensemble; we re-implement it on a new dataset (Goodbooks-10k) and add a small personalized weighting scheme that adapts to each user's history length.

---

## What the project does

In one paragraph: we train a Variational Autoencoder (RecVAE) on user-book interactions to learn shared latent embeddings for users and items. From those embeddings we compute two recommendation signals — a direct user-item similarity score (R) and an item-item neighbourhood score (S) — then mix them with weighted-sum ensembles. The paper tests five global weight ratios; our extension replaces the single global ratio with per-user weights that depend on how many books a user has read. The models are evaluated with HR@K and NDCG@K for K in {5, 10, 20}.

---

## Paper being reproduced

The paper proposes a weighted ensemble that combines:

- **R<sub>u,i</sub>** — user-item cosine similarity between the user embedding `p_u` and the item embedding `q_i` (Eq. 1).
- **S<sub>u,i</sub>** — item-item similarity averaged over the user's interaction history (Eq. 2).
- **Z<sub>u,i</sub>** — weighted combination `(w_R · R + w_S · S) / (w_R + w_S)` (Eq. 3).

Five global ratios are evaluated: 1:4, 2:3, 1:1, 3:2, 4:1. The paper's claim is that the ensemble outperforms either signal used alone.

---

## Dataset

We use the **Goodbooks-10k** dataset (different from the one in the original paper, per the project rules).

| Property | Value |
|---|---|
| Source | https://github.com/zygmuntz/goodbooks-10k |
| Users | ~53,000 (after filtering) |
| Books | 10,000 |
| Ratings | ~981,000 |
| Scale | 1 to 5 |

**Why this dataset.** Goodbooks-10k is a standard implicit-feedback benchmark for top-N book recommendation. It is sparse, has a wide popularity distribution, and gives enough users with rich histories to make the personalized weighting meaningful — which matched what we needed to stress-test the ensemble.

---

## References

- Goodbooks-10k dataset, Zajac Z.: https://github.com/zygmuntz/goodbooks-10k
- Shenbin, I., Alekseev, A., Tutubalina, E., Malykh, V., & Nikolenko, S. I. (2020). *RecVAE: A New Variational Autoencoder for Top-N Recommendations with Implicit Feedback*. WSDM 2020.
- The course paper our project is built on (full citation in the final report PDF).

---

## License

This repository is submitted as coursework for CCAI 422 at the University of Jeddah and is intended for academic use only.
