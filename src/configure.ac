#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.67])
AC_INIT([octave instrument control package], [0.0.0+])
#AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CXX
AC_LANG(C++)

# Define macros needed
#AC_DEFINE(__STDC_CONSTANT_MACROS, [], [workaround for C++ programs to use C99 macros])

AC_CHECK_PROG([HAVE_MKOCTFILE], [mkoctfile], [yes], [no])
if [test $HAVE_MKOCTFILE = "no"]; then
  AC_MSG_ERROR([mkoctfile required to install $PACKAGE_NAME])
fi

TOBUILD=""

# Howto check if usbtmc is available?


# Checks for GPIB 
AC_CHECK_HEADERS([gpib/ib.h],
  [AC_SEARCH_LIBS([ibrd], [gpib],
    [AC_SUBST(BUILD_GPIB, [1])
      TOBUILD="$TOBUILD gpib"] , [])] , [] )

if test "x$ac_cv_search_ibrd" != "xnone required"; then
  AC_SUBST(GPIBLIBS, [$ac_cv_search_ibrd])
fi

# Checks for RPC/VXI11
AC_CHECK_PROG([HAVE_RPCGEN], [rpcgen], [yes], [no])
if test "x$HAVE_RPCGEN" = "xyes"; then
  AC_CHECK_HEADERS([rpc/rpc.h],
    [AC_SEARCH_LIBS([clnt_create], [tirpc],
      [AC_SUBST(BUILD_VXI11, [1])
        TOBUILD="$TOBUILD vxi11"], [])], [])

  if test "x$ac_cv_search_clnt_create" != "xnone required"; then
    AC_SUBST(RPCLIBS, [$ac_cv_search_clnt_create])
  fi
fi


# Checks for openvisa
AC_CHECK_HEADERS([visa/visa.h],
  [AC_SEARCH_LIBS([viOpenDefaultRM], [openvisa], 
    [AC_SUBST(BUILD_VISA, [1])
      TOBUILD="$TOBUILD visa"] , [])] , [] )

if test "x$ac_cv_search_viOpenDefaultRM" != "xnone required"; then
  AC_SUBST(VISALIBS, [$ac_cv_search_viOpenDefaultRM])
fi


AC_SUBST(TOBUILD)
# all done

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

AC_MSG_NOTICE([

$PACKAGE_NAME is now configured with

   TOBUILD:           $TOBUILD

   BUILD GPIB:        $BUILD_GPIB
       LIBS:          $GPIBLIBS
       
   BUILD VXI11:       $BUILD_VXI11
       LIBS:          $VXI11LIBS
       
   BUILD VISA:        $BUILD_VISA
       LIBS:          $VISALIBS

])