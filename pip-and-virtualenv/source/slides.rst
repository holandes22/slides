virtualenv and pip
==================

Using virtualenv and pip as development tools


virtualenv intro
----------------

* **What is it?** A tool developed by Ian Bicking to create Python isolated environments
* **Why?** Think about two web applications living on the same server sharing dependencies (django for example).
  What if you want to update the dependencies of app1, but you don't want to break anything in app2.

virtualenv intro cont.
----------------------

virtualenv creates an environment that has its own installation directories and isolates itself from other virtual
environments.

This allows us to install a different set of dependencies (with regular user permissions) for each of application in the system.


virtualenv installation and usage
---------------------------------

virtualenv is in PyPI, so you can install it using pip (or easy_install if you leave in the stone age)

**As of python 3.3, virtualenv is included in the python standard library: PEP 405**

To create a virtualenv, simply run::

    $virtualenv venv

This creates all the activation scripts, add env to PATH, links to python libraries, etc

virtualenv usage cont.
----------------------

To activate the virtualenv::

    $source venv/bin/activate

Now, runnig the command **which** for python::

    $which python
    virtualenvs/venv/bin/python

Points to the interpreter from venv, instead of the system wide one.

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

pip - pip installs Python packages
----------------------------------

pip is another tool by Ian Bicking. Is a python package installer that comes to replace easy_install
providing improvements suchs requirement files and support for VCS.

pip is included in every virtualenv. 

pip - Why is better than easy_install
-------------------------------------

* All packages are downloaded before installation. Partially-completed installation doesn’t occur as a result.
* pip uninstall!!!
* Actively developed (easy_install has been dead for quite a while now)
* Care is taken to present useful output on the console and error messages are useful

pip - installing packages
-------------------------

Installing packages::

    pip install django

will install the latest django version available along with all it's dependencies

pip editables allows to install a package by adding it to sys.path, instead of copying the files. This is convenient when you depend on a project that
you are developing in parallel and it's bound to change a lot::

    pip install -e /my/cool/project

    
requirement files
-----------------

A pip requirement file::

    Django>=1.3.1
    cherrypy
    celery
    django-celery==1.0
    django-kombu
    -e git+https://github.com/user/project.git#egg=project


consistent recreation of enviroments
------------------------------------

Is highly recommended to pin everything to a version. Not pretty to have a dependency of a dependency changing and 
not knowing what went wrong.

pip freeze if useful to do this::

    $ pip freeze
    CherryPy==3.2.2
    Django==1.3.1
    amqplib==1.0.2
    celery==2.5.1
    django-celery==2.5.1
    django-kombu==0.9.4
    django-nose==0.1.3
    kombu==2.1.1

some tips
---------

You will probably end up installing the same packages over an over for each project.
for this, pip can cache the downloaded packages. In ~/pip/.pip.conf  put::

    [global]
    download-cache=/path/to/some/folder

What if PyPI is down?::

    [global]
    use-mirrors=true


The end
-------

To sum up, if you develope in python, use virtualenv and pip, it's going to make your life
much easier.
