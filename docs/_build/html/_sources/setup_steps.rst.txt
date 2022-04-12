.. Copyright 2022 Lawrence Livermore National Security, LLC

.. _setup_steps:

=========================
Steps for Setting up Docs
=========================

The process of creating a Read the Docs (RtD) site is widely documented (see also :ref:`resources`), though your local environment will introduce variables. The examples that follow use ``pipenv`` as one variation.

The basic steps are:

#. Create repo on GitHub or create local directory to existing repo
#. Install Sphinx
#. Build and configure doc files
#. Set up GitHub and RtD webhook integration
#. Create .rst files

------------------------
1. Create Repo/Directory
------------------------

The instructions below assume that developers understand step 1.

-----------------
2. Install Sphinx
-----------------

* Create a **/docs** folder in your project. Then ``cd docs`` to complete most of the remaining steps (exceptions are noted below).
* Install `RtD template from GitHub <https://github.com/readthedocs/sphinx_rtd_theme>`_ using Sphinx (``pipenv install sphinx-rtd-theme``).
* Initiate Sphinx quickstart (``pipenv run sphinx-quickstart``). Answer the questions that follow installation, such as selecting No for setting up build and source separately.
* Move the makefile into the ``/docs`` folder if it's not there already.
* Confirm the Sphinx version (``pipenv run sphinx-build --version``).
* Confirm that docs can build locally (``pipenv run make html``). You must be in the ``/docs`` directory for this to work. Unlike viewing a site on a local port, where newly saved changes auto-regenerate the site, you will need to run this command after every saved change in order to see the new change.

--------------------------------
3. Build and Configure Doc Files
--------------------------------

* Update the **conf.py** file. For instance, you can change the RtD theme (``html_theme``). In the General Configuration section, add the name of master .rst file::

    # Tells Sphinx the name of the master .rst file.
    master_doc = 'index'

* Create the **.gitignore** file (``touch .gitignore``) so your commits will include only source files, not the HTML-rendered files (`GitHub instructions <https://help.github.com/en/articles/ignoring-files>`_).
* Create the **requirements.txt** file to specify dependency versions (`RtD instructions <https://docs.readthedocs.io/en/stable/config-file/v2.html?highlight=requirements.txt#requirements-file>`_). This file usually contains information like this::

    # These dependencies should be installed using pip in order
    # to build the documentation.

    sphinx==2.0.1
    sphinxcontrib-programoutput==0.14
    sphinx-rtd-theme==0.4.3
    python-levenshtein

* Create the **.readthedocs.yml** file in the *top directory* of the repo. Paste in the `V2 content <https://docs.readthedocs.io/en/stable/config-file/v2.html>`_.
* Commit configuration changes, then open and merge PR before moving on.

--------------------------------
4. Establish Webhook Integration
--------------------------------

This process generates a **readthedocs.io** URL for your project, which you can then link to in your repo's README file.

* Log into the `RtD website <https://readthedocs.org/>`_ via your GitHub account. You will have to go through an account verification process the first time.
* My Projects > Import a Project > select your repo. You may need to refresh the list or filter out an organization.
* Enter repo name and GitHub URL if not pre-populated. Confirm **.git** is appended to the end of the URL.
* Follow `webhook creation instructions <https://docs.readthedocs.io/en/stable/webhooks.html#webhook-creation>`_. When you try to build the docs for the first time, you may get an error: *fatal: could not read Username for 'https://github.com': terminal prompts disabled*. So you must configure the webhook to recognize GitHub's 2FA via ``git config --global --add url."git@github.com:".insteadOf "https://github.com/"``.
* Add doc build status to your repo's README file. Open the file and paste in the badge syntax (where **name** is your repo)::

    [![Documentation Status](https://readthedocs.org/projects/name/badge/?version=latest)](https://name.readthedocs.io/en/latest/?badge=latest)

* Confirm that docs still build locally, then open and merge PR.
* On your RtD dashboard, select the project and initiate a build to test: Projects > your repo > Builds > Build Version.
* You may want to change some of RtD's advanced settings, such as specifying which version is considered "latest" or which branch is the default. Don't forget to update this area if you change the name of your default branch (e.g., ``master`` to ``main``). Projects > your repo > Admin > Advanced Settings. 

---------------------------------
5. Create and Populate .rst Files
---------------------------------

All documentation files should contain your repo's copyright date(s) and license information at the top, set off by two periods (``..``).

* Create the **index.rst** file (or whatever file name you specified as the master file in step *C1* above).
* Set up table of contents (TOC), specifying how many levels deep you want to expose. For example, this site's TOC looks like this::   

    .. toctree::
       :maxdepth: 2
       :caption: Contents:

       setup_steps
       resources

* Create subordinate .rst files with reference to the link you established in the TOC. The page doesn't have to have the same title as the file name. For example, this page is titled *Steps for Setting up Docs* while the TOC linkage is based on the file name of **setup_steps.rst**::

    .. _setup_steps:

* Now you can begin a cycle of adding/editing files, building locally, and pushing to GitHub. The configuration settings above should trigger automatic RtD builds with every commit or PR, but you can always manually build the docs site from your RtD dashboard.

^^^^^^
Images
^^^^^^

Adding inline images to your documentation is as simple as saving, then referencing, the image file at the proper level of the repo directory. This repo's images reside in the ``/docs`` folder.

*Favicon* (displays in the browser tab); in the ``confy.py`` file, add the image file name::

    html_favicon = 'OS-icon-color.png'

*Home image* (displays in the top left corner), also in the ``confy.py`` file::

    html_logo = 'OS-logo-horizontal-white.png'

*Inline image*, for which you can specify dimensions and alignment::

    .. image:: OS-inline-example.png
        :width: 400px
        :align: center

.. image:: OS-inline-example.png
        :width: 400px
        :align: center
