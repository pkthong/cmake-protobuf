option(protobuf_BUILD_SHARED_LIBS "Build Protobuf as Shared Library" OFF)
option(protobuf_BUILD_TESTS "Build Protobuf Tests" ON)

# Useful CMake helper functions
#set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMake;${CMAKE_MODULE_PATH}")
include(cmake/FlagUtilities.cmake)
include (CheckFunctionExists)
include (CheckIncludeFile)
include (CheckIncludeFiles)
include (CheckLibraryExists)
include (CheckSymbolExists)
include (CheckTypeSize)
include (CheckCXXSourceCompiles)
include (CheckCSourceCompiles)

# Protocol Buffers with CMake   
PROJECT(protobuf C CXX)

cmake_minimum_required(VERSION 2.8)

find_package(Threads REQUIRED)
include_directories(src src/google/protobuf ${CMAKE_CURRENT_BINARY_DIR})

set(protobuf_COMMON_SRCS
   src/google/protobuf/stubs/atomicops.h
   src/google/protobuf/stubs/atomicops_internals_arm_gcc.h
   src/google/protobuf/stubs/atomicops_internals_arm_qnx.h
   src/google/protobuf/stubs/atomicops_internals_atomicword_compat.h
   src/google/protobuf/stubs/atomicops_internals_macosx.h
   src/google/protobuf/stubs/atomicops_internals_mips_gcc.h
   src/google/protobuf/stubs/atomicops_internals_pnacl.h
   src/google/protobuf/stubs/atomicops_internals_x86_gcc.h
   src/google/protobuf/stubs/atomicops_internals_x86_msvc.h
   src/google/protobuf/stubs/common.h
   src/google/protobuf/stubs/platform_macros.h
   src/google/protobuf/stubs/once.h
   src/google/protobuf/stubs/template_util.h
   src/google/protobuf/stubs/type_traits.h
   src/google/protobuf/descriptor.h
   src/google/protobuf/descriptor.pb.h
   src/google/protobuf/descriptor_database.h
   src/google/protobuf/dynamic_message.h
   src/google/protobuf/extension_set.h
   src/google/protobuf/generated_enum_reflection.h
   src/google/protobuf/generated_message_util.h
   src/google/protobuf/generated_message_reflection.h
   src/google/protobuf/message.h
   src/google/protobuf/message_lite.h
   src/google/protobuf/reflection_ops.h
   src/google/protobuf/repeated_field.h
   src/google/protobuf/service.h
   src/google/protobuf/text_format.h
   src/google/protobuf/unknown_field_set.h
   src/google/protobuf/wire_format.h
   src/google/protobuf/wire_format_lite.h
   src/google/protobuf/wire_format_lite_inl.h
   src/google/protobuf/io/coded_stream.h
   src/google/protobuf/io/printer.h
   src/google/protobuf/io/tokenizer.h
   src/google/protobuf/io/zero_copy_stream.h
   src/google/protobuf/io/zero_copy_stream_impl.h
   src/google/protobuf/io/zero_copy_stream_impl_lite.h
   src/google/protobuf/compiler/code_generator.h
   src/google/protobuf/compiler/command_line_interface.h
   src/google/protobuf/compiler/importer.h
   src/google/protobuf/compiler/parser.h
   src/google/protobuf/compiler/plugin.h
   src/google/protobuf/compiler/plugin.pb.h
   src/google/protobuf/compiler/cpp/cpp_generator.h
   src/google/protobuf/compiler/java/java_generator.h
   src/google/protobuf/compiler/python/python_generator.h
   )
 #  $(GZHEADERS)

