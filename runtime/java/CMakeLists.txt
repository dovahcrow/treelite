find_package(JNI REQUIRED)

add_library(treelite4j SHARED treelite4j/src/native/treelite4j.cpp)
target_link_libraries(treelite4j
  PRIVATE   objtreelite_runtime objtreelite_common
  PUBLIC    ${JAVA_JVM_LIBRARY} dmlc)
target_include_directories(treelite4j PUBLIC ${JNI_INCLUDE_DIRS})
set_target_properties(treelite4j
  PROPERTIES
  POSITION_INDEPENDENT_CODE ON
  CXX_STANDARD 14
  CXX_STANDARD_REQUIRED ON)
