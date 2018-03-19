add_executable(FaceLandmarkVid FaceLandmarkVid.cpp)
target_link_libraries(FaceLandmarkVid 
                        LandmarkDetector 
                        FaceAnalyser 
                        GazeAnalyser 
                        Utilities 
                        dlib boost tbb
                        opencv_videoio
                        ${BLAS_LIBRARIES})

install (TARGETS FaceLandmarkVid DESTINATION bin)
