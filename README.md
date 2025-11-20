## Mulit-omics clustering of publicly available gene expression + somatic mutation data from TCGA using a deep learning approach
#### Autoencoder + Gaussian Mixture Model Pipeline 



### Intro
This contains the full pipeline used for clustering of TCGA lung cancer samples. 

The workflow combines RNA-seq expression and somatic mutation data into a shared latent feature space using autoencoders, followed by model based clustering. 

A total of 9 clusters are finalized and downstream mutational, pathway, immune signatures, gene expression and clinical outcomes were analyzed. 

### Workflow Summary
1. Pre-processing 
   - Gene expression '.tsv' files )
   - Binary mutation matrices derived from '.maf' files
   - Case/sample mapping file linking TCGA barcodes to Case IDs using mapping file

2. Feature Scaling & Preprocessing
   - Log-transform + 1,  Min–Max scaling for expression values  
   - Binary encoding for mutation data  

3. Autoencoder Compression
   - Expression AE: latent dimension 200  
   - Mutation AE: latent dimension 200  
   - Concatenated latent space = 400 features per sample  

4. Recursive Gaussian Mixture Model Clustering
   - Model-based clustering with automatic BIC selection  
   - Clusters refined recursively; small subclusters merged  
   - Final labels standardized as 'C1–C9'

5. Downstream Analyses
   - Hallmark GSEA (via GSEApy)
   - Mutational signature extraction (SigProfilerExtractor)
   - Mutational status, TMB
   - Immune analysis
   - Differential Gene expression
   - Clinical variable correlations (age, gender, stage, histology)
   - Smoking exposure analysis (years, status)
   - Kaplan–Meier survival analysis  

6. Visualization
   - Heatmaps (seaborn)
   - Barplots and boxplots (seaborn, matplotlib)
   - Kaplan–Meier survival curves (lifelines)
   - Demographic summary figures (gender, race, age distributions)

Input are containted in 'Inputs' folder. 

### How to access TCGA Data: 
Navigate to the GDC Data Portal: https://portal.gdc.cancer.gov/

Use the Cohort Builder Tool to create the Lung cohort. 
Under general, the primary site should be bronchus and lung.
  The tissue or organ of origin should be lung.
  Available data should be masked somatic mutation and gene expression quantification.
  Clinical data can be downloaded directly from GDC data portal. 
  All data was downloaded via GDC transfer tool (https://gdc.cancer.gov/access-data/gdc-data-transfer-tool), however, it can
  alternatively be downloaded directly from https://portal.gdc.cancer.gov. 

All TCGA data utilized was from publicly available, open-accessed tiered data. 
