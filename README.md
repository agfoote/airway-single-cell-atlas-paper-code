# A Single-Cell Atlas of the Upper Respiratory Epithelium Reveals Heterogeneity in Cell Types and Patterning Strategies – _iScience_  
This source code enables the recreation of the results from our iScience 2025 paper ["Cellular heterogeneity and patterning strategies as revealed by upper respiratory epithelium single cell atlas"] [https://www.cell.com/iscience/fulltext/S2589-0042(25)01106-X?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS258900422501106X%3Fshowall%3Dtrue].

## For raw data, please visit our GEO record **GSE287495** at:  
https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE287495

---

> **Note:** this RMarkdown (`single-cell_altas_paper_code.Rmd`) begins **after** the upstream preprocessing steps (filtering, QC, doublet removal and dataset refinement) have already been completed. It covers downstream integration, clustering, annotation, DE testing, visualization and downstream irGSEA and trajectory analyses.

### Outline of `single-cell_altas_paper_code.Rmd`

- **Set up Workspace**  
  - Import filtered & refined `.rds` files (post-QC)  
  - Check and add sample metadata  

- **Integration with CCA**  
  - Find integration anchors & integrate data  
  - Normalize to cell numbers  
  - Visualize integrated object & inspect major cell compartments  
  - Run `FindAllMarkers()` on the integrated object  

- **Dataset refinement**  
  - Subset clusters positive for **EPCAM**  
  - Run `FindAllMarkers()` to identify contaminating populations  
  - Remove low-quality or off-target clusters (e.g. thyroid cells)  
  - Re-subset & re-run `FindAllMarkers()` on the refined dataset  

- **CellType Annotation**  
  - Add custom cluster labels (e.g. “Basal”, “Club”, “Ciliated”)  
  - Run `FindAllMarkers()` on annotated object  
  - Perform MAST-based DE testing via `FindAllMarkers(stat.test = "MAST")`  

- **Visualization of `scRNA_epi_saline` object**  
  - DotPlot of top marker genes per cell type  
  - FeaturePlot highlighting specific subsets  
  - Advanced visualizations (e.g. RidgePlot, SpatialFeaturePlot)  

- **Descriptive Statistics**  
  - Extract and tabulate metadata  
  - Count cells by `Condition × CellType`  
  - Calculate percent of cells expressing each marker  

- **Basal & Club Cell Subpopulation Analysis**  
  - Subset “Basal” clusters  
  - DE analysis of basal subpopulations via `FindAllMarkers()`
 
- **irGSEA Pathway Enrichment**  
  - Prepare ranked gene lists from DE results  
  - Run `irGSEA()` for hallmark and custom gene sets  
  - Visualize enriched pathways with dotplots and enrichment curves  

- **Monocle3 Trajectory Analysis**  
  - Convert Seurat object to `cell_data_set` via `as.cell_data_set()`  
  - Preprocess, reduce dimension, cluster and learn graph (`learn_graph()`)  
  - Perform `graph_test()` to identify trajectory-associated genes  
  - Plot pseudotime trajectories with `plot_cells()` and `RidgePlot()`  

---
