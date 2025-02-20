#
# Copyright (C) 2021 Xiaomi Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may not
# use this file except in compliance with the License. You may obtain a copy of
# the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
# License for the specific language governing permissions and limitations under
# the License.
#
if(CONFIG_LIB_FFI)

  set(SRCS)
  set(FLAGS)

  if("${CONFIG_ARCH}" STREQUAL "arm")
    set(TARGETDIR arm)
  elseif("${CONFIG_ARCH}" STREQUAL "arm64")
    set(TARGETDIR aarch64)
  elseif("${CONFIG_ARCH}" STREQUAL "xtensa")
    set(TARGETDIR xtensa)
  elseif("${CONFIG_ARCH}" STREQUAL "sim")
    set(TARGETDIR x86)
  endif()

  list(
    APPEND
    SRCS
    libffi/src/prep_cif.c
    libffi/src/types.c
    libffi/src/raw_api.c
    libffi/src/java_raw_api.c
    libffi/src/closures.c
    libffi/src/debug.c
    libffi/src/${TARGETDIR}/ffi.c
    libffi/src/${TARGETDIR}/sysv.S)

  list(APPEND INC_DIRS ${CMAKE_CURRENT_LIST_DIR}
       ${CMAKE_CURRENT_LIST_DIR}/libffi ${CMAKE_CURRENT_LIST_DIR}/libffi/src
       ${CMAKE_CURRENT_LIST_DIR}/libffi/src/${TARGETDIR})

  list(APPEND FLAGS -fno-sanitize=all -fno-stack-protector)
  list(APPEND FLAGS -Wno-deprecated-declarations -Wno-undef)

  nuttx_create_symlink(${CMAKE_CURRENT_LIST_DIR}/libffi/include
                       ${CMAKE_CURRENT_BINARY_DIR}/include)

  configure_file(${CMAKE_CURRENT_LIST_DIR}/libffi/src/${TARGETDIR}//ffitarget.h
                 ${CMAKE_CURRENT_BINARY_DIR}/include/ffitarget.h COPYONLY)

  set_property(
    TARGET nuttx
    APPEND
    PROPERTY NUTTX_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_BINARY_DIR}/include)

  nuttx_add_library(libffi STATIC)
  target_sources(libffi PRIVATE ${SRCS})
  target_include_directories(libffi PRIVATE ${INC_DIRS})
  target_compile_options(libffi PRIVATE ${FLAGS})

endif()
