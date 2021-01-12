.. _tool-installation:

Tool installation
=================

Preliminaries
---------------------------------


.. Attention::
   Throughout this course you may see commands or files or directories that are named something like ``my_awesome_file.tab`` or ``my_home_directory`` or ``myresults.txt``. In these cases, you should replace these names with names that are **relevant to you**, or which are descriptive **for you**, or which contain **your** directory names. For example, if you are making a file that contains the results of a quality control analysis of DNA sequences from *E. coli*, you might name the file ``ecoli_qc_results.txt``.


.. Attention::
   One important aspect of organising files and directories (folders) is `naming convention <https://en.wikipedia.org/wiki/Naming_convention_(programming)>`_. When working on the command line, your life will become considerably easier if you avoid using spaces in your files and directory names. Thus, **never** name your file ``my awesome file.txt``. Instead, name it ``my_awesome_file.txt`` ("snake case"), or ``myAwesomeFile.txt`` ("camel case") or ``my-awesome-file.txt`` ("kebab case") or ``my.awesome.file.txt`` but probably not ``MY-AWESOME-FILE.txt`` ("screaming snake case"). You should pick one of these at the start of the course, and *stick to that format throughout the course* (i.e. camel case, or kebab case, etc.).


.. Attention::
   While we are the topic of `naming conventions <https://en.wikipedia.org/wiki/Naming_convention_(programming)>`_, there are certain characters that you should **always** avoid when naming files and folders. Besides spaces, these are (not necessarily exhaustive):


.. code-block:: bash

: ; ` " ' \ / ! @ # $ % ^ & * ( ) + , ? [ ] { } | > <. 
  

Install the conda package manager
---------------------------------


Software packages and tools are pieces of software that have been developed to perform specific jobs, or are used to implement specific methods. Your general view of a software package may be something like Excel or Chrome or TikTok. However, more fundamentally software is simply a group of instructions used to perform a specific task. In bioinformatics, for example, this could be a set of instructions telling the computer how to interpret and display the quality scores from a ``.fastq`` file.


Software packages and tools often have **dependencies**, which are other pieces of software or tools that are necessary to run the software you would like to install. For example, to use Instagram, you also need software that controls your phone's camera. This reliance of Instagram on camera-controlling software is known as a **dependency**. Software like Instagrtam is designed to be **user-friendly**, and during installation will usually check that such camera-controlling software exists, and if it does not, may try to install it.

However, bioinformatics soaftware, much of which is written by inexperienced computer scientists, or worse, biologists, often does not check for dependencies. This can create signficant issues if ytou try to run a price of software but are missing dependencies (the other pieces of software that are also required).


To make sure that we resolve all these dependency issues, we will use the package/tool managing system. This managing system is called |conda|, and it is perhaps the most common package manager used in bioinformatics. |conda| is not installed by default, thus we need to install it first to be able to use it. 


.. code-block:: bash

    # download latest conda installer
    curl -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

    # run the installer
    bash Miniconda3-latest-Linux-x86_64.sh
    
    # delete the installer after successful run
    rm Miniconda3-latest-Linux-x86_64.sh


.. Note::
   Should the conda installer download fail. Please find links to alternative locations on the
   :doc:`../downloads` page.

    
Update ``.bashrc`` and ``.zshrc`` config-files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before we are able to use |conda| we need to tell our shell where it can find the program.
We add the right path to the |conda| installation to our shell config files:

.. code::
   
   echo 'export PATH="/home/manager/miniconda3/bin:$PATH"' >> ~/.bashrc
   echo 'export PATH="/home/manager/miniconda3/bin:$PATH"' >> ~/.zshrc


.. Attention::
   The above assumes that your username is "manager", which is the default on a Biolinux install.
   Replace "manager" with your actual username.
   Find out with ``whoami``.
   

So what is actually happening here? We are appending a line to a file (either ``.bashrc`` or ``.zshrc``).
If we are starting a new command-line shell, either file gets executed first (depending on which shell you are using, either bash or zsh shells).
What this line does, is to put permanently the directory ``~/miniconda3/bin`` first on your ``PATH`` variable.
The ``PATH`` variable contains directories in which our computer looks for installed programs, one directory after the other until the program you requested is found (or not, then it will complain).
Through the addition of the above line we make sure that the program ``conda`` can be found anytime we open a new shell.


Close shell/terminal, **re-open** new shell/terminal.
Now, we should be able to use the |conda| command:


.. code-block:: bash

    conda update conda


Installing conda channels to make tools available
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Different tools are packaged in what |conda| calls channels.
We need to add some channels to make the bioinformatics and genomics tools
available for installation:


.. code-block:: bash
    
    # Install some conda channels
    # A channel is where conda looks for packages
    conda config --add channels defaults
    conda config --add channels bioconda 
    conda config --add channels conda-forge     

   
Create environments
-------------------

We create a |conda| environment for some tools.
This is useful to work **reproducible** as we can easily re-create the tool-set with the same version numbers later on.


.. code-block:: bash

    conda create -n ngs python=3
    # activate the environment
    conda activate ngs

    
So what is happening when you type ``conda activate ngs`` in a shell.
The ``PATH`` variable (mentioned above) gets temporarily manipulated and set to:


.. code-block:: bash
                
   $ conda activate ngs
   # Lets look at the content of the PATH variable
   (ngs) $ echo $PATH
   /home/manager/miniconda3/envs/ngs/bin:/home/manager/miniconda3/bin:/usr/local/bin: ...


Now it will look first in your environment's bin directory but afterwards in the general conda bin (/home/manager/miniconda3/bin).
So basically everything you install generally with conda (without being in an environment) is also available to you but gets overshadowed if a similar program is in ``/home/manager/miniconda3/envs/ngs/bin`` and you are in the ``ngs`` environment.


Install software
----------------

To install software into the activated environment, one uses the command ``conda install``.

.. code-block:: bash
         
    # install more tools into the environment
    conda install package


.. note::
   To tell if you are in the correct conda environment, look at the command-prompt.
   Do you see the name of the environment in round brackets at the very beginning of the prompt, e.g. (ngs)?
   If not, activate the ``ngs`` environment with ``conda activate ngs`` before installing the tools.

    
                
General conda commands
----------------------

.. code-block:: bash

    # to search for packages
    conda search [package]
    
    # To update all packages
    conda update --all --yes

    # List all packages installed
    conda list [-n env]

    # conda list environments
    conda env list

    # create new env
    conda create -n [name] package [package] ...

    # activate env
    conda activate [name]

    # deavtivate env
    conda deactivate
