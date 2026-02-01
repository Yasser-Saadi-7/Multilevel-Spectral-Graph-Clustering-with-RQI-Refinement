# Multilevel-Spectral-Graph-Clustering-with-RQI-Refinement
This project implements a Multilevel Spectral Bisection algorithm to partition an undirected unweighted graph into two distinct clusters. The workflow involves generating a synthetic graph based on a Stochastic Block Model (SBM), coarsening it via Maximal Independent Set (MIS), and refining the partition using Rayleigh Quotient Iteration (RQI).

## Key Features

- **Custom Graph Generation**  
  Generates an undirected graph with **106 nodes**, where the **cluster size ratio** and the **connection probabilities** *(p1, p2)* are derived from two user-defined ID digits *(X, Y)* to achieve a **target average degree**.

- **Graph Coarsening (Multilevel Reduction)**  
  Reduces graph complexity using **MIS (Maximal Independent Set)** seeds. Each fine node is mapped to a nearby MIS representative, producing a **coarsened graph** that preserves global structure while shrinking the problem size.

- **Spectral Bisection (Fiedler Vector Cut)**  
  Builds the **graph Laplacian** and computes the **Fiedler vector** (the eigenvector corresponding to the **second smallest eigenvalue**) to obtain a principled 2-way partition.

- **RQI Refinement (Rayleigh Quotient Iteration)**  
  Applies **Rayleigh Quotient Iteration** to iteratively refine the eigenvector estimate, improving the stability and quality of the spectral partition on the coarsened graph.

- **Quantitative Evaluation**  
  Compares predicted clusters against the **ground truth** using **accuracy metrics**:
  - Accuracy on the **coarsened graph**
  - Accuracy after **expanding (lifting)** the solution back to the original 106-node graph

- **Visualizations**  
  Provides a side-by-side visualization of:
  - **Coarsened Ground Truth**
  - **Coarsened Result after RQI**

---

## Technical Workflow

1. **Generation**  
   Define *(N1, N2)* and *(p1, p2)* based on the user parameters *(X, Y)*.  
   Construct the graph using higher probability *(p1)* inside clusters and lower probability *(p2)* between clusters.

2. **Coarsening**  
   Compute a **Maximal Independent Set (MIS)** and map each fine node to an MIS seed (representative).  
   Build the **coarsened graph** by collapsing edges between representatives.

3. **Partitioning**  
   Compute the **Fiedler vector** on the coarse Laplacian *(second smallest eigenpair)*, then refine it using **RQI**.

4. **Expansion (Lifting)**  
   Project coarse labels back to the original **106 nodes** by inheriting each node’s representative label.

5. **Validation & Visualization**  
   Compute accuracy scores and visualize the ground truth vs. final partition on the coarsened graph.

---

## Requirements

Install the required Python packages:

- `numpy`
- `networkx`
- `scipy`
- `matplotlib`

Example installation:
```bash
pip install numpy networkx scipy matplotlib

