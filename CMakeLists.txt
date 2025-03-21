project(Coral LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

add_library(Coral STATIC
    NetCore/coreclr_delegates.h
    NetCore/hostfxr.h

    Coral.Native/Include/Coral/StableVector.hpp
    Coral.Native/Source/Coral/HostFXRErrorCodes.hpp
    Coral.Native/Source/Coral/Type.cpp
    Coral.Native/Include/Coral/HostInstance.hpp
    Coral.Native/Include/Coral/PropertyInfo.hpp
    Coral.Native/Source/Coral/Memory.cpp
    Coral.Native/Source/CoralPCH.cpp
    Coral.Native/Source/Coral/HostInstance.cpp
    Coral.Native/Source/Coral/StringHelper.cpp
    Coral.Native/Source/Coral/ManagedObject.cpp
    Coral.Native/Include/Coral/FieldInfo.hpp
    Coral.Native/Source/CoralPCH.hpp
    Coral.Native/Include/Coral/Assembly.hpp
    Coral.Native/Source/Coral/MethodInfo.cpp
    Coral.Native/Source/Coral/FieldInfo.cpp
    Coral.Native/Source/Coral/GC.cpp
    Coral.Native/Include/Coral/ManagedObject.hpp
    Coral.Native/Source/Coral/PropertyInfo.cpp
    Coral.Native/Source/Coral/Attribute.cpp
    Coral.Native/Include/Coral/Memory.hpp
    Coral.Native/Source/Coral/CoralManagedFunctions.hpp
    Coral.Native/Include/Coral/String.hpp
    Coral.Native/Source/Coral/TypeCache.cpp
    Coral.Native/Include/Coral/TypeCache.hpp
    Coral.Native/Include/Coral/GC.hpp
    Coral.Native/Include/Coral/MethodInfo.hpp
    Coral.Native/Include/Coral/Attribute.hpp
    Coral.Native/Include/Coral/StringHelper.hpp
    Coral.Native/Source/Coral/Verify.hpp
    Coral.Native/Source/Coral/String.cpp
    Coral.Native/Source/Coral/Assembly.cpp
    Coral.Native/Include/Coral/Array.hpp
    Coral.Native/Include/Coral/Type.hpp
    Coral.Native/Include/Coral/Utility.hpp
    Coral.Native/Include/Coral/MessageLevel.hpp
    Coral.Native/Include/Coral/Core.hpp
)

set_target_properties(Coral PROPERTIES LINKER_LANGUAGE CXX)

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

target_link_libraries(Coral
        stdc++fs
)