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
add_library(minhook STATIC ${SRCS1} ${SRCS2})
install_static_pdb(minhook) # ASV

install(TARGETS minhook ARCHIVE DESTINATION lib)
install(FILES include/MinHook.h DESTINATION include/minhook)
