# 📈 `perf` Analysis for `train_gpt2`

## ✅ **Summary**

CPU Time is:

* **Dominated by matrix multiplications**
* **Highly parallelized with OpenMP**
* **Minor time in activations and attention**

---

## 🔑 **Key Observations**

| % CPU Time          | Function                                          | Explanation                                                      |
| ------------------- | ------------------------------------------------- | ---------------------------------------------------------------- |
| **99.99%**          | `_start` → `__libc_start_main` → `main`           | Almost all time is inside your program — expected for training.  |
| **97.05%**          | `GOMP_parallel`                                   | Workload is parallelized with OpenMP (multi-threaded matmul).    |
| **54.59%**          | `gpt2_backward`                                   | Backpropagation step — expected to be heavier than forward pass. |
| **42.75%**          | `matmul_forward._omp_fn.0`                        | Matrix multiplication in the forward pass.                       |
| **32.36% + 20.90%** | `matmul_backward._omp_fn.{0,1}`                   | Matrix multiplication in the backward pass.                      |
| \~1%                | `attention_forward`, `attention_backward`         | Self-attention kernels — smaller contributor in this case.       |
| <1%                 | `softmax_forward`, `gelu_backward`, `layernorm_*` | Activation and normalization layers — minimal impact.            |

---

## 📊 **Where the Time Goes**

| Component                          | Approx. Contribution    |
| ---------------------------------- | ----------------------- |
| **OpenMP parallel regions**        | \~97% of total CPU time |
| **Forward matrix multiplication**  | \~43%                   |
| **Backward matrix multiplication** | \~53%                   |
| **Attention & Softmax**            | \~1–2%                  |
| **Other layers (GELU, LayerNorm)** | <1%                     |

✅ This breakdown is typical for transformer workloads — large linear layers dominate compute.

---

## ⚙️ **Performance Implications**

* You are **compute-bound on matmul operations** — normal and expected.
* Small share for self-attention implies the MLP layers (feedforward) dominate.
* Vector math is used (`libmvec` with AVX2), so your compiler/runtime is exploiting SIMD.

---
