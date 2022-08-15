Setup
=====
There are different ways how you can access the simulation. Depending on your situation and ressources available you may want to install Carla in a container enviorment or on your local machine. 
.. _installation:

Requirements  
------------
- **Ubuntu 18.04 or later**
- **130 GB disk space**
- **A strong GPU** (Atleast 6GB VRam, 8GB recommended) 
- **2-4 Hours time** (Depending on CPU and Internet speed)

Build Carla in Apptainer 
------------
**1. Install Apptainer**
If you don't have Apptainer (ex-Singularity) installed on your machine / computing cluster refer to  `Installing Apptainer <https://apptainer.org/docs/admin/main/installation.html>`_ for installation. 
**2. Run the Build process using a definition (.def) file**
Once you have installed Apptainer, you can build a new container using a definition file. This file includes everything needed to install Carla in an Apptainer container with all dependencies. 
You can download the build file for the latest version of Carla (0.9.13) here (ToDo):
A: Buildfile including copy of vulkan .json file
B: Buildfile excluding copy of vulkan .json file.
To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

Build Carla in Docker
----------------
.. note::

   ToDo.
  
To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

Build Carla from Source on a local machine
----------------
