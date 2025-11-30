## Process this file with automake to generate Makefile.in

AUTOMAKE_OPTIONS = cygnus

INCLUDES = $(NEWLIB_CFLAGS) $(CROSS_CFLAGS) $(TARGET_CFLAGS)

AM_CCASFLAGS = $(INCLUDES)

if USE_LIBTOOL
noinst_LTLIBRARIES = libx86_64.la
libx86_64_la_SOURCES = setjmp.S memcpy.S memset.S
libx86_64_la_LIBADD = $(LIBADD_OBJS)
libx86_64_la_DEPENDENCIES = $(LIBADD_OBJS)
LIB_COMPILE = $(LTCOMPILE)
noinst_DATA = objectlist.awk.in
else
noinst_LIBRARIES = lib.a
lib_a_SOURCES = setjmp.S memcpy.S memset.S
lib_a_CCASFLAGS=$(AM_CCASFLAGS)
lib_a_CFLAGS = $(AM_CFLAGS)
endif

objectlist.awk.in: $(noinst_LTLIBRARIES) $(SUBLIBS)
	-rm -f objectlist.awk.in
	for i in `ls *.lo` ; \
	  do \
		echo $$i `pwd`/$$i >> objectlist.awk.in ; \
	done
	for j in $(SUBLIBS) ; \
	  do \
		export i=`echo $$j | sed -e 's,\(.*\)\/[^\/]*$$,\1,'`; \
		if test $$i != "." && test -f $$i/objectlist.awk.in; then \
			cat $$i/objectlist.awk.in >> objectlist.awk.in ; \
		fi; \
	done

ACLOCAL_AMFLAGS = -I ../../.. -I ../../../..
CONFIG_STATUS_DEPENDENCIES = $(newlib_basedir)/configure.host