set(libprotobuf_lite_SRCS
   src/google/protobuf/stubs/atomicops.h
   src/google/protobuf/stubs/atomicops_internals_arm_gcc.h
   src/google/protobuf/stubs/atomicops_internals_atomicword_compat.h
   src/google/protobuf/stubs/atomicops_internals_macosx.h
   src/google/protobuf/stubs/atomicops_internals_mips_gcc.h
   src/google/protobuf/stubs/atomicops_internals_x86_gcc.cc
   src/google/protobuf/stubs/atomicops_internals_x86_gcc.h
   src/google/protobuf/stubs/atomicops_internals_x86_msvc.cc
   src/google/protobuf/stubs/atomicops_internals_x86_msvc.h
   src/google/protobuf/stubs/common.h
   src/google/protobuf/stubs/once.h
   src/google/protobuf/stubs/platform_macros.h
   src/google/protobuf/extension_set.h
   src/google/protobuf/generated_message_util.h
   src/google/protobuf/message_lite.h
   src/google/protobuf/repeated_field.h
   src/google/protobuf/unknown_field_set.cc
   src/google/protobuf/unknown_field_set.h
   src/google/protobuf/wire_format_lite.h
   src/google/protobuf/wire_format_lite_inl.h
   src/google/protobuf/io/coded_stream.h
   src/google/protobuf/io/zero_copy_stream.h
   src/google/protobuf/io/zero_copy_stream_impl_lite.h

   src/google/protobuf/stubs/common.cc
   src/google/protobuf/stubs/once.cc
   src/google/protobuf/stubs/hash.h
   src/google/protobuf/stubs/map-util.h
   src/google/protobuf/extension_set.cc
   src/google/protobuf/generated_message_util.cc
   src/google/protobuf/message_lite.cc
   src/google/protobuf/repeated_field.cc
   src/google/protobuf/wire_format_lite.cc
   src/google/protobuf/io/coded_stream.cc
   src/google/protobuf/io/coded_stream_inl.h
   src/google/protobuf/io/zero_copy_stream.cc
   src/google/protobuf/io/zero_copy_stream_impl_lite.cc
   )

 set(libprotobuf_SRCS
    ${libprotobuf_lite_SRCS}
    src/google/protobuf/descriptor.h
    src/google/protobuf/descriptor.pb.h
    src/google/protobuf/descriptor_database.h
    src/google/protobuf/dynamic_message.h
    src/google/protobuf/generated_enum_reflection.h
    src/google/protobuf/generated_message_reflection.h
    src/google/protobuf/message.h
    src/google/protobuf/reflection_ops.h
    src/google/protobuf/service.h
    src/google/protobuf/text_format.h
    src/google/protobuf/wire_format.h
    src/google/protobuf/io/gzip_stream.h
    src/google/protobuf/io/printer.h
    src/google/protobuf/io/tokenizer.h
    src/google/protobuf/io/zero_copy_stream_impl.h
    src/google/protobuf/compiler/code_generator.h
    src/google/protobuf/compiler/command_line_interface.h
    src/google/protobuf/compiler/importer.h
    src/google/protobuf/compiler/java/java_doc_comment.cc
    src/google/protobuf/compiler/java/java_doc_comment.h
    src/google/protobuf/compiler/parser.h
    src/google/protobuf/stubs/strutil.cc
    src/google/protobuf/stubs/strutil.h
    src/google/protobuf/stubs/substitute.cc
    src/google/protobuf/stubs/substitute.h
    src/google/protobuf/stubs/stl_util.h
    src/google/protobuf/stubs/stringprintf.cc
    src/google/protobuf/stubs/stringprintf.h
    src/google/protobuf/stubs/structurally_valid.cc
    src/google/protobuf/stubs/template_util.h
    src/google/protobuf/stubs/type_traits.h
    src/google/protobuf/descriptor.cc
    src/google/protobuf/descriptor.pb.cc
    src/google/protobuf/descriptor_database.cc
    src/google/protobuf/dynamic_message.cc
    src/google/protobuf/extension_set.cc
    src/google/protobuf/extension_set.h
    src/google/protobuf/extension_set_heavy.cc
    src/google/protobuf/generated_message_reflection.cc
    src/google/protobuf/message.cc
    src/google/protobuf/reflection_ops.cc
    src/google/protobuf/service.cc
    src/google/protobuf/text_format.cc
    src/google/protobuf/wire_format.cc
    # This file pulls in zlib, but it's not actually used by protoc, so
    # instead of compiling zlib for the host, let's just exclude this.
    # src/src/google/protobuf/io/gzip_stream.cc
    src/google/protobuf/io/printer.cc
    src/google/protobuf/io/tokenizer.cc
    src/google/protobuf/io/zero_copy_stream_impl.cc
    src/google/protobuf/compiler/importer.cc
    src/google/protobuf/compiler/parser.cc

    )

