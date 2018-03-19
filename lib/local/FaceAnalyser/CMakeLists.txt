SET(SOURCE
    src/Face_utils.cpp
	src/FaceAnalyser.cpp
	src/FaceAnalyserParameters.cpp
	src/PAW.cpp
	src/PDM.cpp	
	src/SVM_dynamic_lin.cpp
	src/SVM_static_lin.cpp
	src/SVR_dynamic_lin_regressors.cpp
	src/SVR_static_lin_regressors.cpp
)

set(LIBNAME FaceAnalyser)

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

target_link_libraries(${LIBNAME} LandmarkDetector Utilities boost tbb)

install (TARGETS ${LIBNAME} EXPORT ${PROJECT_NAME}Targets
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})  # This is for Windows

install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})

