<div align="center">

<b>CS 5463/4953 – Survey Based Term Project</b><br>
<b>Annotated Bibliography of Literature Found</b><br><br>

<b>Survey Title:</b> A Survey of Scalable Graph Neural Network Training Techniques on GPU Architectures

</div>

---

## Category I: Foundational Papers (4)

[F1] Kipf, T. N., & Welling, M. (2017). Semi-Supervised Classification with Graph Convolutional Networks (ICLR 2017).  
URL: https://openreview.net/forum?id=SJU4ayYgl  

**Annotation:** This paper introduces Graph Convolutional Networks (GCNs), one of the most influential baseline architectures in graph learning. It uses neighborhood aggregation in a simple full-batch formulation. The method is computationally efficient on small citation graphs but becomes difficult to scale to large graphs. It is foundational because many later scalable systems are designed around the limitations of GCN training.
---

[F2] Hamilton, W., Ying, Z., & Leskovec, J. (2017). Inductive Representation Learning on Large Graphs (NeurIPS 2017).  
URL: https://dl.acm.org/doi/10.5555/3294771.3294869#purchase-access  

**Annotation:** This paper introduces GraphSAGE, which learns node embeddings by sampling and aggregating neighborhood features. Unlike full-batch GCNs, it supports inductive learning and mini-batch training. This makes it highly relevant to scalable GNN training on large graphs. Many later sampling-based systems build directly on GraphSAGE-style neighborhood expansion.

---

[F3] Veličković, P., Cucurull, G., Casanova, A., Romero, A., Liò, P., & Bengio, Y. (2018). Graph Attention Networks (ICLR 2018).  
URL: https://openreview.net/forum?id=rJXMpikCZ  

**Annotation:** Graph Attention Networks (GAT) replace uniform aggregation with learned attention weights over neighbors. This improves model flexibility and often accuracy but also increases per-edge computation. For large graphs, attention can create additional scalability pressure. The paper is important because many GPU systems must handle both message passing and attention efficiently.

---

[F4] Xu, K., Hu, W., Leskovec, J., & Jegelka, S. (2019). How Powerful Are Graph Neural Networks? (ICLR 2019).  
URL:https://openreview.net/forum?id=ryGs6iA5Km  

**Annotation:** This paper studies the expressive power of graph neural networks and introduces Graph Isomorphism Networks (GIN). It shows that common aggregation functions differ in their ability to distinguish graph structures, with sum aggregation being more powerful than mean or max. GIN is designed to match the discriminative power of the Weisfeiler-Lehman test. This work is important for understanding how model design affects representation quality in scalable GNN systems.

---

## Category II: Recent Journal / Conference Papers (10)

[C1] Chen, J., Ma, T., & Xiao, C. (2018). FastGCN: Fast Learning with Graph Convolutional Networks via Importance Sampling (ICLR 2018).  
URL: https://openreview.net/forum?id=rytstxWAW  

**Annotation:** FastGCN reduces training cost by sampling nodes with importance weights instead of expanding the full neighborhood at every layer. This lowers both memory usage and computation. The paper is one of the earliest attempts to make GCN training practical on larger graphs. It is central to the sampling-based scalability literature.

---

[C2] Huang, W., Zhang, T., Rong, Y., & Huang, J. (2018). Adaptive Sampling Towards Fast Graph Representation Learning.(NeurIPS 2018).  
URL: https://dl.acm.org/doi/10.5555/3327345.3327367  

**Annotation:** This paper proposes an adaptive importance sampling method to accelerate graph representation learning. It formulates graph convolution as an integral transform and samples nodes based on learned importance distributions. The approach reduces the variance of stochastic training while avoiding unnecessary computation over full neighborhoods. It improves both efficiency and convergence compared to earlier sampling-based methods for scalable GNN training.

---

[C3] Chen, J., Zhu, J., & Song, L. (2018).Stochastic Training of Graph Convolutional Networks with Variance Reduction.(ICML 2018).  
URL: https://www.semanticscholar.org/paper/Stochastic-Training-of-Graph-Convolutional-Networks-Chen-Zhu/a60c69c2fae27ebbb73c87f7f2a4765556bd7f9f  

