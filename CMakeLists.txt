cmake_minimum_required(VERSION 3.5)
project(openvdb)

find_package(ament_cmake_auto REQUIRED)

if (CMAKE_SYSTEM_PROCESSOR MATCHES "(aarch64)|(arm)")
  set(ARCH linux-arm64)
else ()
  set(ARCH linux-amd64)
endif ()

set(LIB_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/${ARCH})

add_library(openvdb SHARED IMPORTED GLOBAL)
set_target_properties(openvdb PROPERTIES
  IMPORTED_LOCATION ${LIB_DIR}/libopenvdb.so.10.0.1
)

install(FILES
  ${LIB_DIR}/libopenvdb.so.10.0.1
  ${LIB_DIR}/libopenvdb.so.10.0
  ${LIB_DIR}/libopenvdb.so
  DESTINATION lib
)

ament_export_libraries(openvdb)
ament_auto_package()
