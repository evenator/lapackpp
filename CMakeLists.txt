cmake_minimum_required(VERSION 2.8.3)
project(lapackpp)

find_package(catkin REQUIRED)

include(ExternalProject)
ExternalProject_Add(upstream
   # TODO: Stop depending on sourceforge. It's unreliable. See
   # https://en.wikipedia.org/wiki/SourceForge#2015_Outages
   # https://en.wikipedia.org/wiki/SourceForge#Controversies
   URL http://downloads.sourceforge.net/project/lapackpp/lapackpp-2.5.4.tar.gz
   URL_MD5 9ad74fb73fbcbf378c36a19a5dccbda7
   CONFIGURE_COMMAND <SOURCE_DIR>/configure --prefix=${CMAKE_INSTALL_PREFIX}
   BUILD_IN_SOURCE 1
   BUILD_COMMAND unset MAKEFLAGS && unset MAKELEVEL && unset MFLAGS && make LDFLAGS=-lgcc
   INSTALL_COMMAND make install
)

install(FILES package.xml DESTINATION share/${PROJECT_NAME}) # REP 136
