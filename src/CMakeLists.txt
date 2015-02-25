cmake_minimum_required(VERSION 2.6.0)

# Use root-config to auto-include ROOT (root-config must be in PATH)
EXEC_PROGRAM( root-config ARGS "--incdir" OUTPUT_VARIABLE ROOT_INCLUDE_DIR RETURN_VALUE RETVAR1)
MESSAGE("INFO: Found ROOT include path at ${ROOT_INCLUDE_DIR}")

EXEC_PROGRAM( root-config ARGS "--libdir" OUTPUT_VARIABLE ROOT_LIBRARY_DIR RETURN_VALUE RETVAR2)
MESSAGE("INFO: Found ROOT library path at ${ROOT_LIBRARY_DIR}")


IF(${RETVAR1}${RETVAR2} MATCHES "00")
	include_directories(${ROOT_INCLUDE_DIR})

	add_executable(jAnalyzer jAnalyzer.cpp)
	target_link_libraries(jAnalyzer -L${ROOT_LIBRARY_DIR} Core RIO Tree Hist MathCore)
ELSE()
	MESSAGE(FATAL_ERROR "ERROR: root-config did not provide LIBRARY and INCLUDE path, is ROOT installed and root-config in PATH?")
ENDIF()



 

