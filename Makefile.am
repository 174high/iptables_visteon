# -*- Makefile -*-

ACLOCAL_AMFLAGS  = -I m4
AUTOMAKE_OPTIONS = foreign subdir-objects

SUBDIRS          = libiptc libxtables
if ENABLE_DEVEL
SUBDIRS         += include
endif
if ENABLE_LIBIPQ
SUBDIRS         += libipq
endif
SUBDIRS         += utils
# Depends on libxtables:
SUBDIRS         += extensions
# Depends on extensions/libext.a:
SUBDIRS         += iptables

.PHONY: tarball
tarball:
	rm -Rf /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION};
	pushd ${top_srcdir} && git archive --prefix=${PACKAGE_TARNAME}-${PACKAGE_VERSION}/ HEAD | tar -C /tmp -x && popd;
	pushd /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION} && ./autogen.sh && popd;
	tar -C /tmp -cjf ${PACKAGE_TARNAME}-${PACKAGE_VERSION}.tar.bz2 --owner=root --group=root ${PACKAGE_TARNAME}-${PACKAGE_VERSION}/;
	rm -Rf /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION};

install-data-hook:
	@mkdir -p -m 755 $(DESTDIR)/etc/xtables/ || :
	@test -f /etc/xtables/connlabel.conf || $(INSTALL) -m 644 etc/xtables/connlabel.conf $(DESTDIR)/etc/xtables/connlabel.conf || :

install-data-hook:
	@mkdir -p -m 755 $(DESTDIR)/etc/xtables/ || :
	@test -f /etc/xtables/connlabel.conf || $(INSTALL) -m 644 etc/xtables/connlabel.conf $(DESTDIR)/etc/xtables/connlabel.conf || :

config.status: extensions/GNUmakefile.in \
	include/xtables-version.h.in include/iptables/internal.h.in
