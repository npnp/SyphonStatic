# build syphon as static library
# Nenad Popov 2024

cmake_minimum_required(VERSION 3.21)

set(CMAKE_INSTALL_PREFIX "syphon" CACHE PATH "install prefix" FORCE)
set(CMAKE_OSX_ARCHITECTURES "arm64;x86_64" CACHE STRING "The list of target architectures to build" FORCE)
set(CMAKE_OBJC_FLAGS "-fobjc-arc")
set(CMAKE_OBJCXX_FLAGS "-fobjc-arc")

project(SyphonStatic)


## build

enable_language(OBJC)

include_directories("Syphon")

file(GLOB SOURCES Syphon/Syphon/*.m Syphon/Syphon/*.c Syphon/Syphon/*.metal)

add_library(SyphonStatic STATIC ${SOURCES})

target_precompile_headers(SyphonStatic PUBLIC "Syphon/Syphon/Syphon_Prefix.pch")

target_link_libraries(SyphonStatic "-framework IOSurface")


## install

install(TARGETS SyphonStatic DESTINATION lib)

install(FILES 
		Syphon/Syphon/SyphonSubclassing.h
		Syphon/Syphon/Syphon.h
		Syphon/Syphon/SyphonClient.h
		Syphon/Syphon/SyphonClientBase.h
		Syphon/Syphon/SyphonImage.h
		Syphon/Syphon/SyphonImageBase.h
		Syphon/Syphon/SyphonMetalClient.h
		Syphon/Syphon/SyphonMetalServer.h
		Syphon/Syphon/SyphonOpenGLClient.h
		Syphon/Syphon/SyphonOpenGLImage.h
		Syphon/Syphon/SyphonOpenGLServer.h
		Syphon/Syphon/SyphonServer.h
		Syphon/Syphon/SyphonServerBase.h
		Syphon/Syphon/SyphonServerDirectory.h
	DESTINATION include/Syphon)