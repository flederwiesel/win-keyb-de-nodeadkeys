cmake_minimum_required(VERSION 3.25)

project(win-keyb-de-ndk)

function(add_target TARGET SWITCH)
	add_custom_target(${TARGET} ALL
		COMMAND kbdutool.exe -n ${SWITCH} -u ${PROJECT_SOURCE_DIR}/de_ndk.klc
		WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/${TARGET}
		DEPENDS mkdir_${TARGET}
	)

	add_custom_target(
		mkdir_${TARGET}
		COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_BINARY_DIR}/${TARGET}
	)

	install(DIRECTORY ${CMAKE_BINARY_DIR}/${TARGET} DESTINATION .)
endfunction()

add_target(i386 -x)
add_target(amd64 -m)
add_target(wow64 -o)
