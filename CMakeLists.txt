project(terminal)

cmake_minimum_required(VERSION 2.8.8)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fvisibility=hidden -fvisibility-inlines-hidden -Wall -std=c++0x")

find_package(Qt5Gui REQUIRED)
if(NOT Qt5Gui_FOUND)
    message(FATAL_ERROR "Qt5Gui module is required!")
endif()

find_package(Qt5Qml REQUIRED)
if(NOT Qt5Qml_FOUND)
    message(FATAL_ERROR "Qt5Qml module is required!")
endif()

find_package(Qt5Quick REQUIRED)
if(NOT Qt5Quick_FOUND)
    message(FATAL_ERROR "Qt5Quick module is required!")
endif()

set(SOURCES src/main.cpp)

qt5_add_resources(RESOURCES src/resources.qrc)

add_executable(terminal ${SOURCES} ${RESOURCES})
qt5_use_modules(terminal Quick Gui WebKit)

set(APPLICATION_DATA
    icon.png
    appinfo.json)

install (FILES ${APPLICATION_DATA} DESTINATION
    ${WEBOS_INSTALL_WEBOS_APPLICATIONSDIR}/org.webosports.app.terminal)
install (TARGETS terminal DESTINATION
    ${WEBOS_INSTALL_WEBOS_APPLICATIONSDIR}/org.webosports.app.terminal/bin)
