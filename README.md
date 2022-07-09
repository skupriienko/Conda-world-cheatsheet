# Conda cheat sheet

Managing Conda, Miniconda, and Anaconda, Environments, Python, Configuration, Packages. Removing Packages or Environments

## Install Miniconda

### Install locally in a silent mode on linux-64

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh -b -p $HOME/miniconda
``` 

### Install in jupyter notebook on Google Colab

```bash
%%bash
MINICONDA_INSTALLER_SCRIPT=Miniconda3-latest-Linux-x86_64.sh
MINICONDA_PREFIX=/usr/local
wget https://repo.continuum.io/miniconda/$MINICONDA_INSTALLER_SCRIPT
chmod +x $MINICONDA_INSTALLER_SCRIPT
./$MINICONDA_INSTALLER_SCRIPT -b -f -p $MINICONDA_PREFIX
```

#### Install and update conda packages

```bash
%%bash
conda install --channel defaults conda python=3.9 --yes
conda update --channel defaults --all --yes
```

#### Check conda and python version
```bash
!conda --version 
!python --version 
```

## Managing Conda, Miniconda, and Anaconda

`conda --version` Check conda version

`conda info`	 Verify conda is installed, check version

`conda update conda`	Update conda package and environment manager

`conda update anaconda`	Update the anaconda meta package

`conda update --all` Update all packages in the environment

`conda update --all -y` Update all packages in the environment 

## Managing Environments

`conda info --envs` Verify environment you are right now

`conda info -e`	Get a list of all my environmentsActive environment shown with *

`conda create --name snowflakes biopython`

`conda create -n snowflakes biopython`	Create an environment and install program(s)

`conda activate snowflakes`	Activate the new environment to use it

`conda deactivate`	Deactivate the environment

`conda create -n bunnies python=3.9 astroid`	Create a new environment, specify Python version

`conda create -n foo instrain awscli samtools python=3.8` Create a new environment with a set of packages and specific version of Python

`conda create -n flowers --clone snowflakes`	Make exact copy of an environment

`conda remove -n flowers --all`	Delete an environment

`conda env list` List all envs

`conda env export > env.yml`	Save the current Package-specific environment to a file

`conda env export --file env.yml` Saving an entire environment to a file

`conda env export --from-history > env.yml`	Save the current Cross-platform compitible environment to a file

`conda env create -f env.yml`	Load the Package-specific environment from a file

`conda env update -n coolbase --file environment.yml`	install and/or update packages from environment.yml

`conda env remove --name bamqc` Remove Virtual Environment

`CONDA_SUBDIR=osx-arm64 conda create -n test_env --dry-run python=3.8 llvm-openmp cython numpy pip "matplotlib-base>=3.0.3" "protobuf >=3.11.2,<4.0.0" "scipy >=1.3.2,<2.0.0"`	Conda dry run environment on a specific platform

`for py in 3.8 3.9 3.10; do echo -e "\n*****  python $py  *****"; conda create --dry-run --quiet -n __test__ python=$py pandas=1.4.2; done`	Conda dry run creating an environment and installing packages (pandas 1.4.2) for different python versions

## Managing Python

`conda search --full-name python`

`conda search -f python`	Check versions of Python available to install

`conda search ipython=8.3.0 --info | sed '/file name/,/timestamp/d'` For quick checking package dependencies (for example, for all python versions)

`conda create -n snakes python=3.4`	Install different version of Python in new environment

## Managing .condarc Configuration

`conda config --get`	Get all keys and values from my .condarc file

`conda config --get channels`	Get value of the key channels from .condarc file

`conda config --show channels` Knowing the active channels

`conda config --add channels pandas`	Add a new value to channels so conda looks for packages in this location

`conda config --add channels defaults` Adding a default channel

`conda config --add channels conda-forge` Adding a channel

`conda config --add channels bioconda` Adding a channel

`conda config --set anaconda_upload yes` Enable uploading to Anaconda Cloud

`conda config --set anaconda_upload no` Disable uploading to Anaconda Cloud

`conda config --set auto_activate_base false` Deactivating the activation of the base environment in Python

## Managing Packages, Including Python

`conda list`	View list of packages and versions installed in active environment

`conda list | grep pandas` Search package in the list

`conda list --show-channel-urls` List all installed packages along its channels

`conda list --export > env.txt` Save to a Requirements file all packages in an environment

`conda list > env.txt` Save a package list an a file

`conda search beautiful-soup`	Search for a package to see if it is available to conda install

`conda search -c conda-forge black` Search Alternate Channels specify different channels as well, with the use of the -c flag

`conda search conda-forge::black` Search Alternate Channels

`conda install -n bunnies beautiful-soup`	Install a new package NOTE: If you do not include the name of the environment, it will install in the current active environment.

`conda update beautiful-soup`	Update a package in the current environment

`conda search --override-channels -c pandas bottleneck`	Search for a package in a specific location (the pandas channel on Anaconda.org)

`conda install -c conda-forge black`  Installing black from the conda-forge channel

`conda install -c pandas bottleneck`	Install a package from a specific channel

`conda install scipy --channel conda-forge --channel bioconda` Specifying multiple channels when installing a package

`conda search --override-channels -c defaults beautiful-soup`	Search for a package to see if it is available from the Anaconda repository

`conda install iopro accelerate`	Install commercial Continuum packages

`conda install black isort flake8`	install python linter

`conda install conda-build` Install conda-build

`conda install matplotlib=1.4.3` Install a certain package version

`conda install m2-patch posix`	Windows only

`conda install --use-local click`	

`conda skeleton pypi pyinstrument`

`conda build pyinstrument`	Build a package from a Python Package Index (PyPi) Package

## Removing Packages or Environments

`conda remove --name bunnies beautiful-soup`	Remove one package from any named environment

`conda remove beautiful-soup`	Remove one package from the active environment

`conda remove --name bunnies beautiful-soup astroid`	Remove multiple packages from any environment

`conda remove --name snakes --all`	Remove an environment (remove all packages)

`conda uninstall packagename` Remove one package. Alias for conda remove

`conda clean --all` Delete unused packages and caches


## Conda World

### Anaconda Cloud

`anaconda login` Login in to Anaconda Cloud

`anaconda upload C:\ProgramData\Anaconda3\conda-bld\win-64\conda_gc_test-1.2.1-3.tar.bz2` Upload artifact for win64 to your own channel in Anaconda Cloud

`anaconda upload my-notebook.ipynb` Upload my-notebook.ipynb to `http://notebooks.anaconda.org/<USERNAME>/my-notebook`

