cmake_minimum_required(VERSION 3.5)
project(openvdb)

find_package(ament_cmake_auto REQUIRED)

if (CMAKE_SYSTEM_PROCESSOR MATCHES "(aarch64)|(arm)")
  set(ARCH linux-arm64)
else ()
  set(ARCH linux-amd64)
endif ()

set(LIB_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/${ARCH})
set(LIB_VERSION 10.0.1)
set(LIB_SOVERSION 10.0)

add_custom_command(
  OUTPUT ${LIB_DIR}/libopenvdb.so ${LIB_DIR}/libopenvdb.so.${LIB_SOVERSION}
  COMMAND ${CMAKE_COMMAND} -E create_symlink libopenvdb.so.${LIB_SOVERSION} ${LIB_DIR}/libopenvdb.so
  COMMAND ${CMAKE_COMMAND} -E create_symlink libopenvdb.so.${LIB_VERSION} ${LIB_DIR}/libopenvdb.so.${LIB_SOVERSION}
  DEPENDS ${LIB_DIR}/libopenvdb.so.${LIB_VERSION}
)

add_custom_target(symlinks ALL
  DEPENDS
    ${LIB_DIR}/libopenvdb.so
    ${LIB_DIR}/libopenvdb.so.${LIB_SOVERSION}
)

add_library(openvdb SHARED IMPORTED GLOBAL)
set_target_properties(openvdb PROPERTIES
  IMPORTED_LOCATION ${LIB_DIR}/libopenvdb.so.${LIB_VERSION}
)

# Install actual library, symlinks, and static library if present
install(FILES
  ${LIB_DIR}/libopenvdb.so.${LIB_VERSION}
  ${LIB_DIR}/libopenvdb.so.${LIB_SOVERSION}
  ${LIB_DIR}/libopenvdb.so
  DESTINATION lib
)
install(FILES ${LIB_DIR}/libopenvdb.a DESTINATION lib OPTIONAL)

ament_auto_package()