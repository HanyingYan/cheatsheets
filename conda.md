## 1. Background
Conda is an ***open-source, cross-platform, language-agnostic*** **package manager and environment management system**. <br/>
It was originally developed to solve difficult package management challenges faced by ***Python*** data scientists, and today is a popular package manager for ***Python and R***.

Note that ```conda``` is a ***python package***, not a binrary command. So to make conda work, you have to create a Python environment and install package ```conda``` into it. This is where ***Anaconda installer*** and ***Miniconda installer*** comes in.
* ```Miniconda installer = Python + package conda```
* ```Anaconda installer = Python + package conda + meta package anaconda```<br/>
And hence Anaconda installer = Miniconda installer + conda install anaconda

## 2. Commands
  1. Create an environment<br/>
  ```conda create --name <env_name> python=3.9``` (or whatever Python or R version you need)
  2. List all available envs<br/>
  ```conda env list``` or
  ```conda info --envs```<br/>
  3. Activate an environment<br/>
  ```conda activate <env_name>```
  4. Deactivate current environment<br/>
  ```conda deactivate```
  5. If pip doesn't work using conda to install<br/>
  ```conda install pip```
  6. Install a project dependency (listed in ```requirements.txt``` file)<br/>
  ```conda install --file requirements.txt``` or
  ```pip install -r requirements.txt```
  7. Delete an existing environment<br/>
  ```conda env remove -n <env_name>```
  8. Update conda itself<br/>
  ```conda update conda```
  9. Update all packages in the current environment<br/>
  ```conda update --all```
  10. Update all packages in another env<br/>
  ```conda update -n <env_name> --all```
  11. List installed packages in current environment<br/>
  ```conda list``` or ```conda list <package_name>``` for specific ones
  12. Check conda channels<br/>
  ```conda config --show channels```
  13. Add a channel such as ```conda-forge``` to the top of the channels configuration list with the highest priority<br/>
  ```conda config --add channels <channel_name>```
  14. Add a channel to the end of the channels configuration list with the lowest priority<br/>
  ```conda config --append channels <channel_name>```
  15. Remove a channel<br/>
  ```conda config --remove channels <channel_name>```
  16. Create an environment file from your current environment.<br/>
  ```conda env export --from-history > environment.yml```
  17. Create a new environment and install dependencies listed in YML file.<br/>
  ```conda env create -f environment.yml```
  
## 3. Channels
Anaconda Inc., the main developers of the conda software, also maintain a separate channel of packages, which is the ***default*** when you type ```conda install <package_name>``` without changing any options.

However, ```conda-forge``` is an additional channel and there are several main reasons to use it instead of the ```defaults``` channel maintained by Anaconda. 
* Packages on ```conda-forge``` may be more *up-to-date* than those on the ```defaults``` channel
* There are packages on the ```conda-forge``` channel that aren't available from ```defaults```
* You would prefer to use a dependency such as ```openblas``` (from ```conda-forge```) instead of ```mkl``` (from ```defaults```).
* If you are installing a package that requires a compiled library (e.g., a C extension or a wrapper around a C library), it may reduce the chance of incompatibilities if you install all of the packages in an environment from a single channel due to binary compatibility of the base C library
