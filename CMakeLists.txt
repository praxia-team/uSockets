cmake_minimum_required(VERSION 3.10)

project(uSockets VERSION 0.6)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)
#set(BUILD_SHARED_LIBS True)

if(APPLE)
    set(LIBSSL /usr/local/opt/openssl/lib/libssl.dylib)
    set(LIBCRYPTO /usr/local/opt/openssl/lib/libcrypto.dylib)
else()
    find_library(LIBSSL ssl)
    find_library(LIBCRYPTO crypto)
endif()
find_library(LIBUV uv)

add_library(uSockets STATIC 
            src/crypto/openssl.c 
            src/crypto/wolfssl.c 
            src/eventing/epoll_kqueue.c 
            src/eventing/gcd.c 
            src/eventing/libuv.c 
            src/bsd.c
            src/context.c
            src/loop.c
            src/socket.c
            src/crypto/sni_tree.cpp
            )
target_compile_definitions(uSockets PUBLIC LIBUS_USE_OPENSSL LIBUS_USE_LIBUV )
target_link_libraries(uSockets ${LIBUV} ${LIBSSL} ${LIBCRYPTO})
#target_link_libraries(uSockets ${LIBUV} /usr/local/opt/openssl/lib/libcrypto.a /usr/local/opt/openssl/lib/libssl.a)
target_include_directories(uSockets PUBLIC "src" "/usr/local/opt/openssl/include" "/usr/local/opt/libuv/include")