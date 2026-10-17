Geospace
========

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

In addition to compiling the SWMF, you will need to set up a run directory. This
can be done by running the following command:

.. code-block:: console

   $ make rundir

This will set up a run directory called run that should contain everything 
needed to run whatever models are active, with the exception of run specific
input files.

.. _Changing IM Models:

Changing Models
----------------

While BATSRUS and Ridley_serial are the only GM and IE components currently
supported by the SWMF, there are several different IM components that can be 
used. The currently supported IM components are RCM2, CIMI, HEIDI, and RAM-SCB.
Something to keep in mind when running these models is that non-RCM models will
usually need some additional data files not provided in their own git 
repositories. These files are available in the SWMF_data repository. To clone
this data and link it to the model that needs it, you can run the following 
command:

.. code-block:: console

   $ git clone git@github.com:SWMFsoftware/SWMF_data.git
   $ cd /path/to/SWMF/IM/Model
   $ ln -s /path/to/SWMF_data/IM/Model/data

For example, to link CIMI to its data, assuming you have the SWMF installed in 
your home (~) directory, you would run the following commands:

.. code-block:: console

   $ cd ~
   $ git clone git@github.com:SWMFsoftware/SWMF_data.git
   $ cd SWMF/IM/CIMI
   $ ln -s ~/SWMF_data/IM/CIMI/data

If this linking is done correctly, whenever a run directory is set up for a
model that requires these extra files, these files will automatically be put
where they are needed for running the model. 

.. note:: 
    These files will be put into any new run directory, but they will not be
    automatically copied into current run directories. If you have an existing 
    run directory that is not working due to missing these data files, you 
    will need to manually copy them into the run directory IM folder.

.. _Particle Tracking:

Particle Tracking 
------------------

.. note::
    This section is under active development. 
    
.. _Plasmasphere:

Plasmasphere
------------

.. note::
    This section is under active development. 

.. _Embedded Particle In Cell:

Embedded Particle In Cell
-------------------------

.. note::
    This section is under active development.

.. _Upper Atmosphere:

Upper Atmosphere
----------------

.. note::
    This section is under active development.

.. _Polar Wind:

Polar Wind
----------

.. note::
    This section is under active development.

.. _Radiation Belt:

Radiation Belt
--------------

.. note::
    This section is under active development.


