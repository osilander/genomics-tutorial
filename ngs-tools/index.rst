.. _tool-installation:

Tool installation
=================

Preliminaries
---------------------------------


Note that throughout this course you may see commands or files or directories that are named something like ``my_awesome_file.tab`` or ``my_home_directory`` or ``myresults.txt``. When you see names like this in the instructions, *this does not mean that you should name your files or directories in this way*. Rather, you should replace these placeholder names with names that are **relevant to you**, or which are descriptive **for you**, or which contain **your** directory names. For example, if you are making a file that contains the results of a quality control analysis of DNA sequences from *E. coli*, you might name the file ``ecoli_qc_results.txt``.


.. Attention::
   One important aspect of organising files and directories (folders) is `naming convention <https://en.wikipedia.org/wiki/Naming_convention_(programming)>`_. When working on the command line, your life will become considerably easier if you avoid using spaces in your files and directory names. Thus, **never** name your file ``my awesome file.txt``. Instead, name it ``my_awesome_file.txt`` ("snake case"), or ``myAwesomeFile.txt`` ("camel case") or ``my-awesome-file.txt`` ("kebab case") or ``my.awesome.file.txt`` but probably not ``MY-AWESOME-FILE.txt`` ("screaming snake case"). You should pick one of these at the start of the course, and *stick to that format throughout the course* (i.e. camel case, or kebab case, etc.).


While we are the topic of `naming conventions <https://en.wikipedia.org/wiki/Naming_convention_(programming)>`_, there are certain characters that you should **always** avoid when naming files and folders. Besides spaces, these are (not necessarily exhaustive):


.. code-block:: bash

   : ; ` " ' \ / ! @ # $ % ^ & * ( ) + , ? [ ] { } | > <
  


.. Attention::
   One More Thing.

   Throughout this course we will be interacting with the computer via the command line. There is one fundamental aspect of using the command line that you **must never forget**. It is perhaps the single most powerful method available to save time. That method is...
   

   **tab-complete**
   

   `Tab-complete <https://en.wikipedia.org/wiki/Command-line_completion>`_ can be used to auto-complete commands, directory names, and file names. If you are not sure whether your file is named ``results_QC.txt`` or ``results_qc.txt`` then on the command line you can simply type ``results`` *and then tab*, and the computer will auto-complete the name (assuming there is a file or directory or command that begins with ``results``).

   If you type the first part of a file and then press tab, but find that it does not autocomplete *even though you know you have the correct start of the file name*, then try pressing tab twice. This will give you a list of all the files (directories), etc. that begin with the first few letters that you have typed. This becomes important, for example, if you have a file named ``my_awesome_file.txt`` and ``my_awesome_file2.txt`` but you only type ``my_awes`` and then tab-complete.


.. Attention::
   
   And Yet One More Thing.


   Throughout this lab course, *google is your friend*. If you have errors, or if you are not sure how you might do something, or if you forget a command, google it!

   Thus, **Step One** as you begin the lab is: Approach the command line with confidence and in a calm manner, assured that whatever goes wrong, you can google your way out of it.

   `It's <https://codeahoy.com/2016/04/30/do-experienced-programmers-use-google-frequently/>`_

   `what <https://www.reddit.com/r/programming/comments/3bwo68/how_much_does_an_experienced_programmer_use_google/>`_

   `all <https://www.hanselman.com/blog/am-i-really-a-developer-or-just-a-good-googler>`_

   `good <https://www.freecodecamp.org/news/google-not-learn-not-why-searching-can-be-better-than-knowing-79838f7a0f06/>`_

   `programmers <https://fossbytes.com/do-best-programmers-use-google-stack-overflow-time/>`_

   `do <https://news.ycombinator.com/item?id=11603078>`_

Install the conda package manager
---------------------------------


