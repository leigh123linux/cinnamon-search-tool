dnl -*- mode: m4 -*-
AC_PREREQ([2.63])
AC_INIT([cinnamon-search-tool],
        [3.6.1],
        [http://bugzilla.gnome.org/enter_bug.cgi?product=cinnamon-search-tools],
        [cinnamon-search-tool])

AC_CONFIG_HEADERS(config.h)
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([1.11 foreign dist-xz no-dist-gzip tar-ustar])
AM_MAINTAINER_MODE([enable])

AM_SILENT_RULES([yes])

GETTEXT_PACKAGE=AC_PACKAGE_NAME
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE",[The name of the gettext domain])
IT_PROG_INTLTOOL(0.40.0)
PKG_PROG_PKG_CONFIG([0.22])

AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.17])

# Check for programs
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CXX
AC_HEADER_STDC

# enable libtool
LT_PREREQ([2.2])
LT_INIT([disable-static])

## don't rerun to this point if we abort
AC_CACHE_SAVE

GLIB_GSETTINGS

# User documentation
YELP_HELP_INIT

dnl strftime extension checks
msg_strftime=no

AC_RUN_IFELSE(
  [AC_LANG_SOURCE([[
  #include <time.h>
  int main (void) {
    char buf[100];
    struct tm tm = {0};
    tm.tm_year = 99;
    if (strftime(buf, 100, "%EY", &tm) == 4 && strcmp (buf, "1999")==0)
      return 0;
    return 1;
  }
  ]])],[
    AC_DEFINE([HAVE_STRFTIME_EXTENSION], [1],
              [Define if strftime supports %E and %O modifiers.])
    msg_strftime=yes
  ],
  [],[])

withval=""
AC_ARG_WITH([grep],
            AS_HELP_STRING([--with-grep=@<:@grep command@:>@],
                           [Specify where to find the grep binary]),
            [
              AS_IF([test x$withval != x],
                    [AC_MSG_RESULT(${withval} is used for cinnamon-search-tool.)],

                    [AC_MSG_RESULT(grep is used for cinnamon-search-tool.)]
              )
            ])

AS_IF([test x$withval != x],
      [GREP_COMMAND="$withval"],

      [GREP_COMMAND="grep"]
)

AC_SUBST(GREP_COMMAND)

GLIB_MIN_VERSION=2.30.0
GIO_MIN_VERSION=2.30.0
GTK_MIN_VERSION=3.0.0

PKG_CHECK_MODULES(GSEARCHTOOL,
                  gio-unix-2.0 >= $GIO_MIN_VERSION
                  gio-2.0 >= $GIO_MIN_VERSION
                  glib-2.0 >= $GLIB_MIN_VERSION
                  gtk+-3.0 >= $GTK_MIN_VERSION)

AC_CONFIG_FILES([
Makefile
data/Makefile
help/Makefile
libeggsmclient/Makefile
libgnomeui-deprecated/Makefile
src/Makefile
po/Makefile.in
])

AC_OUTPUT

dnl ==========================================================================
echo "

        CINNAMON Search Tool $VERSION
        ==========================

        prefix:    ${prefix}
        compiler:  ${CC}

        grep command: ${GREP_COMMAND}
        Use strftime extension: ${msg_strftime}

        Now type 'make' to build $PACKAGE
"
