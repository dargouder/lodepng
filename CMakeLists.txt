project(lodepng)

set(SOURCES lodepng.cpp)
add_library(lodepng STATIC ${SOURCES})

if(APPLE)
	add_custom_command(
		TARGET ${PROJECT_NAME} 
		POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy
		  $<TARGET_FILE:${PROJECT_NAME}>
		  ${CMAKE_SOURCE_DIR}/../builtDependencies/apple/$<CONFIGURATION>/$<TARGET_FILE_NAME:${PROJECT_NAME}>)
elseif(UNIX)
	add_custom_command(
		TARGET ${PROJECT_NAME} 
		POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy
			$<TARGET_FILE:${PROJECT_NAME}>
			${CMAKE_SOURCE_DIR}/../builtDependencies/unix/$<CONFIGURATION>/$<TARGET_FILE_NAME:${PROJECT_NAME}>)
elseif(WIN32)
	#copying built lib to the output
	add_custom_command(
		TARGET ${PROJECT_NAME} 
		POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:${PROJECT_NAME}>
			${CMAKE_SOURCE_DIR}/../builtDependencies/windows/$<CONFIGURATION>/$<TARGET_FILE_NAME:${PROJECT_NAME}>)		
endif()

file(COPY lodepng.h DESTINATION ${CMAKE_SOURCE_DIR}/../builtDependencies/includes/lodepng)
file(COPY lodepng_util.h DESTINATION ${CMAKE_SOURCE_DIR}/../builtDependencies/includes/lodepng)