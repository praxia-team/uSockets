cmake_minimum_required(VERSION 3.10)

project(uSockets VERSION 0.6)
add_library(uSockets 
            src/crypto/openssl.c 
            src/crypto/wolfssl.c 
            src/eventing/epoll_kqueue.c 
            src/eventing/gcd.c 
            src/eventing/libuv.c 
            src/bsd.c
            src/context.c
            src/loop.c
            src/socket.c
            )