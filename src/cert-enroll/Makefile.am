REPLACE_TARGETS = \
	cert-enroll \
	cert-install-swanctl \
	cert-install-ipsec \
	cert-enroll.service

$(REPLACE_TARGETS) : Makefile
	$(AM_V_GEN) \
	sed \
	-e "s:@SYSCONFDIR@:$(sysconfdir):" \
	-e "s:@SBINDIR@:$(sbindir):" \
	-e "s:@BINDIR@:$(bindir):" \
	-e "s:@IPSEC_SCRIPT@:$(ipsec_script):" \
	$(srcdir)/$@.in > $@

sbin_SCRIPTS = cert-enroll

cert-enroll : cert-enroll.in

cert_enrolldir = $(sysconfdir)/cert-enroll.d
cert_enroll_DATA = cert-enroll.conf

install-data-local:
	test -e "$(DESTDIR)$(cert_enrolldir)/cert-install.d" || \
	$(INSTALL) -d "$(DESTDIR)$(cert_enrolldir)/cert-install.d" || true

cert_install_availabledir = $(sysconfdir)/cert-enroll.d/cert-install-available
cert_install_available_DATA = \
	cert-install-sssd \
	cert-install-dirsrv \
	cert-install-lighttpd \
	cert-install-openxpki \
	cert-install-gitea \
	cert-install-ipsec \
	cert-install-swanctl

cert-install-swanctl : cert-install-swanctl.in

cert-install-ipsec : cert-install-ipsec.in

man8_MANS = cert-enroll.8

CLEANFILES = cert-enroll cert-install-swanctl cert-install-ipsec

if USE_CERT_ENROLL_TIMER
systemdsystemunit_DATA = cert-enroll.service cert-enroll.timer

cert-enroll.service : cert-enroll.service.in

CLEANFILES += cert-enroll.service
endif
