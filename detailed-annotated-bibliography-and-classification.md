<div align="center">

<b>CS 5463/4953 – Survey Based Term Project</b><br>
<b>Detailed Annotated Bibliography and Classification of the Results</b><br><br>
<b>Survey Title:</b> A Survey of Scalable Graph Neural Network Training Techniques on GPU Architectures

</div>

---

## Class I: Foundational Papers (4)

These papers establish baseline GNN architectures and identify the key scalability bottlenecks that motivate subsequent work.

**Primary Papers:** F1, F2, F3, F4

[F1] Kipf, T. N., & Welling, M. (2017). Semi-Supervised Classification with Graph Convolutional Networks (ICLR 2017).  
URL: https://openreview.net/forum?id=SJU4ayYgl

This paper introduces Graph Convolutional Networks (GCN), the foundational architecture for neural networks on graphs. GCN uses full-batch processing where all nodes are processed simultaneously. This creates three critical scalability problems: (1) full-batch training requires storing all node embeddings in memory, (2) exponential neighbor expansion where memory grows as degree layers, (3) infeasibility on billion-scale graphs. This paper is the motivation for all papers C1-C20, which solve these specific problems.

---

[F2] Hamilton, W., Ying, Z., & Leskovec, J. (2017). Inductive Representation Learning on Large Graphs. (NeurIPS 2017). URL: https://dl.acm.org/doi/10.5555/3294771.3294869#purchase-access

GraphSAGE solves GCN’s full-batch limitation by introducing mini-batch training with neighbor sampling. Instead of all neighbors, samples K fixed neighbors per node. This makes memory independent of graph size. However, sampling introduces gradient variance—small samples produce noisy gradients that slow convergence. This variance problem becomes the focus of papers C1-C10.

---

[F3] Veličković, P., Cucurull, G., Casanova, A., Romero, A., Liò, P., & Bengio, Y. (2018). Graph Attention Networks (ICLR 2018). URL: https://openreview.net/forum?id=rJXMpikCZ 

GAT improves GCN accuracy by adding learned attention weights for each neighbor. However, attention increases computational cost significantly. Computing attention weights for every edge becomes expensive on large graphs. This creates new scalability challenges that papers C15 and C18 specifically address through GPU optimization.

---

[F4] Xu et al. (2019) - How Powerful Are Graph Neural Networks? (Graph Isomorphism Networks). (ICLR 2019). URL: https://openreview.net/forum?id=ryGs6iA5Km

This paper proves theoretically that simple aggregation functions (sum) are as powerful as complex ones. This justifies simplification approaches like paper C8, which removes nonlinearity and achieves 60× speedup while maintaining competitive accuracy.

---

## Class II: Sampling-Based and Algorithmic Solutions (10)

These papers reduce gradient variance in mini-batch training through increasingly sophisticated sampling strategies, enabling convergence with smaller neighborhoods and faster training.

**Primary Papers:** C1, C4, C5, C6, C7, C8, C10  
**Secondary Papers:** C2, C3, C9

[C1] Chen, Ma & Xiao (2018). FastGCN: Fast Learning with Graph Convolutional Networks via Importance Sampling (ICLR 2018). URL: https://openreview.net/forum?id=rytstxWAW

FastGCN improves GraphSAGE’s uniform sampling by using importance-weighted sampling. Samples neighbors proportionally to their importance (degree). This reduces variance in gradient estimates, enabling convergence with 3-5× smaller neighborhoods. Key insight: sampling strategy matters significantly. This insight motivates all subsequent sampling improvements (C2, C4, C6).

---

[C2] Huang, Zhang, Rong & Huang (2018). Adaptive Sampling Towards Fast Graph Representation Learning. (NeurIPS 2018). URL: https://dl.acm.org/doi/10.5555/3327345.3327367

Improves FastGCN by learning importance weights during training instead of using fixed weights. Adaptive importance achieves 5-10% improvement over fixed importance. Shows that importance should evolve as the model learns.

