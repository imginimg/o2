cmake_minimum_required(VERSION 2.8.12)

project( vimeoexample )

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
    if(${o2_QT_VERSION} STREQUAL Qt6)
        find_package(${o2_QT_VERSION} COMPONENTS Core5Compat REQUIRED)
    endif()
endif()



include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} "../../src" )

set(vimeo_SRCS
    main.cpp
    vimeodemo.cpp
    vimeodemo.h
)

add_executable( vimeoexample ${vimeo_SRCS} )

if(${o2_QT_VERSION} STREQUAL Qt4)
    target_link_libraries(vimeoexample ${QT_LIBRARIES} o2)
else()
    target_link_libraries(vimeoexample ${o2_QT_VERSION}::Widgets ${o2_QT_VERSION}::Network o2)
    if(${o2_QT_VERSION} STREQUAL Qt6)
        target_link_libraries(vimeoexample ${o2_QT_VERSION}::Core5Compat)
    endif()
endif()
