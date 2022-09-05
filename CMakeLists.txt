cmake_minimum_required(VERSION 3.14)

project("hwinfo-playground")


add_library(hwinfo STATIC IMPORTED)

set_property(
  TARGET hwinfo APPEND PROPERTY IMPORTED_CONFIGURATIONS RELEASE
)

set_target_properties(hwinfo PROPERTIES
  IMPORTED_LINK_INTERFACE_LANGUAGES_RELEASE "CXX"
  IMPORTED_LOCATION_RELEASE "${HWINFO_ROOT}/lib/HWinfo.lib"
)
  
set_target_properties(hwinfo PROPERTIES
  MAP_IMPORTED_CONFIG_MINSIZEREL Release
  MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
)

target_include_directories(hwinfo INTERFACE "${HWINFO_ROOT}/include")

add_executable(${PROJECT_NAME} 
    "src/main.cpp"
)

target_link_libraries(${PROJECT_NAME} hwinfo)


