Geospace Extended
==================

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


