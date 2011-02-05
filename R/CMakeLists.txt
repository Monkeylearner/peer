find_package(SWIG REQUIRED)

INCLUDE(${SWIG_USE_FILE})

include_directories(./../External)
include_directories(./../External/Eigen)
include_directories(${PEER_SRC_DIR}/External/alglib)
include_directories(${PEER_SRC_DIR}/include)
include_directories("/opt/local/lib/R/include")
include_directories("/opt/local/lib/R/include/x86_64")

set(CMAKE_SWIG_FLAGS "")
SET(R_LIBRARIES "/usr/local/Cellar/r/2.12.0/R.framework/Resources/lib/libR.dylib")
SET(SWIGLINKLIBS ${R_SHARED_LIB_PATH} alglib peerlib)

set_source_files_properties(peer.i PROPERTIES CPLUSPLUS ON)
set_source_files_properties(peer.i PROPERTIES SWIG_FLAGS "-includeall")
set_source_files_properties(peer.i PROPERTIES SWIG_FLAGS "-cpperraswarn")
add_definitions(-DSWIG)
swig_add_module(peerr r peer.i)
swig_link_libraries(peerr ${SWIGLINKLIBS})