Setup
=====

.. _Computer Environment:

Computer Environment
--------------------

The SWMF is a collection of codes primarily written in fortran and C++. The SWMF
runs primarily through a command line interface. As such, usage on Linux and 
MacOS can be done natively through the terminal, while Windows users will need
to use Windows Subsystem for Linux (WSL) or other methods of running a Linux
environment on Windows. Tutorials for using the command line exist elsewhere
online, but importnat commands necessary for running the SWMF will be convered
in this guide. 

.. note::

    If you have never used a compiled language before (C, C++, Fortran, Go, etc.),
    there are a few important differences to know compared to higher level languages
    such as Python or IDL. Python and IDL run based on a single "interpreter" that
    runs the code. This usually comes in the form of a file that looks something
    like "python.exe". Compiled languages work differently. A compiler is used to 
    turn the code into a binary executable file written in machine code. This
    executable can then be run on your computer.

In order to run the SWMF, you will need both a fortran and C compiler installed
on your computer. Exactly what compilers are supported is slightly operating
system dependent, but in general, the following compilers are supported:

- GNU Fortran/C (gfortran, gcc)
- Intel Fortran/C (ifx, ifort, icc, icx)
- Nagfor
- Nvidia Fortran/C (nvfortran)
- PGI Fortran/C (pgf90, pgcc)
- Apple's Clang compiler (clang)

.. note::
    
    If you're ever curious what compilers are supported on a specific OS, you
    can look at the SWMF/share/build directory. Each makefile named for a 
    specific OS and then the compiler. For example, the makefile for ifx on
    Linux is Makefile.linux.ifx .

It is generally recommended to try installing the SWMF on a local machine first.
If you are installing on a High-performance computing (HPC) cluster, such as 
Derecho, Athena, Pleiades, or a university cluster, the computer environment is
built using modules. On HPC clusters, it is recommended to use intel compilers,
as they normally have the best performance. This may look something like:

.. code-block:: console

   $ module load intel

or

.. code-block:: console

   $ module load PrgEnv-intel

.. _Installation:

Installation
------------

Once your computer environment has been set up, it is time to download the SWMF.
Most SWMF models are hosted on Github at github.com/SWMFsoftware. It is
recommended to set up SSH integration with a github account to make downloading
and updating the SWMF easier. A tutorial for setting this up can be found at
https://docs.github.com/en/authentication/connecting-to-github-with-ssh. Once
SSH integration is set up, you can clone the SWMF repository using the following
command:

.. code-block:: console

   git clone git@github.com:SWMFsoftware/SWMF.git

Once the SWMF has been cloned from github, you can navigate to the SWMF 
directory and install it using the Config.pl script. The Config.pl script has 
default compilers for different machines. If you would like to use the default,
simply run the following command:

.. code-block:: console

   $ cd SWMF
   $ ./Config.pl -install

If you would like to specify a compiler, you can use the -compiler flag. You
will usually need to specify both a fortran and C compiler. For example, to use 
the new intel ifx compilers on Athena, you can run the following command:

.. code-block:: console

   $ ./Config.pl -install -compiler=ifxmpif90,icxmpicxx


The first time you run the Config.pl script, it will git clone every 
model that is natively supported by the SWMF. If you want to only install
a specific model, you can do so by appending the models to the -install
flag. For example, to only install the Geospace model, you can run the
following command:

.. code-block:: console

   $ ./Config.pl -install=BATSRUS,Ridley_serial,RCM2

m






