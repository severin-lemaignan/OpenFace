add_executable(FeatureExtraction FeatureExtraction.cpp)
target_link_libraries(FeatureExtraction 
                        LandmarkDetector 
                        FaceAnalyser 
                        GazeAnalyser 
                        Utilities 
                        boost
                        opencv_highgui)

install (TARGETS FeatureExtraction DESTINATION bin)
