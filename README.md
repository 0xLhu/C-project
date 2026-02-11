Client-Server Telemetry Demo in C (Educational, Cross-Platform)

🧠 Introduction

This project is now a **safe educational exercise** to practice C programming with networking and multithreading on Linux and Windows.
It keeps a client/server architecture and demonstrates:

- a long-lived TCP connection,
- simple message framing (`KEY:` and `CMD:` prefixes),
- a telemetry thread running in parallel with a command listener,
- a small command parser with **non-dangerous built-in commands**.

⚠️ Disclaimer: this repository is for learning only. Do not use it for unauthorized monitoring or offensive activity.

## Features

### Client

- 🌐 TCP client connection (`connect_to_server`).
- 🧵 Background telemetry thread (`start_telemetry`) that sends a simulated heartbeat.
- 💬 Safe command execution (`help`, `ping`, `time`) without shell execution.
- 🪟 Cross-platform socket lifecycle helpers for Linux and Windows (`network_init`, `network_cleanup`, `socket_close`).

### Server

- 📥 Receives `KEY:` telemetry lines and appends them to `keylogger.txt`.
- 📄 Receives `CMD:` command results and appends them to `result_commands.txt`.
- ⌨️ Lets the operator type commands in stdin and forwards them to the client.

## Project structure

```
Malware/
├── client/
│   ├── include/
│   │   ├── commands.h
│   │   ├── keylogger.h
│   │   └── network.h
│   └── src/
│       ├── main.c
│       ├── network.c
│       ├── keylogger.c      # simulated telemetry thread
│       ├── commands.c        # safe built-in commands only
│       ├── c2_listener.c
│       ├── demon.c
│       └── Makefile
└── server/
    ├── include/
    │   ├── server.h
    │   └── log.h
    ├── src/
    │   ├── main.c
    │   ├── server.c
    │   └── log.c
    └── Makefile
```

## Build

### Linux

```bash
cd Malware/client/src
make

cd ../../server
make
```

### Windows (MinGW example)

```bash
cd Malware/client/src
gcc -Wall -Wextra -I../include main.c network.c keylogger.c commands.c c2_listener.c demon.c -o client.exe -lws2_32
```

Server uses POSIX APIs in this repo version and is intended to run on Linux.

## Usage

1. Start server:

```bash
cd Malware/server
./server
```

2. Start client:

```bash
cd Malware/client/src
./client
```

3. From the server terminal, send commands:

- `help`
- `ping`
- `time`

The server writes outputs to:

- `keylogger.txt` for telemetry (`KEY:` messages)
- `result_commands.txt` for command output (`CMD:` messages)
