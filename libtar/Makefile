#
# Copyright (C) 2020 Xiaomi Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

include $(APPDIR)/Make.defs

CFLAGS += ${INCDIR_PREFIX}.
CFLAGS += ${INCDIR_PREFIX}libtar/compat
CFLAGS += ${INCDIR_PREFIX}libtar/listhash
CFLAGS += ${INCDIR_PREFIX}libtar/lib
CFLAGS += ${INCDIR_PREFIX}$(APPDIR)/system/zlib/zlib

CFLAGS += -DMAXPATHLEN=PATH_MAX
CFLAGS += -Wno-format-truncation

CSRCS  = $(wildcard libtar/lib/*.c)
CSRCS += $(wildcard libtar/listhash/*.c)
CSRCS += libtar/compat/strmode.c

ifneq ($(CONFIG_UTILS_TAR),)
PROGNAME = $(CONFIG_UTILS_TAR_PROGNAME)
PRIORITY = $(CONFIG_UTILS_TAR_PRIORITY)
STACKSIZE = $(CONFIG_UTILS_TAR_STACKSIZE)

MODULE = $(CONFIG_UTILS_TAR)
MAINSRC = libtar/libtar/libtar.c
endif

include $(APPDIR)/Application.mk
