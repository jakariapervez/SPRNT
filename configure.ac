# A few checks to make sure we have required components
# 
# The configure file will not be removed and should be fairly portable
# To create new configure file, do the following:
#    aclocal -I . 
#    autoconf
#
# use -I flag to make sure that the local m4 will be used.

AC_INIT(sprint_config, version_0.9)
AC_MSG_NOTICE([Checking required libraries for SPRNT])

AC_PREFIX_DEFAULT([.])

# need compilers
AC_PROG_CC
AC_PROG_CXX
AC_PROG_F77

# of course
AC_CHECK_TOOL(MAKEB, make, [
    AC_MSG_ERROR([need make to continue...])
])

# need library utilies
AC_CHECK_TOOL(RANLIB, ranlib, [
    AC_MSG_ERROR([need ranlib to continue ...])
])

AC_CHECK_TOOL(AR, ar, [
    AC_MSG_ERROR([need ar to continue ...])
])

# need curl to fetch dependencies
AC_CHECK_PROG(CURL_CHECK,curl,yes)
if test x"$CURL_CHECK" != x"yes" ; then
    AC_MSG_ERROR([need curl to continue ...])
fi

# need dirname for shell scripts
AC_CHECK_PROG(DIRNAME_CHECK,dirname,yes)
if test x"$DIRNAME_CHECK" != x"yes" ; then
    AC_MSG_ERROR([need dirname to continue ...])
fi

# need realpath for shell scripts
AC_CHECK_PROG(REALPATH_CHECK,realpath,yes)
if test x"$REALPATH_CHECK" != x"yes" ; then
    AC_MSG_ERROR([need realpath to continue ...])
fi

# math library should be here, just in case 
AC_CHECK_LIB(m,cbrt,[],[
   AC_MSG_ERROR([something is wrong with the math lib -m ...]);
])

# check libgfortran, should be installed with gfortran
AC_CHECK_LIB(gfortran,_gfortran_fget,[],[
   AC_MSG_ERROR([unable to locate libgfortran]);
])

# we also need blas
AC_CHECK_LIB(blas,dnrm2_,[],[
   AC_MSG_ERROR([unable to locate the blas library]);
])

# check if c++0x is available
#  if yes, use <unordered_map> for string->integer mapping
#  if not, use <map> (about twice as slow as <unordered_map>)
AX_LOC_CXX_COMPILE_STDCXX_0X

AC_CONFIG_FILES([
Make.rules
Makefile
])

AC_OUTPUT

AC_MSG_NOTICE([==============================================================])
AC_MSG_NOTICE([Required libraries seem to be in place ...... ])
AC_MSG_NOTICE([Build the thirdparty libraries before])
AC_MSG_NOTICE([building SPRNT. Steps: ])
AC_MSG_NOTICE([ make dep])
AC_MSG_NOTICE([ make ])
AC_MSG_NOTICE([ make test (optional)])
AC_MSG_NOTICE([ make install])
AC_MSG_NOTICE([Options to clean])
AC_MSG_NOTICE([ make uninstall - as the name says])
AC_MSG_NOTICE([ make clean     - clean the libraries only ])
AC_MSG_NOTICE([ make realclean - linbraries + binary])
AC_MSG_NOTICE([ make distclean - remove downloadd 3rd party components and Make files])
AC_MSG_NOTICE([==============================================================])

## we are done
