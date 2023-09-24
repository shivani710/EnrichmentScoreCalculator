# EnrichmentScoreCalculator


This project contains a Python script used to calculate enrichment scores for genes based on five different datasets. The enrichment scores represent the significance of the genes across different biological conditions or contexts.

## Table of Contents

1. [Dependencies](#dependencies)
2. [Datasets](#datasets)
3. [How to Run](#how-to-run)
4. [Code Documentation](#code-documentation)
   - [Importing Modules](#importing-modules)
   - [Setting Base Directory](#setting-base-directory)
   - [Reading Datasets](#reading-datasets)
   - [Data Processing](#data-processing)
   - [Finding Common Gene-Pathway Pairs](#finding-common-gene-pathway-pairs)
   - [Score Calculation](#score-calculation)
   - [Saving the Results](#saving-the-results)
5. [Output](#output)
6. [Final Remarks](#final-remarks)

## Dependencies <a name="dependencies"></a>
The following Python libraries are required:

```shell
pandas
gseapy
matplotlib
os
numpy
seaborn
scipy
sys
```

## Datasets <a name="datasets"></a>
The datasets utilized in this project are significant enrichment files with FDR <= 0.05, including:
1. **Compendium**
2. **Embryo Development**
3. **Post-embryonic Development**
4. **Cell Types**
5. **Tissues**

Each dataset needs to be pre-processed and stored in CSV format.

## How to Run <a name="how-to-run"></a>
1. Ensure all [dependencies](#dependencies) are installed.
2. Place the datasets in appropriate paths.
3. Run the Python script.

## Code Documentation <a name="code-documentation"></a>

### Importing Modules <a name="importing-modules"></a>
Import the necessary modules required for reading datasets, performing computations, and plotting.

```python
import pandas as pd
import gseapy as gp
import matplotlib.pyplot as plt
import os
import numpy as np
import seaborn as sns
from scipy import stats as st
```

### Setting Base Directory <a name="setting-base-directory"></a>
Establish the base directory containing the datasets.

```python
Base_dir='/data/nandas/AllDatasets'
os.chdir(Base_dir)
```

### Reading Datasets <a name="reading-datasets"></a>
Load the CSV datasets into Pandas DataFrames.

```python
Compendium=pd.read_csv("Path to Compendium Dataset", index_col=0)
EmbDev=pd.read_csv("Path to Embryo Development Dataset", index_col=0)
...
```

### Data Processing <a name="data-processing"></a>
Pre-process the DataFrames for calculating common gene-pathway pairs.

```python
Compendium.reset_index(inplace=True)
Compendium.set_index(['WormBase','Term'],inplace=True)
...
```

### Finding Common Gene-Pathway Pairs <a name="finding-common-gene-pathway-pairs"></a>
Identify the common gene-pathway pairs across all datasets.

```python
compemb=list(set(Compendium.index).intersection(set(EmbDev.index)))
...
Score['score']=float(-2)
...
```

### Score Calculation <a name="score-calculation"></a>
Compute the enrichment scores for each gene-pathway pair.

```python
for genepathway in Score.index:
    count=0
    if genepathway in Compendium.index:
        count=count+1
    ...
    Score.loc[genepathway,'score']=count
```

### Saving the Results <a name="saving-the-results"></a>
Save the calculated scores to a CSV file.

```python
Score.to_csv("EnrichmentScoreAllDatasetsGeneID_052223.csv")
```

## Output <a name="output"></a>
The result is a CSV file containing the enrichment scores for all gene-pathway pairs derived from the analysis of the datasets.

## Final Remarks <a name="final-remarks"></a>
Ensure to adapt the file paths and names according to your local environment and dataset locations. A detailed description of each dataset, its format, and any prerequisite processing steps should be outlined. Any potential enhancements or improvements for the script can be addressed subsequently, and contributions for refining the script are welcomed.

For any issues, questions, or suggestions, please use the repository's issue tracker or submit a pull request.
