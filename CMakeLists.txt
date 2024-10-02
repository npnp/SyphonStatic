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

include_directories(".")

file(GLOB SOURCES Syphon/*.m Syphon/*.c Syphon/*.metal)

add_library(SyphonStatic STATIC ${SOURCES})

target_precompile_headers(SyphonStatic PUBLIC "Syphon/Syphon_Prefix.pch")

target_link_libraries(SyphonStatic "-framework IOSurface")


## install

install(TARGETS SyphonStatic DESTINATION lib)

install(FILES 
		Syphon/SyphonSubclassing.h
		Syphon/Syphon.h
		Syphon/SyphonClient.h
		Syphon/SyphonClientBase.h
		Syphon/SyphonImage.h
		Syphon/SyphonImageBase.h
		Syphon/SyphonMetalClient.h
		Syphon/SyphonMetalServer.h
		Syphon/SyphonOpenGLClient.h
		Syphon/SyphonOpenGLImage.h
		Syphon/SyphonOpenGLServer.h
		Syphon/SyphonServer.h
		Syphon/SyphonServerBase.h
		Syphon/SyphonServerDirectory.h
	DESTINATION include/Syphon)