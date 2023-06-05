We appreciate all reviewers for their valuable comments and will consider all suggestions to revise the final paper.



**Reviewer 1 & 2**



Q1: Using Python/PyTorch for model unification

A1: Both DGL and PyG have operator implementations and interface definitions independent of PyTorch. Despite works such as ONNX for model conversion across deep learning frameworks, there is still no support for GNN frameworks because each GNN framework maintains its internal data structure for graph-related data. To address the above challenge, we propose GUL for unified model definition and a code transformer for code generation. In contrast, Python-based transformations require defining functional interfaces for each operator, preventing its easy adoption for emerging GNNs.



---

**Reviewer 1**



Q1: Novelty of code transformation

A1: The novelty of GUL and code transformers can be understood as filling the notable gap in the unified definition of GNN frameworks. The code transformer ensures the correctness and compatibility of the transformation. One significant challenge of the code transformer is determining the appropriate order of AST nodes. We access the order of each node in advance to determine the order of code modifications. 

Q2: More detailed performance breakdowns

A2: In this paper, we focus on providing key performance statistics for GNN training, including operation decomposition, GPU utilization, and memory consumption. Leveraging the flexibility of the GNNPerf toolkit, we can integrate various profilers to collect fine-grained performance statistics, such as layer-specific execution time. These statistics can be further visualized through the GUI, offering a comprehensive and intuitive representation.

Q3: Handling multi-GPU scenarios

A3: The GNNPerf toolkit can seamlessly support multi-GPU scenarios without communication. It launches multiple processes, each responsible for profiling a specific GPU to collect detailed statistics. In scenarios requiring communication, GNNPerf can integrate additional profilers for collecting communication-related metrics. The collected statistics can be then visualized in the GUI, providing users with a comprehensive and intuitive representation.



---

**Reviewer 2**



Q1: Conceptual differences between DGL and PyG

A1: DGL and PyG have distinct operator and graph processing implementations. DGL adopts a message passing paradigm to unify GNN variants, while PyG represents GNN operators as neighborhood aggregations. GNNPerf addresses this disparity by offering unified model definitions for performance comparison across frameworks. This enables users to select the most suitable framework based on specific application scenarios.

Q2: Features and syntax of GUL

A2: The GUL includes the basic syntax to define some commonly used GNN models handling various GNN tasks. By explicitly defining classes and functions in C++ header files, GUL enables the representation of model structures and functionalities in a format similar to that of GNN frameworks.

Q3: Design consideration of GUL

A3: GUL simplifies GNN model definition by abstracting complex implementation details into a user-friendly syntax. Using C++ for DSL allows us to leverage LLVM Clang, ensuring flexible and extensible code generation.

Q4: Take away insights from Figure 6

A4: Operator decomposition helps understand performance variance (e.g., memory consumption and execution time). Take Figure 7 as an example, the GSpMM operator of DGL combines graph aggregation and node updates to minimize memory usage and data movement. In contrast, PyG employs message passing to update nodes separately, leading to potentially higher memory requirements.

Q5: More insights

A5: GNNPerf innovatively introduces a unified definition of GNN models, enabling performance comparisons across frameworks. It can be extended to explore underlying concepts for deeper insights by refining the GUL design to the operator level for better functional equivalence. Furthermore, GNNPerf can integrate additional profilers for detailed performance statistics. These extensions are left for future work.

Q6: Inconsistent programming paradigms

A6: DGL and PyG indeed have different programming paradigms. For instance, in the readout layer, DGL processes the graph before using the mean_nodes function, while PyG directly uses the global_mean_pool function. The code transformer handles these inconsistencies by generating separate layers for each framework. In contrast, traditional string search and replace methods are inflexible with high processing costs.

Q7: Discussion extension that states the observations

A7: We agree with the reviewer that the discussion should be provided in Section 4. Fortunately, GNNPerf can collect deeper performance statistics, stating the observations and recommendations for framework designs and GPU architectures. We leave this for future work.

Q8: Display operator decomposition for PyG in Figure 5

A8: Figure 5 excerpts the DGL statistics collected by GNNPerf as an example of GUI visualization. The detailed comparison of GNN frameworks is reflected in Section 4. 

Q9: Group together the bars in Figure 6

A9: PyG and DGL differ significantly in operator composition. It is difficult to group the bars of the two frameworks (only 4 out of the top-8 operators are consistent).

Q10: Open source

A10: We will open source GNNPerf to promote the research of the community upon acceptance.



---

**Reviewer 3**



Q1: Comparison with models generated from GUL or DGL/PyG

A1: Although there have been works (e.g., ONNX) to support the model conversion among deep learning frameworks, GNN frameworks are still not supported. Therefore, GNNPerf is urgently needed to provide unified model definitions for performance comparison across frameworks. GUL DSL serves as a unified representation of the GNN structure, which is transformed into code blocks on DGL and PyG for GNN model generation and training.

Q2: Relationship between GNNPerf and Pytorch profiler

A2: GNNPerf toolkit provides training deployment and performance analysis with high flexibility, capable of integrating various profilers (e.g., PyTorch profiler). Specifically, GNNPerf launches profilers to collect performance statistics, which are further visualized through GUI.

Q3: Easy to support other vendors

A3: Currently, the profilers integrated into GNNPerf only support NVIDIA GPUs. However, GNNPerf is highly flexible to integrate other profilers that handle GPUs from other vendors. Specifically, GNNPerf leverages specific profilers to collect performance metrics of targeted GPUs, then visualizes the statistics through GUI to provide comprehensive insights.