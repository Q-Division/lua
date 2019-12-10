cmake_minimum_required (VERSION 3.1)
project (Lua)

set(CMAKE_CXX_STANDARD 14)

set(LUA_ROOT "${CMAKE_CURRENT_SOURCE_DIR}" CACHE INTERNAL "")

message("LUA_ROOT: ${LUA_ROOT}")
message("BINDIR: ${CMAKE_BINARY_DIR}")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/Build/Bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/Build/Lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

message("ROD: ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}")
message("LOD: ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}")
message("AOD: ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}")

set(source_list
	"${CMAKE_CURRENT_LIST_DIR}/lapi.c"
	"${CMAKE_CURRENT_LIST_DIR}/lcode.c"
	"${CMAKE_CURRENT_LIST_DIR}/lctype.c"
	"${CMAKE_CURRENT_LIST_DIR}/ldebug.c"
	"${CMAKE_CURRENT_LIST_DIR}/ldo.c"
	"${CMAKE_CURRENT_LIST_DIR}/ldump.c"
	"${CMAKE_CURRENT_LIST_DIR}/lfunc.c"
	"${CMAKE_CURRENT_LIST_DIR}/lgc.c"
	"${CMAKE_CURRENT_LIST_DIR}/llex.c"
	"${CMAKE_CURRENT_LIST_DIR}/lmem.c"
	"${CMAKE_CURRENT_LIST_DIR}/lobject.c"
	"${CMAKE_CURRENT_LIST_DIR}/lopcodes.c"
	"${CMAKE_CURRENT_LIST_DIR}/lparser.c"
	"${CMAKE_CURRENT_LIST_DIR}/lstate.c"
	"${CMAKE_CURRENT_LIST_DIR}/lstring.c"
	"${CMAKE_CURRENT_LIST_DIR}/ltable.c"
	"${CMAKE_CURRENT_LIST_DIR}/ltm.c"
	"${CMAKE_CURRENT_LIST_DIR}/lundump.c"
	"${CMAKE_CURRENT_LIST_DIR}/lvm.c"
	"${CMAKE_CURRENT_LIST_DIR}/lzio.c"
	"${CMAKE_CURRENT_LIST_DIR}/lauxlib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lbaselib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lbitlib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lcorolib.c"
	"${CMAKE_CURRENT_LIST_DIR}/ldblib.c"
	"${CMAKE_CURRENT_LIST_DIR}/liolib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lmathlib.c"
	"${CMAKE_CURRENT_LIST_DIR}/loslib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lstrlib.c"
	"${CMAKE_CURRENT_LIST_DIR}/ltablib.c"
	"${CMAKE_CURRENT_LIST_DIR}/lutf8lib.c"
	"${CMAKE_CURRENT_LIST_DIR}/loadlib.c"
	"${CMAKE_CURRENT_LIST_DIR}/linit.c"
)

include_directories("${CMAKE_CURRENT_LIST_DIR}")

if(WIN32)
	add_library(Lua SHARED ${source_list})
	target_compile_definitions(Lua PRIVATE LUA_BUILD_AS_DLL=1)
else()
	add_library(Lua ${source_list})
endif()

set_target_properties(Lua PROPERTIES OUTPUT_NAME "lua53$<$<CONFIG:Debug>:d>")