# Resources:
#  - http://bit.ly/2dfK5L1

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

include(ExternalProject)

ExternalProject_Add(boost
    URL "http://kent.dl.sourceforge.net/project/boost/boost/1.62.0/boost_1_62_0.tar.gz"
    PREFIX ${CMAKE_CURRENT_BINARY_DIR}
    BUILD_IN_SOURCE 1
    UPDATE_COMMAND ""
    CONFIGURE_COMMAND ./bootstrap.sh --with-toolset=clang --with-libraries=context,coroutine2
    BUILD_COMMAND ./b2 toolset=clang cxxflags="-stdlib=libc++" linkflags="-stdlib=libc++"
    INSTALL_COMMAND ""
)

set(BOOST_INCLUDE_DIRS ${CMAKE_CURRENT_BINARY_DIR}/src/boost PARENT_SCOPE)
set(BOOST_LINK_DIRS ${CMAKE_CURRENT_BINARY_DIR}/src/boost/stage/lib PARENT_SCOPE)
set(BOOST_THREAD_LIBRARIES ${CMAKE_CURRENT_BINARY_DIR}/src/boost/stage/lib/libboost_thread.so PARENT_SCOPE)
set(BOOST_SYSTEM_LIBRARIES ${CMAKE_CURRENT_BINARY_DIR}/src/boost/stage/lib/libboost_system.so PARENT_SCOPE)