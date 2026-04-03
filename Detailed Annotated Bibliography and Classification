# CS 5463/4953 – Survey-Based Term Project

## Detailed Annotated Bibliography and Classification of Results

**Survey Title:** *A Survey of Scalable Graph Neural Network Training Techniques on GPU Architectures*

**Paper Classification:** 21 papers are organized into 4 classes based on the major scalability results they achieve.

---

## Class I: Foundational Papers (4)

*These papers establish baseline GNN architectures and identify the key scalability bottlenecks that motivate subsequent work.*

**Primary Papers:** F1, F2, F3, F4

### [F1] Kipf, T. N., & Welling, M. (2017). *Semi-Supervised Classification with Graph Convolutional Networks.* ICLR 2017.

**URL:** https://openreview.net/forum?id=SJU4ayYgl

This paper introduces Graph Convolutional Networks (GCN), a foundational architecture for neural networks on graphs. GCN uses full-batch processing, where all nodes are processed simultaneously. This leads to three major scalability problems: (1) full-batch training requires storing all node embeddings in memory, (2) exponential neighbor expansion causes memory growth proportional to degree^layers, and (3) the method becomes infeasible on billion-scale graphs. This paper motivates many later works that aim to solve these limitations.

---

### [F2] Hamilton, W., Ying, Z., & Leskovec, J. (2017). *Inductive Representation Learning on Large Graphs.* NeurIPS 2017.

**URL:** https://dl.acm.org/doi/10.5555/3294771.3294869#purchase-access

GraphSAGE addresses GCN’s full-batch limitation by introducing mini-batch training with neighbor sampling. Instead of aggregating all neighbors, it samples a fixed number of neighbors per node. This makes memory usage less dependent on graph size. However, sampling introduces gradient variance, since smaller samples can produce noisier gradients and slower convergence. This variance problem becomes a major focus of many later papers.

---

### [F3] Veličković, P., Cucurull, G., Casanova, A., Romero, A., Liò, P., & Bengio, Y. (2018). *Graph Attention Networks.* ICLR 2018.

**URL:** https://openreview.net/forum?id=rJXMpikCZ

GAT improves upon GCN by adding learned attention weights for each neighbor. While this improves model expressiveness and often accuracy, it also increases computational cost. Calculating attention weights for every edge becomes expensive for large graphs. This creates additional scalability challenges that later system-oriented works try to address through GPU optimization.

---

### [F4] Xu, K., Hu, W., Leskovec, J., & Jegelka, S. (2019). *How Powerful Are Graph Neural Networks?* ICLR 2019.

**URL:** https://openreview.net/forum?id=ryGs6iA5Km

This paper provides theoretical insight by showing that simple aggregation functions such as sum can be as powerful as more complex alternatives. This result supports simplification-based approaches, such as removing unnecessary nonlinearities, while still maintaining strong performance. It provides an important theoretical basis for later efficiency-oriented designs.

---

## Class II: Sampling-Based and Algorithmic Solutions (10)

*These papers reduce gradient variance in mini-batch training through increasingly sophisticated sampling strategies, enabling convergence with smaller neighborhoods and faster training.*

**Primary Papers:** C1, C4, C5, C6, C7, C8, C10  
**Secondary Papers:** C2, C3, C9

### [C1] Chen, J., Ma, T., & Xiao, C. (2018). *FastGCN: Fast Learning with Graph Convolutional Networks via Importance Sampling.* ICLR 2018.

**URL:** https://openreview.net/forum?id=rytstxWAW

FastGCN improves GraphSAGE’s uniform sampling by using importance-weighted sampling. It samples neighbors according to their importance rather than treating all neighbors equally. This reduces gradient variance and enables convergence with smaller sampled neighborhoods. The paper shows that the choice of sampling strategy significantly affects efficiency and accuracy.

---

### [C2] Huang, W., Zhang, T., Rong, Y., & Huang, J. (2018). *Adaptive Sampling Towards Fast Graph Representation Learning.* NeurIPS 2018.

**URL:** https://dl.acm.org/doi/10.5555/3327345.3327367

