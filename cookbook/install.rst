DRP installation
================

The MEGARA pipeline is a Python package, for Python 3.5 or greater.

The easiest method of installing megaradrp is using prebuilt packages.
You can also build from source or directly from the development version.
All the commands in the following sections are to be run under **bash
shell**. More details are in the MEGARA DRP *readthedocs*
documentation [2]_.

**Suggestion: what method of installation should I use?**

\* If you are already familiar with one method, use it (conda or
virtualenv), since both a fully supported.

\* In macOS, there is a well-known compatibility problem between
virtualenv and matplotlib [3]_, so we recommend setting up conda.

\* In Linux, virtualenv is easier to setup

Install in virtualenv
----------------------

Virtualenv [4]_ is a tool that allows to create isolated Python
environments. There is also a module in the standard library called venv
with roughly the same functionallity.

The steps to run MEGARA DRP in a virtual environment are:

Create a virtual environment using either virtualenv or venv.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to create a virtual environment called e.g. megara using venv:

bash-3.2$ python3 -m venv megara /path/to/

With virtualenv:

bash-3.2$ virtualenv-3 megara /path/to/

The directory \`/path/to\` represents the location of the environment.
It can be any valid directory path, even the local directory \`.\` .

Activate the environment.
~~~~~~~~~~~~~~~~~~~~~~~~~

After creating the environment, the directory \`/path/to/megara\`
contains a Python tree. One of the directories is
\`/path/to/megara/bin\`, which contains a script called activate. To
activate the environment, we source (a bash shell command) this script
file:

bash-3.2$ source /path/to/megara/bin/activate

which yields a different system prompt to the user:

(megara) bash-3.2$

Now, the name of the environment appears before the standard prompt. We
can use the environment only on those consoles / terminals where we have
previously activated it.

Install megaradrp with pip
~~~~~~~~~~~~~~~~~~~~~~~~~~

After the activation, we can install megaradrp with pip. This is the
standard Python tool for package management. It will download the
package and its dependencies, unpack everything and compile when needed.

What follows is a sample of the output:

(megara) bash-3.2$ pip install megaradrp

Collecting megaradrp

Collecting scikit-image (from megaradrp)

Downloading
https://files.pythonhosted.org/packages/11/c7/ee75c79dcce057a3475763d611ec044737a708eaf5cc53426b0117795ddb/scikit_image-0.14.0-cp35-cp35mu-manylinux1_x86_64.whl
(25.4MB)

Collecting scipy (from megaradrp)

(...)

Building wheels for collected packages: toolz, scandir

Running setup.py bdist_wheel for toolz ... done

Running setup.py bdist_wheel for scandir ... done

Successfully built toolz scandir

Installing collected packages: decorator, networkx, cloudpickle, numpy,
toolz, dask, six, PyWavelets, python-dateutil, subprocess32, cycler,
backports.functools-lru-cache, pytz, pyparsing, kiwisolver, matplotlib,
scipy, pillow, scikit-image, enum34, atomicwrites, more-itertools,
pluggy, attrs, scandir, pathlib2, py, funcsigs, pytest, astropy, PyYaml,
numina, megaradrp

Test the installation.
~~~~~~~~~~~~~~~~~~~~~~

Now we can test the installation by running the numina command:

(megara) bash-3.2$ numina

DEBUG: Numina simple recipe runner version 0.17.3

Update within the environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to update the MEGARA DRP in a virtualenv installation the user
should execute:

(megara) bash-3.2$ pip install -U megaradrp

Deactivate the environment.
~~~~~~~~~~~~~~~~~~~~~~~~~~~

To exit the environment is enough to exit the terminal or run the
command deactivate.

(megara) bash-3.2$ deactivate

bash-3.2$

Install in conda
-----------------

Conda [5]_ was created with a target similar to virtualenv, but know has
extended its functionallity to package management for different
languages.

You can install miniconda [6]_ or anaconda [7]_. The difference is that
miniconda provides a light-weight environment and anaconda comes with
lots of Python packages.

If you have updated the $PATH variable during install, you can call
conda commands directly in the shell, like this:

bash-3.2$ conda info

If not, you will need to add the path to the command (an example path
could be miniconda3/bin), like:

bash-3.2$ /path/to/conda/bin/conda info

If that is the case, you should add that path every time you run a conda
command hereafter. Alternatively, you can initialize conda for your own
shell by doing:

bash-3.2$ conda init bash

This works as it is if you are using a login-shell (terminal), but if
you are using a xterm, you might also need to do:

bash-3.2$ cp ~/.bash_profile ~/.bashrc (do a backup copy of ~/.bashrc if
you have one already),

and open a new terminal/xterm. Below, we will write the commands without
the full path, for simplicity. Once conda is installed according to the
instructions above, the steps to run MEGARA DRP under conda would be the
following [8]_:

Create a conda environment
~~~~~~~~~~~~~~~~~~~~~~~~~~

We first recommend that you update your conda installation to its latest
by doing:

(base) bash-3.2$ conda update conda

With conda, environments are created in a centralised manner (under
directory \`./envs\` in your conda tree), we do not pass the path to the
environment.

(base) bash-3.2$ conda create --name megara python=3

One could remove this environment (and all its content), if needed, by
simply doing:

(base) bash-3.2$ conda remove --name megara --all

Install megaradrp with conda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Packages can be installed before activating the environment. We provide
conda packages for megaradrp in the conda-forge channel [9]_:

(base) bash-3.2$ conda install --name megara -c conda-forge megaradrp

Fetching package metadata .............

Solving package specifications: .

Package plan for installation in environment
/home/spr/devel/miniconda3/envs/megara:

The following NEW packages will be INSTALLED:

astropy: 2.0.8-py35_0 conda-forge

atomicwrites: 1.1.5-py35_0 conda-forge

attrs: 18.1.0-py_1 conda-forge

....

zlib: 1.2.11-h470a237_3 conda-forge

Proceed ([y]/n)? y

Activate the environment
~~~~~~~~~~~~~~~~~~~~~~~~

The functionality is similar to virtualenv:

(base) bash-3.2$ conda activate megara

(megara) bash-3.2$

Again, after activating the environment, the name of the environment
appears before the standard prompt. We can use the environment only on
those consoles / terminals where we have previously activated it.

Test the installation
~~~~~~~~~~~~~~~~~~~~~

Now we can test the installation by running the numina command:

(megara) bash-3.2$ numina

DEBUG: Numina simple recipe runner version 0.17.3

.. _update-within-the-environment-1:

Update within the environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to update the MEGARA DRP within the conda environment the user
should execute:

(megara) bash-3.2$ conda update megaradrp

Deactivate the environment
~~~~~~~~~~~~~~~~~~~~~~~~~~

To exit the environment is enough to exit the terminal or run the
command source deactivate

(megara) bash-3.2$ conda deactivate

(base) bash-3.2$

Update outside the environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once outside the conda environment one can also update the MEGARA DRP
installation by doing:

(base) bash-3.2$ conda update megaradrp -n megara

If you want to deactivate the conda *(base)* environment entirely you
can run again:

(base) bash-3.2$ conda deactivate

bash-3.2$

Development version
-------------------

For those of you interested in installing the development version,
please consult the instructions at the readthedocs.org webpage at
https://megaradrp.readthedocs.io/en/latest/installation.html. The use of
the development version is recommended to have access to the latest DRP
improvements.

.. |image1| image:: _static/image2.png
   :width: 3.65278in
   :height: 2.34722in
.. |image2| image:: _static/image3.jpeg
   :width: 2.60208in
   :height: 2.04792in
.. |image3| image:: _static/image4.png
   :width: 6.81319in
   :height: 3.43194in
.. |image4| image:: _static/image5.png
   :width: 6.81319in
   :height: 3.43194in
.. |image5| image:: _static/image6.png
   :width: 6.81319in
   :height: 3.43194in
.. |image6| image:: _static/image6.png
   :width: 6.81319in
   :height: 3.43194in
.. |image7| image:: _static/image10.png
   :width: 6.63681in
   :height: 3.09306in
.. |image8| image:: _static/image12.png
   :width: 3in
   :height: 2.25in
.. |image9| image:: _static/image13.png
   :width: 3.04167in
   :height: 2.28056in
.. |image10| image:: _static/image19.png
   :width: 6.69306in
   :height: 1.28472in
.. |image11| image:: _static/image21.png
   :width: 6.69306in
   :height: 1.27917in
.. |Imagen que contiene edificio Descripción generada automáticamente| image:: _static/image24.png
   :width: 6.69306in
   :height: 1.38125in
.. |Captura de pantalla en blanco y negro Descripción generada automáticamente| image:: _static/image28.png
   :width: 3.35556in
   :height: 3.38542in
.. |image12| image:: _static/image30.png
   :width: 3.37205in
   :height: 3.36751in
.. |Imagen que contiene monitor, computadora, tabla Descripción generada automáticamente| image:: _static/image31.png
   :width: 3.38422in
   :height: 3.40178in
.. |Imagen que contiene mapa, texto Descripción generada automáticamente| image:: _static/image32.png
   :width: 3.34124in
   :height: 2.79245in
.. |image13| image:: _static/image33.png
   :width: 3.93424in
   :height: 2.80189in
.. |Captura de pantalla de un celular Descripción generada automáticamente| image:: _static/image34.png
   :width: 3.14708in
   :height: 2.41985in
.. |image14| image:: _static/image35.png
   :width: 3.1087in
   :height: 2.36637in
.. |image15| image:: _static/image36.png
   :width: 3.59647in
   :height: 2.66927in
.. |image16| image:: _static/image37.png
   :width: 3.5784in
   :height: 2.70836in


.. [2]
   https://megara-drp.readthedocs.io/en/latest/installation.html

.. [3]
   https://matplotlib.org/faq/osx_framework.html

.. [4]
   https://virtualenv.pypa.io/en/stable/installation/

.. [5]
   https://conda.io/docs/

.. [6]
   See installation instructions at https://conda.io/miniconda.html

.. [7]
   See installation instructions at
   https://docs.anaconda.com/anaconda/install/

.. [8]
   If you are using conda version 4.4+ your terminal will open in the
   conda *(base)* environment. If you want to avoid that permanently
   just do: conda config --set auto_activate_base false

.. [9]
   https://conda-forge.org/

