# src/platform/linux/CMakeLists.txt

# Static assets
target_sources(MyApp PRIVATE ${SHARED_STATIC_ASSETS})

# Copy assets into app bundle
# For development:
add_custom_command(TARGET MyApp POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory
  ${PROJECT_SOURCE_DIR}/assets
  $<TARGET_FILE_DIR:MyApp>/../share)

# For distribution:
install(DIRECTORY ${PROJECT_SOURCE_DIR}/assets
  DESTINATION ${CMAKE_INSTALL_DATADIR})

set(ENTRY_NAME "com.wildgrowthsoftware.myapp")
configure_file(
    ${PROJECT_SOURCE_DIR/src/assets/manifests/MyApp.desktop.in
    ${CMAKE_CURRENT_BINARY_DIR}/${ENTRY_NAME}.desktop)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${ENTRY_NAME}.desktop
    DESTINATION share/applications)
install(FILES
    ${PROJECT_SOURCE_DIR}/src/assets/icons/mannicon.png
    DESTINATION share/pixmaps)

#------------------------------------------------------------

# Copy .so files on Linux to the target MyApp build folder.
# For development:
# add_custom_command(TARGET MyApp POST_BUILD
#   COMMAND ${CMAKE_COMMAND} -E copy_if_different
#   $<TARGET_FILE:SDL2::SDL2>
#   $<TARGET_FILE_DIR:MyApp>)
#
# # For distribution:
# install(FILES $<TARGET_FILE:SDL2::SDL2>
#   DESTINATION ${CMAKE_INSTALL_BINDIR}
#   RENAME MyApp_$<TARGET_FILE_NAME:SDL2::SDL2>)
