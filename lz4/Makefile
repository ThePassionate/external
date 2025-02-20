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

CSRCS += $(wildcard lz4/lib/*.c)
CFLAGS += ${INCDIR_PREFIX}lz4/lib

ifneq ($(CONFIG_UTILS_LZ4),)
PROGNAME += $(CONFIG_UTILS_LZ4_PROGNAME)
PRIORITY += $(CONFIG_UTILS_LZ4_PRIORITY)
STACKSIZE += $(CONFIG_UTILS_LZ4_STACKSIZE)
CSRCS += lz4/programs/lz4io.c
CSRCS += lz4/programs/bench.c
CSRCS += lz4/programs/datagen.c
MAINSRC += lz4/programs/lz4cli.c
endif

ifneq ($(CONFIG_LIB_LZ4_TEST),)
CFLAGS   += ${INCDIR_PREFIX}$(APPDIR)/external/lz4/lz4/programs
CFLAGS   += -D_start=lz4_start
PRIORITY  = $(CONFIG_LIB_LZ4_TEST_PRIORITY)
STACKSIZE = $(CONFIG_LIB_LZ4_TEST_STACKSIZE)
MAINSRC  += lz4/tests/frametest.c
PROGNAME += lz4_frametest
MAINSRC  += lz4/tests/abiTest.c
PROGNAME += lz4_abitest
MAINSRC  += lz4/tests/checkTag.c
PROGNAME += lz4_checktag
MAINSRC  += lz4/tests/freestanding.c
PROGNAME += lz4_freestanding
MAINSRC  += lz4/tests/fullbench.c
PROGNAME += lz4_fullbench
MAINSRC  += lz4/tests/roundTripTest.c
PROGNAME += lz4_roundTripTest
endif

include $(APPDIR)/Application.mk
