SET(SOURCE
    src/CCNF_patch_expert.cpp
	src/LandmarkDetectionValidator.cpp
    src/LandmarkDetectorFunc.cpp
	src/LandmarkDetectorModel.cpp
    src/LandmarkDetectorUtils.cpp
	src/LandmarkDetectorParameters.cpp
	src/Patch_experts.cpp
	src/PAW.cpp
    src/PDM.cpp
	src/SVR_patch_expert.cpp
	src/stdafx.cpp
)

set(LIBNAME LandmarkDetector)

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

target_link_libraries(${LIBNAME} Utilities boost tbb dlib opencv_objdetect opencv_calib3d)

install (TARGETS ${LIBNAME} EXPORT ${PROJECT_NAME}Targets
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})  # This is for Windows

install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})

