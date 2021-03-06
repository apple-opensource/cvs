## Process this file with automake to produce Makefile.in

# *** Under Windows NT and Microsoft Visual C++, we use cvsnt.mak, not
# *** this makefile.  However, we need this file in order for 'make
# *** dist' to work properly on Unix machines.

# Makefile for GNU CVS windows-NT dist.
#
# Copyright (C) 1986-2005 The Free Software Foundation, Inc.
#
# Portions Copyright (C) 1998-2005 Derek Price, Ximbiot <http://ximbiot.com>,
#                                  and others.

# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

EXTRA_DIST = \
	JmgStat.c \
	JmgStat.h \
	config.h \
	config.h.in \
	config.h.in.in \
	config.h.in.footer \
	stamp-chi \
	mkconfig.pl \
	fix-msvc-mak.pl \
	ndir.h \
	pwd.h \
	rcmd.h \
	stdbool.h \
	stdint.h \
	filesubr.c \
	mkdir.c \
	ndir.c \
	netdb.h \
	pwd.c \
	rcmd.c \
	run.c \
	sockerror.c \
	startserver.c \
	arpa/inet.h \
	netinet/in.h \
	sys/socket.h \
	sys/types.h \
	unistd.c \
	unistd.h \
	waitpid.c \
	woe32.c \
	woe32.h \
	.cvsignore

SUBDIRS = SCC

###
### Maintainer targets
###
MAINTAINERCLEANFILES =
DISTCLEANFILES =

all-local: config.h stdbool.h stdint.h
config.h: stamp-ch
stamp-ch: config.h.in $(top_srcdir)/configure
	@echo "/* This file is generated via a rule in Makefile.am from the" \
	  >config.tmp
	@echo " * config.h.in file." >>config.tmp
	@echo " *" >>config.tmp
	@echo " * *** DO NOT EDIT THIS FILE DIRECTLY ***" >>config.tmp
	@echo " *" >>config.tmp
	@echo " * Edit config.h.in instead." >>config.tmp
	@echo " */" >>config.tmp
	sed -e "s/%PACKAGE_STRING%/$(PACKAGE_STRING)/" \
	    -e "s/%PACKAGE_BUGREPORT%/$(PACKAGE_BUGREPORT)/" \
	    <$(srcdir)/config.h.in >>config.tmp
	@cmp -s config.tmp $(srcdir)/config.h \
	  || (echo "Updating config.h"; \
	      cp config.tmp $(srcdir)/config.h)
	-@rm -f config.tmp
	@cp $(srcdir)/config.h $@
DISTCLEANFILES += stamp-ch

# The shell portion of this target is so that this file will be regenerated
# when it is missing, even when not in maintainer mode.
config.h.in: @MAINTAINER_MODE_TRUE@ stamp-chi
	@if test ! -f $(srcdir)/$@; then \
	  rm -f $(srcdir)/stamp-chi; \
	  $(MAKE) stamp-chi; \
	else :; fi

# The following target exists for two reasons.  The first is so that the rule
# for config.h.in above may be conditionally dependent on it and thus only
# built in maintainer mode.  The second reason is so that the config.h.in, and
# thus the config.h file, only gets touched when it actually changes, which
# could potentially save unnecessary rebuilds of many dependent files.
#
# This file is distributed since, without it, config.h.in will always be
# rebuilt on the first run in maintainer mode, even if its dependencies are
# unchanged.
stamp-chi: $(srcdir)/mkconfig.pl $(top_srcdir)/config.h.in \
	   $(srcdir)/config.h.in.in $(srcdir)/config.h.in.footer
	@$(PERL) mkconfig.pl -q $(top_srcdir)/config.h.in \
	                        $(srcdir)/config.h.in \
	                        $(srcdir)/config.h.in.in \
	                        $(srcdir)/config.h.in.footer
	@cp $(srcdir)/config.h.in $(srcdir)/$@
MAINTAINERCLEANFILES += $(srcdir)/config.h.in $(srcdir)/stamp-chi

stdbool.h: stamp-sh
stamp-sh: $(top_srcdir)/lib/stdbool_.h
	@echo "/* This file is generated via a rule in Makefile.am from the" \
	  >stdbool.tmp
	@echo " * ../lib/stdbool_.h.in file." >>stdbool.tmp
	@echo " *" >>stdbool.tmp
	@echo " * *** DO NOT EDIT THIS FILE DIRECTLY ***" >>stdbool.tmp
	@echo " *" >>stdbool.tmp
	@echo " * Edit ../lib/stdbool_.h instead." >>stdbool.tmp
	@echo " */" >>stdbool.tmp
	sed 's/@''HAVE__BOOL''@/0/' <$(top_srcdir)/lib/stdbool_.h \
	  >>stdbool.tmp
	@cmp -s stdbool.tmp $(srcdir)/stdbool.h \
	  || (echo "Updating stdbool.h"; \
	      cp stdbool.tmp $(srcdir)/stdbool.h)
	-@rm -f stdbool.tmp
	@cp $(srcdir)/stdbool.h $@
DISTCLEANFILES += stamp-sh

stdint.h: stamp-sh2
stamp-sh2: $(top_srcdir)/lib/stdint_.h
	@echo "/* This file is generated via a rule in Makefile.am from the" \
	  >stdint.tmp
	@echo " * ../lib/stdint_.h.in file." >>stdint.tmp
	@echo " *" >>stdint.tmp
	@echo " * *** DO NOT EDIT THIS FILE DIRECTLY ***" >>stdint.tmp
	@echo " *" >>stdint.tmp
	@echo " * Edit ../lib/stdint_.h instead." >>stdint.tmp
	@echo " */" >>stdint.tmp
	sed 's/@''HAVE_LONG_64BIT''@/0/g;s/@''HAVE_LONG_LONG_64BIT@/0/g' \
	  <$(top_srcdir)/lib/stdint_.h >>stdint.tmp
	@cmp -s stdint.tmp $(srcdir)/stdint.h \
	  || (echo "Updating stdint.h"; \
	      cp stdint.tmp $(srcdir)/stdint.h)
	-@rm -f stdint.tmp
	@cp $(srcdir)/stdint.h $@
DISTCLEANFILES += stamp-sh2

# for backwards compatibility with the old makefiles
realclean: maintainer-clean
.PHONY: realclean
