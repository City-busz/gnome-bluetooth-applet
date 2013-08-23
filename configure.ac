AC_PREREQ(2.52)

AC_INIT([bluetooth-panel-applet], [3.6.0])

AC_CONFIG_SRCDIR([applet/main.c])
AC_CONFIG_HEADERS([config.h])

AM_INIT_AUTOMAKE([1.11 foreign dist-xz no-dist-gzip tar-ustar])

# Before making a release, the GNOMEBT_LT_VERSION string should be modified.
# The string is of the form C:R:A.
# - If interfaces have been changed or added, but binary compatibility has
#   been preserved, change to C+1:0:A+1
# - If binary compatibility has been broken (eg removed or changed interfaces)
#   change to C+1:0:0
# - If the interface is the same as the previous version, change to C:R+1:A
GNOMEBT_LT_VERSION=11:0:0
AC_SUBST(GNOMEBT_LT_VERSION)

AM_MAINTAINER_MODE

# Support silent build rules, requires at least automake-1.11. Disable
# by either passing --disable-silent-rules to configure or passing V=1
# to make
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_LANG_C
AC_PROG_CC
AC_PROG_INSTALL

dnl Initialize libtool
AM_DISABLE_STATIC
AM_PROG_LIBTOOL

# i18n stuff
IT_PROG_INTLTOOL([0.40.0])

AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.17])

GETTEXT_PACKAGE=bluetooth-panel-applet
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE",
					[The name of the gettext domain])

AC_DEFINE_UNQUOTED(LOCALEDIR, "${prefix}/share/locale", [Directory for the localization files])

GTK_REQUIRED=2.91.3
GLIB_REQUIRED=2.29.90
GNOME_BLUETOOTH_REQUIRED=3.8.0
NOTIFY_REQUIRED=0.7.0

dnl Requires for the properties window
PANELS_DIR="${libdir}/control-center-1/panels"
AC_SUBST(PANELS_DIR)

dnl Missing libgnome-control-center
dnl which will be resolved at run-time
PKG_CHECK_MODULES(PROPS,
		  glib-2.0 >= $GLIB_REQUIRED
		  gnome-bluetooth-1.0 >= $GNOME_BLUETOOTH_REQUIRED
		  gtk+-3.0 >= $GTK_REQUIRED)

dnl Requires for the applet
PKG_CHECK_MODULES(APPLET,
		  gmodule-export-2.0
		  glib-2.0 >= $GLIB_REQUIRED
		  gnome-bluetooth-1.0 >= $GNOME_BLUETOOTH_REQUIRED
		  gtk+-3.0 >= $GTK_REQUIRED
		  libnotify >= $NOTIFY_REQUIRED)

AC_MSG_CHECKING([for gnome-bluetooth-applet])
PKG_CHECK_EXISTS([gnome-bluetooth-1.0 >= 3.9.0],
        [GNOME_BLUETOOTH_APPLET_DIR=`$PKG_CONFIG --variable=applet_libdir gnome-bluetooth-1.0`
	 GNOME_BLUETOOTH_APPLET_LIBS=`$PKG_CONFIG --variable=applet_libs gnome-bluetooth-1.0`
	 AC_SUBST([GNOME_BLUETOOTH_APPLET_LIBS],["$GNOME_BLUETOOTH_APPLET_LIBS"])
	 AC_SUBST([GNOME_BLUETOOTH_APPLET_DIR],["$GNOME_BLUETOOTH_APPLET_DIR"])
	 AC_DEFINE_UNQUOTED([GNOME_BLUETOOTH_APPLET_DIR],["$GNOME_BLUETOOTH_APPLET_DIR"],[Path to installed GnomeBluetooth typelib and library])
	 AC_DEFINE([HAVE_BLUETOOTH],[1],[Define if you have libgnome-bluetooth-applet])
	 AC_SUBST([HAVE_BLUETOOTH],[1])
	 AC_MSG_RESULT([yes])],
	[AC_DEFINE([HAVE_BLUETOOTH],[0])
	 AC_SUBST([HAVE_BLUETOOTH],[0])
	 AC_MSG_RESULT([no])])


AC_CHECK_LIBM
AC_SUBST(LIBM)

GNOME_COMMON_INIT
GNOME_DEBUG_CHECK
GNOME_COMPILE_WARNINGS([maximum])
GNOME_CXX_WARNINGS
GNOME_MAINTAINER_MODE_DEFINES

AC_ARG_ENABLE([documentation],
	AS_HELP_STRING([--enable-documentation], [enable man pages and HTML]),
	[], [enable_documentation=yes])
AM_CONDITIONAL(ENABLE_DOCUMENTATION, test x$enable_documentation = xyes)

YELP_HELP_INIT

AC_OUTPUT(Makefile
	  applet/Makefile
	  applet/bluetooth-applet.desktop.in
	  properties/Makefile
	  properties/bluetooth-properties.desktop.in
	  properties/cut-n-paste/Makefile
	  po/Makefile.in
	  help/Makefile
)

echo "
Configure summary:

	Compiler....................:  ${CC}
	Compiler Flags..............:  ${CFLAGS}
	Prefix......................:  ${prefix}
"