---

[C3] Chen, Zhu & Song (2018). Stochastic Training of Graph Convolutional Networks with Variance Reduction (ICML 2018). URL: https://www.semanticscholar.org/paper/Stochastic-Training-of-Graph-Convolutional-Networks-Chen-Zhu/a60c69c2fae27ebbb73c87f7f2a4765556bd7f9f

Addresses the fundamental problem: small sampled neighborhoods produce high-variance gradients. Uses control variates (mathematical technique) to reduce variance. Enables training with 3-6× smaller neighborhoods while maintaining convergence. Explains why sampling methods work in practice.

---

[C4] Zou et al. (2019). Layer-Dependent Importance Sampling for Training Deep and Large Graph Convolutional Networks (LADIES)(NeurIPS 2019). URL: https://www.researchgate.net/publication/339946989_Layer-Dependent_Importance_Sampling_for_Training_Deep_and_Large_Graph_Convolutional_Networks

Improves FastGCN by making sampling layer-dependent. Conditions neighbor selection on which nodes were selected in the upper layer. Preserves connectivity through sampled path. Enables training deeper networks (6-8 layers vs. 2-3). Shows multi-layer sampling has structure that should be exploited.

---

[C5] Chiang et al. (2019). Cluster-GCN: An Efficient Algorithm for Training Deep and Large Graph Convolutional Networks (KDD 2019). URL: https://dl.acm.org/doi/10.1145/3292500.3330925

Takes different approach from sampling: pre-partitions graph into clusters where intra-cluster edges dominate. Trains on each cluster using all intra-cluster edges (no sampling). Advantages: high memory locality, no sampling variance, simple implementation. Achieves 5-10× memory reduction. Shows partitioning is complementary strategy to sampling.

---

[C6] Zeng et al. (2020). GraphSAINT: Graph Sampling Based Inductive Learning Method. (ICLR 2020). URL: https://openreview.net/forum?id=BJe8pkHFwS

Major advance in sampling: shifts from node-level to subgraph-level sampling. Samples entire connected subgraphs instead of individual nodes. Preserves graph structure, naturally reduces variance through neighbor correlations, improves GPU cache locality. Achieves 2-3× faster convergence than C1 and C4. By 2020, GraphSAINT represents mature sampling method.

---

[C7] Ying et al. (2018). Graph Convolutional Neural Networks for Web-Scale Recommender Systems (PinSage) (KDD 2018). URL: https://dl.acm.org/doi/10.1145/3219819.3219890

Validates sampling approaches at Pinterest scale (billions of nodes). Combines random walk sampling with learned importance and distributed training. Proves that sampling-based methods work on real production graphs. Shows measurable business improvement in recommendations.

---

[C8] Wu et al. (2019). Simplifying Graph Convolutional Networks (SGC). (ICML 2019). URL: https://www.semanticscholar.org/paper/Simplifying-Graph-Convolutional-Networks-Wu-Zhang/7e71eedb078181873a56f2adcfef9dddaeb95602

Achieves scalability through model simplification rather than sampling. Removes nonlinearity and precomputes propagation matrix. Reduces training time from 1 hour to 1 minute (60× speedup) while maintaining competitive accuracy (87% vs. 85%). Shows complexity may not be necessary.

---

[C9] Gasteiger, Bojchevski & Günnemann (2019). Predict then Propagate: Graph Neural Networks meet Personalized PageRank. (ICLR 2019). URL: https://openreview.net/forum?id=H1gL-2A9Ym

Different approach: decouples prediction from propagation. Trains simple feature-based predictor, applies precomputed PageRank for propagation. Eliminates sampling variance and neighborhood expansion. Shows algorithmic innovation in model design provides scalability comparable to sampling optimization.

---

