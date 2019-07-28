---
layout: post
title: "Install Tensorflow (CPU) in PyCharm in Windows"
modified:
categories: blog
excerpt:
tags: [Windows, PyCharm, Tensorflow, Python]
image:
  feature: google/tensorflow-pycharm.jpg
date: 2018-10-17
comments: true
share: true
---

This blog shows how to install **tensorflow** for python in Windows 10, preferably in PyCharm. **Tensorflow** can be installed either with separate python installer or Anaconda open source distribution. 

<!--more-->

## Major steps

1. Download PyCharm Community Edition from [JetBrain official website](https://www.jetbrains.com/pycharm/download/#section=windows) and install it in Windows 10.

2. Download and install Anaconda from [here](https://www.anaconda.com/download/#windows). Choose whatever python version you use.

3. Open PyCharm, click *Create New Project*, give the folder a name (ex. `tensorflow-test`) in *Location*, select *New environment using Virtualenv* and choose *Base interpreter* as python.exe in Anaconda3 folder. Click OK to continue.

![Create new virtual environment](/eric-blogs/images/pycharm/create-project-conda.png)

4. (**alternative of 3**) Open PyCharm, click *Create New Project*, give the folder a name in *Location*, select *Existing interpreter*. If none is shown in the *Interpreter*, click "..." and in *Add Python Interpreter* dialog, choose native python.exe. Click OK to go back and then create.

![Use existing python interpreter](/eric-blogs/images/pycharm/create-project-native.png)

![If no interpreter, click ... to add one](/eric-blogs/images/pycharm/add-exist-python-interpreter.png)

5. Go to File -> Settings, search for *Porject Interpreter*, ensure that corresponding python version is used as the interpreter. Then install the python packages you need to install by clicking "+" on top right, such as `numpy, matplotlib, pandas, python-opencv` etc.

6. To install `tensorflow`, use pip. Click *Start* in Windows (bottom left of your screen), type *Anaconda Prompt* and open the command window. Type in *activate tensorflow-test* to activate your virtual environment in Anaconda. Then type `pip install tensorflow` to install tensorflow.

7. (**alternative of 6**) Open Windows system command prompt (cmd), type following commands to verify that you are installing on correct python versions. Then type in `pip install tensorflow` to install newest tensorflow package. You can also install a previous version using `pip install tensorflow=1.10.0`, for example.

  Make sure python version and pip versions are the same. Use `python --version` and `pip --version` to get the versions.

8. To test whether your installation works, create a python file named `test.py`. Copy the following python scripts in `test.py` and execute it in PyCharm. If it outputs the current tensorflow version, it means that **tensorflow** is successfully installed.

	`import tensorflow as tf`
	`print(tf.__version__)`

![Create a new python file](/eric-blogs/images/pycharm/create-new-python-file.png)


## Common issues

### Choosing default python version to run:

  * Sometimes you might have multiple versions of python installed. You can configure which one to use by running the following:
	`sudo update-alternatives --config python`

  * it might give an error:
	`update-alternatives: error: no alternatives for python3`
  
  * You need to update your update-alternatives , then you will be able to set your default python version. Now you can run the following to setup that:
	`sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1`
	`sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2`


  * now you choose your favoriate python version as default:
	`sudo update-alternatives --config python`
	
  * or use the following command to set python3.6 as default:
	`sudo update-alternatives  --set python /usr/bin/python3.6`

### **"ImportError: DLL load failed: A dynamic link library (DLL) initialization routine failed."**

  * **Reason**: Some old CPUs (typically for CPUs before 2011) do not support AVX type instruction set extension, so you need to check whether your machine support AVX/AVX2 before installing pre-complied tensorflow wheel file.
  * **Solution**: If you indeed have older CPUs, you can still make it work by installing tensorflow compiled compatible with other instruction set extensions, such as `SSE2`. Please download specific version of tensorflow from [here](https://github.com/ericzhng/tensorflow-windows-wheel/tree/master/1.11.0/py36/CPU).
  * Another **option** you can go is to build tensorflow from source. For details, please refer to [3](#reference).
  * Here is a **list of CPUs compatible** with AVX instructions set extensions:https://en.wikipedia.org/wiki/Advanced_Vector_Extensions#CPUs_with_AVX

### **"tensorflow-*.whl is not supported wheel on this platform"**

  * **Reason**: Currently tensorflow is only supported up to Python 36. While newest Anaconda comes with Python 37 package.
  * **Solution**: You can go to File -> Settings, create a new virtual conda environment, and select Python 36. Then install tensorflow either from repository or downloaded file.

![Add Python Interpreter](/eric-blogs/images/pycharm/create-conda-envs.png)

## Reference

* 1. [Check SSE/AVX instruction support](https://gist.github.com/hi2p-perim/7855506#file-ssecheck-cpp).
* 2. [Issues of installing tensorflow with DLL error](https://github.com/tensorflow/tensorflow/issues/17761).
* 3. [Build from source on Windows](https://www.tensorflow.org/install/source_windows).
