dnl Example for use of GNU gettext.
dnl This file is in the public domain.
dnl
dnl Configuration file - processed by autoconf.

AC_INIT
AC_CONFIG_SRCDIR(Hello.java)
AM_INIT_AUTOMAKE(hello-java-qtjambi, 0)

dnl Check whether we can build native executable.
dnl This does currently not work, since QtJambi requires a Java >= 1.5.
dnl AC_ARG_ENABLE(java-exe,
dnl   [  --enable-java-exe       compile Java to native code, not to bytecode],
dnl   :, enable_java_exe=no)
dnl gt_GCJ
dnl if test "$enable_java_exe" != no && test -n "$HAVE_GCJ"; then
dnl   BUILDJAVAEXE=yes
dnl else
dnl   BUILDJAVAEXE=no
dnl fi
BUILDJAVAEXE=no
AC_SUBST(BUILDJAVAEXE)
AM_CONDITIONAL([USEJEXE], [test "$BUILDJAVAEXE" = yes])
AC_PROG_RANLIB

dnl Check whether we can execute Java programs.
gt_JAVAEXEC([Test15], [$srcdir/m4])
dnl Check whether we can build Java programs.
gt_JAVACOMP([1.5], [1.5])
AC_CHECK_PROG(JAR, jar, jar)
if test -n "$HAVE_JAVACOMP" && test -n "$JAR"; then
  BUILDJAVA=yes
else
  BUILDJAVA=no
fi
AC_SUBST(BUILDJAVA)
if test -n "$HAVE_JAVAEXEC" && test "$BUILDJAVA" = yes; then
  TESTJAVA=yes
else
  TESTJAVA=no
fi
AC_SUBST(TESTJAVA)

dnl Checks for compiler output filename suffixes.
AC_OBJEXT
AC_EXEEXT

dnl Checks for needed libraries.
AM_PATH_PROG_WITH_TEST([GETTEXT_WITH_LIBINTL_JAR], [gettext],
  [{ basedir=`echo "$ac_dir" | sed -e 's,/bin$,,'`; test -r "$basedir"/share/gettext/libintl.jar; }])
if test -z "$GETTEXT_WITH_LIBINTL_JAR"; then
  echo "Required library libintl.jar not found." 1>&2
  exit 1
fi
changequote(,)dnl
basedir=`echo "$GETTEXT_WITH_LIBINTL_JAR" | sed -e 's,/[^/]*$,,' | sed -e 's,/bin$,,'`
changequote([, ])dnl
LIBINTL_JAR="$basedir"/share/gettext/libintl.jar
AC_SUBST([LIBINTL_JAR])

dnl Support for the po directory.
AM_PO_SUBDIRS

AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([javacomp.sh])
AC_CONFIG_FILES([javaexec.sh])
AC_CONFIG_FILES([m4/Makefile])
AC_CONFIG_FILES([po/Makefile], [AM_POSTPROCESS_PO_MAKEFILE])
AC_OUTPUT