[C10] Zeng et al. (2021). Deep Graph Neural Networks with Shallow Subgraph Samplers. (ICLR 2021). URL: https://openreview.net/forum?id=GIeGTl8EYx

Solves challenge of training deep networks. Deep networks require exponentially larger neighborhoods. Proposes “deep model, shallow sampler”: 16-layer networks but sample only 1-2 hop neighborhoods. Enables 16-layer networks on billion-node graphs with constant memory. Completes sampling approach to handle both width and depth scalability.

---

## Class III: Systems and Hardware Implementations (10)

Demonstrates practical implementation of scalable GNN training on GPU and distributed systems, achieving billion-scale training in production environments.

**Primary Papers:** C12, C13, C14, C15, C18, C20  
**Secondary Papers:** C11, C16, C17, C19

[C11] Ma et al. (2019). NeuGraph: Parallel Deep Neural Network Computation on Large Graphs (USENIX ATC 2019). URL: https://www.usenix.org/conference/atc19/presentation/ma

First systems paper focused on GPU-accelerated GNN computation. Recognizes graph operations (scatter-gather) are irregular with unpredictable memory access patterns. Proposes GPU kernel fusion, graph-aware memory layout, and workload-aware scheduling. Improves GPU utilization from 10-20% to 60-70%. Establishes importance of hardware-algorithm co-design.

---

[C12] Wang et al. (2019). Deep Graph Library: A Graph-Centric, Highly-Performant Package for Graph Neural Networks. NeurIPS 2019 Workshop on Machine Learning Systems.  URL: https://www.semanticscholar.org/paper/Deep-Graph-Library%3A-A-Graph-Centric%2C-Package-for-Wang-Zheng/381411d740562de1e766dc8cc833844eb99dde01

Creates DGL framework: unified software library for GNNs. Provides optimized graph operators, built-in sampling implementations, GPU support. Enables researchers to implement algorithms without hand-coding GPU kernels. Now standard infrastructure for GNN research, enabling fair comparison across papers.

---

[C13] Zheng et al. (2020). DistDGL: Distributed Graph Neural Network Training for Billion-Scale Graphs. Proceedings of the IEEE/ACM Workshop on Irregular Applications: Architectures and Algorithms (IA3 2020), held with SC 2020. URL: https://doi.org/10.1109/IA351965.2020.00011

Extends DGL to distributed environments across hundreds of machines. Addresses distributed challenges: graph partitioning, communication-aware sampling, distributed feature storage. Communication overhead 20-30% (acceptable for distributed systems). Proves billion-node graphs can be trained across distributed clusters.

---

[C14] Zhu et al. (2019). AliGraph: A Comprehensive Graph Neural Network Platform. (PVLDB 2019). URL: https://dl.acm.org/doi/10.14778/3352063.3352127

Industrial GNN platform deployed at Alibaba for multiple applications. Handles production requirements: distributed storage, multi-tenant support, adaptive caching, offline training with online serving. Operates on billion-scale graphs. Validates that scalable GNN training works in real industrial deployments.

---

[C15] Wang et al. (2021). GNNAdvisor: An Adaptive and Efficient Runtime System for GNN Acceleration on GPUs (OSDI 2021). URL: https://www.semanticscholar.org/paper/GNNAdvisor%3A-An-Adaptive-and-Efficient-Runtime-for-Wang-Feng/a72bbf818135b30ab24835e663bc8dcb7b8274ff

Shows GPU optimization is workload dependent. Profiles workload characteristics at runtime and selects optimal GPU kernel strategies. High-degree nodes use block-per-edge kernels, low-degree nodes use warp-per-node kernels. Achieves 1.5-3× speedup over fixed strategies through runtime adaptation.

---

[C16] Thorpe et al. (2021). Dorylus: Affordable, Scalable GNN Training with Distributed CPU Servers and Serverless Threads (OSDI 2021). URL: https://www.semanticscholar.org/paper/Dorylus%3A-Affordable%2C-Scalable%2C-and-Accurate-GNN-CPU-Thorpe-Qiao/fb1a90bd9179e6d3f754b565847523a3dc775671

