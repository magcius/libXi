
# Initialize Autoconf
AC_PREREQ([2.60])
AC_INIT([libXi], [1.6.99],
	[https://bugs.freedesktop.org/enter_bug.cgi?product=xorg], [libXi])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([src/config.h])

# Initialize Automake
AM_INIT_AUTOMAKE([foreign dist-bzip2])
AM_MAINTAINER_MODE

# Initialize libtool
AC_PROG_LIBTOOL

# Require xorg-macros minimum of 1.12 for DocBook external references
m4_ifndef([XORG_MACROS_VERSION],
          [m4_fatal([must install xorg-macros 1.12 or later before running autoconf/autogen])])
XORG_MACROS_VERSION(1.12)
XORG_DEFAULT_OPTIONS
XORG_ENABLE_DOCS
XORG_ENABLE_SPECS
XORG_WITH_XMLTO(0.0.22)
XORG_WITH_FOP
XORG_WITH_XSLTPROC
XORG_CHECK_SGML_DOCTOOLS(1.8)
XORG_WITH_ASCIIDOC(8.4.5)
XORG_CHECK_MALLOC_ZERO

# Obtain compiler/linker options for dependencies
PKG_CHECK_MODULES(XI, [xproto >= 7.0.13] [x11 >= 1.4.99.1] [xextproto >= 7.0.3] [xext >= 1.0.99.1] [inputproto >= 2.2.99.1])

# Check for xmlto and asciidoc for man page conversion
# (only needed by people building tarballs)
if test "$have_xmlto" = yes && test "$have_asciidoc" = yes; then
	have_doctools=yes
else
	have_doctools=no
fi
AM_CONDITIONAL([HAVE_DOCTOOLS], [test $have_doctools = yes])
if test $have_doctools = no; then
	AC_MSG_WARN([xmlto or asciidoc not found - cannot create man pages without it])
fi

# Determine if the source for man pages is available
# It may already be present (tarball) or can be generated using doctools
AM_CONDITIONAL([INSTALL_MANPAGES],
	[test -f "$srcdir/man/XAllowDeviceEvents.man" || \
	  test $have_doctools = yes])

AC_CONFIG_FILES([Makefile
		src/Makefile
		man/Makefile
		specs/Makefile
		xi.pc])
AC_OUTPUT
