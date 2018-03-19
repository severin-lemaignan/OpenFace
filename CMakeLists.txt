cmake_minimum_required (VERSION 3.0 FATAL_ERROR)
project (OpenFace VERSION 0.4.2)

# Must use GNUInstallDirs to install libraries into correct
# locations on all platforms.
include(GNUInstallDirs)

message("##### This is OpenFace version ${PROJECT_VERSION} #####") 


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

set(CMAKE_CONFIG_DIR etc/OpenFace)
set(CONFIG_DIR "${CMAKE_INSTALL_PREFIX}/${CMAKE_CONFIG_DIR}")
add_definitions(-DCONFIG_DIR="${CONFIG_DIR}")

# Include BLAS as an imported target
find_package(BLAS REQUIRED)
add_library(blas INTERFACE IMPORTED)
set_property(TARGET blas PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${BLAS_INCLUDE_DIRS})
set_property(TARGET blas PROPERTY INTERFACE_LINK_LIBRARIES ${BLAS_LIBRARIES} ${BLAS95_LIBRARIES})
message("BLAS information:") 
message("  BLAS libraries: ${BLAS_LIBRARIES} ${BLAS95_LIBRARIES}") 

# Include OpenCV as an imported target
find_package(OpenCV 3.3 CONFIG REQUIRED core imgproc objdetect highgui videoio calib3d)
message("OpenCV information:") 
message("  Found OpenCV ${OpenCV_VERSION}") 
message("  OpenCV_INCLUDE_DIRS: ${OpenCV_INCLUDE_DIRS}") 
message("  OpenCV_LIBRARIES: ${OpenCV_LIBRARIES}") 
message("  OpenCV_LIBRARY_DIRS: ${OpenCV_LIBRARY_DIRS}") 

# Include Boost as an imported target
find_package(Boost 1.5.9 REQUIRED COMPONENTS filesystem system)
add_library(boost INTERFACE IMPORTED)
set_property(TARGET boost PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${Boost_INCLUDE_DIRS})
set_property(TARGET boost PROPERTY INTERFACE_LINK_LIBRARIES ${Boost_LIBRARIES})
message("Boost information:") 
message("  Found Boost ${Boost_VERSION}") 
message("  Boost_INCLUDE_DIRS: ${Boost_INCLUDE_DIRS}") 
message("  Boost_LIBRARIES: ${Boost_LIBRARIES}") 
message("  Boost_LIBRARY_DIRS: ${Boost_LIBRARY_DIRS}") 

# Include TBB as an imported target
find_package(TBB REQUIRED)
add_library(tbb INTERFACE IMPORTED)
set_property(TARGET tbb PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${TBB_INCLUDE_DIR})
set_property(TARGET tbb PROPERTY INTERFACE_LINK_LIBRARIES ${TBB_LIBRARIES})
message("Found TBB ${TBB_VERSION}") 


# Move LandmarkDetector model
file(GLOB files "lib/local/LandmarkDetector/model/*.txt")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model)
endforeach()

# Move the hierarchical LandmarkDetector models
file(GLOB files "lib/local/LandmarkDetector/model/model*")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model)
	endif(MSVC)

	install(DIRECTORY ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model)
endforeach()

file(GLOB files "lib/local/LandmarkDetector/model/detection_validation/*.txt")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model/detection_validation)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model/detection_validation)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model/detection_validation)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model/detection_validation)
endforeach()

file(GLOB files "lib/local/LandmarkDetector/model/patch_experts/*.txt")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model/patch_experts)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model/patch_experts)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model/patch_experts)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model/patch_experts)
endforeach()

file(GLOB files "lib/local/LandmarkDetector/model/patch_experts/*.dat")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model/patch_experts)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model/patch_experts)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model/patch_experts)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model/patch_experts)
endforeach()

file(GLOB files "lib/local/LandmarkDetector/model/pdms/*.txt")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/model/pdms)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/model/pdms)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/model/pdms)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/model/pdms)
endforeach()

# Move OpenCV classifiers
file(GLOB files "lib/3rdParty/OpenCV3.1/classifiers/*.xml")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/classifiers)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/classifiers)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/classifiers)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/classifiers)
endforeach()

