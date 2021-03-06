cmake_minimum_required(VERSION 2.8)

set(LIBUVDIR libuv)

include_directories(${LIBUVDIR}/include ${LIBUVDIR}/src)
set(SOURCES
  ${LIBUVDIR}/src/fs-poll.c
  ${LIBUVDIR}/src/inet.c
  ${LIBUVDIR}/src/uv-common.c
  ${LIBUVDIR}/src/version.c)

if(WIN32)
  add_definitions(-DWIN32_LEAN_AND_MEAN -D_WIN32_WINNT=0x0600 -D_CRT_SECURE_NO_WARNINGS)
  include_directories(${LIBUVDIR}/src/win)
  set(SOURCES ${SOURCES}
    ${LIBUVDIR}/src/win/async.c
    ${LIBUVDIR}/src/win/core.c
    ${LIBUVDIR}/src/win/dl.c
    ${LIBUVDIR}/src/win/error.c
    ${LIBUVDIR}/src/win/fs-event.c
    ${LIBUVDIR}/src/win/fs.c
    ${LIBUVDIR}/src/win/getaddrinfo.c
    ${LIBUVDIR}/src/win/handle.c
    ${LIBUVDIR}/src/win/loop-watcher.c
    ${LIBUVDIR}/src/win/pipe.c
    ${LIBUVDIR}/src/win/poll.c
    ${LIBUVDIR}/src/win/process-stdio.c
    ${LIBUVDIR}/src/win/process.c
    ${LIBUVDIR}/src/win/req.c
    ${LIBUVDIR}/src/win/signal.c
    ${LIBUVDIR}/src/win/stream.c
    ${LIBUVDIR}/src/win/tcp.c
    ${LIBUVDIR}/src/win/thread.c
    ${LIBUVDIR}/src/win/threadpool.c
    ${LIBUVDIR}/src/win/timer.c
    ${LIBUVDIR}/src/win/tty.c
    ${LIBUVDIR}/src/win/udp.c
    ${LIBUVDIR}/src/win/util.c
    ${LIBUVDIR}/src/win/winapi.c
    ${LIBUVDIR}/src/win/winsock.c)
else()
  include_directories(${LIBUVDIR}/src/unix)
  set(SOURCES ${SOURCES}
    ${LIBUVDIR}/src/unix/async.c
    ${LIBUVDIR}/src/unix/core.c
    ${LIBUVDIR}/src/unix/dl.c
    ${LIBUVDIR}/src/unix/fs.c
    ${LIBUVDIR}/src/unix/getaddrinfo.c
    ${LIBUVDIR}/src/unix/loop-watcher.c
    ${LIBUVDIR}/src/unix/loop.c
    ${LIBUVDIR}/src/unix/pipe.c
    ${LIBUVDIR}/src/unix/poll.c
    ${LIBUVDIR}/src/unix/process.c
    ${LIBUVDIR}/src/unix/signal.c
    ${LIBUVDIR}/src/unix/stream.c
    ${LIBUVDIR}/src/unix/tcp.c
    ${LIBUVDIR}/src/unix/thread.c
    ${LIBUVDIR}/src/unix/threadpool.c
    ${LIBUVDIR}/src/unix/timer.c
    ${LIBUVDIR}/src/unix/tty.c
    ${LIBUVDIR}/src/unix/udp.c)
endif()

add_library(uv ${SOURCES})
