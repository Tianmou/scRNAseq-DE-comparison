# Single-cell RNA-seq Datasets
Single-cell RNA-seq datasets used in comparing different methods of differential expression analysis.

### MDA-MB-231 
The scRNA-seq data set, MDA-MB-231 ("count_MDA.Rdata"), includes 160 single cells from a triple-negative breast cancer cell line, half of which are treated with metformin. The cells are captured using the Fluidigm C1 system and sequenced on Illumina HiSeq 2500 machines for 80 control and 80 treated cells separately. Then we use Cufflinks to estimate the isoform expression. This data set contains a total of 26,775 isoforms across 160 single cells. The average number of reads per cell is $\sim$649,000. 

### mESCs
mESCs ("count_mESCs.Rdata") is collected from a public scRNA-seq data (GSE60749-GPL13112) in the \textit{Conquer} repository (Soneson, C. & Robinson, M.D., 2018), which provides expression estimates of isoforms. The compared single cells are 94 individual v6.5 mouse embryonic stem cells (mESCs) with culture conditions 2i+LIF (group 1) \textit{vs.} 174 v6.5 mESCs with culture conditions in serum+LIF (group 2). The data are prepared with the C\textsubscript{1} System using the SMARTer Ultra Low RNA kit for Illumina Sequencing (Clontech) and protocols provided by Fluidigm. More details of the data can be found in the original paper \citep{kumar2014GSE60749}. Then the \textit{Conquer} pipeline estimates isoform abundances using Salmon. This data set contains 112,593 isoforms across 174 single cells in group 1 and 94 single cells in group 2. The average number of reads per cell is $\sim$1.7M.

### NPCs
NPCs ("count_NPCs.Rdata") is a subset of GSE102934 data from the NCBI Gene Expression Omnibus. This data set has 720 neuronal progenitor cells (NPCs) derived from induced pluripotent stem (iPS) cells, half of which are from a Williams-Beuren patient and the other half are from a healthy donor. The data are sequenced on Illumina HiSeq 2500 platform and then applied massively parallel single-cell RNA sequencing (MARS-Seq) to construct single-cell libraries. This data set contains a total of 41,020 isoforms from 720 single cell, and the average number of reads per cell is 18,600. Thus, this data set has a relatively large number of cells with low sequencing coverage.

### SRP073808
SRP073808 ("count_SRP073808.Rdata") is from the \textit{Conquer} repository (Soneson, C. & Robinson, M.D., 2018).
The compared cells in SRP073808 are 77 in vitro cultured H7 embryonic stem cells (WiCell) and 87 cells from H7-derived downstream early mesoderm progenitors. The protocol type for this data set is SMARTer C1. Library size varies from 9,023 to 3.8M reads. The average number of reads per cell is $\sim$1.5M.

### GSE62270-GPL17021
GSE62270 ("count_GSE62270.Rdata") is also from the \textit{Conquer} repository (Soneson, C. & Robinson, M.D., 2018).
It includes 1344 cells from mouse intestinal organoids and 683 Reg4-positive intestinal cells. This data set was generated by protocol CEL-Seq. Library size varies from 1 to 0.6M reads. The average number of reads per cell is $\sim$9,689.

### Beta-Poisson simulation

The simulated data set for isoform expression of single cells is generated by the beta-Poisson model (Vu, T.N. et al., 2016). In particular, we generate the counts for each isoform from a beta-Poisson distribution with four parameters estimated from a real data set (mESCs). The four-parameter beta-Poisson model is as follows

$BP_4(x|\alpha,\beta,\lambda_1,\lambda_2 ) = \lambda_2 \mbox{Poisson}(x|\lambda_1 \mbox{Beta}(\alpha,\beta)).$

The mean and variance of the model can be written as

$\mu = E(X)=\lambda_1\lambda_2 \phi_1$

and

$Var(X)=\mu \lambda_2 + \mu^2 \phi_2$,

where $\phi_1=\frac{\alpha}{\alpha+\beta}$ and 
$\phi_2=\frac{\beta}{\alpha(\alpha+\beta+1)}$. Crucially, we can modify the parameter $\lambda_1$ to create mean differences between groups. A more detailed description of the model can be referred to in the original study (Vu, T.N. et al., 2016).

Beta-Poisson models fitted on the real mESCs data set are used as baseline distributions for simulation. For each isoform, expression values across samples in the control and the treated group are generated from the same beta-Poisson model. To mimic the biological variation, 5\% of isoforms are selected to be differentially expressed between two groups (true DE isoforms). Specifically, the parameter $\lambda_1$, which controls the mean of the distribution, is fixed in the control group and multiplied by $\log_2$ fold change of 1 or 4 unit in the treated group. The effect direction is randomly determined for each DE isoform, with equal probability of up- and down-regulation. In other words, for dataset "BPsimData_0.05DE_lfc1.Rdata", the quantity change between the two compared groups is either 2- or half-fold change with equal probability. The dataset "BPsimData_0.05DE_lfc4.Rdata" is similar, but with $\log_2$ fold change of 4 unit. The simulated data set consists of 80 samples in each of control and treated groups and a total of 10,000 isoforms measured per sample. Library sizes of the single-cell samples are randomly sampled from a range of 1-3 million. 
We filter out isoforms with zero expression across all samples. 

Related publications: 

Mou, T. et al. Reproducibility of methods to detect differentially expressed genes from  single-cell RNA sequencing.

Vu, T.N. et al. (2016) Beta-Poisson model for single-cell RNA-seq data analyses. Bioinformatics, btw202. http://bioinformatics.oxfordjournals.org/content/early/2016/04/18/bioinformatics.btw202

Soneson, C. & Robinson, M.D. (2018) Bias, robustness and scalability in single-cell differential expression analysis. Nature Methods 15(4):255-261.
