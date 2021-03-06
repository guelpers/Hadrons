AC_PREREQ([2.63])
AC_INIT(Hadrons,[v1.0],[antonin.portelli@ed.ac.uk],[hadrons])
AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_CANONICAL_TARGET
AC_CONFIG_SRCDIR([Hadrons/Global.cpp])
AC_CONFIG_MACRO_DIR([.buildutils/m4])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([-Wall -Werror foreign subdir-objects])
AM_EXTRA_RECURSIVE_TARGETS([tests])
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AC_ARG_WITH([grid],
    [AS_HELP_STRING([--with-grid=<prefix>],
    [try this for a non-standard install prefix of Grid])],
    [PATH="$with_grid/bin$PATH_SEPARATOR$PATH"]
    [CXXFLAGS="$CXXFLAGS -I$with_grid/include"]
    [LDFLAGS="$LDFLAGS -L$with_grid/lib"])

AC_CHECK_PROG([GRIDCONF],[grid-config],[yes])
if test x"$GRIDCONF" != x"yes" ; then
    AC_MSG_ERROR([grid-config not found])
fi
CXXFLAGS="$CXXFLAGS `grid-config --cxxflags`"
LDFLAGS="$LDFLAGS `grid-config --ldflags`"
CXXFLAGS="$AM_CXXFLAGS $CXXFLAGS"
LDFLAGS="$AM_LDFLAGS $LDFLAGS"
LIBS=" -lGrid $LIBS `grid-config --libs`"

AC_PROG_CXX
AC_PROG_RANLIB
AM_PROG_AR
AC_LANG([C++])

AC_MSG_CHECKING([that a minimal Grid program compiles]);
AC_LINK_IFELSE(
	[AC_LANG_SOURCE([[
    #include <Grid/Grid.h>
    
    using namespace Grid;
    
    int main(int argc, char *argv[])
    {
        Grid_init(&argc, &argv);
        Grid_finalize();
        
        return 0;
    }
    
    ]])],
	[AC_MSG_RESULT([yes])],
    [AC_MSG_RESULT([no])]
    [AC_MSG_ERROR([impossible to compile a minimal Grid program])])

AC_SUBST([AM_CXXFLAGS])
AC_SUBST([AM_LDFLAGS])
AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([Hadrons/Makefile])
AC_CONFIG_FILES([utilities/Makefile])
AC_CONFIG_FILES([tests/Makefile])
AC_OUTPUT
