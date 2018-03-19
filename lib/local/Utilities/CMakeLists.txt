SET(SOURCE
    src/ImageCapture.cpp
	src/RecorderCSV.cpp
    src/RecorderHOG.cpp
	src/RecorderOpenFace.cpp
    src/RecorderOpenFaceParameters.cpp
	src/SequenceCapture.cpp
	src/VisualizationUtils.cpp
	src/Visualizer.cpp
)

set(LIBNAME Utilities)

if(WIN32)
    add_library(${LIBNAME} STATIC ${SOURCE})
else()
    add_library(${LIBNAME} SHARED ${SOURCE})
endif()

target_include_directories(${LIBNAME} PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
    PRIVATE src)

set_property(TARGET ${LIBNAME} PROPERTY VERSION ${PROJECT_VERSION})
set_property(TARGET ${LIBNAME} PROPERTY SOVERSION ${PROJECT_VERSION_MAJOR})

target_link_libraries(${LIBNAME} boost blas opencv_highgui opencv_videoio)

install (TARGETS ${LIBNAME} EXPORT ${PROJECT_NAME}Targets
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})  # This is for Windows

install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})


