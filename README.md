# ML-Assisted Fluid Optimization: Supplementary Figures 50-54

This repository contains the data, notebook, and generated figure outputs used for Supplementary Fig. 50-Fig. 54 of the paper supplementary information for machine-learning-assisted dielectric-fluid optimization.

The workflow focuses on molecular descriptor analysis for 260 candidate molecules. It generates hierarchical clustering, t-SNE visualization, cluster centroid heatmaps, and descriptor discriminability plots for two descriptor panels:

- Chemical inertness descriptors: 21 molecular descriptors
- Viscosity-related descriptors: 35 molecular descriptors

## Repository Structure

```text
.
├── data/
│   ├── ALL_molecules_final_20251102.xlsx
│   ├── RDKit_TYPE1_sequence.csv
│   ├── RDKit_TYPE2_sequence.csv
│   ├── TYPE1-tsne-feature.csv
│   ├── TYPE2-tsne-feature.csv
│   ├── data_descriptors_TYPE1.xlsx
│   ├── data_descriptors_TYPE2.xlsx
│   ├── data_ref_descriptors_TYPE1.xlsx
│   └── data_ref_descriptors_TYPE2.xlsx
├── result/
│   ├── Fig.50 | A hierarchical cluster dendrogram based on chemical inertness.svg
│   ├── Fig.51 | A hierarchical cluster dendrogram based on viscosity.svg
│   ├── Fig.52(a) | t-SNE chemical inertness.html
│   ├── Fig.52(b) | t-SNE viscosity.html
│   ├── Fig.53(a) | Cluster centroid heatmap of the standardized chemical inertness..pdf/.svg
│   ├── Fig.53(b) | Cluster centroid heatmap of the standardized viscosity descriptors..pdf/.svg
│   ├── Fig.54(a) | The analysis of molecular descriptors for clusters...pdf/.svg
│   └── Fig.54(b) | The analysis of molecular descriptors for clusters...pdf/.svg
└── src/
    └── visualization.ipynb
```

## Figure Mapping

| Supplementary figure | Output | Description |
| --- | --- | --- |
| Fig. 50 | `result/Fig.50 ... chemical inertness.svg` | Hierarchical clustering alluvial diagram using 21 chemical-inertness descriptors. Agglomerative clustering uses Ward linkage and Euclidean distance, with selected cuts at L1, L2, L4, and L7. |
| Fig. 51 | `result/Fig.51 ... viscosity.svg` | Hierarchical clustering alluvial diagram using 35 viscosity-related descriptors. The same clustering and visualization strategy is used as Fig. 50. |
| Fig. 52a | `result/Fig.52(a) | t-SNE chemical inertness.html` | Interactive t-SNE scatter plot for chemical-inertness descriptor space. Points are colored by cluster label, and hover text shows molecule names. |
| Fig. 52b | `result/Fig.52(b) | t-SNE viscosity.html` | Interactive t-SNE scatter plot for viscosity descriptor space. Points are colored by cluster label, and hover text shows molecule names. |
| Fig. 53a | `result/Fig.53(a) ... chemical inertness..pdf/.svg` | Cluster centroid heatmap for standardized chemical-inertness descriptors. Rows are clusters and columns are descriptors. |
| Fig. 53b | `result/Fig.53(b) ... viscosity descriptors..pdf/.svg` | Cluster centroid heatmap for standardized viscosity descriptors. |
| Fig. 54a | `result/Fig.54(a) ... chemical inertness..pdf/.svg` | Between-cluster effect size, eta squared, for each chemical-inertness descriptor. |
| Fig. 54b | `result/Fig.54(b) ... viscosity features..pdf/.svg` | Between-cluster effect size, eta squared, for each viscosity-related descriptor. |

## Data Notes

- `ALL_molecules_final_20251102.xlsx` provides the molecule list and SMILES strings used for sample labels.
- `data_descriptors_TYPE1.xlsx` and `data_descriptors_TYPE2.xlsx` contain the main descriptor matrices.
- `data_ref_descriptors_TYPE1.xlsx` and `data_ref_descriptors_TYPE2.xlsx` are included in the MinMax normalization step together with the main descriptor matrices. They affect the scaling range and therefore can affect downstream clustering and descriptor statistics.
- `TYPE1-tsne-feature.csv` and `TYPE2-tsne-feature.csv` provide precomputed t-SNE coordinates for Supplementary Fig. 52. Required columns are `tsne_1`, `tsne_2`, `label`, and `name`.
- `RDKit_TYPE1_sequence.csv` and `RDKit_TYPE2_sequence.csv` define descriptor display order for the heatmaps and eta squared plots.

## Analysis Workflow

The notebook [src/visualization.ipynb](src/visualization.ipynb) performs the following steps:

1. Load molecule metadata and descriptor tables.
2. Normalize descriptor values with MinMax scaling.
3. Fit `AgglomerativeClustering` models with `n_clusters=7`, Ward linkage, Euclidean distance, and distance computation enabled.
4. Convert scikit-learn agglomerative clustering outputs into SciPy linkage matrices.
5. Generate alluvial-style hierarchical cluster diagrams for L1, L2, L4, and L7 cuts.
6. Load precomputed t-SNE coordinates and generate interactive Plotly scatter plots.
7. Compute cluster-wise descriptor means and plot centroid heatmaps.
8. Compute eta squared for each descriptor to quantify between-cluster discriminability.

## Environment

The notebook expects a Python environment with:

- `pandas`
- `numpy`
- `rdkit`
- `scikit-learn`
- `scipy`
- `matplotlib`
- `plotly`
- `kaleido`
- `openpyxl`

Example setup with conda:

```bash
conda create -n ai4s python=3.11
conda activate ai4s
conda install -c conda-forge rdkit pandas numpy scikit-learn scipy matplotlib plotly kaleido openpyxl
```

## Reproducing the Figures

From the repository root:

```bash
cd src
jupyter notebook visualization.ipynb
```

Run the notebook cells from top to bottom. Outputs are written to `../result/`.

The t-SNE figures are interactive HTML files. Open them in a browser to inspect molecule names by hovering over points.

## Supplementary Information Reference

The figure descriptions follow the supplementary information:

- Supplementary Fig. 50: hierarchical cluster dendrogram based on chemical inertness
- Supplementary Fig. 51: hierarchical cluster dendrogram based on viscosity
- Supplementary Fig. 52: t-SNE visualization of clustered molecules in descriptor space
- Supplementary Fig. 53: cluster centroid heatmap of standardized chemical inertness and viscosity descriptors
- Supplementary Fig. 54: molecular descriptor analysis using between-cluster effect size, eta squared
