cmake_minimum_required(VERSION 3.20)
project(live-translation-capture LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(live-translation-capture main.cpp)

target_compile_definitions(live-translation-capture PRIVATE UNICODE _UNICODE)

# ActivateAudioInterfaceAsync lives in mmdevapi; the rest are standard COM/audio libs.
target_link_libraries(live-translation-capture PRIVATE mmdevapi ole32)

# Statically link the MSVC runtime so the .exe runs on machines without the VC++ redist.
set_property(TARGET live-translation-capture PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
if(MSVC)
  target_compile_options(live-translation-capture PRIVATE /W4)
endif()
