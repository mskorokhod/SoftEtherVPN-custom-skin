if(NOT WIN32)
  message(FATAL_ERROR "VPN Setup is available only for Windows.")
endif()

set(COMPONENT_NAME "Setup")
set(COMPONENT_INTERNAL_NAME "gamesetup")

add_executable(gamesetup WIN32
  "vpnsetup.c"
  "vpnsetup.rc"

  "${TOP_DIRECTORY}/src/BuildFiles/Manifests/common.manifest"
)

get_filename_component(COMPONENT_FILE_NAME gamesetup NAME)
set(COMPONENT_FILE_NAME "${COMPONENT_FILE_NAME}.exe")

configure_file("${TOP_DIRECTORY}/src/BuildFiles/VerScript/ver.rc" "${CMAKE_CURRENT_BINARY_DIR}/ver.rc")
target_sources(gamesetup PRIVATE "vpnsetup.rc" "${CMAKE_CURRENT_BINARY_DIR}/ver.rc")

set_target_properties(gamesetup
  PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  LIBRARY_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  RUNTIME_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
  PDB_OUTPUT_DIRECTORY "${BUILD_DIRECTORY}"
)

target_link_libraries(gamesetup cedar)
