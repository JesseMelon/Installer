# If using SDL:
# add_custom_command(TARGET MyEngine POST_BUILD
#   COMMAND ${CMAKE_COMMAND} -E copy_if_different
#   $<TARGET_FILE:SDL2::SDL2>
#   $<TARGET_FILE_DIR:MyEngine>/../Frameworks/$<TARGET_FILE_NAME:SDL2::SDL2>)
# Provided the root CMakeLiists.txt used find package.
# This is to conform with apple's sandboxing

# Combining shared with macOS assets
set(MACOSX_STATIC_ASSETS
    ${SHARED_STATIC_ASSETS}
    assets/icons/icon.icns)

# Static assets
set_source_files_properties(${MACOSX_STATIC_ASSETS}
  PROPERTIES MACOSX_PACKAGE_LOCATION ${CMAKE_INSTALL_DATADIR})
target_sources(MyApp PUBLIC ${MACOSX_STATIC_ASSETS})

if(NOT "${CMAKE_GENERATOR}" STREQUAL "Xcode")
# install (FILES $<TARGET_FILE:SDL2::SDL2>
#   DESTINATION $<TARGET_FILE_DIR:MyEngine>/../Frameworks/)
endif ()

set_target_properties(MyApp PROPERTIES
    INSTALL_RPATH @executable_path/../Frameworks
    RESOURCE "${MACOSX_STATIC_ASSETS}")

set_target_properties(MyApp PROPERTIES
  INSTALL_RPATH @executable_path/../Frameworks
  RESOURCE "${SHARED_STATIC_ASSETS}"
  MACOSX_BUNDLE_INFO_PLIST
    "${CMAKE_CURRENT_SOURCE_DIR}/assets/manifests/Info.plist"
  MACOSX_BUNDLE_BUNDLE_VERSION "${BUILD_VERSION}"
  MACOSX_BUNDLE_SHORT_VERSION_STRING "${PROJECT_VERSION}"
  MACOSX_BUNDLE_GUI_IDENTIFIER "com.mycompany.myapp"
  XCODE_ATTRIBUTE_PRODUCT_BUNDLE_IDENTIFIER "com.mycompany.myapp"
  MACOSX_BUNDLE_COPYRIGHT "(c) 2024 My Company")
