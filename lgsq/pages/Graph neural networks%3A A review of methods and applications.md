title:: Graph neural networks: A review of methods and applications
file:: ![Graph neural networks: A review of methods and applications](../assets/zhou2021_1710400525745_0.pdf)
file-path:: ../assets/zhou2021_1710400525745_0.pdf

- # Introduction
	- As a unique non-Euclidean data structure for machine learning, graph analysis focuses on tasks such as node classiﬁcation, link prediction, and clustering. Graph neural networks (GNNs) are deep learning based methods that operate on graph domain. Due to its convincing performance, GNN has become a widely applied graph analysis method recently
	  hl-page:: 1
	  ls-type:: annotation
	  id:: 65f2a7a8-6e54-494d-8a3c-247c467a3898
	  hl-color:: yellow
		- Graph domain models a set of objects and their relationships as edges and nodes respectively.
	- Although being successful, the universal idea behind these methods [Recurrent Neural networks and Feedforward Neural Networks] is building state transition systems on graphs and iterate until convergence, which constrained the extendability and representation ability.
	  hl-page:: 1
	  ls-type:: annotation
	  id:: 65f2a8a7-714e-416a-b3e9-5f8111f41c94
	  hl-color:: yellow
- # General design pipeline of GNNs
	- ... we denote a graph as $G=(V,E)$, where $|V|=N$ is the number of nodes in the graph and $|E=N^e|$ is the number of edges. $A \in R ^ {N \times N}$ is the adjacency matrix. For graph representation learning, we use $h_v$ and $o_v$ as the hidden state and output vector of node $v$.
	  hl-page:: 3
	  ls-type:: annotation
	  id:: 65f2a94c-ee72-40c2-b966-cb28d6d8ff2b
	  hl-color:: yellow
	- Generally, the pipeline contains four steps: (1) ﬁnd graph structure, (2) specify graph type and scale,(3) design loss function and (4) build model using computational modules.
	  hl-page:: 3
	  ls-type:: annotation
	  id:: 65f2abdb-70db-4ea2-9d1d-21c303218b24
	  hl-color:: yellow
	- ## Find Graph Structure
		- There are usually two scenarios: structural scenarios and non-structural scenarios
		  ls-type:: annotation
		  hl-page:: 3
		  hl-color:: yellow
		  id:: 65f2ac9f-3bd9-4394-9de7-f36779600987
		- In **structural scenarios**, the graph structure is explicit in the applications, such as applications on molecules, physical systems, knowledge graphs and so on.
		  ls-type:: annotation
		  hl-page:: 3
		  hl-color:: yellow
		  id:: 65f2aca5-99d0-463d-89e2-a5ba7e45cf8c
		- In **non-structural scenarios**, graphs are implicit so that we have to ﬁrst build the graph from the task, such as building a fully-connected “word” graph for text or building a scene graph for an image.
		  ls-type:: annotation
		  hl-page:: 3
		  hl-color:: yellow
		  id:: 65f2acac-f0aa-49f4-aa3b-e173754d3d3f
	- ## Specify graph type and scale
		- **Directed/Undirected Graphs** - Edges directed from one node to another. Directed is one-way until specified, Undirected is two-way.
		- **Homogeneous/Heterogeneous Graphs** - In homo- nodes and edges have same types. It is different in hetero-.
		- **Static/Dynamic Graphs** - Input features or topology of graph varies with time in dynamic graphs.
		- Categories are orthogonal, which means they can be combined.
		- There is no clear classification criterion for scale, it could be "small" or it could be "large"
	- ## Design loss function
		- **Kinds of tasks:**
			- **Node-level** tasks focus on nodes (classification, regression, clustering, etc.)
			- **Edge-level** tasks are edge classification and link predictions, which require the model to classify edge types or predict whether there is an edge existing between two given nodes.
			- **Graph-level** tasks work on graph (classification, regression, clustering, etc.) all of which need model to learn graph representation.
		- **Training settings:**
			- Supervised setting provides labeled data for training.
			- Semi-supervised setting gives small amount of labeled nodes and a large amount of unlabeled nodes.
				- In the test phase, the transductive setting requires the model to predict the labels of the given unlabeled nodes, while the inductive setting provides new unlabeled nodes from the same distribution to infer. Most node and edge classiﬁcation tasks are semi-supervised
				  ls-type:: annotation
				  hl-page:: 3
				  hl-color:: yellow
				  id:: 65f2af29-1b85-4bd0-bb3c-1bc51bba42c2
			- Unsupervised setting only offers unlabeled data for model to find patterns. Node clustering is typical for this kind of task.
		- With the task type and the training setting, we can design a speciﬁc loss function for the task. For example, for a node-level semi-supervised classiﬁcation task, the cross-entropy loss can be used for the labeled nodes in the training set.
		  ls-type:: annotation
		  hl-page:: 3
		  hl-color:: yellow
		  id:: 65f2af5e-9b29-4c71-bebb-9eb888ad5e75
	- ## Build model using computational modules
		- **Common modules:**
			- Propagation modules
				- The propagation module is used to propagate information between nodes so that the aggregated information could capture both feature and topological information.
				  ls-type:: annotation
				  hl-page:: 4
				  hl-color:: yellow
				  id:: 65f2afac-c374-488c-a056-cf6f694cfdeb
			- Sampling module
				- When graphs are large, sampling modules are usually needed to conduct propagation on graphs.
				  ls-type:: annotation
				  hl-page:: 4
				  hl-color:: yellow
				  id:: 65f2afb6-3c99-48cf-bddf-191c0e217112
			- Pooling module
				- When we need the representations of high-level subgraphs or graphs, pooling modules are needed to extract information from nodes.
				  ls-type:: annotation
				  hl-page:: 4
				  hl-color:: yellow
				  id:: 65f2afbd-d3c6-4a4e-9bca-064683dd6ae1
		- [:span]
		  ls-type:: annotation
		  hl-page:: 5
		  hl-color:: yellow
		  id:: 65f2b0a0-3e19-4f32-949f-c6b487a8ff4b
		  hl-type:: area
		  hl-stamp:: 1710403742759
	- [:span]
	  ls-type:: annotation
	  hl-page:: 4
	  hl-color:: yellow
	  id:: 65f2b04d-f813-43b8-8c12-55e546024c99
	  hl-type:: area
	  hl-stamp:: 1710403661653