### Installation on Windows
The Windows installation process differs more widely from installation on Linux or MacOSX and has different issues you may run into.

### Process
   * Increase the maximum size of your pagefile to 64G or more (http://www.tomshardware.com/faq/id-2864547/manage-virtual-memory-pagefile-windows.html ) - The Windows memmap interface is sensitive to the maximum setting and leaving it at the default can cause errors when processing larger datasets
   * Remove any associations you may have made between .py files and an existing python interpreter or editor
   * Download and install Anaconda (Python 3.x, not 2.x) <http://docs.continuum.io/anaconda/install>. Allow the installer to modify your PATH variable
   * Use Conda to install git (With "conda install git") - use of another commandline git is acceptable, but may lead to issues depending on default settings
   * Install Visual Studio (Community Edition is fine). <https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017>. You will want the complete desktop install (other major components are not necessary, like mobile development). Click into the details and be sure that the Windows SDK is selected (the most recent version matching your Windows version is fine - you only need/want one). There also may be mention of CLI build tools (for C/C++) under the details window - hopefully these are selected by default but if not, select them too. Follow any instructions you find on the Microsoft website to complete the VC++ install.

Use the following menu item to launch a anaconda-enabled command prompt: start>programs>anaconda3>anaconda prompt
From that prompt. issue the following commands (if you wish to use the dev branch, you may switch branches after the clone):

   ```bash
   git clone https://github.com/flatironinstitute/CaImAn
   cd CaImAn
   conda env create -f environment.yml -n caiman
   ```

   ```bash
   conda activate caiman
   pip install . (OR pip install -e . if you want to develop code)
   copy caimanmanager.py ..
   cd ..
   ```

### Setting up a data directory with caimanmanager

Now that you have stepped out of the caiman source directory, you are ready to make a data directory with code samples and datasets. You will not use the source tree directory any more. 

  ```
  caimanmanager.py install
  ```
  or 
  ```
  python caimanmanager.py install --inplace
  ```
  if you used "pip install -e ." 

This will place that directory under your home directory in a directory called caiman_data. If you have, some of the demos or datafiles may have changed since your last install, to follow API changes. You can check to see if they have by doing `caimanmanager.py check`. If they have not, you may keep using them. If they have, we recommend moving your old caiman data directory out of the way (or just remove them if you have no precious data) and doing a new data install as per above.

If you prefer to manage this information somewhere else, the `CAIMAN_DATA` environment variable can be set to customise it. The caimanmanager tool and other libraries will respect that.

### Setting up environment variables 

To make the package work *efficiently* and eliminate "crosstalk" between different processes, run these commands before launching Python:

   ```bash
   set MKL_NUM_THREADS=1
   set OPENBLAS_NUM_THREADS=1
   set KERAS_BACKEND=tensorflow
   ```   

The commands should be run every time you enter the caiman conda environment. We recommend you save these values inside your environment so you do not have to repeat this process every time. You can do this by following the instructions [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#saving-environment-variables).

