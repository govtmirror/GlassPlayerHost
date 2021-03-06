dnl configure.ac
dnl
dnl Autoconf configuration
dnl
dnl Use autoconf to process this into a configure script
dnl
dnl   (C) Copyright 2014-2016 Fred Gleason <fredg@paravelsystems.com>
dnl
dnl   This program is free software; you can redistribute it and/or modify
dnl   it under the terms of the GNU General Public License version 2 as
dnl   published by the Free Software Foundation.
dnl
dnl   This program is distributed in the hope that it will be useful,
dnl   but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl   GNU General Public License for more details.
dnl
dnl   You should have received a copy of the GNU General Public
dnl   License along with this program; if not, write to the Free Software
dnl   Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
dnl

AC_INIT(glassplayerhost,m4_esyscmd(cat PACKAGE_VERSION))
AM_INIT_AUTOMAKE
AC_SUBST(RPM_RELEASE,1)
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

#
# Basic Compiler Checks
#
AC_PROG_CXX
AC_LANG(C++)

# to avoid rpath usage :
# http://wiki.debian.net/index.cgi?RpathIssue
case ${host} in
  *-pc-linux-gnu)
    AC_MSG_RESULT([Fixing libtool for -rpath problems.])
    sed < libtool > libtool-2 \
    's/^hardcode_libdir_flag_spec.*$/hardcode_libdir_flag_spec=" -D__LIBTOOL_IS_A_FOOL__ "/'
    mv libtool-2 libtool
    chmod 755 libtool
  ;;
esac

#
# Option Switches
#
AC_ARG_ENABLE(docbook,[  --disable-docbook       disable building of DocBook documentation],[DOCBOOK_DISABLED=yes],[])

#
# Check for Qt (Mandatory)
#
PKG_CHECK_MODULES(QT4,QtGui QtCore QtNetwork,[],[AC_MSG_ERROR([*** Qt4 not found ***])])
AC_CHECK_PROG(MOC_NAME,moc-qt4,[moc-qt4],[moc])
AC_SUBST(MOC,$MOC_NAME)

#
# Check for WebHost (Mandatory)
#
PKG_CHECK_MODULES(WEBHOST,webhost,[],[AC_MSG_ERROR([*** WebHost not found ***])])

#
# Check for DocBook Toolchain
#
if test -z $DOCBOOK_DISABLED ; then
  USING_DOCBOOK=yes
fi
AM_CONDITIONAL([DOCBOOK_AM], [test "$USING_DOCBOOK" = yes])

#
# Determine the target architecture
#
AR_GCC_TARGET()
AC_SUBST(VENDOR,$ar_gcc_distro)
AC_SUBST(ARCH,$ar_gcc_arch)

#
# Determine Distro
#
AR_GET_DISTRO()
AC_SUBST(DISTRO,$ar_gcc_distro)

#
# Linux vs. OS X Setup
#
if test $ar_gcc_os = "darwin10" ; then
  AC_SUBST(SIRLIBS,"")
  AC_SUBST(SIRFLAGS,"-framework QtCore -framework QtNetwork")
  AC_SUBST(GUILIBS,"")
  AC_SUBST(GUIFLAGS,"-framework QtCore -framework QtNetwork -framework QtGui")
  AC_DEFINE(OSX)
else
  AC_SUBST(SIRLIBS,"-lQtCore -lQtNetwork")
  AC_SUBST(SIRFLAGS,"")
  AC_SUBST(GUILIBS,"-lQtCore -lQtNetwork -lQtGui")
  AC_SUBST(GUIFLAGS,"")
  AC_DEFINE(LINUX)
fi

#
# Configure RPM Build
#
AC_CHECK_PROG(RPMBUILD_FOUND,rpmbuild,[yes],[])
if test -z $RPMBUILD_FOUND ; then
  AC_SUBST(RPMBUILD,rpm)
else
  AC_SUBST(RPMBUILD,rpmbuild)
fi
if test -d /usr/src/redhat ; then
  AC_SUBST(RPM_ROOT,/usr/src/redhat)
  AC_SUBST(VENDOR,redhat)
else
  AC_SUBST(RPM_ROOT,/usr/src/packages)
  AC_SUBST(VENDOR,suse)
fi 

AC_CONFIG_FILES([ \
    conf/Makefile \
    helpers/Makefile \
    src/Makefile \
    src/cgi-src/Makefile \
    src/common/Makefile \
    src/common/paths.h \
    src/glassformatter/Makefile \
    src/glassplayerhost/Makefile \
    glassplayerhost-embed.spec \
    glassplayerhost-fastembed.spec \
    Makefile ])
AC_OUTPUT()

#
# Link Common Elements
#
rm -f src/glassformatter/config.cpp
ln -s ../../src/common/config.cpp src/glassformatter/config.cpp
rm -f src/glassformatter/config.h
ln -s ../../src/common/config.h src/glassformatter/config.h
rm -f src/glassformatter/paths.h
ln -s ../../src/common/paths.h src/glassformatter/paths.h

rm -f src/glassplayerhost/config.cpp
ln -s ../../src/common/config.cpp src/glassplayerhost/config.cpp
rm -f src/glassplayerhost/config.h
ln -s ../../src/common/config.h src/glassplayerhost/config.h
rm -f src/glassplayerhost/paths.h
ln -s ../../src/common/paths.h src/glassplayerhost/paths.h

rm -f src/cgi-src/config.cpp
ln -s ../../src/common/config.cpp src/cgi-src/config.cpp
rm -f src/cgi-src/config.h
ln -s ../../src/common/config.h src/cgi-src/config.h
rm -f src/cgi-src/paths.h
ln -s ../../src/common/paths.h src/cgi-src/paths.h

AC_MSG_NOTICE()
AC_MSG_NOTICE(Now enter 'make' to build the software.)
AC_MSG_NOTICE()
