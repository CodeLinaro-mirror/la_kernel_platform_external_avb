ACLOCAL_AMFLAGS = -I m4

AUTOMAKE_OPTIONS = subdir-objects

AM_CFLAGS = -Wundef \
        -Wstrict-prototypes \
        -Wno-trigraphs \
        -g -O0 \
        -fno-inline \
        -fno-short-enums \
        -fpic \
        -D_FILE_OFFSET_BITS=64 \
        -D_POSIX_C_SOURCE=199309L \
        -Wa,--noexecstack \
        -Werror \
        -Wall \
        -Wextra \
        -Wformat=2 \
        -Wmissing-prototypes \
        -Wno-psabi \
        -Wno-unused-parameter \
        -Wno-format \
        -Wno-maybe-uninitialized \
        -Wno-format-security \
        -ffunction-sections \
        -fstack-protector-strong \
        -fno-stack-protector \
        -fno-strict-aliasing \
        -fno-tree-pre \
        -DAVB_ENABLE_DEBUG \
        -DAVB_COMPILATION

AM_CPPFLAGS = $(AM_CFLAGS) \
     -I$(WORKSPACE)/external/avb/libavb/sha

### Build libavb library
libavb_h_sources := \
    libavb/sha/avb_crypto_ops_impl.h

libavb_c_sources := \
    libavb/avb_chain_partition_descriptor.c \
    libavb/avb_cmdline.c \
    libavb/avb_crc32.c \
    libavb/avb_crypto.c \
    libavb/avb_descriptor.c \
    libavb/avb_footer.c \
    libavb/avb_hash_descriptor.c \
    libavb/avb_hashtree_descriptor.c \
    libavb/avb_kernel_cmdline_descriptor.c \
    libavb/avb_property_descriptor.c \
    libavb/avb_rsa.c \
    libavb/avb_slot_verify.c \
    libavb/avb_util.c \
    libavb/avb_vbmeta_image.c \
    libavb/avb_sysdeps_posix.c \
    libavb/avb_version.c     \
    libavb/sha/sha256_impl.c \
    libavb/sha/sha512_impl.c

library_includedir := $(pkgincludedir)
pkgconfigdir := $(libdir)/pkgconfig

### Export library
lib_LTLIBRARIES = libavb.la
libavb_la_SOURCES := $(libavb_c_sources)

libavb_la_requiredlibs := -lm

if USE_GLIB
libavb_la_CFLAGS := $(AM_CFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libavb_la_LDFLAGS = @GLIB_LIBS@ -shared -version-info 1:0:0
libavb_la_CPPFLAGS := $(AM_CPPFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libavb_la_LIBADD := $(libavb_la_requiredlibs) @GLIB_LIBS@
else
libavb_la_CFLAGS := $(AM_CFLAGS)
libavb_la_LDFLAGS = -shared -version-info 1:0:0
libavb_la_CPPFLAGS := $(AM_CPPFLAGS)
libavb_la_LIBADD := $(libavb_la_requiredlibs)
endif
