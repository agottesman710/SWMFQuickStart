Geospace
========

Running the Geospace Model
--------------------------

The standard Geospace model is a combination of the BATSRUS, Ridley_serial, 
and RCM models. To configure the SWMF to run the Geospace model, use the 
Config.pl script with the -v flag to specify which models to use. The 
general syntax for this command is COMPONENT/Model. For example, to run the
Geospace model, you can run the following command:

.. code-block:: console

   $ ./Config.pl -v=GM/BATSRUS,IE/Ridley_serial,IM/RCM2

This command sets BATSRUS to run as the Global Magnetosphere (GM) component, 
Ridley_serial to run as the Ionosphere Electrodynamics (IE) component, and
RCM2 to run as the Inner Magnetosphere (IM) component. After doing this, you
can optionally run the Config.pl script with no flags to have it print out 
the current configuration of the SWMF and verify that everything is set up
correctly. Assuming compilers have been set up correctly, you can then simply
run "make" to compile the SWMF and the currently active models. The -j flag can
be used to compile in paralle, which significantly speeds up the compilation.

.. code-block:: console

   $ make -j

In addition to compiling the SWMF, you will need to set up a run directory, and
compile the postprocessing script. This can be done by running the following 
commands:

.. code-block:: console

   $ make PIDL 
   $ make rundir

This will set up a run directory called run that should contain everything 
needed to run whatever models are active, with the exception of run specific
input files. 

These run specific input files are a PARAM.in, and usually an IMF.dat. The 
PARAM.in file is the primary file that tells the SWMF how to run. These will
configure how the run is set up, including the use of processors, the time and
duration of the run, the output files that will be generated, the domain and
resolution of the simulation, and many other parameters. The IMF.dat file is
used to specify the interplanetary magnetic field (IMF) conditions for the run.
These files are often very large, containing many different parameters. As such,
it is not recommended to write these files from scratch. Instead, it is 
recommended to start with a baseline provided by the SWMF nightly test 
configurations, and make edits as desired. For Geospace runs, these files can
be found in SWMF/Param/SWPC. For the standard Geospace configuration, the file
of choice is PARAM.in_SWPC_simple_init. 

Once your run directory is set up, run the SWMF in its simplest form by running 
the following command from within the run directory:

.. code-block:: console

   $ ./SWMF.exe

This however will only run the simulation on a single processor. To run the 
simulation in parallel, you will need to use the mpirun or mpiexec command. 
To run on N processors, you can run the following command:

.. code-block:: console

   $ mpirun -np N ./SWMF.exe

While this runs, it will output information to the console, including the 
PARAM options used, number of time steps completed, simulation time, cross polar
cap potential, and files being saved. It is recommended to save this information
to a log file for later reference. To do this, you can run the following 
command:

.. code-block:: console

   $ mpirun -np N ./SWMF.exe > runlog

Or, to output to both your console and a log file, you can run the following 
command:

.. code-block:: console

   $ mpirun -np N ./SWMF.exe | tee runlog

After a Geospace Run
----------------------

Once a geospace run has completed, it will usually be required to do 
postprocessing. This is necessary as the parallel processing of the simulation
usually requires the generation of multiple files for each time saved that are 
combined into a single file for analysis. The postprocessing script is also
parallelized. In addition, it has some other flags that can be given to do 
additional work. Some examples include: -g will zip output IE files, -M will
concatenate all the output GM .out files into .outs files by type, -n=N will
run the postprocessing script on N processors, and -h will print out a list of
all the flags that can be used. The first unflagged argument given to the 
postprocessing script is taken as the output directory. For example, the 
following command will run the postprocessing script on 4 processors, zip the
IE output files, and concatenate the GM output files into .outs files, with all
the GM, IE, and IM output, along with the runlog and a copy of the PARAM.in 
files being put into a directory called MyFirstRun:

.. code-block:: console

   $ ./PostProc.pl -n=4 -g -M MyFirstRun


.. _Compile Time Options:

Compile Time Options
--------------------

MHD Equations
~~~~~~~~~~~~~~~

.. note::
    This section is under active development.

.. _IE Grid Changing:

IE Grid Changing
~~~~~~~~~~~~~~~

.. note::
    This section is under active development.

Outputs
-----------------

.. _Virtual Magnetometers:

Virtual Magnetometers
~~~~~~~~~~~~~~~


.. note::
    This section is under active development.

.. _Satellite Extraction:

Satellite Extraction
~~~~~~~~~~~~~~~

.. note::
    This section is under active development.