This paper improves on FastGCN by learning importance weights dynamically during training rather than using fixed ones. Adaptive importance weighting gives better performance than static importance sampling, showing that the sampling policy should evolve as the model learns.

---

### [C3] Chen, J., Zhu, J., & Song, L. (2018). *Stochastic Training of Graph Convolutional Networks with Variance Reduction.* ICML 2018.

**URL:** https://www.semanticscholar.org/paper/Stochastic-Training-of-Graph-Convolutional-Networks-Chen-Zhu/a60c69c2fae27ebbb73c87f7f2a4765556bd7f9f

This work addresses the fundamental problem of high-variance gradients in sampled GNN training. It uses control variates to reduce variance, allowing smaller sampled neighborhoods without hurting convergence. The paper helps explain why stochastic sampling methods can remain effective in practice.

---

### [C4] Zou, D., Hu, Z., Wang, Y., Jiang, S., Sun, Y., & Gu, Q. (2019). *Layer-Dependent Importance Sampling for Training Deep and Large Graph Convolutional Networks.* NeurIPS 2019.

**URL:** https://www.researchgate.net/publication/339946989_Layer-Dependent_Importance_Sampling_for_Training_Deep_and_Large_Graph_Convolutional_Networks

This paper improves FastGCN by making the sampling process layer-dependent. Instead of sampling independently at each layer, it conditions selection on the structure of the upper layer. This preserves connectivity through the sampled computation graph and helps train deeper GNNs more effectively.

---

### [C5] Chiang, W., Liu, X., Si, S., Li, Y., Bengio, S., & Hsieh, C. (2019). *Cluster-GCN: An Efficient Algorithm for Training Deep and Large Graph Convolutional Networks.* KDD 2019.

**URL:** https://dl.acm.org/doi/10.1145/3292500.3330925

Cluster-GCN takes a different approach by partitioning the graph into clusters and training on each cluster as a subgraph. This avoids neighbor sampling and instead benefits from improved memory locality and reduced variance. It shows that graph partitioning can be an effective alternative to pure sampling methods.

---

### [C6] Zeng, H., Zhou, H., Srivastava, A., Kannan, R., & Prasanna, V. (2020). *GraphSAINT: Graph Sampling Based Inductive Learning Method.* ICLR 2020.

**URL:** https://openreview.net/forum?id=BJe8pkHFwS

GraphSAINT advances sampling by moving from node-level sampling to subgraph-level sampling. Instead of selecting isolated nodes, it samples connected subgraphs. This preserves structural information, reduces variance, and improves GPU memory access patterns. It represents a major step forward in sampling-based GNN training.

---

### [C7] Ying, R., He, R., Chen, K., Eksombatchai, P., Hamilton, W., & Leskovec, J. (2018). *Graph Convolutional Neural Networks for Web-Scale Recommender Systems.* KDD 2018.

**URL:** https://dl.acm.org/doi/10.1145/3219819.3219890

This paper validates sampling-based GNN methods at Pinterest-scale recommendation systems. It combines random-walk sampling, learned importance, and distributed training. The work is significant because it demonstrates that these methods can scale to real industrial graphs with billions of nodes and edges.

---

### [C8] Wu, F., Souza, A., Zhang, T., Fifty, C., Yu, T., & Weinberger, K. (2019). *Simplifying Graph Convolutional Networks.* ICML 2019.

**URL:** https://www.semanticscholar.org/paper/Simplifying-Graph-Convolutional-Networks-Wu-Zhang/7e71eedb078181873a56f2adcfef9dddaeb95602

This paper improves scalability through model simplification rather than sampling. It removes nonlinearities and precomputes feature propagation. By doing so, it greatly reduces training time while maintaining competitive accuracy. The result suggests that simpler GNN architectures can still perform well.

---

### [C9] Gasteiger, J., Bojchevski, A., & Günnemann, S. (2019). *Predict then Propagate: Graph Neural Networks meet Personalized PageRank.* ICLR 2019.

**URL:** https://openreview.net/forum?id=H1gL-2A9Ym

