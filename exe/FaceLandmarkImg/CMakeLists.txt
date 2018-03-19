add_executable(FaceLandmarkImg FaceLandmarkImg.cpp)
target_link_libraries(FaceLandmarkImg 
                        LandmarkDetector 
                        FaceAnalyser 
                        GazeAnalyser 
                        Utilities 
                        boost
                        opencv_highgui)

install (TARGETS FaceLandmarkImg DESTINATION bin)
