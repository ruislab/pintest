# PIntest Installation

> For Windows System

### 1. Intallation of Python

Download Python installation package via website

<div>
https://www.python.org/ftp/python/3.7.9/python-3.7.9-amd64.exe
</div>

After downloading the package, open the exe file

select **Customize installation**.

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-42-46-image.png?msec=1658395405482)

Select the following Optional Features, especially the **pip**

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-45-16-image.png?msec=1658395405484)Click Next and In the <u>Advanced Options</u> select **Download debug binaries**.

Choose install location as **C:\python**

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-43-22-image.png?msec=1658395405484)

**<u>After installation of python finished, we need to set up the environment variables.</u>**

### 2. Enviroment Variable Set Up

Open<u> File Explorer</u>, Right click <u>This PC</u>, select **<u>Properties</u>**

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-56-07-image.png?msec=1658395405473)

Scroll down, in the Related Settings filed, select **<u><mark>Advanced system settings</mark></u>**

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-58-02-image.png?msec=1658395405472)

Select **<u><mark>Environment Variables</mark></u>**

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-16-59-29-image.png?msec=1658395405472)

In the **System Variables**, <u>double clicked</u> the <u><mark>**Path** </mark></u>

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-04-30-image.png?msec=1658395405473)

Add two new PATHs and Save the changes

> ```
> C:\python
> C:\python\Scripts
> ```

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-04-53-image.png?msec=1658395405473)

Back to the System Variables, add new variable by clicking the **New** button.

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-06-05-image.png?msec=1658395405474)

New variable name as **PYTHONHOME** and Variable value as **C:\PYTHON**, and click OK

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-07-30-image.png?msec=1658395405474)

### 3. Installation of dependent libraries

Enter cmd in the current directory path and press "Enter" key on the keyboard,

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-17-43-image.png?msec=1658395405475)

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

![](file:///C:/Users/dell/AppData/Roaming/marktext/images/2022-07-20-17-25-41-image.png?msec=1658395405474)

#### **Now, you can use PIntest for analysis!**
