cmake_minimum_required(VERSION 3.21)
project(dicom LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets)

find_package(VTK REQUIRED COMPONENTS
  CommonColor
  CommonCore
  FiltersSources
  InteractionStyle
  RenderingContextOpenGL2
  RenderingCore
  RenderingFreeType
  RenderingGL2PSOpenGL2
  RenderingOpenGL2
  GUISupportQt
)

qt_standard_project_setup()

qt_add_executable(dicom
    WIN32 MACOSX_BUNDLE
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
)

target_link_libraries(dicom
    PRIVATE
        Qt::Core
        Qt::Widgets
        VTK::CommonColor
        VTK::CommonCore
        VTK::FiltersSources
        VTK::InteractionStyle
        VTK::RenderingContextOpenGL2
        VTK::RenderingCore
        VTK::RenderingFreeType
        VTK::RenderingGL2PSOpenGL2
        VTK::RenderingOpenGL2
        VTK::GUISupportQt
)

include(GNUInstallDirs)

install(TARGETS dicom
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET dicom
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
