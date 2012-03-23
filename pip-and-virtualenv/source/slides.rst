virtualenv and pip
==================

Using virtualenv and pip as development tools


virtualenv intro
----------------

* **What is it?** A tool developed by Ian Bicking to create Python isolated environments
* **Why?** Think about two web applications living on the same server which share some dependencies (django for instance).
  What if you want to update the dependencies of app1, but you don't want to break anything in app2.
  This is where virtualenv comes to the rescue.

virtualenv intro cont.
----------------------

virtualenv creates an environment that has its own installation directories and isolates itself from other virtual
environments. The environment contains a site-packages directory, installs setuptools (pip and virtualenv) and a Python 
interpreter that is aware of its environment.

This allows us to install a different set of dependencies (with regular user permissions) for each of application in the system.


virtualenv installation and usage
---------------------------------

virtualenv is in PyPI, so you can install it using pip (or easy_install if you leave in the stone age)

To create a virtualenv, simply run::

    $virtualenv venv

This creates all the activation scripts, add env to PATH, links to python libraries, etc

virtualenv usage cont.
----------------------

To activate the virtualenv::

    $source venv/bin/activate

Now, runnig the command which on python::

    $which python
    virtualenvs/venv/bin/python

I now points to the interpreter from venv, instead of the system wide one.

virtualenv and site-packages
----------------------------

By default, virtualenv inherits the packages from the system's default site-packages directory. This is good when there
are tools that you know you will use in every project (ipython, sphinx, mock, etc) so you won't have to install them
separetly for every virtualenv.

But, you can still override this if you want so::

    $virtualenv --no-site-packages venv

will create an environment without the system's site-pakages

vitualenv outro
---------------

**That is it, all you basically need to know to use virtualenv.**
For more advance features, such as creating boostraping scripts that can be run after each install, visit virtualenv.org
You can also check virtualenvwrapper, a set of tools that provide some nice wrappers and hooks for virtualenv. Can be
found at PyPI.

virtualenv future
-----------------

todo: sacar de pycon sunday morning lightning talks, frank meyer (~minuto 13)


pip
---
