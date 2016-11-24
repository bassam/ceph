include(ExternalProject)

# set the external root directory
set(EXTERNAL_ROOT ${CMAKE_BINARY_DIR}/external)

# set external download/cache dir
set(EXTERNAL_DOWNLOAD_DIR ${PROJECT_SOURCE_DIR}/external/download)

# this is used to track all external dependencies
set(EXTERNAL_DEPENDENCIES)

# whether to log the configure, build and install commands
# or have them go to stdout.
set(EXTERNAL_LOGGING ON)

#
# Boost
#

# if set to AUTO we will use system boost if we found the appropriate version
# otherwise we will download and build boost from source. If set to ON then
# we will always use system boost, and of the appropriate version is not found
# the build will fail. If set to OFF, we will always build boost from source
# and ignore the version of boost on the system.
set(WITH_SYSTEM_BOOST "AUTO" CACHE STRING "Whether to use system Boost or build it")

# the minimum boost version expected
set(Boost_SYSTEM_VERSION 1.62.0)

# the version of boost we will download and build if the system version is not
# found or we are asked to build our own.
set(Boost_EXTERNAL_VERSION 1.62.0)
set(Boost_EXTERNAL_SHA256 36c96b0f6155c98404091d8ceb48319a28279ca0333fba1ad8611eb90afb2ca0)

# the components of boost that we use
set(Boost_COMPONENTS thread system regex random program_options date_time iostreams python)

# other settings for find_package
if(ENABLE_SHARED)
  set(Boost_USE_STATIC_LIBS OFF)
else()
  set(Boost_USE_STATIC_LIBS ON)
endif()

set(Boost_USE_MULTITHREADED ON)

include(external/boost.cmake)

include_directories(SYSTEM ${Boost_INCLUDE_DIRS})
