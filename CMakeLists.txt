
if(BIICODE)
              # Initializes block variables
              INIT_BIICODE_BLOCK()

              SET(BII_LIB_TYPE SHARED)
              LIST(APPEND BII_LIB_SRC expat/lib/libexpat.def)

              include(expat/ConfigureChecks.cmake)
              LIST(REMOVE_ITEM BII_LIB_SRC expat/xmlwf/ct.c)

              # Actually create targets: EXEcutables and libraries.
              ADD_BIICODE_TARGETS()

              target_include_directories( ${BII_LIB_TARGET} PUBLIC "${PROJECT_BINARY_DIR}") 

              # Load some useful config
                            #ifdef COMPILED_FROM_DSP
                            #include "winconfig.h"
                            #elif defined(MACOS_CLASSIC)
                            #include "macconfig.h"
                            #elif defined(__amigaos__)
                            #include "amigaconfig.h"
                            #elif defined(__WATCOMC__)
                            #include "watcomconfig.h"
                            #elif defined(HAVE_EXPAT_CONFIG_H)
                            #include <expat_config.h>
                            #endif /* ndef COMPILED_FROM_DSP */
              #ADD_DEFINITIONS(-DCOMPILED_FROM_DSP) #! \TODO: This should be detected from CMake.

else()
    cmake_minimum_required(VERSION 2.6)
    include_directories("${PROJECT_BINARY_DIR}/expat")
    add_subdirectory(expat)
endif()

