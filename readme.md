# Development and Validation of a Breast Cancer Recurrence Model Demonstrates Accurate Identification of Patients with Favorable Long-Term Outcomes
Here, we present the development and validation of a machine leraning model to predict breast cancer recurrence risk using clinicopathologic variables in the National Cancer Database. We developed models using quantitative ER/PR/Ki-67 status, ER/PR status alone, and no quantitative data. We identified 'rule-out' thresholds, identifying very low risk (95% sensitivity for high Oncotype score) and low risk (90% sensitvitiy) patients. These patients have excellent long term prognosis and may be candidates for hormonal therapy alone without further testing, although additional prospecitve study is needed.
<br>
<img src="https://github.com/fmhoward/NCDBRS/blob/main/overview.png?raw=true" width="400">

## Attribution
If you find our work useful, please cite our paper in <a href=https://www.nature.com/articles/s41523-024-00651-5>NPJ Breast Cancer</a>
```
@article{howard_rsncdb_2023,
	title = {Development and Validation of a Clinical Breast Cancer Tool for Accurate Prediction of Recurrence},
	copyright = {2023 The Author(s)},
	url = {[https://www.nature.com/articles/s41523-024-00651-5](https://www.nature.com/articles/s41523-024-00651-5)},
	abstract = {The Oncotype DX (ODX) test is a 21-gene expression assay widely used for the prediction of risk recurrence in early-stage breast cancer, but due to the high costs of testing, previous studies have attempted to replicate ODX with quantitative clinicopathologic variables. However, such models have only been evaluated on small cohorts of patients which may not be nationally applicable. Using a cohort of patients from the National Cancer Database (NCDB, n = 53,346), we trained machine learning models for prediction of low-risk (0-25) or high-risk (26-100) ODX score using quantitative ER/PR/Ki-67 status, quantitative ER/PR status alone, and no quantitative features. Models were externally validated on a diverse cohort of 970 patients for accuracy in ODX prediction and recurrence, with longitudinal follow-up spanning more than 10 years. When comparing the area under the receiver operating characteristic curve (AUROC) in a held-out test set from NCDB, models incorporating quantitative ER/PR (AUROC 0.78, 95% CI 0.77–0.80) and quantitative ER/PR/Ki-67 (AUROC 0.81, 95% CI 0.80–0.83) both performed better than the non-quantitative model (AUROC 0.70, 95% CI 0.68–0.72). These results were preserved in the validation cohort, where the quantitative ER/PR/Ki-67 model (AUROC 0.87, 95% CI 0.81–0.93) outperformed the non-quantitative model (AUROC 0.80, 95% CI 0.73–0.87, p = 0.009). Using a high sensitivity rule-out threshold, the quantitative ER/PR and ER/PR/Ki-67 models identified 30% and 43% of patients as likely having low ODX. Of these low-risk patients, recurrence was <3% at 5 years, and no patient who recurred had a high ODX score. These models may be useful to identify patients who can forgo genomic testing and proceed with endocrine therapy alone, and an online calculator is provided to facilitate further study.},
	language = {en},
	author = {Dhungana, Asim and Vannier, Augustin and Zhao, Fangyuan and Freeman, Jincong Q. and Saha, Poornima and Sullivan, Megan and Yao, Katherine and Elbio, Flores M. and Olopade, Olufunmilayo I. and Pearson, Alexander T. and Huo, Dezheng and Howard, Frederick M.},
}

```

## Installation
This github repository should be downloaded to a project directory. Installation takes < 5 minutes on a standard desktop computer. Runtime for hyperparameter optimization / model selection is approximately 48 hours. Runtime for model fitting in the training dataset for the optimal model and computation of performance characteristics in the held out test set / external dataset is approximately 20 minutes. All software was tested on Ubunutu 22.04 with an AMD Ryzen 9 5900X 12-Core Processor.

Requirements:
* python 3.10.6
* xgboost 1.5.0
* pandas 1.4.4
* numpy 1.24.3
* lifelines 0.27.0
* tableone 0.7.12
* sklearn 1.2.1
* statsmodels 0.13.5
* scipy 1.10.1
* openpyxl 3.0.10
* seaborn 0.12.1

## Replication of Results
The primary results of our study can be replicated by running the cells within the RSNCDB-main.ipynb notebook file. The NCDB dataset should be downloaded, and the appropriate file location of the dataset should be specified in the "Loading the NCDB File" of the notebook. Subsequent section of the notebooks describe our process for model building and validation:

* Minimal Feature Set - graphs variables based on availability in NCDB and univariate predictive accuracy to identify candidate features for the study
* Model Training - selects appropriate patients from NCDB, splits the dataset into training / testing cohorts, and performs sequential forward feature selection in the training cohort with the specified model to identify features for inclusion. 
* ROC Analyses - contains the code for generating receiver operating characteristic curves within NCDB (under NCDB Model Assessment header) and the external University of Chicago Datasets (UCMC Model Validation header). Also contains subgroup analyses (Race Subgroup Analyses, Histologic Subgroup Analyses and Node Subgroup Analyses headers). 
* Compiling Results - reformats the results dataframe to enable printing results in a readable format
* Generating Baseline Demographics - prints baseline demogrpahics tables for the respective cohorts
* Manuscript Figures - generates the figures in the accompanying manuscript
* Tables - generates the tables in the accompanying manuscript
* Pickles for Calculator - pickles the trained models for use in an online calculator
* Gridsearch Results - prints a table of results of a gridsearch for optimal model / hyperparameters

The code to conduct a gridsearch for optimal model is in the RSNCDB-explore_models.py file.