This work decouples prediction from propagation. It first trains a simple predictor based on node features and then uses precomputed Personalized PageRank for propagation. This design avoids repeated neighborhood expansion during training and provides an efficient alternative to standard message passing.

---

### [C10] Zeng, H., Zhang, M., Xia, Y., Srivastava, A., Malevich, A., Kannan, R., Prasanna, V., Jin, L., & Chen, R. (2021). *Deep Graph Neural Networks with Shallow Subgraph Samplers.* ICLR 2021.

**URL:** https://openreview.net/forum?id=GIeGTl8EYx

This paper addresses the challenge of training deep GNNs, where deeper models typically require exponentially larger neighborhoods. It proposes using deep models together with shallow samplers, allowing deep architectures without the usual memory explosion. This makes deeper GNN training more practical on very large graphs.

---

## Class III: Systems and Hardware Implementations (10)

*These papers focus on practical implementation strategies for scalable GNN training on GPUs and distributed systems, enabling billion-scale training in real environments.*

**Primary Papers:** C12, C13, C14, C15, C18, C20  
**Secondary Papers:** C11, C16, C17, C19

### [C11] Ma, L., Yang, Z., Miao, Y., et al. (2019). *NeuGraph: Parallel Deep Neural Network Computation on Large Graphs.* USENIX ATC 2019.

**URL:** https://www.usenix.org/conference/atc19/presentation/ma

NeuGraph is one of the earliest system-focused papers on GPU-accelerated GNN computation. It observes that graph operations are highly irregular and lead to poor memory access behavior on GPUs. The paper proposes kernel fusion, graph-aware memory layouts, and workload-aware scheduling to improve GPU utilization.

---

### [C12] Wang, M., Yu, L., Zheng, D., Gan, Q., Gai, Y., Ye, Z., Li, M., Zhou, J., & Karypis, G. (2019). *Deep Graph Library: A Graph-Centric, Highly-Performant Package for Graph Neural Networks.* NeurIPS 2019 Workshop on Machine Learning Systems.

**URL:** https://www.semanticscholar.org/paper/Deep-Graph-Library%3A-A-Graph-Centric%2C-Package-for-Wang-Zheng/381411d740562de1e766dc8cc833844eb99dde01

This paper introduces DGL, a widely used software framework for GNN development. It provides optimized graph operators, built-in sampling methods, and GPU support. DGL is important because it lowers implementation difficulty and helps standardize GNN experimentation across research papers.

---

### [C13] Zheng, D., Ma, C., Wang, M., Zhou, J., Su, Q., Song, X., Gan, Q., Zhang, Z., & Karypis, G. (2020). *DistDGL: Distributed Graph Neural Network Training for Billion-Scale Graphs.* IA3 2020, held with SC 2020.

**URL:** https://doi.org/10.1109/IA351965.2020.00011

DistDGL extends DGL into distributed environments spanning many machines. It addresses issues such as graph partitioning, communication-aware sampling, and distributed feature storage. This work shows that billion-scale GNN training is feasible in distributed settings.

---

### [C14] Zhu, R., Zhao, K., Yang, H., Lin, W., Zhou, C., Ai, B., Li, Y., & Zhou, J. (2019). *AliGraph: A Comprehensive Graph Neural Network Platform.* PVLDB 2019.

**URL:** https://dl.acm.org/doi/10.14778/3352063.3352127

AliGraph is an industrial GNN platform developed at Alibaba. It supports distributed storage, adaptive caching, multi-tenant execution, offline training, and online serving. The paper is important because it demonstrates GNN scalability in large-scale industrial deployment.

---

### [C15] Wang, Y., Feng, B., Li, G., Li, S., Deng, L., Xie, Y., & Ding, Y. (2021). *GNNAdvisor: An Adaptive and Efficient Runtime System for GNN Acceleration on GPUs.* OSDI 2021.

**URL:** https://www.semanticscholar.org/paper/GNNAdvisor%3A-An-Adaptive-and-Efficient-Runtime-for-Wang-Feng/a72bbf818135b30ab24835e663bc8dcb7b8274ff

