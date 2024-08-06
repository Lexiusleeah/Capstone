## Rough Draft 2 is the Final copy 
# An Exploratory Analysis of Alzheimer’s Disease: Unraveling the Complexities of single cell RNA sequence Data
### Lexius Lynch MSDS.; Advisor: Bishnu Sarker PH.D.; Meharry School of Applied Computational Sciences. 
#### Background:
Single cell biology enables cell level understanding of human health as well as diseases focusing precision medicine. The identification of cell types precisely in major brain disorders is a critical area of research. The complex cellular architecture of the brain, characterized by a diverse set of cell types, makes it challenging to determine the primary pathological cell type for a particular disease.  Recent studies have used single-cell RNA and expression weighted cell type enrichment to identify specific neuronal cell types associated with brain disorders such as Alzheimer's disease (AD). These studies have revealed statistically significant enrichment of certain neuronal cell types in the context of these disorders, providing valuable insights into the differentially expressed genes as well as cell signaling pathways critical to the understanding of variants associated with brain diseases. The development of analytical methods and gene interaction networks for the identification of cell type-specific disease gene modules holds promise for promoting a better understanding of the cell type specificity of brain diseases and the development of more targeted therapeutic interventions. 

 
#### Introduction: 
In this study, an exploratory data Analysis of sc-RNA-seq gene expression data was performed to identify which cells contributed to brain diseases. It is a challenge to determine the primary pathway for diseases because of their complexity, so single cell type annotation can be beneficial in that regard.	

The disease of interest for this study is Alzheimer’s Disease. According to the Alzheimer’s Association, nearly 7 million Americans are living with Alzheimer’s disease. Alzheimer’s disease is a brain disorder caused by certain proteins in the brain that are overproduced. That protein is the amyloid Beta protein(Aβ). Over time, the over production of the amyloid beta protein will cause the brain to decrease in size. This will directly leave patients with an increase in memory loss and a decrease in mental functions. 

According to the CDC, dementia is the most common type of Alzheimer's disease.  Dementia is the inability to remember, think, or make decisions. This ultimately interferes with everyday activities. This disease mostly affects older adults, but it is not a part of the normal aging process. It is a progressive disease that worsens over time. By the year 2060, it is projected that the number of people living with Alzheimer’s disease will affect 14 million people.
There is not a single cause of Alzheimer’s disease, but there are several contributing factors. Age has been linked as a contributor to Alzheimer’s disease—where older individuals over the age of 65 usually develop it. It is also believed that genetics plays a role in the disease along with environment. But it has been said that a healthier lifestyle could prevent the progression or development of the disease. 

 Along with factors, it’s important to note that a care team plays a vital role in quality of life of individuals. Alzheimer’s disease affects patients and families emotionally and financially as well as the healthcare system. A treatment would allow people to live longer independently. But it is vital that the treatment addresses the root cause of the disease. 

#### Methods: 
The methods for my project utilized an unsupervised machine learning pipeline for clustering. My data was read into an Anndata frame that contained the observations and features. Processing the data included performing quality control and dimensional analysis. I initially began with 32,738 genes and after preprocessing, 1,139 genes were left for analysis.

For this study, Scanpy, was utilized. Scanpy is a python-based toolkit used for analyzing single-cell gene expression data. Its main functions include preprocessing, visualization, clustering, trajectory inference, and differential expression testing for single cell genomic data.   
There were two file types for this project, mtx and tsv. The tsv files are tab separated values, but also contained two subsets’ barcodes and features. The barcodes were stored under the tsv file type. The barcodes contain the sequences for each cell/column in the feature-barcode matrix. The barcodes represent unique identifiers for each cell. In summary, the TSV barcodes file contains the unique cell identifiers that allow the sequencing data to be properly associated with each individual cell in a single-cell RNA-seq experiment. The features tsv file type contains information about the genes features that were measured. It includes an ID, the name of the gene, and expression level of the gene. 

