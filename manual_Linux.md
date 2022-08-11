
# **PIn test Manual**

---

## Usage

```
 python [path of main.py] --cfg [path of configuration file]
```

In the package of PIn test, there are two files that needs attention

<u>**main.py**</u> and **<u>config.yaml</u>**

#### main.py

the the main file for the software to run

#### **config.yaml**

the configuration file, which users could edit the parameters to achieve different functions.

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
  Default is 0.01. *Set p.input 1 for exhaustive pairwise calculation.*
  
- **p_output**
  
  A p-value threshold for filtering the output of mode 1.
  
  When specified, only results with p-values smaller than the *p.output* will be listed in the output file.
  Default is 0.01. *Set p.output 1 for listing all the results.
  
- **P_LINK**
  
  *True* or *False*
  
  If set to *True*, read data from .raw file, otherwise read from isolated geno and pheno data
  
- **P_LINK_FN**
  
  Valid only when **P_LINK** is *True*
  
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
    
  2. SNP2 - the second SNP names of a pair
    
  3. stat - Statistics of the PIn test
    
  4. df - degree of freedoms used for calculating p-value
    
  5. p - p-value of interaction testing
    
- HWE file
  
  A file names as [NAME].hwe contains the p-value of HWE test of all the input SNPs
  
- Deletion File
  
  Two deletion files will be generated.
  
  A file named [NAME].del1 contains *SNPs* excluded during the embedded quality control process.
  
  A file named [NAME].del contains *SNP pairs* excluded during the embedded quality control process.
  
- Chisquare test file
  
  A file named [NAME].chisq will be generated for mode 1, which contains chi-squared test results of main effect associations.
  

### Log File

To allow for replication and problem tracking, a log file named *[Name].log* is generated for each run, which contain the all the commands used for the analysis and information regarding filtering etc.

### Examples

> In the folder of packages

```
 python main.py --cfg config.yaml
```
