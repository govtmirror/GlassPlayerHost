## automake.am
##
## Top level automake.am
##
## Use automake to process this into a Makefile.in
##
##   (C) Copyright 2014,2016 Fred Gleason <fredg@paravelsystems.com>
##
##   This program is free software; you can redistribute it and/or modify
##   it under the terms of the GNU General Public License version 2 as
##   published by the Free Software Foundation.
##
##   This program is distributed in the hope that it will be useful,
##   but WITHOUT ANY WARRANTY; without even the implied warranty of
##   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
##   GNU General Public License for more details.
##
##   You should have received a copy of the GNU General Public
##   License along with this program; if not, write to the Free Software
##   Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
##

##if DOCBOOK_AM
##  DOCBOOK_AM_OPT = docs
##endif

##SUBDIRS = $(DOCBOOK_AM_OPT) src
SUBDIRS = conf\
          helpers\
          src

#rpm:	dist
#	cp glassplayerhost-$(VERSION).tar.gz $(HOME)/rpmbuild/SOURCES/
#	$(RPMBUILD) -ba --target $(ARCH)-$(VENDOR)-linux glassplayerhost.spec
#	mv $(HOME)/rpmbuild/RPMS/$(ARCH)/glassplayerhost-*.rpm $(top_srcdir)/
#	mv $(HOME)/rpmbuild/SRPMS/glassplayerhost-*.src.rpm $(top_srcdir)/
#	rm $(HOME)/rpmbuild/SOURCES/glassplayerhost-$(VERSION).tar.gz
#	rm -rf $(HOME)/rpmbuild/BUILD/glassplayerhost-$(VERSION)

embed:	dist
	cp glassplayerhost-$(VERSION).tar.gz $(HOME)/rpmbuild/SOURCES/
	$(RPMBUILD) -ba --target $(ARCH)-$(VENDOR)-linux glassplayerhost-embed.spec
	mv $(HOME)/rpmbuild/RPMS/$(ARCH)/glassplayerhost-*.rpm $(top_srcdir)/
	mv $(HOME)/rpmbuild/SRPMS/glassplayerhost-*.src.rpm $(top_srcdir)/
	rm $(HOME)/rpmbuild/SOURCES/glassplayerhost-$(VERSION).tar.gz
	rm -rf $(HOME)/rpmbuild/BUILD/glassplayerhost-$(VERSION)

fastembed:	dist
	cp glassplayerhost-$(VERSION).tar.gz $(HOME)/rpmbuild/SOURCES/
	$(RPMBUILD) -ba --target $(ARCH)-$(VENDOR)-linux glassplayerhost-fastembed.spec
	mv $(HOME)/rpmbuild/RPMS/$(ARCH)/glassplayerhost-*.rpm $(top_srcdir)/
	mv $(HOME)/rpmbuild/SRPMS/glassplayerhost-*.src.rpm $(top_srcdir)/
	rm $(HOME)/rpmbuild/SOURCES/glassplayerhost-$(VERSION).tar.gz
	rm -rf $(HOME)/rpmbuild/BUILD/glassplayerhost-$(VERSION)

EXTRA_DIST = glassplayerhost-embed.spec.in\
             glassplayerhost-fastembed.spec.in\
             autogen.sh\
             get_distro.sh\
             get_target.sh\
             PACKAGE_VERSION

CLEANFILES = *~\
             *.deb\
             *.mo\
             *.rpm\
             *.tar.gz\
             *.tgz\
             *.zip

DISTCLEANFILES = glassplayerhost.spec\
                 config.guess\
                 config.sub\
                 ltmain.sh

MAINTAINERCLEANFILES = *~\
                       *.spec\
                       *.tar.gz\
                       aclocal.m4\
                       config.guess\
                       config.status\
                       config.sub\
                       configure\
                       depcomp\
                       install-sh\
                       libtool\
                       ltmain.sh\
                       Makefile.in\
                       missing\
                       mkinstalldirs
