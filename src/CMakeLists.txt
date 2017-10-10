set(SOURCE_FILES
        cmsalpha.c
        cmscam02.c
        cmscgats.c
        cmscnvrt.c
        cmserr.c
        cmsgamma.c
        cmsgmt.c
        cmshalf.c
        cmsintrp.c
        cmsio0.c
        cmsio1.c
        cmslut.c
        cmsmd5.c
        cmsmtrx.c
        cmsnamed.c
        cmsopt.c
        cmspack.c
        cmspcs.c
        cmsplugin.c
        cmsps2.c
        cmssamp.c
        cmssm.c
        cmstypes.c
        cmsvirt.c
        cmswtpnt.c
        cmsxform.c
)

set(PUBLIC_INCLUDE_FILES
        ../include/lcms2.h
        ../include/lcms2_plugin.h
)

add_library(lcms2 ${SOURCE_FILES} ${PUBLIC_INCLUDE_FILES})

target_include_directories(lcms2 PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
    $<INSTALL_INTERFACE:include>
)

include(GenerateExportHeader)

install(TARGETS lcms2 EXPORT lcms2Targets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(FILES ../include/lcms2.h ../include/lcms2_plugin.h
        DESTINATION include
)

install(FILES ${PUBLIC_INCLUDE_FILES}
        DESTINATION include/lcms2
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/lcms2/lcms2ConfigVersion.cmake"
    VERSION 2.8
    COMPATIBILITY AnyNewerVersion
)

export(EXPORT lcms2Targets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/lcms2/lcms2Targets.cmake"
  NAMESPACE lcms2::
)
configure_file(../cmake/lcms2Config.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/lcms2/lcms2Config.cmake"
    COPYONLY
)

set(ConfigPackageLocation lib/cmake/lcms2)
install(EXPORT lcms2Targets
  FILE
    lcms2Targets.cmake
  NAMESPACE
    lcms2::
  DESTINATION
    ${ConfigPackageLocation}
)
install(
  FILES
    ../cmake/lcms2Config.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/lcms2/lcms2ConfigVersion.cmake"
  DESTINATION
    ${ConfigPackageLocation}
  COMPONENT
    Devel
)

# Define alias to be able to refer to target lcms2::lcms2 when using lcms2 as a subproject
# This technique is explained here:
# https://github.com/boostcon/cppnow_presentations_2017/blob/master/05-19-2017_friday/effective_cmake__daniel_pfeifer__cppnow_05-19-2017.pdf
add_library(lcms2::lcms2 ALIAS lcms2)
