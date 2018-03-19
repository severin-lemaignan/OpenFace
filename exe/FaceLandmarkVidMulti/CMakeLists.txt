add_executable(FaceLandmarkVidMulti FaceLandmarkVidMulti.cpp)
target_link_libraries(FaceLandmarkVidMulti 
                        LandmarkDetector 
                        FaceAnalyser 
                        GazeAnalyser 
                        Utilities 
                        boost tbb
                        opencv_videoio
                        opencv_highgui
                        opencv_imgproc)

install (TARGETS FaceLandmarkVidMulti DESTINATION bin)
