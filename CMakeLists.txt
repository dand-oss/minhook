PROJECT(minhook)
cmake_minimum_required(VERSION 2.8)

# Note this is for windows ONLY

###############
# ASI default settings
list(APPEND CMAKE_MODULE_PATH "$ENV{ASI}/cmake/Modules")
include(asv_cmake_defaults)
asv_cmake_defaults( )
###############

FILE(GLOB SRCS1 ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c)
FILE(GLOB SRCS2 ${CMAKE_CURRENT_SOURCE_DIR}/src/HDE/*.c)
set(libname minhook)
add_library(${libname} SHARED ${SRCS1} ${SRCS2})

install(TARGETS ${libname} ARCHIVE DESTINATION lib)
install(TARGETS ${libname} RUNTIME DESTINATION bin)
install(FILES include/MinHook.h DESTINATION include/minhook)
set_target_properties(${libname} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