Demonstrates GPU acceleration is not essential. Achieves billion-scale training using distributed CPU servers (slower per operation but abundant memory). Cost analysis shows CPU approach may be more cost-efficient than GPU approach. Shows scalability depends on system architecture beyond GPU optimization.

---

[C17] Lin et al. (2020). PaGraph: Scaling GNN Training on Large Graphs via Computation-Aware Caching. ACM Symposium on Cloud Computing (SoCC 2020). URL: https://dl.acm.org/doi/10.1145/3419111.3421281. 

Identifies data movement is the bottleneck, not computation. Uses computation-aware caching to pre-fetch features and partitioning to maximize cache locality. Achieves 3-5× speedup through memory hierarchy optimization. Shows end-to-end performance requires optimizing complete pipeline.

---

[C18] Yang et al. (2022). GNNLab: A Factored System for Sample-Based GNN Training over GPUs. (EuroSys 2022). URL: https://dl.acm.org/doi/10.1145/3492321.3519557

Separates training pipeline into independent modules: sampling, feature loading, computation, gradient aggregation. Reveals sampling and feature loading consume 40-60% of training time. Optimizes each component separately: GPU sampling kernels, pinned memory, cuDNN computation. Achieves 2-3× speedup through pipeline optimization.

---

[C19] Kaler et al. (2022). Accelerating Training and Inference of Graph Neural Networks with Fast Sampling and Pipelining (SALIENT). (MLSys 2022). URL: https://www.researchgate.net/publication/360217523_Accelerating_Training_and_Inference_of_Graph_Neural_Networks_with_Fast_Sampling_and_Pipelining

Shows sampling is bottleneck in training pipeline. Provides GPU sampling kernels and pipelining to overlap operations. Achieves 2-4× speedup by optimizing complete pipeline, not just neural computation. Demonstrates sampling optimization is critical to overall performance.

---

[C20] Yang et al. (2023). Betty: Enabling Large-Scale GNN Training with Batch-Level Graph Partitioning. (ASPLOS 2023). URL: https://www.researchgate.net/publication/367550869_Betty_Enabling_Large-Scale_GNN_Training_with_Batch-Level_Graph_Partitioning

Addresses memory capacity constraints. Even with sampling, GPU memory overflows. Dynamically partitions computation across GPU and CPU memory. Achieves 3-5× memory reduction. Latest optimization frontier, showing fine-grained memory management enables larger training workloads.

---

## Class IV: Survey Reference (1)

Provides general context for GNN literature and related work.

[C21] Wu et al. (2021). A Comprehensive Survey on Graph Neural Networks. IEEE Transactions on Neural Networks and Learning Systems. URL: https://www.researchgate.net/publication/330132719_A_Comprehensive_Survey_on_Graph_Neural_Networks 

Broader survey on all GNN research. Useful for background context and positioning scalable training within larger GNN literature. Supporting reference rather than main focus.

---
## Sub-Hierarchies Within Classes

### Class II Sampling Progression
- C1 (importance weighting)
- C2 (adaptive importance)
- C4 (layer-dependent importance)
- C6 (subgraph sampling)
- C10 (shallow samplers for deep GNNs)

### Class III Systems Progression
- C11 (GPU kernels)
- C12 (framework)
- C13, C14 (distributed systems and platforms)
- C15 (adaptive runtime)
- C18 (pipeline optimization)
- C20 (memory optimization)

---

## Proposed Survey Organization

This classification suggests the following structure for the final survey paper:

- **Chapter 1:** Introduction and foundational challenges (Class I)
- **Chapter 2:** Algorithmic scalability solutions (Class II)
- **Chapter 3:** Systems and implementation approaches (Class III)
- **Chapter 4:** Conclusion and future directions