Software **packages** and tools are pieces of software that have been developed to perform specific jobs, or are used to implement specific methods. Your general view of a software package may be something like Excel or Chrome or TikTok. More fundamentally, software is simply a group of instructions used to perform a specific task. In bioinformatics, for example, this could be a set of instructions telling the computer how to interpret and display the quality scores from a ``.fastq`` file.


*However*, software packages and tools often have **dependencies**, which are other pieces of software or tools that are necessary to run the software you would like to install. For example, to use Instagram, you also need software that controls your phone's camera. This reliance of Instagram on camera-controlling software is known as a **dependency**. Importantly, software like Instagram is designed to be **user-friendly**, and during installation will usually check that such camera-controlling software exists, and if it does not, may try to install it.

However, bioinformatics software, much of which is written by inexperienced computer scientists (or worse, biologists) often does not check for dependencies. This can create significant issues if you try to run a price of software but are missing dependencies (the other pieces of software that are also required).


To make sure that we resolve all these dependency issues, we will use a package/tool managing system. This managing system is called |conda|, and it is perhaps the most common package manager used in bioinformatics. The process of installing a software package is called a *recipe*, and these recipes are contained in places called *channels*. Most recipes for bioinformatic software is contained in the `bioconda <https://bioconda.github.io/>`_ channel, which currently has reciupes for more than 7000 software packages). |conda| is not installed by default, thus you need to install it first to be able to use it.

The installation of this tool is perhaps the most complicated installation we will do in this course. However, after the installation of |conda|, your life will become far easier and you will be on your way to becoming a seasoned bioinformatician (`binfie <https://soundcloud.com/microbinfie>`_).


.. code-block:: bash

    # download latest conda installer
    curl -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

**Explanation**: ``curl`` is a program that is used to transfer data to or from a server on the command line. Thus, this command is simply using this program to find the file at the location indicated. This file (with the extension ``.sh``) is a ``bash`` file, which is usually run using the command line program ``bash``.


.. Attention::
   Noting the *extension* of a file can be very helpful in figuring out what is in it, or what it does. For example, you should never end a ``bash`` file with ``.txt`` as that suggests it is a simple text file, when in fact it is not. Similarly, you would never end a Microsoft Word file with ``.xlsx``, you would end it with ``.doc`` or ``.docx``

.. code-block:: bash

    # run the installer
    bash Miniconda3-latest-Linux-x86_64.sh
    
    # delete the installer after successful run
    rm Miniconda3-latest-Linux-x86_64.sh


.. Tip::
   #. Ask yourself what ``rm`` means in the above command. Why should you be careful when using this command?
   #. The name ``Miniconda3-latest-Linux-x86_64.sh`` is quite long, will take you a while to type out, and you will be prone to making mistakes when typing it. What should you do instead of typing the full name?


.. Note::
   Should the conda installer download fail. Please find links to alternative locations on the
   :doc:`../downloads` page.

    
Update ``.bashrc`` and ``.zshrc`` config-files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before you are able to use |conda| you need to tell our shell where it can find the program.
We add the right path to the |conda| installation to our shell config files:

.. code::
   
   echo 'export PATH="/home/manager/miniconda3/bin:$PATH"' >> ~/.bashrc
   echo 'export PATH="/home/manager/miniconda3/bin:$PATH"' >> ~/.zshrc


.. Attention::
   The above assumes that your username is "manager", which is the default on a Biolinux install.
   Replace "manager" with your actual username.
   Find out with ``whoami``. (What does the ``whoami`` command do?)
   
.. Tip::
   #. What does ``echo`` mean in the above command?
   #. What does the ``>>`` do in the above command? (hint: google "redirect")
   #. What is inside of the "shell config files" (e.g. ``.bashrc``)?
   #. Why are the shell configuration files preceeded by a ``.``? What effect does this have? (hint: google "hidden file") 

