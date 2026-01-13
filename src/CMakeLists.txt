# src/CMakeLists.txt

add_executable(MyApp WIN32 MACOSX_BUNDLE
    main.cpp
)

set(SHARED_STATIC_ASSETS ../assets/dummy.txt)

install(TARGETS MyApp
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

target_link_libraries(MyApp
    # PUBLIC SDL2::SDL2
)

if (CMAKE_SYSTEM_NAME STREQUAL "Windows")
  include(platform/windows/CMakeLists.txt)
elseif (CMAKE_SYSTEM_NAME STREQUAL "Linux")
  include(../platform/linux/CMakeLists.txt)
elseif (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  include(platform/darwin/CMakeLists.txt)
endif ()
