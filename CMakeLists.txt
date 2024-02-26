cmake_minimum_required(VERSION 3.8)

project(broadcaster LANGUAGES CXX)

# Set version number.
set(broadcaster_VERSION_MAJOR 0)
set(broadcaster_VERSION_MINOR 1)

# C++ standard requirements.
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

message("\n=========== mediasoup-broadcaster-demo Build Configuration ===========\n")
message(STATUS "LIBWEBRTC_INCLUDE_PATH : " ${LIBWEBRTC_INCLUDE_PATH})
message(STATUS "LIBWEBRTC_BINARY_PATH  : " ${LIBWEBRTC_BINARY_PATH})
message(STATUS "OPENSSL_INCLUDE_DIR    : " ${OPENSSL_INCLUDE_DIR})
message(STATUS "CMAKE_USE_OPENSSL      : " ${CMAKE_USE_OPENSSL})
message("")

# Add some compile flags to our source files.
set_source_files_properties(${SOURCE_FILES}
	PROPERTIES COMPILE_FLAGS -Wall -Wextra -Wpedantic)

# Create target.
add_executable(${PROJECT_NAME} ${SOURCES})

set(CUSTOM_LIBC_OBJ_FILES
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/algorithm.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/any.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/atomic.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/barrier.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/bind.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/charconv.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/chrono.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/condition_variable_destructor.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/condition_variable.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/d2fixed.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/d2s.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/directory_entry.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/directory_iterator.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/error_category.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/exception.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/f2s.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/filesystem_clock.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/filesystem_error.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/functional.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/future.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/hash.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/ios.instantiations.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/ios.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/iostream.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/legacy_pointer_safety.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/locale.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/memory.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/mutex_destructor.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/mutex.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/new_handler.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/new_helpers.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/new.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/operations.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/optional.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/path.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/random.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/random_shuffle.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/regex.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/shared_mutex.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/stdexcept.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/string.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/strstream.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/system_error.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/thread.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/typeinfo.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/valarray.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/variant.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/vector.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++/libc++/verbose_abort.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/abort_message.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_aux_runtime.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_default_handlers.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_demangle.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_exception.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_exception_storage.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_guard.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_handlers.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_personality.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_thread_atexit.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_vector.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/cxa_virtual.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/fallback_malloc.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/private_typeinfo.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/stdlib_exception.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/stdlib_stdexcept.o
	${LIBWEBRTC_BINARY_PATH}/buildtools/third_party/libc++abi/libc++abi/stdlib_typeinfo.o	
)

# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc")
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdinc++")

# Extra libs required in order to use Apple media devices.
if(APPLE)
	find_library(APPLICATION_SERVICES ApplicationServices)
	find_library(AUDIO_TOOLBOX AudioToolbox)
	find_library(AV_FOUNDATION AVFoundation)
	find_library(CORE_AUDIO CoreAudio)
	find_library(CORE_FOUNDATION Foundation)
	find_library(CORE_MEDIA CoreMedia)
	find_library(CORE_VIDEO CoreVideo)
	find_library(CORE_SERVICES CoreServices)

	target_link_libraries(${PROJECT_NAME} PUBLIC
		${APPLICATION_SERVICES}
		${AUDIO_TOOLBOX}
		${AV_FOUNDATION}
		${CORE_AUDIO}
		${CORE_FOUNDATION}
		${CORE_MEDIA}
		${CORE_VIDEO}
		${CORE_SERVICES}
	)
endif(APPLE)

include(FetchContent)

message(STATUS "\nFetching mediasoupclient...\n")
FetchContent_Declare(
  mediasoupclient
  GIT_REPOSITORY https://github.com/copiltembel/libmediasoupclient.git
  GIT_TAG m120_custom_libc
)
FetchContent_MakeAvailable(mediasoupclient)

message(STATUS "Fetching cpr...\n")
FetchContent_Declare(
	cpr
	GIT_REPOSITORY https://github.com/whoshuu/cpr
	GIT_TAG 1.10.5
)
FetchContent_MakeAvailable(cpr)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fno-delete-null-pointer-checks -fno-ident -fno-strict-aliasing -fstack-protector -funwind-tables -fPIC -pthread -fcolor-diagnostics -fmerge-all-constants -fcrash-diagnostics-dir=../../../tools/clang/crashreports -mllvm -instcombine-lower-dbg-declare=0 -mllvm -split-threshold-for-reg-with-hint=0 -ffp-contract=off -fcomplete-member-pointers -m64 -msse3 -Wno-builtin-macro-redefined -D__DATE__= -D__TIME__= -D__TIMESTAMP__= -ffile-compilation-dir=. -no-canonical-prefixes -ftrivial-auto-var-init=pattern -O0 -fno-omit-frame-pointer -gdwarf-4 -g2 -gdwarf-aranges -gsplit-dwarf -ggnu-pubnames -Xclang -fuse-ctor-homing -fvisibility=hidden -Xclang -add-plugin -Xclang find-bad-constructs -Xclang -plugin-arg-find-bad-constructs -Xclang raw-ref-template-as-trivial-member -Xclang -plugin-arg-find-bad-constructs -Xclang check-stack-allocated -Xclang -plugin-arg-find-bad-constructs -Xclang check-raw-ptr-to-stack-allocated -Xclang -plugin-arg-find-bad-constructs -Xclang raw-ptr-fix-crbug-1449812 -Xclang -plugin-arg-find-bad-constructs -Xclang check-ipc -Wheader-hygiene -Wstring-conversion -Wtautological-overlap-compare -fstrict-aliasing -fPIC -Wall -Wno-unused-variable -Wno-c++11-narrowing -Wno-unused-but-set-variable -Wno-misleading-indentation -Wno-missing-field-initializers -Wno-unused-parameter -Wno-psabi -Wloop-analysis -Wno-unneeded-internal-declaration -Wenum-compare-conditional -Wno-ignored-pragma-optimize -Wno-deprecated-builtins -Wno-bitfield-constant-conversion -Wno-deprecated-this-capture -Wno-invalid-offsetof -Wno-vla-extension -Wno-thread-safety-reference-return -Wno-delayed-template-parsing-in-cxx20")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-undefined-bool-conversion -Wno-tautological-undefined-compare -std=c++17 -Wno-trigraphs -gsimple-template-names -nostdinc++ -fvisibility-inlines-hidden -fexceptions -frtti")
set(CMAKE_SYSROOT "/mnt/large4/src/google/libwebrtc/m120_webrtc/src/build/linux/debian_bullseye_amd64-sysroot")

