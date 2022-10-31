# **PIn test Installation**

PIn test depends on <u>python and other dependencies</u>, **we strongly recommend users to read through <u><mark>installation guide</mark></u> before using it!**

For installation guide, please visit the following link:

<div>
https://github.com/ruislab/pintest/blob/main/Installation_guide.md
</div>

# **PIn test Manual**

---

## Introduction

<u>**P**</u>ure <u>**In**</u>teraction (PIn) test is a non-parametric test for detecting the pure interaction effect without dominant single locus or additive effects in case-control GWAS data. The method is constructed by measuring the genetic structural difference of LD between cases and controls.

For pairwise interaction calculation, the software has 3 modes: (1) calculate the pairwise interaction exhaustively for all SNPs, (2) calculate pairwise interaction between a given SNP set and all SNPs, (3) calculate the pairwise interaction for a list of SNP pairs. The software embeds a quality control step to filter out SNPs that violate the assumptions of this method. For mode 1, the output can be filtered by p-values, such that only SNP pairs with smaller p-value than a threshold (p.output) will be returned.

Only Linux version supports input files in PLINK binary files format

## Windows system Usage

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
  
  **Extra data for mode 2 and mode 3.**
  No header needed for extra data.
  
  If mode 2 is set, a data frame containing a list of specified SNPs name should be provided as extra data.
  
  If mode 3 is set, a data frame containing specified SNP pairs should be provided as extra data.
  provided as extra data.


### **Parameters**

- **-mode**
  
  **An integer value of 1, 2, 3.** <u>Default is 1.</u>
  
  -mode 1 for exhaustive pairwise epistasis testing <u>(ALL * ALL)</u>
  
  -mode 2 for epistasis testing in specified SNPs interacting with all markers <u>(SET1 * ALL)</u>
  
  -mode 3 for epistasis testing in specified SNP pairs <u>(SNP1 * SNP2)</u>
  
- **-p.hwe**
  
  P-value threshold of Hardy-Weinberg equilibrium (HWE) test for filtering the genetic markers. Markers that failed the HWE test will be excluded from the testing.
  Default is 0.01
  
- **-p.input**
  
  A p-value threshold to select markers for pairwise calculation.
  
  When specified, only markers with main effect p-value from Chi-square test smaller than *p.input* will be passed to the interaction effect calculation. 
  Default is 0.01. *Set p.input 1 for exhaustive pairwise calculation.*
  
- **-p.output**
  
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
    
  2. SNP2 - the second SNP name of a pair
    
  3. stat - Statistics of the PIn test
    
  4. df - degree of freedom used for calculating p-value
    
  5. p - p-value of interaction testing
    
- HWE file
  
  A file named [NAME].hwe contains the p-value of HWE test of all the input SNPs
  
- Deletion File
  
  A file named [NAME].del1 contains *SNPs* excluded during the embedded quality control process.

  A file named [NAME].del contains *SNP pairs* excluded during the embedded quality control process.
  
- Chisquare test file
  
  A file named [NAME].chisq will be generated for mode 1, which contains chi-squared test results of main effect associations.
  

### Log File

To allow for replication and problem tracking, a log file named *[Name].log* is generated for each run, which contains all the commands used for the analysis and information regarding filtering etc.

### Examples

> For example, our software was stored in E disk PIntest folder (E:\PIntest) as well as all the input files

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt
```

This will process mode 1 (exhaustive pairwise epistasis testing) and SNPs are filtered using main effect p-value < 0.01, and HWE > 0.01, and the output will be filtered using interaction p-value < 0.0001 in the default setting.

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt --ep E:\PIntest\subset.txt -mode 2
```

This will process mode 2 epistasis testing in specified SNPs (SNPs in the subset.txt file) interacting with all markers.

```
PIntest.exe -gp E:\PIntest\example_genotype.txt -pp E:\PIntest\example_phenotype.txt --ep E:\PIntest\pairs.txt -mode 3
```

This will process mode 3 epistasis testing in specified SNP pairs (SNP pairs in the pairs.txt file)



## Linux system usage

```
 python [path of main.py] --cfg [path of configuration file]
```

In the package of PIn test, there are two files that need attention

