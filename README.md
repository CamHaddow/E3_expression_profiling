# E3_expression_profiling

## Python script aimed at 3 objectives:

## 1. Identify overall tissue distribution of key E3 ubiquitin ligases for PROTAC development
## 2. Identify cell line expression of key E3 ubiquitin ligases for PROTAC development
## 3. Identify the 'best' E3 ubiquitin ligase for a pair of drug targets

# Firstly need to import required packages and then tissue expression data from the human genome atlas:
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import torch

## Importing data in TSV format from protein genome atlas ##

r_filenameTSV = 'https://www.proteinatlas.org/download/rna_tissue_consensus.tsv.zip'
w_filenameTSV = 'https://www.proteinatlas.org/download/rna_tissue_consensus.tsv.zip'
tsv_read_Tissue = pd.read_csv(r_filenameTSV, sep='\t')
print(tsv_read_Tissue.head(10))

# 1. We can then look at the expression of any E3 ligase of our choosing and print these. Initially we will look at those currently enabled with at least moderate affinity (KD < 1 uM) reversibly binding small molecule ligands: "CRBN", "VHL", "BIRC2", "XIAP", "MDM2", "KEAP1", "DCAF1", "DCAF15"

## Review cellular expression profile of E3 ligases prospectively discovered as effectors of degradation: FBXL12, FBXL15, KLHDC2, KLHL6, STUB1, ZER1, PRAME, GID8.
compare_list_expression(["CRBN", "VHL", "BIRC2", "XIAP", "MDM2", "KEAP1", "DCAF1", "DCAF15"] , tsv_read_Tissue)

# 2. We can then repeat the exceriseat the cellular level, importing cellular expression data from the human genome atlas. The same genes can then be investigated and printed:
## Importing data in TSV format from protein genome atlas ##

r_rna_single_cellTSV = 'https://www.proteinatlas.org/download/rna_single_cell_type.tsv.zip'
w_rna_single_cellTSV = 'https://www.proteinatlas.org/download/rna_single_cell_type.tsv.zip'
tsv_read_single_cell = pd.read_csv(r_rna_single_cellTSV, sep='\t')
print(tsv_read_single_cell.head(10))

# We now have both tissue and cellular expression data available to be analysed and with which we will investigate ligases prospectively discovered as effectors of degradation: "FBXL12", "FBXL15", "KLHDC2", "KLHL6", "STUB1", "ZER1", "PRAME", "GID8".

# From these the expression of ligase "KLHL6" appears to have an interesting profile and will be investigated further. 

# 3. The next step is to indentify the 'best' E3 to degrade eiher "TYMS" or "IRAK4" as targets, by selecting ligases which are poorly expressed in cardiomyocytes and highly expressed in the skin respectively. 

# Identifying cardiomyocyte sparing ligases
# Initially we will make a slice of the cell type data for cardiomyocytes then a sub-set of these for all the ligases under investigation: "CRBN", "VHL", "BIRC2", "XIAP", "MDM2", "KEAP1", "DCAF1", "DCAF15", "FBXL12", "FBXL15", "KLHDC2", "KLHL6", "STUB1", "ZER1", "PRAME", "GID8", "RNF4", "RNF114", "RNF126", "FEM1B", "FBXO22", "DCAF16", "DCAF11". 
# Those data can then be graphed and the ligase with minimum cardiomyocyte expression calculated. 
# Expression of "PRAME" was then investigated and give its extremely narrow expression profile a broader search was performed using a threshold of nTPM<5 which could then be visualised. 
# Based upon these data STUB1 offers a broad expression profile while sparing cardiomyocytes and may offer an opportunity for tissue selectivity.

# Identifying ligases highly expressed in the Skin for IRAK4 degradation
# First we need to look at IRAK4 expression, by creating a slice for tussye expression of IRAK4
# Secondly we will create a slice of the skine tissue then a subselcetion of this for or all the ligases under investigation (as the above list).
# Although this cna be done visually, we can use the max function to identify the most highly expressed E3.
# We can also add onto the expression graph the expression level of IRAK4, to identify all the ligases expressed in excess and which may be of greatest use. 
 

