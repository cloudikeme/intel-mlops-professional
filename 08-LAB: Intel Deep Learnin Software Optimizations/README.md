### Lab Learning Objective: The lab teaches how to optimize deep learning using Intel's Extension for PyTorch and covers essential parallel computing concepts through OpenMP and NUMA systems. Students will also gain hands-on experience in setting OpenMP environment variables.

### Problem Statement: As a member of the AI engineering team at Fancy Orchards, our mandate is clear: improve operational efficiencies and enhance worker safety by applying computer vision and deep learning. We've set our sights on automating high-risk and labor-intensive tasks in the orchard and the factory.


Made using AI with Nightcafe
To get the best out of our hardware, we plan to employ the Intel Extension for PyTorch, optimizing our deep learning models with its advanced features. Simultaneously, we intend to delve into OpenMP concepts to fine-tune compute resource utilization and explore parallelism for better workload management.

Our first step involves basic testing on open-source datasets, with the long-term objective of deploying a highly efficient, production-ready solution.

Value of Exercise: This lab offers hands-on experience optimizing deep learning models using Intel's Extension for PyTorch, equipping the team to build more efficient and faster production-ready solutions. It also provides a deep dive into OpenMP and related environment variables, enabling more effective utilization of compute resources through parallelism.

### Supplemental Foundational Knowledge - Parallel Computing and OpenMP:

OpenMP (Open Multi-Processing): OpenMP is an industry-standard API for writing multi-threaded applications. This API supports C, C++, and Fortran multi-platform shared-memory parallel programming.
Importance in Optimizing Workloads: OpenMP allows you to parallelize your code without explicitly managing threads. By merely adding compiler directives (pragmas) in your code, OpenMP enables you to take advantage of multi-core processors more effectively. It helps in:
Load Balancing: Distributes the workload evenly across multiple threads.
Resource Utilization: All the CPU cores are utilized to their full potential, thereby reducing idle time.
Data Locality: Enhances data caching and reduces cache miss rates.
Non-Uniform Memory Access (NUMA) Systems: In a NUMA system, each processor has its own local memory, and access to this local memory is faster than access to non-local memory (memory local to another processor).
Importance in Optimizing Workloads: In the context of deep learning and other compute-intensive tasks, understanding and optimizing for NUMA can provide performance benefits:
Reduced Latency: Data needed by a CPU core can be kept in the closest memory, reducing the time needed to fetch data.
Increased Throughput: More tasks can be performed concurrently by keeping data and computations local to specific CPUs and their memory.
Scalability: NUMA systems are designed to scale; the more processors you add, the more local memories you have, potentially increasing the performance linearly.
OpenMP Environment Variables and Their Importance
OMP_NUM_THREADS: This environment variable specifies the number of threads used in an OpenMP program's parallel regions.
By manually setting this variable, you can optimize the number of threads according to the task. For instance, for I/O-bound tasks, you might limit the number of threads to avoid overloading the system, while for CPU-bound tasks, you could set it to the number of available cores to maximize CPU utilization.
KMP_BLOCKTIME: This variable sets the time, in milliseconds, that a thread will wait after the completion of the parallel region before going to sleep.
Setting an optimal block time can reduce the overhead of waking up threads, thereby improving performance in scenarios where parallel regions frequently alternate with serial regions.
KMP_HW_SUBSET: This variable specifies the subset of hardware resources to use for OpenMP tasks. You can define how many cores and threads per core to utilize.
It allows you to fine-tune the hardware resources that your application uses. This can be useful in shared or cloud environments, where you may not want to utilize all available resources.
Example: Setting KMP_HW_SUBSET=1s,1n,56c,2t would result in using a single socket, one Numa node, 56 cores per Numa node, and two threads per core. In total, 112 threads for the process
KMP_AFFINITY: This variable provides more precise control over the placement of threads on physical processing units.
Thread affinity ensures that threads stick to specific cores, which can improve cache locality and reduce the overhead of context switching. This is especially important for performance-sensitive applications like deep learning, where even minor optimizations can lead to substantial performance gains.
By understanding and leveraging these concepts and environment variables, you can significantly improve the performance and efficiency of your deep learning workloads. Proper utilization of OpenMP and optimal setting of its environment variables can result in more efficient multi-threading, better CPU utilization, and, ultimately, faster training and inference times.

Access to Intel Developer Cloud Resource: Training and Workshop Jupyter Lab

 

Step-by-step Instructions for the Lab:

Setup
Open a Jupyter Lab window from the “Training and Workshops” IDC page.

Open a terminal inside of Jupyter.
If you have not done so, clone the course code repository into the Jupyter environment.
Navigate to the lab5 directory.
Use the code in the "sample" directory as a reference for this lab.
Activate the pre-configured conda environment by running:

Test #1: Experiment with OpenMP Environment Variables and run PyTorch Script. The configurations below will reduce the number of threads available to the workload during runtime to 6. The dtype set to “fp32” and optimizations set to “avx” result in full precision training with AVX-512 instead of Intel® Advanced Matrix Extensions.
Set the following environment variable before running the script: OMP_NUM_THREADS=6
b. Select the VNNI instructions by setting the following environment variable before running the script: ONEDNN_MAX_CPU_ISA= “AVX512_CORE_VNNI”
In the command line run:  

Open an additional terminal, run “top” and then press 1 + t to bring up a comprehensive summary of thread utilization.
Test #2: Experiment with OpenMP Environment Variables and run PyTorch Script. The configurations below will reduce the number of threads available to the workload during runtime to 6. The dtype set to “bf16” and optimizations set to “amx” result in mixed-precision training with Intel® Advanced Matrix Extensions. This configuration should yield increased training and inference performance over Test #1.
Set the following environment variable before running the script: OMP_NUM_THREADS=6
Select the AMX instructions by setting the following environment variable before running the script: ONEDNN_MAX_CPU_ISA= “AVX512_CORE_AMX”
In the command line run: 

Continue to test the OMP parameters, explore using KMP_BLOCKTIME or KMP_AFFINITY, and see the impact on the workload. Toggle between fp32/bf16 and amx/avx to see the impact on training/inference times.
Feel free to use the following table track your parameters and workload performance. For an added challenge you could hack the script to add mlflow experiment tracking!
Name

dtype

Number of threads

Instruction AMX/AVX

Train Time

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

Challenge Questions:

How does setting the OMP_NUM_THREADS environment variable to 6 affect the performance of the PyTorch script compared to not setting it at all?
What is the difference between setting the dtype to "fp32" and "bf16" when running the script, and how does it impact the training and inference performance?
What is the benefit of using KMP_AFFINITY for fine-tuning thread placement, especially in a deep learning context?
 Challenge Question Answers:

Setting OMP_NUM_THREADS to 6 limits the number of threads available to the workload during runtime. This can lead to optimized CPU utilization for specific tasks, potentially improving performance. However, it could also reduce performance if the task could benefit from more threads.
Setting the dtype to "fp32" uses 32-bit floating-point numbers for computations, offering higher precision but potentially slower performance. On the other hand, "bf16" uses 16-bit floating-point numbers, which may result in faster computations but at the cost of reduced numerical precision.
KMP_AFFINITY allows for more precise control over the placement of threads on physical processing units. This can improve cache locality and reduce the overhead of context switching, leading to substantial performance gains in deep learning tasks where even small optimizations can have a significant impact.