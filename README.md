# Geometric Repairability of Compressed Sentence Embeddings

**A Cross-Dataset Study Using Procrustes Alignment and Low-Rank Residual Correction**

**Manseerat Kaur Aulakh**, Nupur Choudhary, Vikhyat Gupta, Vishwanath Bijalwan, Rajni Mohana
Amity School of Engineering & Technology, Amity University Punjab, Mohali, India

*Accepted at the International Conference on Emerging Digital Intelligence and Generative Engineering (EDIGE 2026), IEEE.*

## TL;DR
Compression damages sentence-embedding spaces in different ways. **Distillation mostly rotates the space**, so a closed-form Procrustes rotation recovers roughly half of the lost accuracy. **Quantisation noise and dimension pruning** leave different geometric signatures that rotation cannot fix. We introduce the **Procrustes Repairability Score (PRS)**, a parameter-free diagnostic that predicts from a small calibration set whether repair will work.

## Setup
- **Compression families:** quantisation, weight/dimension pruning, knowledge distillation, each at 7 severity levels
- **Datasets:** AG News, TREC-6, Web of Science (WOS), IMDB, SciFact
- **Encoders:** `all-MiniLM-L6-v2`, `bert-base-uncased`
- **Repair ladder:** R0 identity baseline · R1 closed-form Procrustes rotation · R2 Procrustes plus a learned low-rank residual
- **Evaluation:** a strictly frozen downstream probe, trained on clean embeddings and never retrained, as in a real deployment

## Key results
| Finding | Result |
|---|---|
| Distillation repaired by rotation alone (R1) | +11.8 to +24.1 accuracy points (about half of the loss) |
| Recovery vs. task complexity | rises with task complexity; largest on 7-class WOS (24.1 points) |
| Quantisation and pruning | resist rotation-based repair |
| 2-bit quantisation | `bert-base-uncased` collapses to 6.8%; `all-MiniLM-L6-v2` stays at 81.4% |
| R2 vs. R1 | little extra benefit except with large calibration sets (k > 5000) |

## Limitations
Compression is modelled at the embedding level rather than the weight level. Each configuration was run once, so differences under 1 point should not be relied on. Only one distilled student was tested. Repairs learned on classification data transfer poorly to STS-B and SciFact.

## Code
The code is not yet public.

## Citation
```bibtex
@inproceedings{aulakh2026repairability,
  title     = {Geometric Repairability of Compressed Sentence Embeddings: A Cross-Dataset Study Using Procrustes Alignment and Low-Rank Residual Correction},
  author    = {Aulakh, Manseerat Kaur and Choudhary, Nupur and Gupta, Vikhyat and Bijalwan, Vishwanath and Mohana, Rajni},
  booktitle = {International Conference on Emerging Digital Intelligence and Generative Engineering (EDIGE)},
  publisher = {IEEE},
  year      = {2026},
  note      = {Accepted}
}
```