### conda-build 

`conda-build .` Build a recipe from the current folder

`conda build --test /home/user/miniconda3/conda-bld/noarch/pytest-cov-2.12.1-py_0.tar.bz2`	test the package in your environment (for regression testing)

`conda build gdal-feedstock	`

`conda build sep`	

`conda-build --python 2.7 click`

`conda build gdal-feedstock --variant-config-file conda_build_config.yaml`

### conda convert

`conda convert --platform all ~/anaconda/conda-bld/linux-64/click-7.0-py37_0.tar.bz2 -o outputdir/`

`conda convert package-1.0-py33.tar.bz2 -p win-64`

### conda sekeleton

`conda skeleton pypi --pypi-url <mirror-url> package_name`
  
`conda skeleton pypi <package name on pypi>`
  
`conda skeleton pypi click`
  
`conda skeleton pypi --recursive pyinstrument`

### conda + jake

`conda install -y conda-forge::jake && conda list | jake ddt`	A helpful oneliner to check your conda environments for vulnerable Open Source packages

### conda + boa + mambasolver

`conda install boa -c conda-forge`	Install boa. Use the mamba solver through mambabuild. It not only has a faster solve speed but also prints better error messages that make debugging simpler.

`conda mambabuild .`	build the recipe with mambasolver

`conda mambabuild myrecipe`	build the recipe with mambasolver
