# The name of our project is "HELLO". CMakeLists files in this project can
# refer to the root source directory of the project as ${HELLO_SOURCE_DIR} and
# to the root binary directory of the project as ${HELLO_BINARY_DIR}.
cmake_minimum_required (VERSION 2.6)

#if(COMMAND cmake_policy)
#  if(POLICY CMP0005)
#    cmake_policy(SET CMP0005 NEW) # automatic quoting of brackets
#  endif(POLICY CMP0005)

#  if(POLICY CMP0011)
    # we do want the includer to be affected by our updates,
    # since it might define project-global settings.
#    cmake_policy(SET CMP0011 OLD)
#  endif(POLICY CMP0011)
#  if(POLICY CMP0015)
    # .vcproj contains relative paths to additional library directories, thus we need to be able to cope with that
#    cmake_policy(SET CMP0015 NEW)
#  endif(POLICY CMP0015)
#endif(COMMAND cmake_policy)
SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/")


#include_directories (${PROJECT_SOURCE_DIR}  {LIBUSB_1_INCLUDE_DIRS} )
project( MfgToolLib )

find_package(libusb-1.0 REQUIRED)
include_directories(${LIBUSB_1_INCLUDE_DIRS})
set(LIBS ${LIBS} ${LIBUSB_1_LIBRARIES})

    set(SOURCES_files
      CmdOperation.cpp
      ControllerClass.cpp
      Device.cpp
      DeviceClass.cpp
      DeviceManager.cpp
      Disk.cpp
      DiskDeviceClass.cpp
      ExceptionHandle.cpp
      HidDevice.cpp
      HidDeviceClass.cpp
      HubClass.cpp
      LogMgr.cpp
      MfgToolLib.cpp
      MfgToolLib.def
      MxHidDevice.cpp
      MxHidDeviceClass.cpp
      MxRomDevice.cpp
      MxRomDeviceClass.cpp
      ParameterT.cpp
      SetupApi.cpp
      StApi.cpp
      stdafx.cpp
      StFwComponent.cpp
      StHidApi.cpp
      StPitc.cpp
      StVersionInfo.cpp
      UpdateTransportProtocol.cpp
      UsbController.cpp
      UsbHub.cpp
      UsbPort.cpp
      Volume.cpp
      VolumeDeviceClass.cpp
			libusbVolume.cpp
      XMLite.cpp
      CdcDeviceClass.cpp
      CdcDevice.cpp
      KblHidDeviceClass.cpp
    )
    source_group("Source Files" FILES ${SOURCES_files})

    set(SOURCES_Source_Files
      ${SOURCES_files}
    )

    set(SOURCES_Header_Files
      CallbackDef.h
      CmdOperation.h
      ControllerClass.h
      Device.h
      DeviceClass.h
      DeviceManager.h
      Disk.h
      DiskDeviceClass.h
      ExceptionHandle.h
      HidDevice.h
      HidDeviceClass.h
      HubClass.h
      LogMgr.h
      MfgToolLib.h
      MfgToolLib_Export.h
      MxHidDevice.h
      MxHidDeviceClass.h
      MxRomDevice.h
      MxRomDeviceClass.h
      ParameterT.h
      Property.h
      SetupApi.h
      StApi.h
      StApiFactory.h
      stdafx.h
      StFwComponent.h
      StHidApi.h
      StMedia.h
      StPitc.h
      StVersionInfo.h
      targetver.h
      UpdateTransportProtocol.Api.h
      UpdateTransportProtocol.h
      UpdateUIInfo.h
      UsbController.h
      UsbHub.h
      UsbPort.h
      version.h
      Volume.h
      VolumeDeviceClass.h
			libusbVolume.h
			CString.h
      WindowsVersionInfo.h
      XMLite.h
    )
    source_group("Header Files" FILES ${SOURCES_Header_Files})

    set(SOURCES_Header_Files
      ${SOURCES_Header_Files}
    )

  set(SOURCES_
    ${SOURCES_Source_Files}
    ${SOURCES_Header_Files}
  )

include_directories(BEFORE ${PROJECT_SOURCE_DIR}  )
SET( CMAKE_VERBOSE_MAKEFILE on )

if(CMAKE_BUILD_TYPE STREQUAL "Debug")

  set(CMAKE_CXX_FLAGS "-g")


  set(SOURCES ${SOURCES_})



  add_library( MfgToolLib ${SOURCES} )



endif(CMAKE_BUILD_TYPE STREQUAL "Debug")
if(TARGET MfgToolLib)

  set_property(TARGET MfgToolLib APPEND PROPERTY COMPILE_DEFINITIONS_DEBUG
    WIN32
    _CRT_SECURE_NO_DEPRECATE
    _DEBUG
    _USRDLL
    _WINDOWS
  )
endif(TARGET MfgToolLib)

if(CMAKE_CONFIGURATION_TYPES OR CMAKE_BUILD_TYPE STREQUAL "Release")


  set(SOURCES  ${SOURCES_})


  add_library( MfgToolLib ${SOURCES} )


endif(CMAKE_CONFIGURATION_TYPES OR CMAKE_BUILD_TYPE STREQUAL "Release")
if(TARGET MfgToolLib)

  set_property(TARGET MfgToolLib APPEND PROPERTY COMPILE_DEFINITIONS_RELEASE
    NDEBUG
    WIN32
    _CRT_SECURE_NO_DEPRECATE
    _USRDLL
    _WINDOWS
  )
endif(TARGET MfgToolLib)
set (CMAKE_CXX_FLAGS "-std=c++11 -O0 -fpic -I/usr/lib/jvm/java-8-oracle/include -I/usr/lib/jvm/java-8-oracle/include/linux -fpermissive -g -Wno-write-strings")
set(SOURCES ${SOURCES_})

add_library( MfgToolLib SHARED ${SOURCES} )
add_library( MfgToolLibStatic STATIC ${SOURCES} )
target_link_libraries(MfgToolLib ${LIBS})
