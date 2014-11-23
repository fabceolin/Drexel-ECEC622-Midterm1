set(CMAKE_LEGACY_CYGWIN_WIN32 0)
project(CholThread)
cmake_minimum_required(VERSION 2.8)
aux_source_directory(. SRC_LIST)

FILE(GLOB CHOL_THREADS_SRCS
         *.c
    )


INCLUDE_DIRECTORIES(
    SYSTEM
    ${CMAKE_INSTALL_PREFIX}/include
    )


if (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
    SET(CMAKE_FIND_LIBRARY_PREFIXES "" "lib")
    SET(CMAKE_FIND_LIBRARY_SUFFIXES ".dll" ".lib" ".a" )
ENDIF (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")

FIND_LIBRARY(PTHREADS NAMES pthreadVC2d.lib PATHS ${CMAKE_INSTALL_PREFIX}/lib)

ADD_EXECUTABLE(CholThread ${CHOL_THREADS_SRCS} )
target_link_libraries(CholThread 
    ${PTHREADS}
    )
INSTALL(
    TARGETS
    CholThread
    DESTINATION 
    bin
    )
