#
# Makefile for SWIG processing of SNAP Python
#	Use this Makefile to compile SNAP Python from scratch
#
# Build instructions for Mac OS X and Linux:
#		make
#		make dist
# 
# Build instructions for Windows:
#	- run swig in Cygwin to generate snap_wrap.cxx and snap.py
#		make swig-win
#	- build Snappy solution in Visual Studio to generate _snap.pyd
#	- run setup.py in Cygwin to generate the package,
#	  NOT OVER SSH, but locally
#		make dist-win

# set the path to your SNAP directory here
GITDIR = ../../snap
SNAPDIR = $(GITDIR)/$(SNAP)
GLIBDIR = $(GITDIR)/$(GLIB)

# include compilation parameters
include $(GITDIR)/Makefile.config
include ../Makefile.config

all: snap.py _snap.so

snap_wrap.cxx: snap.i snap_types.i tvec.i pneanet.i pungraph.i pngraph.i pgraph.i \
	snapswig.h snap_types.h printgraph.h goodgraph.cpp
	swig $(SWIGFLAGS) -python -c++ -w302,312,317,325,362,383,384,389,401,503,508,509 -O -I$(SNAPDIR) -I$(GLIBDIR) snap.i

snap_wrap.o: snap_wrap.cxx
	g++ $(CXXFLAGS) -c snap_wrap.cxx -I$(SNAPDIR) -I$(GLIBDIR)  -I/usr/include/python2.6 -I/usr/include/python2.7

Snap.o: 
	$(CC) $(CXXFLAGS) -c $(SNAPDIR)/Snap.cpp -I$(SNAPDIR) -I$(GLIBDIR)

_snap.so: snap_wrap.o Snap.o
	g++ $(LDFLAGS) -o _snap.so snap_wrap.o Snap.o $(LIBS)

snap.py: snap_wrap.cxx

install: setup.py snap.py _snap.so
	sudo python setup.py install

dist: setup.py snap.py _snap.so
	cp MANIFEST.nx MANIFEST
	python setup.py sdist

swig-win: snap_wrap.cxx

install-win: setup.py snap.py _snap.pyd
	/cygdrive/c/Python27/python.exe setup.py install

dist-win: setup.py snap.py _snap.pyd
	cp MANIFEST.win MANIFEST
	/cygdrive/c/Python27/python.exe setup.py sdist

clean:
	rm -f *.o *_wrap.cxx _*.so *.pyc snap.py _snap.*

