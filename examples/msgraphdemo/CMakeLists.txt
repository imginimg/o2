cmake_minimum_required(VERSION 2.8.11)

project( msgraphexample )

set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

if(${o2_QT_VERSION} STREQUAL Qt4)
    set(QT_USE_QTNETWORK true)
    set(QT_USE_QTSCRIPT true)
    find_package(Qt4 REQUIRED)
    include( ${QT_USE_FILE} )
    add_definitions(${QT4_DEFINITIONS})
else()
    find_package(${o2_QT_VERSION} COMPONENTS Widgets Network REQUIRED)
endif()

include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} "../../src" )

set(msgraph_SRCS
    main.cpp
    msgraphdemo.cpp
    msgraphdemo.h
)

add_executable( msgraphexample ${msgraph_SRCS} )

if(${o2_QT_VERSION} STREQUAL Qt4)
    target_link_libraries(msgraphexample ${QT_LIBRARIES} o2)
else()
    target_link_libraries(msgraphexample ${o2_QT_VERSION}::Widgets ${o2_QT_VERSION}::Network o2)
endif()
