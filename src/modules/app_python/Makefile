# 
# WARNING: do not run this directly, it should be run by the main Makefile

include ../../Makefile.defs
auto_gen=
NAME=app_python.so

# If you have multiple Python versions installed make sure to modify the
# the following to point to the correct instance. Module has been tested
# to work with 2.6 and 2.5. Python 2.4 has been only confirmed to compile,
# but no testing has been done with that.
PYTHON=$(shell which python2)

# workaround for some OS (like MacOS) that don't have a python2 link
ifeq ($(PYTHON),)
PYTHON=$(shell which python2.7)
ifeq ($(PYTHON),)
PYTHON=python
endif
endif

PYTHON_VERSION=${shell ${PYTHON} -c "import distutils.sysconfig;print distutils.sysconfig.get_config_var('VERSION')"}
PYTHON_LIBDIR=${shell ${PYTHON} -c "import distutils.sysconfig;print distutils.sysconfig.get_config_var('LIBDIR')"}
PYTHON_LDFLAGS=${shell ${PYTHON} -c "import distutils.sysconfig;print distutils.sysconfig.get_config_var('LINKFORSHARED')"}
PYTHON_INCDIR=${shell ${PYTHON} -c "import distutils.sysconfig;print distutils.sysconfig.get_python_inc()"}

LIBS=-L${PYTHON_LIBDIR} ${PYTHON_LDFLAGS} -lpython${PYTHON_VERSION}

ifeq ($(OS), freebsd)
LIBS+=-pthread
endif

DEFS+=-I${PYTHON_INCDIR}

ifeq ($(CC_NAME), gcc)
DEFS+= -fno-strict-aliasing
endif

include ../../Makefile.modules

