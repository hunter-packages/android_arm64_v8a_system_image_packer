# Copyright (c) 2018, Ruslan Baratov
# All rights reserved.

cmake_minimum_required(VERSION 3.3)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.40.tar.gz"
    SHA1 "a500979296b4b6b1542a2881151ceb9c984f3e36"
)

project(android_arm64_v8a_system_image_packer)

hunter_add_package(android_sdk_packer)

# android_sdk_packer_unified_install
# android_sdk_packer_parse_version_revision
find_package(android_sdk_packer CONFIG REQUIRED)

hunter_add_package(Android-ARM64-v8a-System-Image)
file(GLOB x "${ANDROID-ARM64-V8A-SYSTEM-IMAGE_ROOT}/*")

android_sdk_packer_parse_version_revision(
    FULL "${HUNTER_Android-ARM64-v8a-System-Image_VERSION}"
    VERSION version
    REVISION revision
)

android_sdk_packer_unified_install(
    OBJECTS ${x}
    DESTINATION "system-images/android-${version}/default/arm64-v8a"
)
