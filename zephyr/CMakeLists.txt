zephyr_library()
zephyr_library_include_directories(${ZEPHYR_CURRENT_MODULE_DIR}/include)
zephyr_library_include_directories(${CMAKE_CURRENT_BINARY_DIR}/include)

zephyr_library_sources_ifdef(CONFIG_MICRO_CDR
  ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/common.c
  ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/types/basic.c
  ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/types/string.c
  ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/types/array.c
  ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/types/sequence.c
)

# temporarily set them
set(PROJECT_VERSION_MAJOR 2)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
set(PROJECT_VERSION 2.0.1)
# if (CONFIG_BIG_ENDIAN)
  # set(CONFIG_MACHINE_ENDIANNESS UCDR_BIG_ENDIANNESS)
# else()
  set(CONFIG_MACHINE_ENDIANNESS UCDR_LITTLE_ENDIANNESS)
# endif()
configure_file(${ZEPHYR_CURRENT_MODULE_DIR}/include/ucdr/config.h.in
  ${CMAKE_CURRENT_BINARY_DIR}/include/ucdr/config.h
)

set(MICRO_CDR_INCLUDE_DIR
  ${ZEPHYR_CURRENT_MODULE_DIR}/include
  ${CMAKE_CURRENT_BINARY_DIR}/include
  PARENT_SCOPE
)

add_custom_target(micro_cdr
  DEPENDS ${ZEPHYR_CURRENT_MODULE_DIR}/src/c/common.c
)