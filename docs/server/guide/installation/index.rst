Installation
*************

The examples below are for a typical Ubuntu/Debian system.

Installation of oZone libraries and examples
============================================

oZone is a portable solution with a very easy installation process.
This example assumes you want all the ozone libraries (including dependencies) to be installed at ~/ozoneroot.
This is a great way to isolate your install from other libraries you may already have installed.

.. code-block:: bash

	# -------------------install dependencies------------------------

	sudo apt-get update
	sudo apt-get install git cmake nasm libjpeg-dev libssl-dev 
	sudo apt-get install libatlas-base-dev

	# ---------------------clone codebase----------------------------

	git clone https://github.com/ozonesecurity/ozonebase
	cd ozonebase
	git submodule update --init --recursive

	# --------------- build & install --------------------------------
	export INSTALLDIR=~/ozoneroot/ # change this to whatever you want

	cmake -DCMAKE_INSTALL_PREFIX=$INSTALLDIR -DOZ_EXAMPLES=ON

	# Note, the above command builds a release version. To enable a debug build
	# add -DCMAKE_BUILD_TYPE=Debug -- this adds -g and -O0

	make 
	make install

	# ---- Optional: For ad-hoc in-source re-building----------------
	cd server
	cmake -DCMAKE_INSTALL_PREFIX=$INSTALLDIR -DOZ_EXAMPLES=ON
	make
	make install

	# ----- Optional: build nvrcli - a starter NVR example ----------
	cd nvrcli
	export LD_LIBRARY_PATH=$INSTALLDIR/lib/

	# modify the library and header file paths
	# in the Makefile to point to your path, then

	make

That's all!

Building Documentation
=======================
oZone documentation has two parts: 

* The API document that uses Doxygen
* The User Guide which is developed using Sphinx

API docs
---------
To build the APIs all you need is :code:`Doxygen` and simply run :code:`doxygen` inside :code:`ozonebase/server`.
This will generate HTML documents. oZone uses :code:`dot` to genarate API class and relationship graphs, so you should also install dot, which is typically part of the :code:`graphviz` package.

User docs
---------
You need sphinx and dependencies for generating your own user guide. The user guide source files are located in :code:`ozonebase/docs/server/guide` 

.. code-block:: bash

	# Install dependencies
	sudo apt-get install python-sphinx
	sudo apt-get install python-pip
	pip install sphinx_rtd_theme

And then all you need to do is :code:`make html` inside :code:`ozonebase/docs/server/guide` and it generates beautiful documents inside the :code:`build` directory.




Using oZone libraries in your own app
=========================================

Take a look at nvrcli's Makefile `here <https://github.com/ozonesecurity/ozonebase/blob/master/server/src/examples/nvrcli/Makefile>`_ and modify it for your needs.