The mtx file format contains genes on the rows and cells on the columns. After uploading the dataset into python, it is uploaded into an anndata frame. 
The anndata frame is a dataframe that contains the observations vs the variables. So, the variables would be the gene names.  
After uploading the file into the anndata frame, the next step is preprocessing. A boxplot was created to showcase the top 20 genes detected from the peripheral blood sample. The top 13 had the most outliers. Gene MALAT1, MT-CO2, and MT-CO1 had the most outliers. Upon further research, malat1 is associated with many cancers. And MT is associated with mitochondrial cells. To ensure quality control, mitochondrial cells had to be removed from the sample. High quantities of mitochondrial genes are indicative of poor -quality cells. In order to remove the mitochondrial cells, they had to be annotated, which allowed me to remove the higher percentage contained within the sample. Cells that had too many cell counts were also removed because they provided too many outliers.
 
  <img width="270" alt="image" src="https://github.com/user-attachments/assets/a64f3e5a-e10c-4502-970a-5f532857a214">

Figure 1. Graphical representation of the quality control steps which show the mitochondrial data and genes by counts.

So, the above is a violin plot that shows the density of genes by count. It showcases the total counts and the percentage counts of the mitochondria genes. So approximately a little more than 10 % of the composition of the sample had mitochondria data.
The principal component analysis (PCA) was utilized to reduce the number of variables in the dataset while also identifying the patterns within the data. The purpose of the PCA is to reduce the high dimensional data, which allowed for better visualization of the clusters. The cluster of cells showcases the similarities that those cells share. This is also a linear graphical approach.
 
 <img width="101" alt="image" src="https://github.com/user-attachments/assets/e0cc2a80-4540-4c8f-b67c-085abd922133">

Figure 2. Graphical representation of the principal component analysis of the CST3 gene. 
CST3 is a gene variant associated with brain diseases. And it often associated with dementia and strokes. The CST3 gene plays a part in the process of producing amyloid protein deposits. 
 
   <img width="283" alt="image" src="https://github.com/user-attachments/assets/fd027fa8-5f56-4e45-8b94-ac62203a4281">

Figure 3. Graphical representation of the neighborhood graph. This is the precursor for making the clusters. APOE and APP are proteins that are associated with Alzheimer’s Disease. Each dot represents cells, and the color will dictate if the gene is expressed. The purple represents no expression.


Embedding the neighborhood graph is beneficial in making the clusters. The graph was embedded in two dimensions using UMAP. UMAP stands for uniform manifold approximation and projection for dimensional reduction. This step is helpful in forming the clusters because the data is nonlinear and aids the program in detecting the clusters. For research purposes, I inputted genes that contributed the most to AD, and APOE and APP were most associated. This visualization step revealed how minimal these AD associated genes were present in the sample.  

<img width="278" alt="image" src="https://github.com/user-attachments/assets/d288f153-8dd5-4eb3-8a7c-f34a5967b156">

 
Figure 4. Leiden clustering algorithm 


The next step in the methods is plotting the genes into their appropriate clusters, utilizing the Leiden method. The Leiden method is a graph-based clustering algorithm that is able to identify clusters within the data. The Leiden clustering algorithm is faster and can identify cluster efficiently.  It is able to identify and group data points based on certain similarities. It utilizes k-nearest neighbor.  Figure 4 reveals the clusters by number and differentiates by color. This is the precursor step to labeling the clustered graph. 

In order to label the clustered graph, it’s important to find the marker genes. Marker genes allow me to create a baseline of what genes are within the sample.  Figure 6 is a graphical representation of the marker genes and clusters. I utilized the Wilcoxon rank sum test to help with visualization. The Wilcoxon rank sum test is able to compare the data because it is not a normal distribution of data. The test required 23 trials where I tested the condition for each of the genes individually against the rest of the genes. T test was used to see the difference between the means of two group of data. Figure 5 shows the results of clustering via the Wilcoxon rank sum test. There was a total of 23 cluster and each cluster represents a cluster of cells.
. 

<img width="153" alt="image" src="https://github.com/user-attachments/assets/4dba0114-5d0f-488f-b30d-d60e7219bb5e">

Figure 5. Clustering results. 23 total clusters where each cluster represents a cluster of cells.
 
 <img width="143" alt="image" src="https://github.com/user-attachments/assets/3323d609-5f63-4667-9c92-830a5dd41696">

