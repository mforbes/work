.. -*- rst -*- -*- restructuredtext -*-

.. This file should be written using the restructure text conventions.
.. It will be displayed on the bitbucket or github source page and
.. serves as the documentation of the project.

=============================
 Michael McNeil Forbes' Work
=============================

This is a meta-repository that contains ``mrconfig`` and ``mrfreeze`` files to
allow [myrepos](http://myrepos.branchable.com) to manage a collection of
all my work as subrepositories.  These can be stored under almost any type of
version control system.

.. contents::

Usage
=====
Here is how you can use a similar strategy:

Prerequisites
+++++++++++++

Install all the prerequisites:

* myrepos_ (``mr``)
* mercurial_ (``hg``)

One or more distributed version control systems (DVCs):

* git_, git-annex_, subversion_ (``svn``), bazaar_ (``bzr``), darcs_, ...

Mac OS X
--------

To install these on Mac OS X you can use MacPorts_ (``port``)
as follows::

   port install mercurial git subversion bazaar darcs

Only git-annex_ needs special attention, however, you might like to install the
application packages instead because the might come with some GUI goodies and
better integration with the operating system.  (There are other options: for
example, I install mercurial_ from within my python distribution with ``conda
install mercurial`` or ``pip install mercurial`` so that I do not need
MacPorts_ to install a second copy of python.)

Linux
-----

Most of these tools should be available with your favourite package manager.
Otherwise you can install them from source.

Windows
-------

I do not use windows, so I have no idea how to install these tools.  I think
most of them come with a windows installer.

Setup the ``~/work`` folder
+++++++++++++++++++++++++++

1. Create a folder for your work.  I use the convention of ``~/work`` on all of
   my machines, symlinking this as needed.  (Note: previously I use the folder
   ``hg_work``.  I am trying to remove this from everything, but it might still
   appear squirrelled away in a few places.)

2. Initialize it with your favourite version control tool.

3. Create a ``.mrconfig`` file.

4. Make a ``README.rst`` file.  If you host this on bitbucket_ or github_, then
   then this will provide the overview.  You can use any supported format you
   like, but I use ReStructuredText_ since it allows one to use math, hence the
   ``.rst`` extension.

.. code:: bash

   mkdir ~/work
   cd work
   hg init
   touch .mrconfig mrfreeze

   cat > README.rst <<"EOF"
   .. -*- rst -*- -*- restructuredtext -*-

   .. This file should be written using the restructure text conventions.
   .. It will be displayed on the bitbucket or github source page and
   .. serves as the documentation of the project.
   EOF

   cat > .hgignore <<"EOF"
   # Ignore everything except for files like README.rst, mrconfig and .hgignore
   syntax: glob
   *
   EOF

   hg add .hgignore .mrconfig README.rst
   hg com -m "Initialize work folder"

Regular Use
+++++++++++

The general cycle is ``clone``, ``register``, and then regularly ``freeze``.
When you need to work on a new repository, clone it here, then add it to the
``.mrconfig`` file.  For example, I might do the following::

   cd ~/work
   hg clone ssh://hg@bitbucket.org/mforbes/pymmf projects/pymmf
   mr register projects/pymmf
   mr freeze   # Optional: freezes the current versions to the mrfreeze file.
   hg com -m "Added and freeze pymmf"

The ``mr freeze`` part of the cycle is my custom addition which allows you to
tag exactly which version of each project you are using.  If needed, you and
revert to a particular state by ``hg update``, then ``mr unfreeze``.

.. _myrepos: http://myrepos.branchable.com
.. _mr: http://myrepos.branchable.com
.. _mercurial: http://mercurial.selenic.com
.. _hg: http://mercurial.selenic.com
.. _git: http://git-scm.com
.. _git-annex: https://git-annex.branchable.com
.. _subversion: http://subversion.apache.org
.. _svn: http://subversion.apache.org
.. _bazaar: http://bazaar.canonical.com/en/
.. _bzr: http://bazaar.canonical.com/en/
.. _darcs: http://darcs.net
.. _macports: https://www.macports.org
.. _bitbucket: http://bitbucket.org
.. _github: http://github.com
.. _ReStructuredText: http://docutils.sourceforge.net/rst.html