This paper shows that GPU optimization for GNNs should adapt to workload characteristics. It profiles graph structure at runtime and chooses different execution strategies depending on node degree and workload type. The work demonstrates that runtime adaptation can significantly improve GNN efficiency on GPUs.

---

### [C16] Thorpe, J., et al. (2021). *Dorylus: Affordable, Scalable, and Accurate GNN Training with Distributed CPU Servers and Serverless Threads.* OSDI 2021.

**URL:** https://www.semanticscholar.org/paper/Dorylus%3A-Affordable%2C-Scalable%2C-and-Accurate-GNN-CPU-Thorpe-Qiao/fb1a90bd9179e6d3f754b565847523a3dc775671

Dorylus shows that GPU acceleration is not the only path to scalable GNN training. By using distributed CPU servers and serverless threads, it achieves large-scale training with a different cost-performance tradeoff. This broadens the system perspective beyond GPU-only solutions.

---

### [C17] Lin, Z., Li, C., Miao, Y., Liu, Y., & Xu, Y. (2020). *PaGraph: Scaling GNN Training on Large Graphs via Computation-Aware Caching.* SoCC 2020.

**URL:** https://dl.acm.org/doi/10.1145/3419111.3421281

PaGraph identifies data movement as a major bottleneck in GNN training. It improves performance through computation-aware caching and better partitioning, which increase locality and reduce memory transfer overhead. The paper highlights the importance of optimizing the memory hierarchy, not only the computation itself.

---

### [C18] Yang, J., Tang, D., Song, X., Wang, L., Yin, Q., Chen, R., Yu, W., & Zhou, J. (2022). *GNNLab: A Factored System for Sample-Based GNN Training over GPUs.* EuroSys 2022.

**URL:** https://dl.acm.org/doi/10.1145/3492321.3519557

GNNLab breaks the training pipeline into separate stages such as sampling, feature loading, computation, and gradient aggregation. This modular analysis reveals that sampling and feature movement consume a large fraction of total time. By optimizing each stage independently, the system achieves notable speedups.

---

### [C19] Kaler, T., Stathas, N., Ouyang, A., Iliopoulos, A.-S., Schardl, T., Leiserson, C., & Chen, J. (2022). *Accelerating Training and Inference of Graph Neural Networks with Fast Sampling and Pipelining.* MLSys 2022.

**URL:** https://www.researchgate.net/publication/360217523_Accelerating_Training_and_Inference_of_Graph_Neural_Networks_with_Fast_Sampling_and_Pipelining

This paper emphasizes that sampling is often a system bottleneck. It introduces fast GPU sampling kernels and pipeline overlap to improve both training and inference. The work shows that end-to-end efficiency requires optimizing the full pipeline rather than only neural computation.

---

### [C20] Yang, S., et al. (2023). *Betty: Enabling Large-Scale GNN Training with Batch-Level Graph Partitioning.* ASPLOS 2023.

**URL:** https://www.researchgate.net/publication/367550869_Betty_Enabling_Large-Scale_GNN_Training_with_Batch-Level_Graph_Partitioning

Betty addresses GPU memory limitations that remain even after sampling is applied. It dynamically partitions computation across GPU and CPU memory at the batch level, reducing memory pressure and enabling larger workloads. This paper represents a more recent direction in memory-aware GNN system design.

---

## Class IV: Survey Reference (1)

*This paper provides general background on GNN literature and related work.*

### [C21] Wu, Z., Pan, S., Chen, F., Long, G., Zhang, C., & Yu, P. (2021). *A Comprehensive Survey on Graph Neural Networks.* IEEE Transactions on Neural Networks and Learning Systems.

**URL:** https://www.researchgate.net/publication/330132719_A_Comprehensive_Survey_on_Graph_Neural_Networks

This is a broad survey of Graph Neural Networks. It is useful for general background and for positioning scalable GNN training within the larger GNN literature. It serves as a supporting reference rather than a central paper in this survey.

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

- **Chapter 1:** Introduction and foundational challenges
- **Chapter 2:** Algorithmic scalability solutions
- **Chapter 3:** Systems and implementation approaches
- **Chapter 4:** Conclusion and future directions