<u>**main.py**</u> and **<u>config.yaml</u>**

#### main.py

the main file for the software to run

#### **config.yaml**

the configuration file in the *config folder*, which users could edit the parameters to achieve different functions.

### **Parameters**

- **Mode**
  
  **An integer value of 1, 2, 3.** <u>Default is 1.</u>
  
  -mode 1 for exhaustive pairwise epistasis testing <u>(ALL * ALL)</u>
  
   -mode 2 for epistasis testing in specified SNPs interacting with all markers <u>(SET1 *  ALL)</u>
  
  -mode 3 for epistasis testing in specified SNP pairs <u>(SNP1 * SNP2)</u>
  
- **HWE**
  
  P-value threshold of Hardy-Weinberg equilibrium (HWE) test for filtering the genetic markers. Markers that failed the HWE test will be excluded from the testing.
  Default is 0.01
  
- **p_input**
  
  A p-value threshold to select markers for pairwise calculation.
  
  When specified, only markers with main effect p-value from Chi-square test smaller than *p.input* will be passed to the interaction effect calculation. 
  Default is 0.01. *Set p_input **1.0** for exhaustive pairwise calculation.*
  
- **p_output**
  
  A p-value threshold for filtering the output of mode 1.
  
  When specified, only results with p-values smaller than the *p.output* will be listed in the output file.
  Default is 0.01. *Set p_output **1.0** for listing all the results.
  
- **P_LINK**
  
  *True* or *False*
  
  If set to *True*, Pintest will read data from the **PLINK binary format file**, otherwise read from isolated geno and pheno data based on *GENO_FN and PHENO_FN*
  
- **P_LINK_FN**
  
  If **P_LINK** is *True*, input target dataset in <u>PLINK binary format</u> : **.bed**, **.bim**, and a **.fam** file - where bed contains the compressed genotype 
  data, bim contains the SNP information and fam contains the family information.

  The **.bed** ,**.bim** , and **.fam**file must have the same prefix.
  
- **GENO_FN**
  
  Genotype data.
  
  A data frame containing genotype information in the column. Genotypes should be coded as **(0, 1, 2) or (0, 1)**.
  
- **PHENO_FN**
  
  Phenotype data.
  
  A data frame containing phenotype information in the column. Phenotype should be coded as (0, 1). Length of the phenotype data should be equal to the number of rows of the genotype data.
  
-  **EXTRA_FN**
  
  **Extra file path for mode 2 and mode 3.**
  
  If mode 2 is set, a data frame containing a list of specified SNPs name should be provided as extra data.
  
  If mode 3 is set, a data frame containing specified SNP pairs should be provided as extra data.
  
- **sort**
  
  TRUE or FALSE. A parameter for sorting the output in an ascending order based on p-values of PIn test.
  
  Default is TRUE.
  
- **OUTPUT_NAME**
  
  Output filename
  
  Default is "OUTPUT"
  
- **OUTPUT_DIR**
  
  The folder for logs and output files.
  
  If it does not exist, it will be created automatically.
  

### **Output**

- OUTPUT
  
  A file named [NAME].txt includes the final results of the PIn test.
  
  If -sort was specified as TRUE, the results will be ordered based on p-value. The files contains the following fields
  
  1. SNP1 - the first SNP name of a pair
    
  2. SNP2 - the second SNP name of a pair
    
  3. stat - Statistics of the PIn test
    
  4. df - degree of freedom used for calculating p-value
    
  5. p - p-value of interaction testing
    
- HWE file
  
  A file named [NAME].hwe contains the p-value of HWE test of all the input SNPs
  
- Deletion File
  
  Two deletion files will be generated.
  
  A file named [NAME].del1 contains *SNPs* excluded during the embedded quality control process.
  
  A file named [NAME].del contains *SNP pairs* excluded during the embedded quality control process.
  
- Chisquare test file
  
  A file named [NAME].chisq will be generated for mode 1, which contains chi-squared test results of main effect associations.
  

### Log File

To allow for replication and problem tracking, a log file named *[Name].log* is generated for each run, which contains all the commands used for the analysis and information regarding filtering etc.

### Examples

> In the folder of packages

```
 python main.py --cfg configs/config.yaml
```