**Annotation:** This paper uses control variates to reduce the variance introduced by stochastic neighborhood sampling. The key idea is that training can use very small sampled neighborhoods while still converging reliably. It is relevant because it addresses one of the main problems of mini-batch GNN training: unstable gradient estimates. The paper provides both algorithmic and theoretical insight into scalable training.

---

[C4] Zou, D., Hu, Z., Wang, Y., Jiang, S., Sun, Y., & Gu, Q. (2019).Layer-Dependent Importance Sampling for Training Deep and Large Graph Convolutional Networks. (NeurIPS 2019).  
URL:https://www.researchgate.net/publication/339946989_Layer-Dependent_Importance_Sampling_for_Training_Deep_and_Large_Graph_Convolutional_Networks  

**Annotation:** LADIES improves layer-wise sampling by conditioning the sampled nodes on the current upper-layer nodes. This preserves connectivity better than earlier layer-independent methods. The method is effective for deeper GCNs and large graphs. It is relevant because it highlights how smarter sampling can improve both scalability and model quality.

---

[C5] Chiang, W., Liu, X., Si, S., Li, Y., Bengio, S., & Hsieh, C. (2019). Cluster-GCN: An Efficient Algorithm for Training Deep and Large Graph Convolutional Networks. (KDD 2019).  
URL: https://dl.acm.org/doi/10.1145/3292500.3330925  

**Annotation:** Cluster-GCN partitions the graph into clusters and trains on subgraphs instead of randomly sampled neighbors. This reduces memory overhead and improves locality during training. The method is important because it connects graph partitioning with scalable mini-batch optimization. It is one of the most widely cited partition-based GNN training methods.

---

[C6] Zeng, H., Zhou, H., Srivastava, A., Kannan, R., & Prasanna, V. (2020). GraphSAINT: Graph Sampling Based Inductive Learning Method (ICLR 2020).  
URL: https://openreview.net/forum?id=BJe8pkHFwS  

**Annotation:** GraphSAINT samples entire subgraphs, not only nodes or edges, and normalizes training to reduce bias. This preserves more graph structure than many previous samplers. It is highly relevant because it improves both scalability and accuracy on large graphs. The paper is now a standard reference for scalable mini-batch GNN training.

---

[C7] Ying, R., He, R., Chen, K., Eksombatchai, P., Hamilton, W., & Leskovec, J. (2018). Graph Convolutional Neural Networks for Web-Scale Recommender Systems.(KDD 2018).  
URL: https://dl.acm.org/doi/10.1145/3219819.3219890  

**Annotation:** This paper presents PinSage, a large-scale GNN system used at Pinterest for recommendation. It combines random-walk-based neighborhood construction with graph convolutions. The work is important because it demonstrates GNN training at true industrial scale. It is one of the clearest examples of scalability in a real production setting.

---

[C8] Wu, F., Souza, A., Zhang, T., Fifty, C., Yu, T., & Weinberger, K. (2019). Simplifying Graph Convolutional Networks. (ICML 2019).  
URL: https://www.semanticscholar.org/paper/Simplifying-Graph-Convolutional-Networks-Wu-Zhang/7e71eedb078181873a56f2adcfef9dddaeb95602  

**Annotation:** This paper proposes SGC, which removes nonlinearities and collapses repeated graph propagation into a simpler linear model. The resulting method is much faster while often retaining competitive accuracy. It is relevant because it shows that simplifying the model itself can be a strong scalability strategy. This paper is useful for discussing speed–accuracy trade-offs in GNN design.

---

[C9] Gasteiger, J., Bojchevski, A., & Günnemann, S. (2019). Predict then Propagate: Graph Neural Networks meet Personalized PageRank.(ICLR 2019).  
URL: https://openreview.net/forum?id=H1gL-2A9Ym  

**Annotation:** This paper decouples prediction from propagation using personalized PageRank. By separating these steps, it allows large receptive fields without deep neighborhood expansion during training. It is relevant because it reduces the training burden of recursive message passing. The paper also shows a useful direction for scalable GNNs based on precomputation.

---

