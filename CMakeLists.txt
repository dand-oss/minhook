cmake_minimum_required(VERSION 3.10)

PROJECT(
    "minhook"
    VERSION 1.0.0
    LANGUAGES C
    )

# Note this is for windows ONLY

###############
# ASI default settings
list(APPEND CMAKE_MODULE_PATH "$ENV{ASV_CMAKE}")
include(asv_cmake_defaults)
asv_cmake_defaults( )
###############

set(SRCS
    src/buffer.c
    src/hook.c
    src/trampoline.c

    src/buffer.h
    src/trampoline.h

    src/hde/hde32.c
    src/hde/hde64.c

    src/hde/hde32.h
    src/hde/hde64.h
    src/hde/pstdint.h
    src/hde/table32.h
    src/hde/table64.h
)

set(libname minhook)
add_library(${libname} SHARED ${SRCS})

install(TARGETS ${libname}
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin)
set_target_properties(${libname} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)

# do not remove - WG7 requires the static lib
set(staticlibname minhookstatic)

add_library(${staticlibname} STATIC ${SRCS})
install(TARGETS ${staticlibname}
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin)

install(FILES include/MinHook.h DESTINATION include/minhook)

include(CPack)