Figure 6. Represents the dot plot of 23 marker genes.  The highest expressed genes were represented by circle size and color intensity. X-axis genes, y-axis clusters. 


#### Results: 
After defining the clusters, select genes were found in certain clusters. When comparing known Alzheimer’s disease genes, they did not show up as dominantly after processing the data and producing the clusters. Based on figure 6, the highest expressed genes were represented by circle size and color intensity. The x-axis represented the genes and y-axis represented the clusters. Due to preprocessing, all the cells had the same size. It was found that majority of the genes were found in all the clusters. There were mitochondrial data still within many of the clusters of cells. Highly concentrated genes within the clusters included HLAC (T cell), FOXP3 (T cell), MALAT1(cancer). Least concentrated gene within the cluster included CST7 (Aβ). 

This revealed that certain genes might not show up relating to Alzheimer’s disease. However, the composition of the clusters contained many genes that were associated with T cells and Cancerous cells. Meaning these T cells could be the contributors to Alzheimer’s disease. While the genes that were cancerous could be something underlying for those specific patients. 
#### Discussion:
Given a single cell RNA-Seq gene expression matrix, perform a comprehensive exploratory data analysis with following objectives:
1.	 Clustering the cells into distinct groups.
2.	 Identifying differentially expressed genes in each cluster
3.	 Using marker genes to annotate the cell types.


The data set was obtained from the Gene Expression Omnibus, which is a public data repository that contains genomics data. The title of the study is: Single-cell RNA sequencing of peripheral blood reveals immune cell signatures in Alzheimer's disease. The study was conducted by the Capital Medical University in August 2021. The study contained 36,849 peripheral blood mononuclear cells from three patients with AD and two cognitively normal controls. The patients had a confirmed status of AD because of their amyloid(Aβ) positive status. The study revealed five immune cell subsets. CD4+ T cells, CD8+ cells, B cells, Natural Killer cells, and monocytes-macrophages cells. 
The result produced 23 clusters. Each cluster contains a cluster of cells. 

Results of the study: 
After defining the clusters, select genes were found in certain clusters. When comparing known Alzheimer’s disease genes like Aβ & APP & CAA, they did not show up dominantly after processing the data and producing the clusters. This leads me to the assumption that certain genes might not show up relating to AD. However, the composition of the clusters contained many genes associated with T cells and Cancerous cells. Which means the T cells may have a role in the pathogenesis of AD. T cells are known natural killer cells that destroy infected and diseased cells. In this case, patients with higher counts of these T cells have a higher likelihood of having AD. While the cancerous cells could be something underlying for those specific patients. 

 Further research is needed to identify specific cells like Aβ, so that patients can get proper treatment.  The future study could possibly see if inhibiting the genes could slow down the progression of AD. The future study would need to study patients over a long period of time, from onset dementia to full on Alzheimer's disease. Inhibiting the genes could possibly slow down the progression of Alzheimer’s disease, but there are many cells and factors that need to be studied.


 
 






References:
1.	Wolf, F. Alexander, Philipp Angerer, and Fabian J. Theis. "SCANPY: large-scale single-cell gene expression data analysis." Genome biology 19 (2018): 1-5.
2.	Pasquini, Giovanni, et al. "Automated methods for cell type annotation on scRNA-seq data." Computational and Structural Biotechnology Journal 19 (2021): 961-969.
3.	Yang, Fan, et al. "scBERT as a large-scale pretrained deep language model for cell type annotation of single-cell RNA-seq data." Nature Machine Intelligence 4.10 (2022): 852-866. 
4.	Farhadian, Shelli F et al. “Single-cell RNA sequencing reveals microglia-like cells in cerebrospinal fluid during virologically suppressed HIV.” JCI insight vol. 3,18 e121718. 20 Sep. 2018, doi:10.1172/jci.insight.121718 
5.	https://gseapy.readthedocs.io/en/latest/introduction.html 
6.	Corley, M.J., Farhadian, S.F. Emerging Single-cell Approaches to Understand HIV in the Central Nervous System. Curr HIV/AIDS Rep 19, 113–120 (2022). https://doi.org/10.1007/s11904-021-00586-7 
