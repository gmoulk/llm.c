op Hotspots
Function                   Module         CPU Time  % of CPU Time(%)
-------------------------  ------------  ---------  ----------------
matmul_forward._omp_fn.0   train_gpt2    3218.773s             44.6%
matmul_backward._omp_fn.0  train_gpt2    1276.404s             17.7%
matmul_backward._omp_fn.1  train_gpt2    1272.025s             17.6%
func@0x25680               libgomp.so.1   619.992s              8.6%
func@0x25820               libgomp.so.1   522.282s              7.2%
[Others]                   N/A            303.532s              4.2%
Collection and Platform Info
    Application Command Line: ./train_gpt2 
    Operating System: 6.11.0-28-generic DISTRIB_ID=Ubuntu DISTRIB_RELEASE=24.04 DISTRIB_CODENAME=noble DISTRIB_DESCRIPTION="Ubuntu 24.04.2 LTS"
    Computer Name: gmoulkiotis-OMEN-by-HP-Laptop
    Result Size: 146.0 MB 
    Collection start time: 17:38:18 02/07/2025 UTC
    Collection stop time: 17:51:04 02/07/2025 UTC
    Collector Type: User-mode sampling and tracing
    CPU
        Name: Unknown
        Frequency: 2.208 GHz
        Logical CPU Count: 12
        Cache Allocation Technology
            Level 2 capability: not detected
            Level 3 capability: not detected

vtune: Collection stopped.
vtune: Using result path `/home/gmoulkiotis/final/llm.c/vtune_roofline2'
vtune: Executing actions 19 % Resolving information for `libgomp.so.1'         
vtune: Warning: Cannot locate debugging information for file `/lib/x86_64-linux-gnu/libgomp.so.1'.
vtune: Executing actions 75 % Generating a report                              Elapsed Time: 1200.364s
    Allocation Size: 2.6 GB 
    Deallocation Size: 2.6 GB 
    Allocations: 83
    Total Thread Count: 12
    Paused Time: 0s

Top Memory-Consuming Functions
Function        Memory Consumption  Allocation/Deallocation Delta  Allocations  Module    
--------------  ------------------  -----------------------------  -----------  ----------
malloc_check               1.6 GB                          0.0 B            40  train_gpt2
gpt2_update              995.8 MB                          0.0 B             2  train_gpt2
fread                     45.1 KB                          0.0 B            11  train_gpt2
fopen_check                4.7 KB                          0.0 B            10  train_gpt2
matmul_forward             4.4 KB                         4.4 KB             3  train_gpt2
[Others]                   1.7 KB                         1.1 KB            17  N/A       
Collection and Platform Info
    Application Command Line: ./train_gpt2 
    Operating System: 6.11.0-28-generic DISTRIB_ID=Ubuntu DISTRIB_RELEASE=24.04 DISTRIB_CODENAME=noble DISTRIB_DESCRIPTION="Ubuntu 24.04.2 LTS"
    Computer Name: gmoulkiotis-OMEN-by-HP-Laptop
    Result Size: 4.0 MB 
    Collection start time: 18:05:09 02/07/2025 UTC
    Collection stop time: 18:25:10 02/07/2025 UTC
    Collector Type: User-mode sampling and tracing
    CPU
        Name: Unknown
        Frequency: 2.208 GHz
        Logical CPU Count: 12
        Cache Allocation Technology
            Level 2 capability: not detected
            Level 3 capability: not detected


Effective CPU Utilization: 74.9% (8.982 out of 12 logical CPUs)
 | The metric value is low, which may signal a poor logical CPU cores
 | utilization caused by load imbalance, threading runtime overhead, contended
 | synchronization, or thread/process underutilization. Explore sub-metrics to
 | estimate the efficiency of MPI and OpenMP parallelism or run the Locks and
 | Waits analysis to identify parallel bottlenecks for other parallel runtimes.
 |
    Total Thread Count: 12
        Thread Oversubscription: 0s (0.0% of CPU Time)
    Wait Time with poor CPU Utilization: 0.326s (98.1% of Wait Time)

        Top Waiting Objects
        Sync Object                                                            Wait Time with poor CPU Utilization  (% from Object Wait Time)(%)  Wait Count
        ---------------------------------------------------------------------  -----------------------------------  ----------------------------  ----------
        Stream gpt2_124M.bin 0x6ce89cb7                                                                     0.325s                        100.0%           2
        Stream 0xe86311a0                                                                                   0.001s                         17.9%          29
        Stream gpt2_tokenizer.bin 0xc039f0d5                                                                0.000s                        100.0%           4
        Stream dev/data/tinyshakespeare/tiny_shakespeare_val.bin 0x3d3bfa3d                                 0.000s                        100.0%           5
        Stream dev/data/tinyshakespeare/tiny_shakespeare_train.bin 0x32969a8c                               0.000s                        100.0%           1
        [Others]                                                                                            0.000s                          0.2%           4
    Spin and Overhead Time: 0s (0.0% of CPU Time)

        Top Functions with Spin or Overhead Time
        Function  Module  Spin and Overhead Time  (% from CPU Time)(%)
        --------  ------  ----------------------  --------------------
Collection and Platform Info
    Application Command Line: ./train_gpt2 
    Operating System: 6.11.0-28-generic DISTRIB_ID=Ubuntu DISTRIB_RELEASE=24.04 DISTRIB_CODENAME=noble DISTRIB_DESCRIPTION="Ubuntu 24.04.2 LTS"
    Computer Name: gmoulkiotis-OMEN-by-HP-Laptop
    Result Size: 156.8 MB 
    Collection start time: 18:37:20 02/07/2025 UTC
    Collection stop time: 18:51:36 02/07/2025 UTC
    Collector Type: User-mode sampling and tracing
    CPU
        Name: Unknown
        Frequency: 2.208 GHz
        Logical CPU Count: 12
        Cache Allocation Technology
            Level 2 capability: not detected
            Level 3 capability: not detected