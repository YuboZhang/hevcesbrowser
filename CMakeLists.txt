cmake_minimum_required(VERSION 3.12)

project(HEVCESBROWSER)

set (BUILD_DIR
	${CMAKE_CURRENT_SOURCE_DIR}/build
)

if(NOT IS_DIRECTORY ${BUILD_DIR})
	file (MAKE_DIRECTORY
		${BUILD_DIR}
	)
endif()

set (EXECUTABLE_OUTPUT_PATH ${BUILD_DIR})
set (LIBRARY_OUTPUT_PATH ${BUILD_DIR})

ADD_DEFINITIONS(-std=c++11)
if(MINGW)
	#for workaround https://github.com/g-truc/glm/issues/300#issue-54185474%C2%A0
	ADD_DEFINITIONS(-D__NO_INLINE__)
endif()
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
endif()
add_subdirectory(hevcparser)
add_subdirectory(utils)
enable_testing()