[C10] Zeng, H., Zhang, M., Xia, Y., Srivastava, A., Malevich, A., Kannan, R., Prasanna, V., Jin, L., & Chen, R. (2021). Deep Graph Neural Networks with Shallow Subgraph Samplers. (ICLR 2021).  
URL: https://openreview.net/forum?id=GIeGTl8EYx  

**Annotation:** This paper proposes the “deep model, shallow sampler” design principle. Instead of using large sampled neighborhoods for deep GNNs, it uses carefully chosen shallow subgraphs. This helps reduce computation while supporting deeper architectures. It is important because it addresses both oversmoothing and scalability at the same time.

---

## Category III: Systems, Frameworks, and GPU/Distributed Training (10)

[C11] Ma, L., Yang, Z., Miao, Y., et al. (2019). NeuGraph: Parallel Deep Neural Network Computation on Large Graphs. (USENIX ATC 2019).  
URL: https://www.usenix.org/conference/atc19/presentation/ma  

**Annotation:** NeuGraph is one of the first systems papers focused on efficient GNN computation over large graphs. It combines graph-style execution with dataflow optimization. The paper is highly relevant because it studies how graph partitioning, scheduling, and operator design affect GPU performance. It provides a systems perspective that pure algorithm papers do not.

---

[C12] Wang, M., Yu, L., Zheng, D., Gan, Q., Gai, Y., Ye, Z., Li, M., Zhou, J., & Karypis, G. (2019). Deep Graph Library: A Graph-Centric, Highly-Performant Package for Graph Neural Networks. NeurIPS 2019 Workshop on Machine Learning Systems.  
URL: https://www.semanticscholar.org/paper/Deep-Graph-Library%3A-A-Graph-Centric%2C-Package-for-Wang-Zheng/381411d740562de1e766dc8cc833844eb99dde01  

**Annotation:** This work describes the design of DGL, a graph-focused framework for implementing and optimizing GNNs. It exposes common graph operators while enabling backend optimizations across deep learning frameworks. It is relevant because many scalable GNN experiments and systems are built on DGL. The paper is useful for understanding the software support layer of high-performance GNN training.

---

[C13] Zheng, D., Ma, C., Wang, M., Zhou, J., Su, Q., Song, X., Gan, Q., Zhang, Z., & Karypis, G. (2020). DistDGL: Distributed Graph Neural Network Training for Billion-Scale Graphs. Proceedings of the IEEE/ACM Workshop on Irregular Applications: Architectures and Algorithms (IA3 2020), held with SC 2020.  
URL: https://doi.org/10.1109/IA351965.2020.00011  

**Annotation:** DistDGL extends DGL to distributed environments and supports training on billion-scale graphs. It combines graph partitioning, distributed storage, and communication-aware execution. This paper is directly aligned with the survey topic because it addresses large-scale multi-machine GNN training. It is one of the key references for distributed GNN systems.

---

[C14] Zhu, R., Zhao, K., Yang, H., Lin, W., Zhou, C., Ai, B., Li, Y., & Zhou, J. (2019). AliGraph: A Comprehensive Graph Neural Network Platform. (PVLDB 2019).  
URL: https://dl.acm.org/doi/10.14778/3352063.3352127  

**Annotation:** AliGraph presents a large-scale industrial GNN platform with distributed graph storage, sampling operators, and runtime support. It is designed to serve real production workloads at Alibaba. The paper is relevant because it connects algorithm design with deployment-scale system constraints. It also shows how scalable GNN training is handled in industry rather than only on academic benchmarks.

---

[C15] Wang, Y., Feng, B., Li, G., Li, S., Deng, L., Xie, Y., & Ding, Y. (2021). GNNAdvisor: An Adaptive and Efficient Runtime System for GNN Acceleration on GPUs. (OSDI 2021).  
URL: https://www.semanticscholar.org/paper/GNNAdvisor%3A-An-Adaptive-and-Efficient-Runtime-for-Wang-Feng/a72bbf818135b30ab24835e663bc8dcb7b8274ff  

**Annotation:** GNNAdvisor focuses on runtime optimization for GNNs on GPUs. It uses workload-aware scheduling and memory-hierarchy-aware execution to improve utilization. This paper is central to the GPU systems side of your survey topic. It shows that runtime design can significantly change the practical performance of GNN training.

---

