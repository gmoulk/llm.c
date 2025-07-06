# 📑 GPT-2 Multi-Threading Performance Analysis Report

## 1️⃣ Experiment Goal

This experiment investigates how the number of OpenMP threads (`OMP_NUM_THREADS`) ,the use of AVX and BLAS affects the training speed and behavior of a GPT-2 model on CPU.

## 2️⃣ Experimental Setup

| Item                    | Value                                                  |
| ----------------------- | ------------------------------------------------------ |
| **Model**               | GPT-2 (12 layers, 12 heads, 768 channels, 124M params) |
| **Max sequence length** | 1024                                                   |
| **Vocab size**          | 50,257 (padded: 50,304)                                |
| **Dataset batches**     | Train: 1,192; Val: 128                                 |
| **Hardware**            | CPU-only, varying OpenMP threads                       |
| **Threads tested**      | 8, 4, 2, 1                                             |

## 3️⃣ Collected Results

### ✅ 3.1 Validation Loss

| Step     | Val Loss |
| -------- | -------- |
| Initial  | 5.325522 |
| After 10 | 4.416494 |
| After 20 | 4.329332 |
| After 30 | 4.300248 |
| After 40 | 4.291717 |

### ⏱️ 3.2 Per-Step Timing (ms)

| Step | 8 Threads | 4 Threads | 2 Threads | 1 Thread  | AVX      |
| ---- | --------- | --------- | --------- | --------- | -------- |
| 0    | 3,896.70  | 4,698.63  | 7,228.34  | 13,199.73 | 3,615.54 |
| 1    | 2,915.41  | 3,895.10  | 6,373.63  | 12,088.12 | 2,860.43 |
| 2    | 2,990.39  | 3,876.27  | 6,194.58  | 12,511.87 | 2,882.21 |
| 3    | 3,046.20  | 3,942.91  | 6,146.60  | 11,633.46 | 2,786.05 |
| 4    | 3,204.75  | 4,001.90  | 6,361.35  | 14,561.65 | 2,843.50 |
| 5    | 3,554.02  | 3,958.23  | 6,354.29  | 12,558.19 | 2,916.13 |
| 10   | 3,215.70  | 3,831.97  | 6,479.13  | 12,874.17 | 2,957.00 |
| 20   | 3,673.17  | 3,916.89  | 7,590.05  | 11,143.64 | 3,187.12 |
| 30   | 3,270.47  | 3,936.57  | 6,366.67  | 11,098.38 | 3,008.11 |
| 40   | 3,585.95  | 3,799.79  | 6,247.21  | 10,981.01 | 3,130.84 |


## 📊 4️⃣ Average Step Time (Approximate)

| Threads | Average Time (sec) | Slowdown (vs 8 Threads) |
| ------- | ------------------ | ----------------------- |
| 8       | \~3.5 sec          | Baseline                |
| 4       | \~3.9 sec          | \~1.1× slower           |
| 2       | \~6.5 sec          | \~1.9× slower           |
| 1       | \~11.5 sec         | \~3.3× slower           |
| AVX     | \~3.0 sec          | \~1.1× faster           |
| BLAS    | \~1.46 sec         | \~2.4× faster           |

## 📈 5️⃣ Scalability Insights

* Training time increases nearly linearly as thread count decreases.
* Validation loss and generated text remain identical across runs.
* OpenMP scaling is effective up to 8 threads.
* Below 4 threads, training slows substantially.

## ✍️ 6️⃣ Example Generated Text

**Step 10:**

> "I am pale and ill-smyth'd: Quoth the poor rascal..."

**Step 40:**

> "EditBOOK IX: Under the boasted sute of Georges..."

## ✅ 7️⃣ Conclusions

| Aspect               | Observation                                                 |
| -------------------- | ----------------------------------------------------------- |
| **Correctness**      | ✅ Identical loss and generation                             |
| **Speed**            | ⚡ Best with `OMP_NUM_THREADS=8` and openBlas                |
| **Scalability**      | ✅ Good up to 8 threads; slowdown is near-linear             |
| **Resource sharing** | ✅ Lower threads can free CPU for other tasks, but at a cost |


## 📌 8️⃣ Recommendation

| Goal                 | Recommended Threads              |
| -------------------- | --------------------------       |
| **Fastest Training** | `OMP_NUM_THREADS=8` with openBlas|
| **Balanced Usage**   | `OMP_NUM_THREADS=4`              |
| **Low Priority**     | `OMP_NUM_THREADS=1` or `2`       |

## 📁 9️⃣ Notes

* These results are CPU-only. GPUs may scale differently.
* Multi-threading effectively utilizes CPU cores for tensor operations.


## Performance Counter Stats for `./train_gpt2`

| Metric                  | Value                         | Notes                           |
|-------------------------|-------------------------------|---------------------------------|
| **Task Clock**          | 708,147.03 msec               | 1.000 CPUs utilized             |
| **Context Switches**    | 13,372                        | 18.883 /sec                     |
| **CPU Migrations**      | 297                           | 0.419 /sec                      |
| **Page Faults**         | 873,210                       | 1.233 K/sec                     |
| **CPU Cycles**          | 2,828,715,460,760             | ~3.995 GHz                      |
| **Instructions**        | 3,450,675,515,172             | 1.22 instructions per cycle     |
| **Branches**            | 459,440,125,539               | 648.792 M/sec                   |
| **Branch Misses**       | 3,699,080,215                 | 0.81% of all branches           |
| **Time Elapsed**        | 708.374812244 seconds         |                                 |
| **User Time**           | 706.835405000 seconds         |                                 |
| **System Time**         | 1.274672000 seconds           |                                 |

### Total Time (User + System)
**708.110077 seconds**