set(libprotoc_SRCS
   src/google/protobuf/compiler/code_generator.cc
   src/google/protobuf/compiler/command_line_interface.cc
   src/google/protobuf/compiler/plugin.cc
   src/google/protobuf/compiler/plugin.pb.cc
   src/google/protobuf/compiler/subprocess.cc
   src/google/protobuf/compiler/subprocess.h
   src/google/protobuf/compiler/zip_writer.cc
   src/google/protobuf/compiler/zip_writer.h
   src/google/protobuf/compiler/cpp/cpp_enum.cc
   src/google/protobuf/compiler/cpp/cpp_enum.h
   src/google/protobuf/compiler/cpp/cpp_enum_field.cc
   src/google/protobuf/compiler/cpp/cpp_enum_field.h
   src/google/protobuf/compiler/cpp/cpp_extension.cc
   src/google/protobuf/compiler/cpp/cpp_extension.h
   src/google/protobuf/compiler/cpp/cpp_field.cc
   src/google/protobuf/compiler/cpp/cpp_field.h
   src/google/protobuf/compiler/cpp/cpp_file.cc
   src/google/protobuf/compiler/cpp/cpp_file.h
   src/google/protobuf/compiler/cpp/cpp_generator.cc
   src/google/protobuf/compiler/cpp/cpp_helpers.cc
   src/google/protobuf/compiler/cpp/cpp_helpers.h
   src/google/protobuf/compiler/cpp/cpp_message.cc
   src/google/protobuf/compiler/cpp/cpp_message.h
   src/google/protobuf/compiler/cpp/cpp_message_field.cc
   src/google/protobuf/compiler/cpp/cpp_message_field.h
   src/google/protobuf/compiler/cpp/cpp_options.h
   src/google/protobuf/compiler/cpp/cpp_primitive_field.cc
   src/google/protobuf/compiler/cpp/cpp_primitive_field.h
   src/google/protobuf/compiler/cpp/cpp_service.cc
   src/google/protobuf/compiler/cpp/cpp_service.h
   src/google/protobuf/compiler/cpp/cpp_string_field.cc
   src/google/protobuf/compiler/cpp/cpp_string_field.h
   src/google/protobuf/compiler/java/java_enum.cc
   src/google/protobuf/compiler/java/java_enum.h
   src/google/protobuf/compiler/java/java_enum_field.cc
   src/google/protobuf/compiler/java/java_enum_field.h
   src/google/protobuf/compiler/java/java_extension.cc
   src/google/protobuf/compiler/java/java_extension.h
   src/google/protobuf/compiler/java/java_field.cc
   src/google/protobuf/compiler/java/java_field.h
   src/google/protobuf/compiler/java/java_file.cc
   src/google/protobuf/compiler/java/java_file.h
   src/google/protobuf/compiler/java/java_generator.cc
   src/google/protobuf/compiler/java/java_helpers.cc
   src/google/protobuf/compiler/java/java_helpers.h
   src/google/protobuf/compiler/java/java_message.cc
   src/google/protobuf/compiler/java/java_message.h
   src/google/protobuf/compiler/java/java_message_field.cc
   src/google/protobuf/compiler/java/java_message_field.h
   src/google/protobuf/compiler/java/java_primitive_field.cc
   src/google/protobuf/compiler/java/java_primitive_field.h
   src/google/protobuf/compiler/java/java_service.cc
   src/google/protobuf/compiler/java/java_service.h
   src/google/protobuf/compiler/java/java_string_field.cc
   src/google/protobuf/compiler/java/java_string_field.h
   src/google/protobuf/compiler/java/java_doc_comment.cc
   src/google/protobuf/compiler/java/java_doc_comment.h
   src/google/protobuf/compiler/python/python_generator.cc
   )

