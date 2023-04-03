# PIntest Installation

Download software

| Operating Systems | Link |
| --- | --- |
| Windows 64bit | [V1.0](https://github.com/ruislab/pintest/releases/latest/download/PInteste_V1.0.zip) |
| Linux | [V1.0](https://github.com/ruislab/pintest/releases/latest/download/PIntest_linux_V1.1.zip) |

# For Windows Users:
## Set up

### 1. Intallation of Python

Download Python installation package via website

<div>
https://www.python.org/ftp/python/3.7.9/python-3.7.9-amd64.exe
</div>

After downloading the package, open the exe file
select **Customize installation**.

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-42-46-image.png)

<br/><br/>
Select the following Optional Features, especially the **pip**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-44-05-image.png)

Click Next and In the <u>Advanced Options</u> select **Download debug binaries**.

<br/><br/>
Choose install location as **C:\python**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-27-16-43-22-image.png)

<br/><br/>
**<u>After installation of python finished, we need to set up the environment variables.</u>**
<br/><br/>

### 2. Environment Variable Set Up

Open<u> File Explorer</u>, Right click <u>This PC</u>, select **<u>Properties</u>**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-56-07-image.png)
<br/><br/>
In the Related Settings filed, select **<u><mark>Advanced system settings</mark></u>**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-58-02-image.png)
<br/><br/>
Select **<u><mark>Environment Variables</mark></u>**
<br/><br/>
![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-59-29-image.png)
<br/><br/>
In the **System Variables**, <u>double clicked</u> the <u><mark>**Path** </mark></u>
<br/><br/>
![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-04-30-image.png)

<br/><br/>
Add two new PATHs and Save the changes

> ```
> C:\python
> C:\python\Scripts
> ```

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-04-53-image.png)

Back to the System Variables, add new variable by clicking the **New** button.

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-06-05-image.png)
<br/><br/>
New variable name as **PYTHONHOME** and Variable value as **C:\PYTHON**, and click OK

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-27-17-07-30-image.png)

### 3. Installation of dependent libraries

Enter cmd in the current directory path and press "Enter" key on the keyboard,

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-17-43-image.png)

Input the following commands:

```
pip install scipy
```

> Sometimes, due to network fluctuation or limited internet speed, errors may happen during installation. If terms such as "*socket. timeout* ", appeared in the error message, could use **pip --timeout=100 install scipy** as command.

After installation, input command

```
pip install pybind11
```

All of the dependencies have been installed.

### 4. Testing software running

In the folder where PIntest.exe is located, enter cmd, input command

```
PIntest.exe 
```

If the following appears, the software has been installed successfully!

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-25-41-image.png)

#### **Now, you can use PIntest for analysis!**

# For Linux users:

The Linux version of PIn test requires installation of **virtualenv or conda** before use:

Download site for virtualenv:

<div>
https://virtualenv.pypa.io/en/latest/installation.html
</div>

Download site for conda:

<div>
https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html
</div>

Running the following commands using virtualenv or conda

```
 pip install -r requirements.txt
```

If warning appears such as

> ERROR: Could not find a version that satisfies the requirement yaml~=0.2.5 (from versions: none)
> ERROR: No matching distribution found for yaml~=0.2.5

Then, run the following and do not need to re-run the last step

```
    pip install yacs
```

Now, you should be able to use the PIn test Linux version successfully!
