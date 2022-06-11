set(COMPONENT_NAME "Testing Utility")
set(COMPONENT_INTERNAL_NAME "gametest")

add_executable(gametest vpntest.c)

set_target_properties(gametest
  PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  LIBRARY_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  RUNTIME_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
)

if(WIN32)
  set_target_properties(gametest
    PROPERTIES
    PDB_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  )

  get_filename_component(COMPONENT_FILE_NAME gametest NAME)
  set(COMPONENT_FILE_NAME "${COMPONENT_FILE_NAME}.exe")

  configure_file("${TOP_DIRECTORY}/src/BuildFiles/VerScript/ver.rc" "${CMAKE_CURRENT_BINARY_DIR}/ver.rc")

  target_sources(gametest PRIVATE
    "vpntest.rc"
    "ver.rc"

    "${TOP_DIRECTORY}/src/BuildFiles/Manifests/common.manifest"
  )
endif()

target_link_libraries(gametest cedar)
