set(SCENE_QPAINTER_SRCS scene_qpainter.cpp)

add_library(KWinSceneQPainter MODULE scene_qpainter.cpp)
set_target_properties(KWinSceneQPainter PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/org.ukui.kwin.scenes/")
target_link_libraries(KWinSceneQPainter
    ukui-kwin
    SceneQPainterBackend
)

install(
    TARGETS
        KWinSceneQPainter
    DESTINATION
        ${PLUGIN_INSTALL_DIR}/org.ukui.kwin.scenes/
)
