AC_PREREQ([2.63])

AC_INIT([spice-common],
        [noversion],
        [spice-devel@lists.freedesktop.org])

AC_CONFIG_SRCDIR([common/bitops.h])
AC_CONFIG_MACRO_DIR([m4])
AM_CONFIG_HEADER([config.h])
AC_CONFIG_AUX_DIR([build-aux])

# For automake >= 1.12
m4_ifdef([AM_PROG_AR], [AM_PROG_AR])

# For autoconf <= 2.63
m4_ifndef([AS_VAR_APPEND],
          AC_DEFUN([AS_VAR_APPEND], $1=$$1$2))

# Checks for programs
AM_INIT_AUTOMAKE([1.11 dist-xz no-dist-gzip tar-ustar foreign -Wall -Werror])
AM_MAINTAINER_MODE
AM_SILENT_RULES([yes])
LT_INIT

AC_PROG_CC
AC_PROG_CC_C99
if test "x$ac_cv_prog_cc_c99" = xno; then
    AC_MSG_ERROR([C99 compiler is required.])
fi
AM_PROG_CC_C_O

SPICE_CHECK_SYSDEPS

# Checks for libraries
AC_CONFIG_SUBDIRS([spice-protocol])
PROTOCOL_CFLAGS='-I ${top_srcdir}/spice-protocol'
AC_SUBST(PROTOCOL_CFLAGS)

SPICE_CHECK_PYTHON_MODULES()

SPICE_CHECK_PIXMAN(SPICE_COMMON)
SPICE_CHECK_SMARTCARD(SPICE_COMMON)
SPICE_CHECK_CELT051(SPICE_COMMON)
SPICE_CHECK_GLIB2(SPICE_COMMON)
SPICE_CHECK_OPUS(SPICE_COMMON)
SPICE_CHECK_OPENGL(SPICE_COMMON)
AC_SUBST(SPICE_COMMON_CFLAGS)
AC_SUBST(SPICE_COMMON_LIBS)

# The End!
AC_CONFIG_FILES([
  Makefile
  common/Makefile
  python_modules/Makefile
])

AH_BOTTOM([
/* argh.. this is evil */
#if defined(FIXME_SERVER_SMARTCARD) && defined(USE_SMARTCARD)
%:undef USE_SMARTCARD
#endif
])

AC_OUTPUT
