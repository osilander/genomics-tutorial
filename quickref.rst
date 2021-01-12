Quick command reference
=======================

Shell commands
--------------

There is one fundamental aspect of using the command line that you **must never forget**. It is perhaps the single most powerful method available to save time. That method is...


**tab-complete**


Tab-complete can be used to auto-complete commands, directory names, and file names. If you are not sure whether your file is named ``results_QC.txt`` or ``results_qc.txt`` then oin the command line you can simply type ``results`` *and then tab*, and the computer will auto-complete the name (assuming there is a file or directory or command that begins with ``results``).


Other important commands.

.. code:: bash

    # Where in the directory tree am I?
    pwd

    # List the documents and sub-directories in the current directory
    ls

    # a bit nicer listing with more information
    ls -laF

    # Change into your home directory
    cd

    # Change back into the last directory
    cd -

    # Change one directory up in the tree
    cd ..

    # Change explicitly into a directory "temp"
    cd temp

    # Quickly show content of a file "temp.txt"
    # exist the view with "q", navigate line up and down with "k" and "j" and "spacebar"
    less temp.text

    # Show the first ten lines of a file "temp.txt"
    head temp.txt

    # Show the last ten lines of a file "temp.txt"
    tail temp.txt

    # I don't know a command means
    man unknown command

General conda commands
----------------------

.. code:: bash

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
