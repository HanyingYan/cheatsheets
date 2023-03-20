## 1. Python, Ipython and Jupyter Notebook
**Python**: a general-purpose ***programming language***.
  * The most common way to use Python is to write scripts, files with the ```.py``` extension.
  * A python script contains a list of commands to execute in order. It runs from start to finish and display some output. 

**IPython**: an ***interactive command line interface*** to python where you generally write one command at a time and get the results instantly.

**Jupyter Notebook**<br/>
* In 2011, IPython introduced a new tool named the ```Notebook```, which offers a modern and powerful ***web interface*** to Python. 
  * It offers a more convenient *text editor*, the possibility to write rich text, and improved graphical capabilities. 
  * Also, since it is a web interface, it can integrate many of the existing *web libraries* for data visualization, including plotly.js.
* In 2015, the IPython developers made a major code reorganization of their ever-growing project. The Notebook is now called the **Jupyter Notebook**. 
  * This interface can be used not only with Python but with dozens of other languages such as **R** and **Julia**. 
  * IPython is now the name of the Python backend (aka  ```kernel```).


## 2. Conda and Kernel
**Kernels** are programming language-specific processes that run independently and interact with the Jupyter notebook. 

**ipykernel** is the wrapper around IPython which enables using IPython as a kernel, providing a robust environment for interactive computing in Python.

Kernels are configured by specifying the interpreter and a name and some other parameters, and configuration can be stored system-wide, for the active environment (or virtualenv) or per user. 

There are three options how to use a conda environment and Jupyter.
* **Option 1: Run Jupyter server and kernel inside the conda environment**
  ```
  conda create -n <env_name>            # creates new virtual env
  conda activate <env_name>             # activate environment in terminal
  conda install jupyter                 # install jupyter + notebook
  jupyter notebook                      # start server + kernel inside my-conda-env
  ```
  * Jupyter will be completely installed in the conda environment. 
  * Different versions of Jupyter can be used for different conda environments, but this option might be a bit of overkill.
  
* **Option 2: Create a special kernel for the conda environment**
  ```
  conda create -n <env_name>                                 # creates new virtual env
  conda activate <env_name>                                  # activate environment in terminal
  conda install ipykernel                                    # install Python kernel in new conda env
  ipython kernel install --user --name=<kernel_name>         # configure Jupyter to use Python kernel
  ```
  Then run jupyter from the system installation or a different conda environment:
  ```
  conda deactivate              # this step can be omitted by using a different terminal window than before
  conda install jupyter         # optional, might be installed already in system
  jupyter notebook              # run jupyter from system
  ```
  * Only the Python kernel will be run inside the conda environment
  * Jupyter from system or a different conda environment will be used - it is not installed in the conda environment. 
  * By calling ```ipython kernel install``` the jupyter is configured to use the conda environment as kernel.

* **Option 3: Use [nb_conda_kernels](https://github.com/Anaconda-Platform/nb_conda_kernels) to use a kernel in the conda environment**
  ```      
  conda install -n <notebook_env> nb_conda_kernels  # this could be base or some other environment
  conda create -n <python_env>                      # this is the environment for your project and code, it can be <notebook_env> or any other envs.
  conda install ipykernel                           # To utilize an python environment, install ipykernel
  conda install -n <r_env> r-irkernel               # To utilize an R environment, it must have the r-irkernel package; e.g.
  jupyter notebook
  ```
  * You should be able to choose the Kernel ```Python [conda env:my-conda-env]```. 
  * Note that ```nb_conda_kernels``` is only available via ```conda```, not ```pip```
  
  ## 3. My Setups
  ```
  conda activate base
  conda install -c conda-forge nb_conda_kernels               
  conda create -n cheatsheet python=3.9                       
  conda install -n cheatsheet ipykernel                       # To utilize an python environment, install ipykernel
  
  conda install -c conda-forge jupyter_contrib_nbextensions   # I also install jupyter_contrib_nbextensions
  jupyter nbextension enable codefolding/main
  jupyter nbextension enable collapsible_headings/main  
  jupyter notebook
  ```
  * Check [here](./conda.md#3-channels) to see why we use channel ```conda-forge```.
  * Now if we open [```python_and_pandas_basics.ipynb```](./python_and_pandas_basics.ipynb), we will be able to change the kernel to ```Python [conda env:cheatsheet]```
  * I also include [```jupyter_contrib_nbextensions```](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/install.html) to use extensions.
  * I also enable the extension to collapse the headings and fold the codes.
  
  
