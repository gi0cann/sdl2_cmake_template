cmake_minimum_required(VERSION 3.10)

project(Game)

if (WIN32)
    set(SDL2_DIR "c:/libs/SDL2")
    set(SDL2MAIN_INCLUDE_DIR "c:/include")
    set(SDL2IMAGE_INCLUDE_DIR "${SDL2_DIR}/SDL2_image-2.0.5/include")
    set(SDL2MIXER_INCLUDE_DIR "${SDL2_DIR}/SDL2_mixer-2.0.4/include")
    set(SDL2NET_INCLUDE_DIR "${SDL2_DIR}/SDL2_net-2.0.1/include")
    set(SDL2TTF_INCLUDE_DIR "${SDL2_DIR}/SDL2_ttf-2.0.15/include")
    file(GLOB SDL2MAIN_LIBS "${SDL2_DIR}/SDL2-2.0.14/lib/x64/*.lib")
    set(SDL2IMAGE_LIBS "${SDL2_DIR}/SDL2_image-2.0.5/lib/x64/SDL2_image.lib")
    set(SDL2MIXER_LIBS "${SDL2_DIR}/SDL2_mixer-2.0.4/lib/x64/SDL2_mixer.lib")
    set(SDL2NET_LIBS "${SDL2_DIR}/SDL2_net-2.0.1/lib/x64/SDL2_net.lib")
    set(SDL2TTF_LIBS "${SDL2_DIR}/SDL2_ttf-2.0.15/lib/x64/SDL2_ttf.lib")

    set(SDL2_LIBRARIES "${SDL2MAIN_LIBS};${SDL2IMAGE_LIBS};${SDL2MIXER_LIBS};${SDL2NET_LIBS};${SDL2TTF_LIBS}")

    set(SDL2_INCLUDE_DIRS "${SDL2MAIN_INCLUDE_DIR};${SDL2IMAGE_INCLUDE_DIR};${SDL2MIXER_INCLUDE_DIR};${SDL2NET_INCLUDE_DIR};${SDL2TTF_INCLUDE_DIR}")

    file(GLOB SRC src/*.cpp)
    add_executable(${PROJECT_NAME} ${SRC})

    target_include_directories(${PROJECT_NAME} PUBLIC ${SDL2MAIN_INCLUDE_DIR} ${SDL2TTF_INCLUDE_DIR})

    target_link_libraries(${PROJECT_NAME} PUBLIC ${SDL2MAIN_LIBS} ${SDL2TTF_LIBS})
elseif (APPLE)
    set(SDL2TTF_LIBS "/usr/local/Cellar/sdl2_ttf/2.0.15/lib/libSDL2_ttf-2.0.0.dylib")
    set(SDL2TTF_DIR "/usr/local/Cellar/sdl2_ttf/2.0.15/include/SDL2")
    find_package(SDL2 REQUIRED)

    file(GLOB SRC src/*.c)
    add_executable(${PROJECT_NAME} ${SRC})
    message(${SDL2_INCLUDE_DIRS}) 
    target_include_directories(${PROJECT_NAME} PUBLIC ${SDL2_INCLUDE_DIRS} ${SDL2TTF_DIR})
    target_link_libraries(${PROJECT_NAME} PUBLIC SDL2::SDL2 SDL2::SDL2main ${SDL2TTF_LIBS}) 
else()
    set(SDL2TTF_LIBS "/usr/lib/libSDL2_ttf-2.0.so.0")
    find_package(SDL2 REQUIRED)
    
    file(GLOB SRC src/*.c)
    add_executable(${PROJECT_NAME} ${SRC})

    
    target_include_directories(${PROJECT_NAME} PUBLIC include ${SDL2_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PUBLIC SDL2::SDL2 SDL2::SDL2main ${SDL2TTF_LIBS} m)

endif()
