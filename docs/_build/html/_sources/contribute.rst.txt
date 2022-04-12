.. Copyright 2022 Lawrence Livermore National Security, LLC

.. _contribute:

===========================
Contribute to Existing Docs
===========================

To contribute to a repo that already has Sphinx/RtD set up, you will need to initiate a temporary virtual environment where you can build docs locally before pushing your changes.

------------------------
Install requirements.txt
------------------------
After forking/cloning the repo normally, locate the ``requirements.txt`` file in the project directory and navigate into that folder.

Create a virtual environment for the repo's docs::

    $ pipenv install -r requirements.txt

.. note::

    * An error means a requirement is missing from your system or you are not in the correct directory.
    * A repo's *gemfile* says what you need to install; the *lockfile* conveys the particular versions needed.

Activate the virtual environment::

    $ pipenv shell

------------------
Build Docs Locally
------------------

Build the docs as static HTML files for editing::

    $ pipenv run make html

The resulting information should indicate that the docs are ready in ``_build/html``.

.. note::

    * Run this in the directory where the ``Makefile`` lives.
    * Run this again after installing any missing requirements.
    * Run this when you want to view the docs (i.e., as a QA check before committing and opening a PR).
    * Run this whenever you need to rebuild docs (e.g., after un-staging a staged file).
    * Prepend ``pipenv run`` when building docs via a virtual environment (otherwise, it would just be ``make html``).

You can open a file in your browser to QA your changes::

    $ open _build/html/Filename.html

Commit your edits and submit a PR normally.

---------------------
When Finished Editing
---------------------

You may want to update your ``.gitignore`` file with any changes to system files that you do not want committed.

Exit the virtual environment before switching to another repo by pressing ``ctrl-d``. *If you don't do this, repo B will look at the requirements in repo A instead of finding its own.*
