AUTOMAKE_OPTIONS = foreign 1.10 dist-bzip2 subdir-objects
ACLOCAL_AMFLAGS = -I m4

INCLUDES = -I$(top_srcdir)/include -I.
AM_CFLAGS = -ansi -std=gnu99 -Wall -Wextra -Wno-long-long -O0 -Wno-unused -g

SUBDIRS = docs

EXTRA_DIST = \
	AUTHORS README LICENSE \
	cubeb-uninstalled.pc.in \
	m4/as-ac-expand.m4 \
	m4/pkg.m4 \
	m4/ax_create_stdint_h.m4

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = cubeb.pc

cubebincludedir = $(includedir)/cubeb
cubebinclude_HEADERS = include/cubeb/cubeb.h include/cubeb/cubeb-stdint.h

lib_LTLIBRARIES = src/libcubeb.la

src_libcubeb_la_SOURCES = src/cubeb.c

if PULSE
src_libcubeb_la_SOURCES += src/cubeb_pulse.c
endif
if ALSA
src_libcubeb_la_SOURCES += src/cubeb_alsa.c
endif
if AUDIOUNIT
src_libcubeb_la_SOURCES += src/cubeb_audiounit.c
endif
if AUDIOQUEUE
src_libcubeb_la_SOURCES += src/cubeb_audioqueue.c
endif
if WINMM
src_libcubeb_la_SOURCES += src/cubeb_winmm.c
endif
if DIRECTSOUND
src_libcubeb_la_SOURCES += src/cubeb_directsound.cpp
endif
if SNDIO
src_libcubeb_la_SOURCES += src/cubeb_sndio.c
endif
if OPENSL
src_libcubeb_la_SOURCES += src/cubeb_opensl.c
endif
if AUDIOTRACK
src_libcubeb_la_SOURCES += src/cubeb_audiotrack.c
endif

EXTRA_src_libcubeb_la_SOURCES = \
        src/cubeb.c \
	src/cubeb_alsa.c src/cubeb_pulse.c \
	src/cubeb_audiounit.c src/cubeb_audioqueue.c \
	src/cubeb_sndio.c src/cubeb_directsound.cpp \
	src/cubeb_winmm.c src/cubeb_opensl.c src/cubeb_audiotrack.c

src_libcubeb_la_LDFLAGS = -pthread -export-symbols-regex '^cubeb_' $(platform_lib) -no-undefined

noinst_PROGRAMS = test/test_sanity test/test_tone

test_test_sanity_SOURCES = test/test_sanity.c
test_test_sanity_LDADD = -lm src/libcubeb.la $(platform_lib)

test_test_tone_SOURCES = test/test_tone.c
test_test_tone_LDADD = -lm src/libcubeb.la $(platform_lib)

TESTS = test/test_sanity

DISTCLEANFILES = include/cubeb/cubeb-stdint.h

dist-hook:
	find $(distdir) -type d -name '.git' | xargs rm -rf

debug:
	$(MAKE) all CFLAGS="@DEBUG@"

profile:
	$(MAKE) all CFLAGS="@PROFILE@"
