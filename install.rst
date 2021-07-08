
Download and Install
********************

All of the packages and libraries distributed within in the AutoMech suite can be obtained in a similar manner. 
Therefore the following instructions should be generally applicable to any code of interest.
Each code can be compiled on Linux or Mac, however we have more support for Linux in terms of ease of installation.

Install via Conda
-----------------

The simplest and most direct way to install any code is by using the Conda package manager, which allows the user to obtain pre-compiled versions of the code and its dependencies.

This is the recommended method of installation as Conda environments will deal with dependency issues. Also, it will make installing updates much easier as the codes are developed.

Installation via Conda can be conducted in several means:
    (1) Use one of our pre-defined AutoMech environments
    (2) Install a package directly into

All of the packages are available on Anaconda cloud: <link>

Users unfamiliar with Conda, refer to <link below>.

Build AutoMech Environments
~~~~~~~~~~~~~~~~~~~~~~~~~~~

We have generated a pre-set `AutoMech` environment which includes binaries for all codes in the suite. This is the easiest way to get any package, particularly if the user does not care about which one they want. Useful for running higher-level codes, e.g. MechDriver and MechAnalyzer.

This environment can be created and activated with the commands:

.. code-block:: console

    conda env create auto-mech/amech-env
    conda activate amech-env

Alternatively, the user may download the corresponding the Auto-Mech environment file directly (https://anaconda.org/Auto-Mech/amech-env/files) and create the environment uing this file:

.. code-block:: console
    
    conda env create -f auto-mech-env.yml
    conda activate amech-env

The user may also build an environment for working with specific AutoMech packages. This is useful for facilitating builds from source code as well as debugging. These environments are defined in environment.yml files that are availablein the package's GitHub repository

.. code-block:: console
    
    cd <package-top-directory>
    conda env create create -f environment.yml
    conda activate <package-env>

Install into Existing MiniConda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Activate an environment in you wish to use to install a given package and run the install command:

.. code-block:: console

    conda install -c auto-mech <package name>

If you do not have a preferred Conda environment set up, an empty environment with no packages can be created and activated with the following commands

.. code-block:: console

    conda create --name myenv
    conda activate myenv

where `myenv` should be replaced with your preferred name for the environment.


Updating Packages
~~~~~~~~~~~~~~~~~

Packages can be installed simply using teh following command:

.. code-block:: console

    conda install -c auto-mech <package name>


Building from Source 
--------------------

The source codes for all AutoMech codes can be obtained from their respective GitHub repositories, which are collectively listed on the main AutoMech GitHub page: <https://github.com/Auto-Mech/>. 

Each code can be nominally built by executing the build script in the repository via:

.. code-block:: console

    bash build.sh

The build process depends slightly on the package. For C++/C/Fortran codes, the script will
use cmake to build the code according to the accompanying CMakeLists.txt file. Whereas Python
codes will execture the accompanying setup.py files. The user may have to further modify the
build.sh, CMakeLists.txt, or setup.py files to deal with the requirements of their specific system. 

Of course, building from source requires proper installation of the dependencies of the desired
package. One method involves generating and activating the Conda environment using the 
environment.yml file, as discussed previously. Alternatively, each of the dependencies can
be built from source if they are not already installed. Dependencies corresponding to AutoMech
packages can be resolved by downloading their GitHub. Other libraries are the user's responsibility.

Extra Help
----------

Installing Conda
~~~~~~~~~~~~~~~~

Builds an `environment` where all of the executables...

For users on systems, contact administrator to see if Conda installed.

A MiniConda distribution can be installed using the following script.

.. code-block:: console

    #!/usr/bin/env bash
    
    if [ "$(uname)" == "Darwin" ]; then
        wget https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
        bash Miniconda3-latest-MacOSX-x86_64.sh -b -p $CONDA
    elif [ "$(uname)" == "Linux" ]; then
        wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
        bash Miniconda3-latest-Linux-x86_64.sh -b -p $CONDA
    fi

If Conda is installed but the commands are not functioning, you may need to iniliatize Conda via the command

.. code-block:: console

    . /path/to/conda.sh

which places Conda executables in your PATH. The specific location of conda.sh depends on the Conda install. This may also be placed in .bashrc (or shell equivalent).

For more instructions, see <https://conda.io/projects/conda/en/latest/user-guide/index.html>


Fake Install Script
~~~~~~~~~~~~~~~~~~~

Quick script to place executables in PATH for a given terminal session.

Note that the above command does not **permanently** alter your PATH, it only affects PATH for the current login session.

.. code-block:: console

    # run with: . /path/to/fake-install.sh
    export _THIS_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
    
    for d in ls $_THIS_DIR/\*/; do
        export PATH=$d:$PATH
        export PYTHONPATH=$d:$PYTHONPATH
    done
    
    for d in ls $_THIS_DIR/\*/\*; do
       export PATH=$d:$PATH
       export PYTHONPATH=$d:$PYTHONPATH
    done

