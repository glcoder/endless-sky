cmake_minimum_required(VERSION 3.1)

project(endless-sky)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake")

file(GLOB SOURCE_FILES source/*.cpp source/*.h)

find_package(SDL2 REQUIRED)
find_package(OpenAL REQUIRED)
find_package(GLEW REQUIRED)
find_package(PNG REQUIRED)
find_package(JPEG REQUIRED)
find_package(ZLIB REQUIRED)

add_definitions("-std=c++11")

include_directories(
	${PROJECT_SOURCE_DIR}/source
	${SDL2_INCLUDE_DIR}
	${OPENAL_INCLUDE_DIR}
	${GLEW_INCLUDE_DIR}
	${PNG_PNG_INCLUDE_DIR}
	${JPEG_INCLUDE_DIR}
	${ZLIB_INCLUDE_DIR}
)

link_libraries(
	${SDL2_LIBRARY}
	${OPENAL_LIBRARY}
	${GLEW_LIBRARY}
	${PNG_LIBRARY_RELEASE}
	${JPEG_LIBRARY}
	${ZLIB_LIBRARY}
)

if(WIN32)
link_libraries(winmm imm32 version opengl32)
endif()

if(MINGW)
link_libraries(-mwindows)
endif()

add_executable(endless-sky ${SOURCE_FILES})
