# src/platform/windows/CMakeLists.txt

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

#------------------------------------------------------------

# Copy .dll files on Windows to the target MyApp build folder.

# For development:
# add_custom_command(TARGET MyApp POST_BUILD
#   COMMAND ${CMAKE_COMMAND} -E copy_if_different
#   $<TARGET_FILE:SDL2::SDL2>
#   $<TARGET_FILE_DIR:MyApp>)
#
# # For distribution:
# install(FILES $<TARGET_FILE:SDL2::SDL2>
#   DESTINATION ${CMAKE_INSTALL_BINDIR})
