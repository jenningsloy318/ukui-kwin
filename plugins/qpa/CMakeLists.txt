include_directories(${Qt5Core_PRIVATE_INCLUDE_DIRS})
include_directories(${Qt5Gui_PRIVATE_INCLUDE_DIRS})

set(QPA_SOURCES
    abstractplatformcontext.cpp
    backingstore.cpp
    eglhelpers.cpp
    integration.cpp
    main.cpp
    offscreensurface.cpp
    platformcursor.cpp
    screen.cpp
    sharingplatformcontext.cpp
    window.cpp
)

include(ECMQtDeclareLoggingCategory)
ecm_qt_declare_logging_category(QPA_SOURCES HEADER logging.h IDENTIFIER KWIN_QPA CATEGORY_NAME kwin_qpa_plugin DEFAULT_SEVERITY Critical)

add_library(UKUIKWinQpaPlugin MODULE ${QPA_SOURCES})
set_target_properties(UKUIKWinQpaPlugin PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/platforms/")

set(QT5PLATFORMSUPPORT_LIBS
    Qt5FontDatabaseSupport::Qt5FontDatabaseSupport
    Qt5ThemeSupport::Qt5ThemeSupport
    Qt5EventDispatcherSupport::Qt5EventDispatcherSupport
)

target_link_libraries(UKUIKWinQpaPlugin
    ${QT5PLATFORMSUPPORT_LIBS}
    ${FREETYPE_LIBRARIES} # Must be after QT5PLATFORMSUPPORT_LIBS
    Fontconfig::Fontconfig
    ukui-kwin
)

install(
    TARGETS
        UKUIKWinQpaPlugin
    DESTINATION
        ${PLUGIN_INSTALL_DIR}/platforms/
)
