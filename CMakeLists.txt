cmake_minimum_required(VERSION 3.14)
project(parasolid_frustrum)

add_library(parasolid_frustrum STATIC "frustrum.cpp" "parasolid.cpp")

IF (WIN32)
	target_link_libraries(parasolid_frustrum PUBLIC $ENV{PARASOLID_BASE}/pskernel_archive.lib)
ELSEIF(APPLE)
	set(THREADS_PREFER_PTHREAD_FLAG ON)
	find_package(Threads REQUIRED)
	target_link_libraries(parasolid_frustrum PUBLIC $ENV{PARASOLID_BASE}/pskernel_archive.lib Threads::Threads)
ELSE()
	set(THREADS_PREFER_PTHREAD_FLAG ON)
	find_package(Threads REQUIRED)
	target_link_libraries(parasolid_frustrum PUBLIC $ENV{PARASOLID_BASE}/pskernel_archive.lib Threads::Threads)
ENDIF()

target_include_directories(parasolid_frustrum PUBLIC $ENV{PARASOLID_BASE})
