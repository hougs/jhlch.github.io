---
layout: post
title: "Using virtualenv to manage dependencies in projects."
description: ""
category: 
tags: []
---
{% include JB/setup %}

This helps us manage and keep our dependencies consistent 
within a project. With virtualenv, virtualenvwrapper, and autoenv it will be 
easy to maintain consistent python environments. 

* virtualenv
* virtualenvwrapper
* autoenv


Autoenv allows us to execute 
a script when we cd into a directory. This script runs pip install -r 
requirements.txt when you cd into the root dir of a project. If your current 
environment does not conform to the requirements listed, pip will try to 
install the packages. The way to make this very easy for ourselves is to create
a base working environment that includes numpy, scipy, and pandas, and build 
off that as needed.

Install Virtualenv, VirtualenvWrapper, and Autoenv
===================================================
You should install virtualenv, virtualenvwrapper, and autoenv as described in 
this virtualenv site. Virtualenv allows us to manage dependencies and versions
on a project by project basis. VirtualEnv allows you to define and work n 
isolated python environment. VirtualenvWrapper makes it more convenient to 
work with virtualenv. Autoenv allows us to automatically set a virtual env 
when you cd into a directory.

You should execute the following commands:

    pip install virtualenv
    pip install virtualenvwrapper
Also, when installing virtualenv wrapper, add the following lines to you ~/.bash_profile.

    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/<your source dir>
    source /usr/local/bin/virtualenvwrapper.sh

and source ~/.bash_profile.

Then you should also install autoenv. Autoenv allow us to execute a .env script
 that is in the root of a project directory. This is useful for setting 
 environment variables and checking at an env conforms to version requirements
  listed in requirements.txt.

Configure a scipy/numpy/pandas/scikit-learn virtual env
In a more perfect world, we could use pip to install packages listed in the 
requirements.txt file that is stored in a project's repo. In reality, it is 
better to have a virtualenv that already works and just check that it conforms
to the requirements.txt. This is because installing these packages is hard and
`pip install -r requirements.txt` will likely not work without you first 
setting up an env that satisifes those requirements. Give it a try, but if it
doesn't work there are instructions below for using pip and brew to install 
packages into a useful virtualenv.

Assuming you installed and configured virtualenvwrapper, you can create a new virtual env with:

    mkvirtualenv myenv

This creates a new virtual env named `myenv'.
You can then start installing
the following packages into your virtual env with pip:
    
    pip install -U setuptools
    pip install -U pip
    pip install argparse
    pip install numpy

Scipy depends on a Fortran compiler. If you need one, you can easily install it with brew:

    brew install gfortran
    pip install scipy

I had to uninstall and reinstall py2cairo in order to install matplotlib. Check out the simple solution here. This may not be required for you, but if it is just:

    brew rm py2cairo
    brew install py2cairo

Then you can install matplotlib, and ipython:

    pip install matplotlib
    pip install ipython[all]

If you run into trouble installing python, perhaps with a clang error or a 
message like "cc failed with exit code 1" then you may be running into trouble
with unused flags to the c compiler. Run these commands in your shell before 
running `pip install`, and it may help the compiler not fail when there are unused args:

    export CFLAGS=-Qunused-arguments
    export CPPFLAGS=-Qunused-arguments

pandas need PyTables, which in turn depends on hdf5. You have to get that from a special tap:

    brew install homebrew/science/hdf5

Then you can install PyTables, and potential upgrade libs like Cython and numexpr:

    pip install -U numexpr
    pip install -U Cython
    pip install tables
    pip install statsmodels
    pip install pandas
    pip install scikit-learn

You may now check if everything is installed correctly for a project by going 
to that project's root dir and typing `pip install -r requirements.txt`.

You can deactivate you virtual env by typing `deactivate`.

