project(Coral
        VERSION 0.0.1
        LANGUAGES CXX)

add_subdirectory(Coral.Native)

target_precompile_headers(Coral PUBLIC Coral.Native/Source/CoralPCH.hpp)

target_include_directories(Coral PRIVATE
    NetCore
    Coral.Native/Source
    Coral.Native/Include/Coral
)

if(WIN32)
target_compile_definitions(Coral PRIVATE
        _CRT_SECURE_NO_WARNINGS
        CORAL_WINDOWS
)
elseif(UNIX AND NOT APPLE)
    target_compile_definitions(Coral PRIVATE
            _CRT_SECURE_NO_WARNINGS
            CORAL_LINUX
    )
else ()
    message("No MacOS support at this time")
endif ()

target_link_libraries(Coral)