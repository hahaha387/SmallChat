cmake_minimum_required(VERSION 3.26)

project(appWechat-Client VERSION 0.1 LANGUAGES CXX)

find_package(Qt6 REQUIRED COMPONENTS Widgets)
find_package(Qt6 6.4 REQUIRED COMPONENTS Quick)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_AUTOUIC ON)


find_package(Qt6 COMPONENTS Quick REQUIRED)
find_package(Qt6 REQUIRED COMPONENTS Qml)
qt_standard_project_setup()

qt_add_executable(appWechat-Client
    main.cpp
    client.h                            client.cpp
    network.h                           network.cpp
    messagepreviewpagecontroller.h      messagepreviewpagecontroller.cpp
    communicationpagecontroller.h       communicationpagecontroller.cpp
    addfriendpagecontroller.h           addfriendpagecontroller.cpp
    personalpagecontroller.h            personalpagecontroller.cpp
    getfirstletter.h                    getfirstletter.cpp
    listenthread.h listenthread.cpp

    qml.qrc
    assets.qrc
    othersource.qrc
    myimageprovider.h myimageprovider.cpp
    filetools.h filetools.cpp
)

target_compile_features(appWechat-Client PRIVATE cxx_std_20)

include_directories("/root/WeChat-Imitate-Client/ffmpeg-source/include/ffmpeg4.4")
link_directories("/root/WeChat-Imitate-Client/ffmpeg-source/lib/ffmpeg4.4")
link_libraries(avformat)

find_package(Qt6 REQUIRED COMPONENTS Widgets)
find_package(Qt6 REQUIRED COMPONENTS Quick)
find_package(Qt6 REQUIRED COMPONENTS Qml)
find_package(Qt6 REQUIRED COMPONENTS Gui)
add_subdirectory(json)
target_link_libraries(appWechat-Client
    PRIVATE
        nlohmann_json
        Qt6::Widgets
        Qt6::Qml
        Qt6::Quick
        Qt6::Gui
    )
find_package(Qt6 REQUIRED COMPONENTS Quick)
target_link_libraries(appWechat-Client PRIVATE Qt6::Quick)
find_package(Qt6 REQUIRED COMPONENTS Qml)
target_link_libraries(appWechat-Client PRIVATE Qt6::Qml)

set_target_properties(appWechat-Client PROPERTIES
    AUTORCC TRUE
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

include(GNUInstallDirs)
install(TARGETS appWechat-Client
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_finalize_executable(appWechat-Client)

# Define target properties for Android with Qt 6 as:
#    set_property(TARGET appWechat-Client APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
#                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
# For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation














































# target_sources(appWechat-Client
#     PRIVATE
#         main.cpp
#         mainwindow.cpp
#         mainwindow.h
#     @if true
#         mainwindow.ui
#     @endif
#     @if false
#         
#     @endif
#         
#     PUBLIC
#         
# )

# qt_standard_project_setup()     #set(CMAKE_AUTOUIC ON)  set(CMAKE_AUTOMOC ON)
# set_target_properties(appWechat-Client PROPERTIES
#     MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
#     MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
#     MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
#     MACOSX_BUNDLE TRUE
#     WIN32_EXECUTABLE TRUE
# )
# 
# install(TARGETS appWechat-Client
#     BUNDLE DESTINATION .
#     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
#     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
# )
# 
# if(QT_VERSION_MAJOR EQUAL 6)
#     qt_finalize_executable(appWechat-Client)
# endif()





#qt_add_executable(appWechat-Client)  //Creates and finalizes an application target of a platform-specific type.
#This command performs the following tasks:

#    1. Create a CMake target of the appropriate type for the target platform.
#    2. Link the target to the Qt::Core library.
#    3. Handle finalization of the CMake target.












# cmake_minimum_required(VERSION 3.5)
# 
# project(appWechat-Client VERSION 0.1 LANGUAGES CXX)
# 
# set(CMAKE_AUTOUIC ON)
# set(CMAKE_AUTOMOC ON)
# set(CMAKE_AUTORCC ON)
# 
# set(CMAKE_CXX_STANDARD 20)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
# 
# @if false
# find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets LinguistTools)
# find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets LinguistTools)
# 
# set(TS_FILES )
# @else
# find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
# find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)
# @endif
# 
# set(PROJECT_SOURCES
#         main.cpp
#         mainwindow.cpp
#         mainwindow.h
#     @if true
#         mainwindow.ui
#     @endif
#     @if false
#         ${TS_FILES}
#     @endif
# )
# 
# if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
#     qt_add_executable(appWechat-Client
#         MANUAL_FINALIZATION
#         ${PROJECT_SOURCES}
#     )
# # Define target properties for Android with Qt 6 as:
# #    set_property(TARGET appWechat-Client APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
# #                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
# # For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation
# @if false
# 
#     qt_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
# @endif
# else()
#     if(ANDROID)
#         add_library(appWechat-Client SHARED
#             ${PROJECT_SOURCES}
#         )
# # Define properties for Android with Qt 5 after find_package() calls as:
# #    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#     else()
#         add_executable(appWechat-Client
#             ${PROJECT_SOURCES}
#         )
#     endif()
# @if false
# 
#     qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
# @endif
# endif()
# 
# target_link_libraries(appWechat-Client PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)
# 
# # Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# # If you are developing for iOS or macOS you should consider setting an
# # explicit, fixed bundle identifier manually though.
# if(${QT_VERSION} VERSION_LESS 6.1.0)
#   set(BUNDLE_ID_OPTION MACOSX_BUNDLE_GUI_IDENTIFIER com.example.appWechat-Client)
# endif()
# set_target_properties(appWechat-Client PROPERTIES
#     ${BUNDLE_ID_OPTION}
#     MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
#     MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
#     MACOSX_BUNDLE TRUE
#     WIN32_EXECUTABLE TRUE
# )
# 
# include(GNUInstallDirs)
# install(TARGETS appWechat-Client
#     BUNDLE DESTINATION .
#     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
#     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
# )
# 
# if(QT_VERSION_MAJOR EQUAL 6)
#     qt_finalize_executable(appWechat-Client)
# endif()
