# **PIn test Installation**

For installation guide, please visit the following link

<div>
https://github.com/ruislab/pintest/blob/main/Installation%20guide.md
</div>

# **PIn test Manual**

---

## Introduction

<u>**P**</u>ure <u>**In**</u>teraction (PIn) test is a non-parametric test for detecting the pure interaction effect without dominant single locus or additive effects in case-control GWAS data. The method is constructed by measuring the genetic structural difference of LD between cases and controls.

For pairwise interaction calculation, the software has 3 modes: (1) calculate the pairwise interaction exhaustively for all SNPs, (2) calculate pairwise interaction between a given SNP set and all SNPs, (3) calculate the pairwise interaction for a list of SNP pairs. The software embeds a quality control step to filter out SNPs that violate the assumptions of this method. For mode 1, the output can be filtered by p-values, such that only SNP pairs with smaller p-value than a threshold (p.output) will be returned.

## Download softwares

| Operating Systems | Link |
| --- | --- |
| Windows 64bit | [V4.1](https://github.com/ruislab/pintest/releases/download/V4.1/PInteste_V4.zip) |
| Linux | coming soon |


## Usage

```
PIntest.exe -gp [genotype data] -pp [phenotype data] -mode [mode] -ep [extra data] -p.hwe [p.hwe] -p.input [p.input] -p.output [p.output] -sort -op [output data]
```

### Input Files

- **-gp**
  
  Genotype data. A data frame containing genotype information in the column. Genotypes should be coded as **(0, 1, 2) or (0, 1)**.  
  | SNP1 | SNP2 | SNP3 | SNP4 | SNP5 | SNP6 | SNP7 | SNP8 | SNP9 | SNP10 | SNP11 | SNP12 |
  | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
  | 0   | 0   | 2   | 0   | 1   | 1   | 1   | 0   | 1   | 0   | 2   | 0   |
  | 1   | 1   | 2   | 1   | 2   | 1   | 0   | 0   | 0   | 0   | 1   | 1   |
  | 1   | 0   | 1   | 2   | 2   | 0   | 0   | 1   | 1   | 0   | 1   | 0   |
  | 2   | 0   | 0   | 1   | 1   | 0   | 0   | 2   | 1   | 2   | 2   | 1   |
  | 1   | 1   | 0   | 0   | 0   | 1   | 1   | 0   | 0   | 1   | 0   | 0   |
  
- **-pp**
  
  Phenotype data. A data frame containing phenotype information in the column. Phenotype should be coded as (0, 1). Length of the phenotype data should be equal to the number of rows of the genotype data.
  
  <p align="center">
  <img title="" src="https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-22-14-59-10-image.png" alt="" data-align="center" width="126">
  </p>
  
-  **-ep**
  
  **Extra file path for mode 2 and mode 3.**
  
  If mode 2 is set, a data frame containing a list of specified SNPs name should be provided as extra data.
  
  <p align="center">
  <img title="" src="https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-22-14-52-32-image.png" alt="" data-align="center" width="134">
  </p>
  
  If mode 3 is set, a data frame containing specified SNP pairs should be provided as extra data.
  provided as extra data.
  
  <p align="center">
  <img title="" src="https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-22-14-51-47-image.png" alt="" data-align="center" width="175">
  </p>

### **Parameters**

- **-mode**
  
  **An integer value of 1, 2, 3.** <u>Default is 1.</u>
  
  -mode 1 for exhaustive pairwise epistasis testing <u>(ALL * ALL)</u>
  
  -mode 2 for epistasis testing in specified SNPs interacting with all markers <u>(SET1 * ALL)</u>
  
  -mode 3 for epistasis testing in specified SNP pairs <u>(SNP1 * SNP2)</u>
  
- **-p.hwe**
  
  P-value threshold of Hardy-Weinberg equilibrium (HWE) test for filtering the genetic markers. Markers that failed the HWE test will be excluded from the testing.
  Default is 0.01
  
- **p.input**
  
  A p-value threshold to select markers for pairwise calculation.
  
  When specified, only markers with main effect p-value from Chi-square test smaller than *p.input* will be passed to the interaction effect calculation. 
  Default is 0.01. *Set p.input 1 for exhaustive pairwise calculation.*
  
- **p.output**
  
  A p-value threshold for filtering the output of mode 1.
  
  When specified, only results with p-values smaller than the *p.output* will be listed in the output file.
  Default is 0.0001. *Set p.output 1 for listing all the results.*
  
- **-sort**
  
  TRUE or FALSE. A parameter for sorting the output in an ascending order based on p-values of PIn test.
  
  Default is TRUE.
  
- **-op**
  
  Output file name. No file name extension needed.
  
  Default name is "OUTPUT".
  

### **Output**

- OUTPUT
  
  A file named [NAME].txt includes the final results of the PIn test.
  
  If -sort was specified as TRUE, the results will be ordered based on p-value. The files contains the following fields
  
  1. SNP1 - the first SNP name of a pair
    
  2. SNP2 - the second SNP names of a pair
    
  3. stat - Statistics of the PIn test
    
  4. df - degree of freedoms used for calculating p-value
    
  5. p - p-value of interaction testing
    
- HWE file
  
  A file names as [NAME].hwe contains the p-value of HWE test of all the input SNPs
  
- Deletion File
  
  A file named [NAME].del1 contains *SNPs* excluded during the embedded quality control process.

  A file named [NAME].del contains *SNP pairs* excluded during the embedded quality control process.
  
- Chisquare test file
  
  A file named [NAME].chisq will be generated for mode 1, which contains chi-squared test results of main effect associations.
  

### Log File

To allow for replication and problem tracking, a log file named *[Name].log* is generated for each run, which contain the all the commands used for the analysis and information regarding filtering etc.

### Examples

> For example, our software was stored in E disk PIntest folder (E:\PIntest) as well as all the input files

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt
```

This will process mode 1 (exhaustive pairwise epistasis testing) and SNPs are filtered using main effect p-value < 0.01, and HWE > 0.01, and the output will be filtered using interaction p-value < 0.0001 in the default setting.

The final results would be

  
| SNP1  | SNP2  | stat    | df  | p        |
|:-----:|:-----:|:-------:|:---:|:--------:|
| SNP73 | SNP78 | 42.0294 | 6   | 1.81E-07 |
| SNP63 | SNP78 | 25.5566 | 3   | 1.18E-05 |
| SNP54 | SNP73 | 24.3812 | 3   | 2.08E-05 |
| SNP48 | SNP78 | 26.8461 | 4   | 2.14E-05 |
| SNP38 | SNP78 | 23.9462 | 3   | 2.56E-05 |
| SNP33 | SNP78 | 30.9649 | 6   | 2.57E-05 |
| SNP74 | SNP78 | 30.8585 | 6   | 2.70E-05 |
| SNP70 | SNP78 | 30.6097 | 6   | 3.01E-05 |
| SNP33 | SNP73 | 28.9338 | 6   | 6.26E-05 |
| SNP78 | SNP81 | 28.6709 | 6   | 7.02E-05 |
| SNP68 | SNP78 | 28.369  | 6   | 8.01E-05 |
| SNP4  | SNP73 | 28.2112 | 6   | 8.57E-05 |
| SNP54 | SNP78 | 21.4248 | 3   | 8.59E-05 |
| SNP4  | SNP78 | 25.784  | 5   | 9.83E-05 |
  

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt --ep E:\PIntest\subset.txt -mode 2
```

This will process mode 2 epistasis testing in specified SNPs (SNPs in the subset.txt file) interacting with all markers.

The final results would be

| SNP1 | SNP2 | stat | df  | p   |
| --- | --- | --- | --- | --- |
| SNP38 | SNP57 | 34.221 | 6   | 6.10E-06 |
| SNP38 | SNP4 | 24.5274 | 3   | 1.94E-05 |
| SNP46 | SNP57 | 28.8015 | 5   | 2.54E-05 |
| SNP8 | SNP57 | 27.5407 | 5   | 4.47E-05 |
| SNP38 | SNP69 | 22.565 | 3   | 4.98E-05 |
| SNP38 | SNP47 | 28.6395 | 6   | 7.12E-05 |
| SNP106 | SNP57 | 23.645 | 4   | 9.41E-05 |

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt --ep E:\PIntest\pairs.txt -mode 3
```

This will process mode 3 epistasis testing in specified SNP pairs (snp pairs in the pairs.txt file)

The final results would be

| SNP1 | SNP2 | stat | df  | p   |
| --- | --- | --- | --- | --- |
| SNP44 | SNP81 | 9.03227 | 2   | 1.09E-02 |
| SNP96 | SNP17 | 8.27003 | 2   | 1.60E-02 |
| SNP102 | SNP96 | 10.8958 | 4   | 2.78E-02 |
| SNP40 | SNP84 | 3.98812 | 1   | 4.58E-02 |
| SNP56 | SNP20 | 6.00808 | 2   | 4.96E-02 |
| SNP36 | SNP32 | 7.07911 | 3   | 6.94E-02 |
| SNP84 | SNP71 | 5.05871 | 2   | 7.97E-02 |
| SNP32 | SNP76 | 5.49955 | 3   | 1.39E-01 |
| SNP31 | SNP37 | 8.02078 | 6   | 2.37E-01 |
| SNP108 | SNP16 | 2.78324 | 2   | 2.49E-01 |
| SNP19 | SNP74 | 4.86663 | 5   | 4.32E-01 |
| SNP18 | SNP55 | 2.66299 | 3   | 4.47E-01 |
| SNP73 | SNP25 | 1.60111 | 2   | 4.49E-01 |
| SNP64 | SNP67 | 1.96964 | 3   | 5.79E-01 |
| SNP93 | SNP80 | 3.48862 | 5   | 0.625111 |
| SNP103 | SNP97 | 3.15864 | 5   | 0.675544 |
| SNP86 | SNP92 | 0.991538 | 3   | 0.8033 |
| SNP55 | SNP9 | 1.2591 | 4   | 0.868275 |
| SNP59 | SNP69 | 0.345499 | 3   | 0.951256 |