**Explanation**: So what is actually happening here? We are appending a line to a file (either ``.bashrc`` or ``.zshrc``).
If you are starting a new command-line shell, either file gets executed first (depending on which shell you are using, either bash or zsh shells).
What this line does is to put permanently the directory ``~/miniconda3/bin`` first on your ``PATH`` variable. **Why** is this needed? Read on:

The ``PATH`` variable contains places (directories) in which your computer looks for  programs. These directories are listed one after the other. The computer will search these in the order they are listed until the program you requested is found (or not, then it will complain). For example, you might have a ``PATH`` variable that says: first look in my home directory (``~/``), and then in the ``/usr/bin/`` directory, and then in my friend's directory (``friends_dir/sneaky_files_i_saved_there/``). However, those are *the only* places the computer will look. If youwant the computer to look in more places, you have to add those locations to the ``PATH`` variable.


Through the addition of the above line you have now told the computer to also look in ``/home/manager/miniconda3/bin`` so that the program ``conda`` can be found anytime you open a new shell.


Finally, close the shell/terminal and open a **new** shell/terminal.
Now, you should be able to use the |conda| command. One useful way to check that |conda| (*or any other command line program*) is to ask what the program does. This is **almost always** done by typing ``--help`` or ``-h`` after the command. For example:


.. code-block:: bash

    conda --help

This will bring up a list of sub-commands that |conda| can do. Try it.


Next, make sure you have the current version of |conda|:


.. code-block:: bash

    conda update conda


Configure conda channels to make tools available
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The methods to install different tools are called recipes, and these are stored in what |conda| calls channels (as noted above). to make sure |conda| looks in the right places for these recipes, we need to tell it what channels to look in, and in wehat order to search them. This will make the bioinformatics and genomics tools easily find-able for installation:


.. code-block:: bash
    
    # Install some conda channels
    # A channel is where conda looks for recipes to install pakcages
    conda config --add channels defaults
    conda config --add channels bioconda 
    conda config --add channels conda-forge     

   
Create environments
-------------------

Now that we have a method to manage the installation of software packages (the |conda| *package manager*), there may be times that we want to have multiple different versions of a software tools installed (e.g. ``python 2.7`` and ``python 3.7``. In addition, there may be some software tools that *conflict* with other software tools. This creates a new problem for us. However, we can solve this by creating different |conda| environments. In these environments we can install only certain versions of a software tool, or only certain pieces of software.


.. code-block:: bash

    conda create -n ngs python=3
    # activate the environment
    conda activate ngs

    
So what is happening when you type ``conda activate ngs`` in a shell?
The ``PATH`` variable (mentioned above) gets temporarily manipulated and set to:


.. code-block:: bash
                
   $ conda activate ngs
   # Lets look at the content of the PATH variable
   (ngs) $ echo $PATH
   /home/manager/miniconda3/envs/ngs/bin:/home/manager/miniconda3/bin:/usr/local/bin: ...


The colons (``:``) in the above text indicate separations between the directory listings.

Now it will look first in your environment's ``bin/`` directory but afterwards in the general conda ``bin/`` (``/home/manager/miniconda3/bin``).
So basically everything you install generally with conda (without being in an environment) is also available to you but gets overshadowed if a similar program is in ``/home/manager/miniconda3/envs/ngs/bin`` and you are in the ``ngs`` environment.

The **huge** additional advantage of making separate |conda| environments in which you do your work is that it makes your work **reproducible**, as you can easily re-create the entire tool-set with exactly the same software versions numbers later on (e.g. years later, when the functionality of the current software version may have changed completely).

.. Tip::
   Ask yourself: What are all these ``bin/`` directories, and why are they called "bin"?


Install software
----------------

To install software into the activated environment, use the command ``conda install``.

.. code-block:: bash
         
    # install more tools into the environment
    conda install cool-new-package

.. Tip::
   Does this instruction *really* mean that you install all packages using the phrase "cool-new-package"?

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
    conda create -n [environment-name] package [package] ...

    # activate env
    conda activate [environment-name]

    # deavtivate env
    conda deactivate
