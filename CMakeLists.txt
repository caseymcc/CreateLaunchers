cmake_minimum_required(VERSION 3.3) #config uses IN_LIST

project(CreateLaunchers VERSION 0.1.0)

#install
set(config_install_dir "lib/cmake/${PROJECT_NAME}")
set(generated_dir "${CMAKE_CURRENT_BINARY_DIR}/generated")
set(version_config "${generated_dir}/${PROJECT_NAME}ConfigVersion.cmake")
set(project_config "${generated_dir}/${PROJECT_NAME}Config.cmake")
set(MODULE_INSTALL_DIR "cmake/module")

include(CMakePackageConfigHelpers)

write_basic_package_version_file(
    "${version_config}" COMPATIBILITY SameMajorVersion
)

configure_package_config_file(
    cmake/Config.cmake.in
    ${project_config}
    INSTALL_DESTINATION "${config_install_dir}"
    PATH_VARS MODULE_INSTALL_DIR
)

#install config and version files
install(
    FILES "${project_config}" "${version_config}"
    DESTINATION "${config_install_dir}"
)

#install module files
install(
    FILES
        cmake/CreateLaunchers.cmake
        cmake/CleanDirectoryList.cmake
    DESTINATION ${MODULE_INSTALL_DIR}
)

#install templates
install(
    DIRECTORY
        cmake/launcher-templates
    DESTINATION ${MODULE_INSTALL_DIR}
)