# Move AU prediction modules
file(GLOB files "lib/local/FaceAnalyser/AU_predictors/*.txt")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/AU_predictors)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/AU_predictors)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/AU_predictors)
	endif(MSVC)

	install(FILES ${file} DESTINATION ${CMAKE_CONFIG_DIR}/AU_predictors)
endforeach()

# Move AU prediction modules
file(GLOB files "lib/local/FaceAnalyser/AU_predictors/svr*")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/AU_predictors)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/AU_predictors)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/AU_predictors)
	endif(MSVC)

	install(DIRECTORY ${file} DESTINATION ${CMAKE_CONFIG_DIR}/AU_predictors)
endforeach()

# Move AU prediction modules
file(GLOB files "lib/local/FaceAnalyser/AU_predictors/svm*")
foreach(file ${files})
	if (MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Debug/AU_predictors)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/Release/AU_predictors)
	else(MSVC)
		file(COPY ${file} DESTINATION ${CMAKE_BINARY_DIR}/bin/AU_predictors)
	endif(MSVC)

	install(DIRECTORY ${file} DESTINATION ${CMAKE_CONFIG_DIR}/AU_predictors)
endforeach()

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
    execute_process(COMMAND ${CMAKE_CXX_COMPILER} -dumpversion OUTPUT_VARIABLE GCC_VERSION)
    if (GCC_VERSION VERSION_LESS 4.7)
        set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -msse -msse2 -msse3")
    else ()
        set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -msse -msse2 -msse3")
    endif ()
else ()
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -msse -msse2 -msse3")
endif ()

# Boost
if(WIN32)
	include_directories(lib/3rdParty/boost)
	include_directories(lib/3rdParty/boost/boost)
	link_directories( ${PROJECT_SOURCE_DIR}/lib/3rdParty/boost/lib )
endif()

# dlib
find_package(dlib 18.18 CONFIG)
 
if(${dlib_FOUND})
	add_library(dlib INTERFACE IMPORTED)
	set_property(TARGET dlib PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${dlib_INCLUDE_DIRS})
	set_property(TARGET dlib PROPERTY INTERFACE_LINK_LIBRARIES ${dlib_LIBRARIES})

	message("dlib information:") 
	message("  Found dlib version: ${dlib_VERSION}") 
	message("  dlib_INCLUDE_DIRS: ${dlib_INCLUDE_DIRS}") 
else()
	message(WARNING "dlib not found in the system. We will compile it.") 
	include_directories(lib/3rdParty/dlib/include)

	# dlib library
	add_subdirectory(lib/3rdParty/dlib)

endif()

# LandmarkDetector library
add_subdirectory(lib/local/LandmarkDetector)
# Facial Expression analysis library
add_subdirectory(lib/local/FaceAnalyser)
# Gaze library
add_subdirectory(lib/local/GazeAnalyser)
# Utilities library
add_subdirectory(lib/local/Utilities)

# executables
add_subdirectory(exe/FaceLandmarkImg)
add_subdirectory(exe/FaceLandmarkVid)
add_subdirectory(exe/FaceLandmarkVidMulti)
add_subdirectory(exe/FeatureExtraction)


# generation of OpenFaceConfig.cmake
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/${PROJECT_NAME}ConfigVersion.cmake"
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

# This makes the project importable from the build directory
export(EXPORT ${PROJECT_NAME}Targets
	FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/${PROJECT_NAME}Targets.cmake"
	NAMESPACE OpenFace::
)
configure_file(cmake/${PROJECT_NAME}Config.cmake
			   "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/${PROJECT_NAME}Config.cmake"
			   COPYONLY
)

set(ConfigPackageLocation share/${PROJECT_NAME}/cmake)

# This makes the project importable from the install directory
install(EXPORT ${PROJECT_NAME}Targets
	FILE ${PROJECT_NAME}Targets.cmake
		NAMESPACE OpenFace::
		DESTINATION ${ConfigPackageLocation}
)

install(FILES
	"${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/${PROJECT_NAME}ConfigVersion.cmake"
	"${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/${PROJECT_NAME}Config.cmake"
  DESTINATION ${ConfigPackageLocation}
)

