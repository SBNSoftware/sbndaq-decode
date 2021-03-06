# ======================================================================
#  sbndaq_decode main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/sbndaq-decode/ups/setup_for_development <-d|-p>
#  cmake [-DCMAKE_INSTALL_PREFIX=/install/path]
#        -DCMAKE_BUILD_TYPE=$CETPKG_TYPE
#        $CETPKG_SOURCE
#  make
#  make test
#  make install
#  make package (builds distribution tarfile)
# ======================================================================


# use cmake 3.11 or later
cmake_minimum_required (VERSION 3.14)

project(sbndaq_decode)

# cetbuildtools contains our cmake modules
find_package(cetbuildtools REQUIRED)

list(APPEND CMAKE_MODULE_PATH
     $ENV{CANVAS_ROOT_IO_DIR}/Modules
     $ENV{ART_DIR}/Modules
#     ${CMAKE_CURRENT_SOURCE_DIR}/Modules
)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic
  EXTRA_CXX_FLAGS -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
find_ups_product( nutools )
find_ups_product( art )
find_ups_product( cetbuildtools v7_13_02 ) # LIBRARY_OUTPUT_DIRECTORY, etc.
find_ups_product( artdaq_core v3_05_09 )
find_ups_product( sbndaq_artdaq_core v0_04_02 )
find_ups_product( lardataobj )

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# add cet_find_library commands here when needed

# ADD SOURCE CODE SUBDIRECTORIES HERE
add_subdirectory(sbndaq-decode)

# tests
add_subdirectory(test)

# ups - table and config files
# must be AFTER all other subdirectories
add_subdirectory(ups)

# packaging utility - must be last
include(UseCPack)