add_definitions(-D_LIBCPP_OVERRIDABLE_FUNC_VIS=__attribute__\(\(__visibility__\(\"default\"\)\)\) -DLIBCXX_BUILDING_LIBCXXABI -DUSE_UDEV -DUSE_AURA=1 -DUSE_GLIB=1 -DUSE_OZONE=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D_GNU_SOURCE -D_LIBCPP_ENABLE_SAFE_MODE=1 -DCR_CLANG_REVISION=\"llvmorg-18-init-9505-g10664813-1\" -D_LIBCPP_DISABLE_VISIBILITY_ANNOTATIONS -D_LIBCXXABI_DISABLE_VISIBILITY_ANNOTATIONS -DCR_LIBCXX_REVISION=a429c26ae25c26a569ff12390d5f9be70c5e286b -DCR_SYSROOT_KEY=20230611T210420Z-2 -D_DEBUG -DDYNAMIC_ANNOTATIONS_ENABLED=1 -D_LIBCPP_BUILDING_LIBRARY)

include_directories(SYSTEM
	${LIBWEBRTC_INCLUDE_PATH}/buildtools/third_party/libc++/
	${LIBWEBRTC_INCLUDE_PATH}/third_party/libc++/src/include
	${LIBWEBRTC_INCLUDE_PATH}/third_party/libc++abi/src/include)

target_sources(${PROJECT_NAME} PRIVATE
	src/Broadcaster.cpp
	src/main.cpp
	src/MediaStreamTrackFactory.cpp
)

# Private (implementation) header files.
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/include)

# set(CMAKE_C_COMPILER ${LIBWEBRTC_INCLUDE_PATH}/third_party/llvm-build/Release+Asserts/bin/clang)
# set(CMAKE_CXX_COMPILER ${LIBWEBRTC_INCLUDE_PATH}/third_party/llvm-build/Release+Asserts/bin/clang++)

# set(CC ${LIBWEBRTC_INCLUDE_PATH}/third_party/llvm-build/Release+Asserts/bin/clang)
# set(CXX ${LIBWEBRTC_INCLUDE_PATH}/third_party/llvm-build/Release+Asserts/bin/clang++)




# Source Dependencies.
add_subdirectory(deps/libwebrtc "${CMAKE_CURRENT_BINARY_DIR}/libwebrtc")

# Public (interface) headers from dependencies.
target_include_directories(${PROJECT_NAME} PUBLIC
	${LIBWEBRTC_INCLUDE_PATH}/buildtools/third_party/libc++/
	${LIBWEBRTC_INCLUDE_PATH}/third_party/libc++/src/include
	# ${LIBWEBRTC_INCLUDE_PATH}/build/linux/debian_bullseye_amd64-sysroot/usr/include/c++/10/
	# ${LIBWEBRTC_INCLUDE_PATH}/build/linux/debian_bullseye_amd64-sysroot/usr/include/x86_64-linux-gnu/c++/10/
	# ${LIBWEBRTC_INCLUDE_PATH}/third_party/libc++abi/src/include
	${mediasoupclient_SOURCE_DIR}/include
	${cpr_SOURCE_DIR}/include
	"${PROJECT_SOURCE_DIR}/deps/libwebrtc"
)

# Public (interface) dependencies.
target_link_libraries(${PROJECT_NAME} PUBLIC
	# ${CUSTOM_LIBC_OBJ_FILES}
	${LIBWEBRTC_BINARY_PATH}/api/video_codecs/libbuiltin_video_encoder_factory${CMAKE_STATIC_LIBRARY_SUFFIX}
	${LIBWEBRTC_BINARY_PATH}/api/video_codecs/libbuiltin_video_decoder_factory${CMAKE_STATIC_LIBRARY_SUFFIX}
	${LIBWEBRTC_BINARY_PATH}/media/librtc_simulcast_encoder_adapter${CMAKE_STATIC_LIBRARY_SUFFIX}
	${LIBWEBRTC_BINARY_PATH}/media/librtc_internal_video_codecs${CMAKE_STATIC_LIBRARY_SUFFIX}
	${LIBWEBRTC_BINARY_PATH}/libwebrtc${CMAKE_STATIC_LIBRARY_SUFFIX}
	dl
	pthread
	ssl
	crypto
	cpr
	mediasoupclient
	webrtc_broadcaster
)

