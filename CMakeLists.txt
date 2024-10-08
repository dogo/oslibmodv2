cmake_minimum_required(VERSION 3.10)
project(OSLib C CXX ASM)

# Load the PSP platform configuration
set(CMAKE_SYSTEM_NAME PSP)
set(CMAKE_SYSTEM_VERSION 1)
set(CMAKE_SYSTEM_PROCESSOR mips)
set(CMAKE_SYSTEM_CMAKE_PLATFORM_PATH "${CMAKE_SOURCE_DIR}/Platform")

include("${CMAKE_SYSTEM_CMAKE_PLATFORM_PATH}/PSP.cmake")

# PSP Firmware version
add_definitions(-DPSP_FW_VERSION=371)

# Set the output library
set(TARGET_LIB osl)
add_library(${TARGET_LIB} STATIC)

# Specify the output directory for the .a file (project root directory)
set_target_properties(${TARGET_LIB} PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

# Include directories
include_directories(
    src
    src/intraFont
    src/libpspmath
    src/adhoc
)

# Define the source files
set(SOURCE_DIR src)
set(SFONT_SOURCES ${SOURCE_DIR}/sfont.c)
set(PSPMATH_SOURCES
    ${SOURCE_DIR}/libpspmath/printMatrixFloat.c
    ${SOURCE_DIR}/libpspmath/vfpu_srand.c
    ${SOURCE_DIR}/libpspmath/vfpu_randf.c
    ${SOURCE_DIR}/libpspmath/vfpu_rand_8888.c
    ${SOURCE_DIR}/libpspmath/vfpu_identity_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_translate_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_perspective_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_ortho_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_sinf.c
    ${SOURCE_DIR}/libpspmath/vfpu_cosf.c
    ${SOURCE_DIR}/libpspmath/vfpu_tanf.c
    ${SOURCE_DIR}/libpspmath/vfpu_asinf.c
    ${SOURCE_DIR}/libpspmath/vfpu_acosf.c
    ${SOURCE_DIR}/libpspmath/vfpu_atanf.c
    ${SOURCE_DIR}/libpspmath/vfpu_sinhf.c
    ${SOURCE_DIR}/libpspmath/vfpu_coshf.c
    ${SOURCE_DIR}/libpspmath/vfpu_tanhf.c
    ${SOURCE_DIR}/libpspmath/vfpu_sincos.c
    ${SOURCE_DIR}/libpspmath/vfpu_expf.c
    ${SOURCE_DIR}/libpspmath/vfpu_logf.c
    ${SOURCE_DIR}/libpspmath/vfpu_fabsf.c
    ${SOURCE_DIR}/libpspmath/vfpu_sqrtf.c
    ${SOURCE_DIR}/libpspmath/vfpu_powf.c
    ${SOURCE_DIR}/libpspmath/vfpu_fmodf.c
    ${SOURCE_DIR}/libpspmath/vfpu_fminf.c
    ${SOURCE_DIR}/libpspmath/vfpu_fmaxf.c
    ${SOURCE_DIR}/libpspmath/vfpu_ease_in_out.c
    ${SOURCE_DIR}/libpspmath/vfpu_normalize_vector.c
    ${SOURCE_DIR}/libpspmath/vfpu_zero_vector.c
    ${SOURCE_DIR}/libpspmath/vfpu_scale_vector.c
    ${SOURCE_DIR}/libpspmath/vfpu_add_vector.c
    ${SOURCE_DIR}/libpspmath/vfpu_envmap_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_sphere_to_cartesian.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_identity.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_copy.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_multiply.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_normalize.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_exp.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_ln.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_sample_linear.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_from_euler.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_to_matrix.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_sample_hermite.c
    ${SOURCE_DIR}/libpspmath/vfpu_quaternion_hermite_tangent.c
)

set(LIB_SOURCES
    ${SOURCE_DIR}/adhoc/pspadhoc.c
    ${SOURCE_DIR}/audio/audio.c
    ${SOURCE_DIR}/audio/bgm.c
    ${SOURCE_DIR}/audio/media.c
    ${SOURCE_DIR}/audio/mod.c
    ${SOURCE_DIR}/browser.c
    ${SOURCE_DIR}/dialog.c
    ${SOURCE_DIR}/drawing.c
    ${SOURCE_DIR}/gif/dev2gif.c ${SOURCE_DIR}/gif/dgif_lib.c ${SOURCE_DIR}/gif/egif_lib.c
    ${SOURCE_DIR}/gif/gif_err.c ${SOURCE_DIR}/gif/gifalloc.c ${SOURCE_DIR}/gif/quantize.c
    ${SOURCE_DIR}/image.c
    ${SOURCE_DIR}/image/oslConvertImageTo.c
    ${SOURCE_DIR}/image/oslDrawImage.c
    ${SOURCE_DIR}/image/oslDrawImageBig.c
    ${SOURCE_DIR}/image/oslDrawImageSimple.c
    ${SOURCE_DIR}/image/oslGetImagePixel.c
    ${SOURCE_DIR}/image/oslLockImage.c
    ${SOURCE_DIR}/image/oslMoveImageTo.c
    ${SOURCE_DIR}/image/oslResetImageProperties.c
    ${SOURCE_DIR}/image/oslScaleImage.c
    ${SOURCE_DIR}/image/oslSetDrawBuffer.c
    ${SOURCE_DIR}/image/oslSetImagePixel.c
    ${SOURCE_DIR}/image/oslSwizzleImage.c
    ${SOURCE_DIR}/image/oslUnswizzleImage.c
    ${SOURCE_DIR}/intraFont/intraFont.c
    ${SOURCE_DIR}/intraFont/libccc.c
    ${SOURCE_DIR}/keys.c
    ${SOURCE_DIR}/map.c
    ${SOURCE_DIR}/mem/oslGetRamStatus.c
    ${SOURCE_DIR}/messagebox.c
    ${SOURCE_DIR}/net.c
    ${SOURCE_DIR}/osk.c
    ${SOURCE_DIR}/oslHandleLoadNoFailError.c
    ${SOURCE_DIR}/oslib.c
    ${SOURCE_DIR}/palette.c
    ${SOURCE_DIR}/saveload.c
    ${SOURCE_DIR}/shape.c
    ${SOURCE_DIR}/Special/oslLoadImageFile.c
    ${SOURCE_DIR}/Special/oslLoadImageFileGIF.c
    ${SOURCE_DIR}/Special/oslLoadImageFileJPG.c
    ${SOURCE_DIR}/Special/oslLoadImageFilePNG.c
    ${SOURCE_DIR}/Special/oslWriteImageFile.c
    ${SOURCE_DIR}/Special/oslWriteImageFilePNG.c
    ${SOURCE_DIR}/splash/oslShowSplashScreen1.c
    ${SOURCE_DIR}/splash/oslShowSplashScreen2.c
    ${SOURCE_DIR}/stub.S
    ${SOURCE_DIR}/text.c
    ${SOURCE_DIR}/usb.c
    ${SOURCE_DIR}/vfile/vfsFile.c
    ${SOURCE_DIR}/vfile/VirtualFile.c
    ${SOURCE_DIR}/vfpu.c
    ${SOURCE_DIR}/vram_mgr.c
)

# Specify that stub.S is an assembly file
set_source_files_properties(${SOURCE_DIR}/stub.S PROPERTIES LANGUAGE ASM)

# Add sources to the target
target_sources(${TARGET_LIB} PRIVATE ${SFONT_SOURCES} ${PSPMATH_SOURCES} ${LIB_SOURCES})

# Define preprocessor defines
target_compile_definitions(${TARGET_LIB} PRIVATE _DEBUG PSP)

# Set the C flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -G0 -ggdb -Wall -DHAVE_AV_CONFIG_H -fno-strict-aliasing -fverbose-asm")

# Set the C++ flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${CMAKE_C_FLAGS} -fno-exceptions -fno-rtti")

# Linker flags
target_link_libraries(${TARGET_LIB}
    -lpspsdk
    -lpspctrl -lpsphprm
    -lpspumd
    -lpsprtc
    -lpspgu -lpspgum
    -lpspaudiolib
    -lpspaudio -lpspaudiocodec
    -lpsppower
    -lpspusb -lpspusbstor
    -lpsputility
    -lpspssl -lpsphttp -lpspwlan
    -lpspnet_adhoc -lpspnet_adhocctl -lpspnet_adhocmatching
    -lpng -ljpeg -lz -lm
)

# Get the PSP prefix using psp-config
execute_process(
    COMMAND psp-config --psp-prefix
    OUTPUT_VARIABLE PSPDIR
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

# Installation instructions
install(TARGETS ${TARGET_LIB} DESTINATION ${PSPDIR}/lib)

# Include directories installation (headers)
install(FILES ${SOURCE_DIR}/intraFont/intraFont.h ${SOURCE_DIR}/intraFont/libccc.h
    DESTINATION ${PSPDIR}/include/oslib/intraFont)

install(FILES ${SOURCE_DIR}/libpspmath/pspmath.h
    DESTINATION ${PSPDIR}/include/oslib/libpspmath)

install(FILES ${SOURCE_DIR}/adhoc/pspadhoc.h
    DESTINATION ${PSPDIR}/include/oslib/adhoc)

install(FILES ${SOURCE_DIR}/oslmath.h ${SOURCE_DIR}/net.h ${SOURCE_DIR}/browser.h ${SOURCE_DIR}/audio.h
    ${SOURCE_DIR}/bgm.h ${SOURCE_DIR}/dialog.h ${SOURCE_DIR}/drawing.h ${SOURCE_DIR}/keys.h
    ${SOURCE_DIR}/map.h ${SOURCE_DIR}/messagebox.h ${SOURCE_DIR}/osk.h ${SOURCE_DIR}/saveload.h
    ${SOURCE_DIR}/oslib.h ${SOURCE_DIR}/text.h ${SOURCE_DIR}/usb.h ${SOURCE_DIR}/vfpu_ops.h
    ${SOURCE_DIR}/VirtualFile.h ${SOURCE_DIR}/vram_mgr.h ${SOURCE_DIR}/ccc.h ${SOURCE_DIR}/sfont.h
    DESTINATION ${PSPDIR}/include/oslib)

# Add Cppcheck execution
find_program(CPPCHECK cppcheck)

if(CPPCHECK)
    set(CPPCHECK_COMMAND
        ${CPPCHECK} --enable=all --inconclusive --quiet
        --suppressions-list=${CMAKE_SOURCE_DIR}/.cppcheck-suppress
    )
    add_custom_target(
        cppcheck
        COMMAND ${CPPCHECK_COMMAND} ${CMAKE_SOURCE_DIR}/src
        COMMENT "Running Cppcheck..."
    )
else()
    message(WARNING "Cppcheck not found, skipping static analysis.")
endif()

# Add Uncrustify execution
find_program(UNCRUSTIFY uncrustify)

if(UNCRUSTIFY)
    set(UNCRUSTIFY_COMMAND ${UNCRUSTIFY} -c ${CMAKE_SOURCE_DIR}/uncrustify.cfg --no-backup)
    add_custom_target(
        uncrustify
        COMMAND ${UNCRUSTIFY_COMMAND} --replace ${CMAKE_SOURCE_DIR}/src/*.c ${CMAKE_SOURCE_DIR}/src/*.h
        COMMENT "Running Uncrustify to format the code without creating backups..."
    )
else()
    message(WARNING "Uncrustify not found, skipping code formatting.")
endif()