set(protoc_SRCS
   src/google/protobuf/compiler/main.cc
   )

if(WIN32)
   include_directories(vsprojects)
   #   add_definitions(-D_WIN32 -DLIBPROTOBUF_EXPORTS -D_CRT_SECURE_NO_WARNINGS)
   ADD_COMPILER_FLAGS("-wd4244 -wd4996 -D_WIN32 -DLIBPROTOBUF_EXPORTS -D_CRT_SECURE_NO_WARNINGS" CACHE)
else()
    # POSIX common
   ADD_COMPILER_FLAGS("-D_GNU_SOURCE" CACHE)
   check_library_exists("c" ftruncate "" HAVE_FTRUNCATE)
   check_library_exists("c" memset "" HAVE_MEMSET)
   check_library_exists("c" mkdir "" HAVE_MKDIR)
   check_library_exists("c" strchr "" HAVE_STRCHR)
   check_library_exists("c" strtol "" HAVE_STRTOL)
   CHECK_INCLUDE_FILES(dlfcn.h HAVE_DLFCN_H)
   CHECK_INCLUDE_FILES(fcntl.h HAVE_FCNTL_H)
   CHECK_INCLUDE_FILES(inttypes.h HAVE_INTTYPES_H)
   CHECK_INCLUDE_FILES(limits.h HAVE_LIMITS_H)
   CHECK_INCLUDE_FILES(stdlib.h HAVE_STDLIB_H)
   CHECK_INCLUDE_FILES(stdint.h HAVE_STDINT_H)
   CHECK_INCLUDE_FILES(unistd.h HAVE_UNISTD_H)
   CHECK_INCLUDE_FILES(memory.h HAVE_MEMORY_H)
   CHECK_INCLUDE_FILES(strings.h HAVE_STRINGS_H)
   CHECK_INCLUDE_FILES(string.h HAVE_STRING_H)
   CHECK_INCLUDE_FILES("stdlib.h;stdarg.h;float.h;string.h" STDC_HEADERS)
   CHECK_INCLUDE_FILES("sys/stat.h" HAVE_SYS_STAT_H)
   CHECK_INCLUDE_FILES("sys/types.h" HAVE_SYS_TYPES_H)

   # TODO Move to separate cmake file
   if (NOT hashMapFound)
      foreach(hashMapName hash_map unordered_map)
         foreach(hashMapLocation "<${hashMapName}>" "<tr1/${hashMapName}>")
            foreach(hashMapNamespace std std::tr1 stdext)
               if (NOT hashMapFound)
                  set( hashMapTest "
                     #include ${hashMapLocation}
                     int main(int argc, char * argv[]) 
                     { 
                        const ${hashMapNamespace}::${hashMapName}<int, int> t;
                        return t.find(4) == t.end();
                     }")
                  CHECK_CXX_SOURCE_COMPILES("${hashMapTest}" HAVE_HASH_MAP)
                  if(HAVE_HASH_MAP)
                     set(HASH_MAP_H ${hashMapLocation})
                     set(HASH_NAMESPACE ${hashMapNamespace})
                     set(HASH_MAP_CLASS ${hashMapName})
                     set(hashMapFound 1)
                  else()
                     unset(HAVE_HASH_MAP CACHE)
                  endif()
               endif()
            endforeach(hashMapNamespace)
         endforeach(hashMapLocation)
      endforeach(hashMapName)
   endif()
   if (NOT hashSetFound)
      foreach(hashSetName hash_set unordered_set)
         foreach(hashSetLocation "<${hashSetName}>" "<tr1/${hashSetName}>")
            foreach(hashSetNamespace std std::tr1 stdext)
               if (NOT hashSetFound)
                  set( hashSetTest "
                     #include ${hashSetLocation}
                     int main(int argc, char * argv[]) 
                     { 
                        const ${hashSetNamespace}::${hashSetName}<int> t;
                        return 0;
                     }")
                  CHECK_CXX_SOURCE_COMPILES("${hashSetTest}" HAVE_HASH_SET)
                  if(HAVE_HASH_SET)
                     set(HASH_SET_H ${hashSetLocation})
                     set(HASH_SET_CLASS ${hashSetName})
                     set(hashSetFound 1)
                  else()
                     unset(HAVE_HASH_SET CACHE)
                  endif()
               endif()
            endforeach(hashSetNamespace)
         endforeach(hashSetLocation)
      endforeach(hashSetName)
   endif()
   # END TODO

   if(Threads_FOUND)
      set(HAVE_PTHREAD 1)
   endif()
   CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h)
   ADD_COMPILER_FLAGS("-DHAVE_CONFIG_H" CACHE)
endif()

add_library(libprotoc ${libprotoc_SRCS})
add_library(libprotobuf ${libprotobuf_SRCS})
add_library(libprotobuf_lite ${libprotobuf_lite_SRCS})
add_executable(protoc ${protoc_SRCS})
target_link_libraries(protoc libprotoc)
target_link_libraries(libprotoc libprotobuf)

if (protobuf_BUILD_SHARED_LIBS)
   set_target_properties(libprotoc
      PROPERTIES
      COMPILE_DEFINITIONS "PROTOBUF_USE_DLLS=1")
   set_target_properties(libprotobuf
      PROPERTIES
      COMPILE_DEFINITIONS "PROTOBUF_USE_DLLS=1")
   set_target_properties(libprotobuf_lite
      PROPERTIES
      COMPILE_DEFINITIONS "PROTOBUF_USE_DLLS=1")
endif()

if (protobuf_BUILD_TESTS)
   include_directories(${protobuf_BINARY_DIR})

if(WIN32)
   set(protoc_WORKING_DIR ${protobuf_BINARY_DIR}/Debug)
else()
   set(protoc_WORKING_DIR ${protobuf_BINARY_DIR})
endif()
   # Define protobuf_lite source files
   set (protobuf_lite_test_SRCS
      src/google/protobuf
      src/google/protobuf/lite_unittest.cc
      src/google/protobuf/test_util_lite.cc
      ${protobuf_BINARY_DIR}/google/protobuf/unittest_import_lite.pb.cc
      ${protobuf_BINARY_DIR}/google/protobuf/unittest_import_public_lite.pb.cc
      ${protobuf_BINARY_DIR}/google/protobuf/unittest_lite.pb.cc
      )
   ADD_CUSTOM_COMMAND(
      OUTPUT ${protobuf_BINARY_DIR}/google/protobuf/unittest_import_lite.pb.cc
      COMMAND protoc -I${protobuf_SOURCE_DIR}/src --cpp_out=${protobuf_BINARY_DIR} ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_import_lite.proto
      DEPENDS protoc ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_import_lite.proto
      WORKING_DIRECTORY ${protobuf_WORKING_DIR}
      )

   ADD_CUSTOM_COMMAND(
      OUTPUT ${protobuf_BINARY_DIR}/google/protobuf/unittest_import_public_lite.pb.cc
      COMMAND protoc -I${protobuf_SOURCE_DIR}/src --cpp_out=${protobuf_BINARY_DIR} ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_import_public_lite.proto
      DEPENDS protoc ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_import_public_lite.proto
      WORKING_DIRECTORY ${protobuf_WORKING_DIR}
      )
   ADD_CUSTOM_COMMAND(
      OUTPUT ${protobuf_BINARY_DIR}/google/protobuf/unittest_lite.pb.cc
      COMMAND protoc -I${protobuf_SOURCE_DIR}/src --cpp_out=${protobuf_BINARY_DIR} ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_lite.proto
      DEPENDS protoc ${protobuf_SOURCE_DIR}/src/google/protobuf/unittest_lite.proto
      WORKING_DIRECTORY ${protobuf_WORKING_DIR}
      )

   add_executable(protobuf_lite_test ${protobuf_lite_test_SRCS})
   target_link_libraries(protobuf_lite_test libprotobuf_lite)
endif()

# Tests

