cmake_minimum_required(VERSION 3.10)

project(uSockets VERSION 0.6)
add_library(uSockets 
            crypto/openssl.c 
            crypto/wolfssl.c 
            eventing/epoll_kqueue.c 
            eventing/gcd.c 
            eventing/libuv.c 
            bsd.c
            context.c
            loop.c
            socket.c
            )