[C16] Thorpe, J., et al. (2021). Dorylus: Affordable, Scalable, and Accurate GNN Training with Distributed CPU Servers and Serverless Threads. (OSDI 2021)  
URL: https://www.semanticscholar.org/paper/Dorylus%3A-Affordable%2C-Scalable%2C-and-Accurate-GNN-CPU-Thorpe-Qiao/fb1a90bd9179e6d3f754b565847523a3dc775671

**Annotation:** Dorylus explores a different systems direction by using distributed CPU servers and serverless threads for scalable GNN training. The paper is important because it highlights that large-scale GNN training is not only a GPU problem but also a system architecture problem. It is useful in the survey for comparing GPU-heavy and distributed alternatives. It also emphasizes cost-aware scalability.

---

[C17] Lin, Z., Li, C., Miao, Y., Liu, Y., & Xu, Y. (2020). PaGraph: Scaling GNN Training on Large Graphs via Computation-Aware Caching.  
ACM Symposium on Cloud Computing (SoCC 2020).  
URL: https://dl.acm.org/doi/10.1145/3419111.3421281  

**Annotation:** PaGraph targets sampling-based GNN training on a single server with multiple GPUs. Its main idea is to use caching and partitioning that match the computation pattern of GNNs. This reduces data loading overhead and improves utilization of GPU resources. It is directly relevant because it studies scalable training under practical multi-GPU constraints.

---

[C18] Yang, J., Tang, D., Song, X., Wang, L., Yin, Q., Chen, R., Yu, W., & Zhou, J. (2022). GNNLab: A Factored System for Sample-Based GNN Training over GPUs. (EuroSys 2022).  
URL: https://dl.acm.org/doi/10.1145/3492321.3519557  

**Annotation:** GNNLab separates sampling and model training into a factored GPU system design. It also adds feature caching to reduce memory contention and improve throughput. This is important because mini-batch GNN training often spends substantial time outside the neural network layers themselves. The paper gives a clear systems explanation of where the bottlenecks are.

---

[C19] Kaler, T., Stathas, N., Ouyang, A., Iliopoulos, A.-S., Schardl, T., Leiserson, C., & Chen, J. (2022). Accelerating Training and Inference of Graph Neural Networks with Fast Sampling and Pipelining. (MLSys 2022).  
URL: https://www.researchgate.net/publication/360217523_Accelerating_Training_and_Inference_of_Graph_Neural_Networks_with_Fast_Sampling_and_Pipelining  

**Annotation:** OThis paper introduces SALIENT, a system that focuses on sampling, slicing, and data transfer bottlenecks in mini-batch GNN workloads. It uses pipelining and optimized neighborhood sampling to overlap work efficiently. The paper is highly relevant because it studies the end-to-end training pipeline rather than only the core aggregation operator. It is especially useful for discussing hardware utilization and data movement.

---

[C20] Yang, S., et al. (2023). Betty: Enabling Large-Scale GNN Training with Batch-Level Graph Partitioning. (ASPLOS 2023).  
URL: https://www.researchgate.net/publication/367550869_Betty_Enabling_Large-Scale_GNN_Training_with_Batch-Level_Graph_Partitioning  

**Annotation:** Betty reduces memory pressure in GNN training by partitioning the batch-level computation graph and by using both CPU and GPU memory. This makes larger training workloads feasible even when a single GPU cannot hold the whole working set. The paper is relevant because it addresses memory capacity, one of the biggest practical barriers to scalable GNN training. It also shows how partitioning can be applied after sampling.

---

## Category IV: Survey Reference (1)

[C21] Wu, Z., Pan, S., Chen, F., Long, G., Zhang, C., & Yu, P. (2021). A Comprehensive Survey on Graph Neural Networks. IEEE Transactions on Neural Networks and Learning Systems.  
URL: https://www.researchgate.net/publication/330132719_A_Comprehensive_Survey_on_Graph_Neural_Networks  

**Annotation:** This survey is broader than your project, but it is useful as a reference map for the overall GNN literature. It explains the main model families, training settings, and application areas. For your term project, it helps position scalable training papers within the larger GNN landscape. It is best used as a supporting survey rather than as the main focus of your final paper.
