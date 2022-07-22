# PIntest Installation

> For Windows System

Download softwares

| Operating Systems | Link |
| --- | --- |
| Windows 64bit | [V1.0](https://github.com/ruislab/pintest/releases/latest/download/PInteste_V1.0.zip) |
| Linux | coming soon |

## Usage

### 1. Intallation of Python

Download Python installation package via website

<div>
https://www.python.org/ftp/python/3.7.9/python-3.7.9-amd64.exe
</div>

After downloading the package, open the exe file

select **Customize installation**.

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-42-46-image.png)

Select the following Optional Features, especially the **pip**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-44-05-image.png)

Click Next and In the <u>Advanced Options</u> select **Download debug binaries**.

Choose install location as **C:\python**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-43-22-image.png)

**<u>After installation of python finished, we need to set up the environment variables.</u>**

### 2. Environment Variable Set Up

Open<u> File Explorer</u>, Right click <u>This PC</u>, select **<u>Properties</u>**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-56-07-image.png)


Scroll down, in the Related Settings filed, select **<u><mark>Advanced system settings</mark></u>**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-58-02-image.png)


Select **<u><mark>Environment Variables</mark></u>**

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-16-59-29-image.png)


In the **System Variables**, <u>double clicked</u> the <u><mark>**Path** </mark></u>

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-04-30-image.png)

Add two new PATHs and Save the changes

> ```
> C:\python
> C:\python\Scripts
> ```

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-04-53-image.png)

Back to the System Variables, add new variable by clicking the **New** button.

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-06-05-image.png)

New variable name as **PYTHONHOME** and Variable value as **C:\PYTHON**, and click OK

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-07-30-image.png)

### 3. Installation of dependent libraries

Enter cmd in the current directory path and press "Enter" key on the keyboard,

![](https://github.com/ruislab/pintest/blob/main/img_storage/2022-07-20-17-17-43-image.png)

input the following commands

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
