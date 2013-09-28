option(protobuf_BUILD_SHARED_LIBS "Build Protobuf as Shared Library" OFF)

# Useful CMake helper functions
include(cmake/FlagUtilities.cmake)

PROJECT(protobuf C CXX)

cmake_minimum_required(VERSION 2.8)

include_directories(src src/google/protobuf)

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
#    set(UV_SRCS ${UV_WIN32_SRCS} ${UV_COMMON_SRCS})
#    set(UV_TESTRUNNER_SRCS test/runner-win.c test/runner-win.h)
#    set(UV_LIBS ws2_32 psapi iphlpapi)
else()
    # POSIX common
#    include_directories(src/unix/ev)
#    add_definitions(-D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -DEIO_STACKSIZE=262144)
#    set(UV_TESTRUNNER_SRCS test/runner-unix.c test/runner-unix.h)
#
#    # OS specific thingy
#    # FIXME: solaris here
#    if(APPLE)
#        add_definitions(
#            -D_DARWIN_USE_64_BIT_INODE=1)
#        set(UV_SRCS
#            ${UV_POSIX_SRCS}
#            ${UV_COMMON_SRCS}
#            src/unix/darwin.c
#            src/unix/fsevents.c
#            src/unix/kqueue.c)
#        set(UV_LIBS m)
#    elseif(${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
#        set(UV_SRCS
#            ${UV_POSIX_SRCS}
#            ${UV_COMMON_SRCS}
#            src/unix/linux/linux-core.c
#            src/unix/linux/inotify.c
#            src/unix/linux/syscalls.c
#            src/unix/linux/syscalls.h
#            )
#        set(UV_LIBS rt m dl)
#    elseif(${CMAKE_SYSTEM_NAME} STREQUAL "FreeBSD")
#        set(UV_SRCS
#            ${UV_POSIX_SRCS}
#            ${UV_COMMON_SRCS}
#            src/unix/freebsd.c
#            src/unix/kqueue.c
#            )
#        set(UV_LIBS m pthread kvm)
#    elseif(${CMAKE_SYSTEM_NAME} STREQUAL "CYGWIN")
#        set(UV_SRCS
#            ${UV_POSIX_SRCS}
#            ${UV_COMMON_SRCS}
#            src/unix/cygwin.c
#            )
#        set(UV_LIBS rt m dl)
#    else()
#        message(FATAL_ERROR
#            "We don't support this system for now: ${CMAKE_SYSTEM_NAME}")
#    endif()
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

# Tests

