DEF_SUBDIRS = applet po properties help

SUBDIRS = applet po properties

if ENABLE_DOCUMENTATION
SUBDIRS += help
endif

EXTRA_DIST = intltool-extract.in intltool-update.in intltool-merge.in

DISTCLEANFILES = intltool-extract intltool-update intltool-merge

MAINTAINERCLEANFILES = \
	Makefile.in \
	aclocal.m4 \
	config.guess \
	config.h.in \
	config.sub \
	configure \
	depcomp \
	install-sh \
	intltool-extract.in \
	intltool-merge.in \
	intltool-update.in \
	ltmain.sh \
	missing \
	mkinstalldirs
