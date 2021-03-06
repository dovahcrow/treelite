add_executable(treelite_cpp_test)
set_target_properties(treelite_cpp_test
    PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON)
target_link_libraries(treelite_cpp_test
    PRIVATE objtreelite objtreelite_runtime objtreelite_common rapidjson
    GTest::GTest GTest::gmock)
set_output_directory(treelite_cpp_test ${PROJECT_BINARY_DIR})

if(MSVC)
  target_compile_options(treelite_cpp_test PRIVATE
                         /utf-8 -D_CRT_SECURE_NO_WARNINGS -D_CRT_SECURE_NO_DEPRECATE)
endif()

if(TEST_COVERAGE)
  if(MSVC)
    message(FATAL_ERROR "Test coverage not available on Windows")
  endif()
  target_compile_options(treelite_cpp_test PUBLIC -g -O0 --coverage)
  target_link_options(treelite_cpp_test PUBLIC --coverage)
endif()

target_sources(treelite_cpp_test
  PRIVATE  test_main.cc
           test_serializer.cc
           test_frontend.cc
)

target_include_directories(treelite_cpp_test
  PRIVATE  ../../src/frontend
)

msvc_use_static_runtime()
