---
title: Setup
---

## Setup

This lesson is designed to be run on a personal computer.
All of the software and data used in this lesson are freely available online,
and instructions on how to obtain them are provided below.

## Install Python

Users of the NOC Data Science Platform or Binder Hub can skip this section and move on to the "Obtain lesson materials" section below.

### Install Miniforge

If Conda has not been installed on your machine, then install [Miniforge](https://conda-forge.org/download/) for your OS. As the name
suggests, Miniforge is a "mini" version of the
[Anaconda Python distribution](https://www.anaconda.com/download) that includes only Conda, a
Python 3 distribution, and any necessary OS-specific dependencies.

For convenience here are links to the 64-bit Miniconda installers.

* [Windows](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe)
* [Mac OSX - Intel CPU](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-x86_64.sh)
* [Mac OSX - Apple M1/2/3 CPU](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh)
* [Linux](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh)


#### Windows installation

After you downloaded the [Windows installer](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe), double click on it and follow the instructions (accept license, etc.).
Make sure you tick on **"Add Miniforge3 to my PATH environment variable"** option.

#### Mac OSX or Linux installation

First, download the 64-bit Python 3 install script for Miniforge
either by clicking the link above or using this command in your terminal:

```bash
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

Run the Miniforge install script from your terminal. Follow the prompts on the installer screens. If you are unsure
about any setting, accept the defaults (you can change them later if necessary).

```bash
bash Miniforge3-$(uname)-$(uname -m).sh
```

Once the install script completes, you can remove it.

```bash
rm Miniforge3-$(uname)-$(uname -m).sh
```


### Verifying your Conda installation

In order to verify that you have installed Conda correctly run the `conda help` command. Output
of the command should look similar to the following.

```bash
$ conda help
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (/Users/drpugh/.condarc) by default.
    create       Create a new conda environment from a list of specified
                 packages.
    help         Displays a list of available conda commands and their help
                 strings.
    info         Display information about current conda install.
    init         Initialize conda for shell interaction. [Experimental]
    install      Installs a list of packages into a specified conda
                 environment.
    list         List linked packages in a conda environment.
    package      Low-level conda package utility. (EXPERIMENTAL)
    remove       Remove a list of packages from a specified conda environment.
    uninstall    Alias for conda remove.
    run          Run an executable in a conda environment. [Experimental]
    search       Search for packages and display associated information. The
                 input is a MatchSpec, a query language for conda packages.
                 See examples below.
    update       Updates conda packages to the latest compatible version.
    upgrade      Alias for conda update.

optional arguments:
  -h, --help     Show this help message and exit.
  -V, --version  Show the conda version number and exit.

conda commands available from other packages:
  env
```

At the bottom of the help menu you will see a section with some optional arguments for the
`conda` command. In particular you can pass the `--version` flag which will return the version
number. Again output should look similar to the following.

```bash
$ conda --version
conda 4.8.2
```


### Install the Required Python Libraries

Run the following command to install the required dependencies.
```bash
$ conda install jupyterlab pip python=3.11 "numpy>2.0" matplotlib-base matplotlib-inline netcdf4
```


## Obtain lesson materials

1. Download [python-esces-data.zip][zipfile1].
2. Create a folder called `swc-python` on your Desktop.
3. Move downloaded files to `swc-python`.
4. Unzip the files.

You should see a folder called `data` in the `swc-python` directory on your
Desktop.


## Launch Python interface

To start working with Python, we need to launch a program that will interpret and execute our
Python commands. Below we list several options. If you don't have a preference, proceed with the
top option in the list that is available on your machine. Otherwise, you may use any interface
you like.


### Option A: Jupyter Notebook

A Jupyter Notebook provides a browser-based interface for working with Python.
If you installed Miniforge, you can launch a notebook from the terminal:


::::::::::::::::::::::::::::::::::::::::::  prereq

## Command line (Terminal)

1. Navigate to the `data` directory:

- Unix shell
If you're using a Unix shell application, such as Terminal app in macOS, Console or Terminal
in Linux, or [Git Bash][gitbash] on Windows, execute the following command:
```
cd ~/Desktop/swc-python/data
```


- Command Prompt (Windows)
On Windows, you can use its native Command Prompt program.  The easiest way to start it up is
pressing `Windows Logo Key`+`R`, entering `cmd`, and hitting
`Return`. In the Command Prompt, use the following command to navigate to
the `data` folder:
```
cd /D %userprofile%\Desktop\swc-python\data
```

2. Start Jupyter server

- Unix shell
```
jupyter notebook
```


- Command Prompt (Windows)
```
python -m notebook
```

3. Launch the notebook by clicking on the "New" button on the right and selecting "Python 3" from the drop-down menu:

![Anaconda Navigator Notebook directory](
episodes/fig/jupyter-notebook-launch-notebook2.png){alt="Anaconda Navigator Notebook directory"}

::::::::::::::::::::::::::::::::::::::::::::::::::

### Option B: IPython interpreter

IPython is an alternative solution situated somewhere in between the plain-vanilla Python
interpreter and Jupyter Notebook. It provides an interactive command-line based interpreter with
various convenience features and commands.  You should have IPython on your system if you installed
[Anaconda][anaconda-instructions].

To start using IPython, execute:
```bash
ipython
```

### Option C: plain-vanilla Python interpreter

To launch a plain-vanilla Python interpreter, execute:
```bash
python
```


If you are using [Git Bash on Windows][gitbash], you have to call Python _via_ `winpty`:
```bash
winpty python
```


[anaconda-install]: https://docs.anaconda.com/anaconda/install
[anaconda-instructions]: https://carpentries.github.io/workshop-template/#python
[anaconda-website]: https://www.anaconda.com/
[gitbash]: https://gitforwindows.org
[zipfile1]: https://github.com/NOC-OI/python-novice-esces/raw/refs/heads/gh-pages/data/python-esces-data.zip
