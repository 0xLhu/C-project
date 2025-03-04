# Client Trojan in C (Educational Project)

## Introduction

This project is an educational exercise aimed at improving C programming skills, focusing on networking, system programming, and multithreading. It demonstrates how to structure a client-side program that interacts with a Command & Control (C2) server. The project follows best practices in modularization, threading, and daemonization.

**Disclaimer:** This project is strictly for learning purposes. Unauthorized use of such techniques for malicious activities is illegal.

## Features

- **Daemonization:** Runs in the background without a terminal.
- **Keylogger:** Captures keyboard events and sends them in buffered packets to the C2 server.
- **Command Execution:** Receives commands from the C2 server and executes system commands.
- **Multithreading:** Uses threads to handle both keylogging and command reception simultaneously.
- **Network Communication:** Establishes a TCP connection with a remote server.

## Project Structure

```
client/
│── src/
│   ├── main.c          # Initializes the daemon and starts threads
│   ├── demon.c         # Converts the process into a daemon
│   ├── keylogger.c     # Captures and sends keystrokes
│   ├── c2_listener.c   # Listens for commands from the server
│   ├── commands.c      # Handles command execution (e.g., whoami)
│   ├── network.c       # Manages the TCP connection
│── include/
│   ├── demon.h
│   ├── keylogger.h
│   ├── c2_listener.h
│   ├── commands.h
│   ├── network.h
│── Makefile
│── README.md          # This documentation file
```

## Installation

### Prerequisites

- Linux OS
- GCC compiler
- Root privileges (for keylogger access to `/dev/input/event0`)

### Compilation

Run the following command in the root directory:

```sh
make
```

This will generate an executable named `client`.

## Usage

Once compiled, execute the binary as follows:

```sh
./client
```

Since it runs as a daemon, it will detach from the terminal.
To check if it's running, use:

```sh
ps aux | grep client
```

## Learning Goals

- Understanding process management in Linux (fork, setsid, umask).
- Implementing multithreading with `pthread`.
- Using raw input event handling for keylogging.
- Managing socket programming for remote command execution.

This project is a work in progress and serves as a practical exercise in C programming.

## Disclaimer

This project is solely for educational purposes. Any misuse of this code is strictly prohibited. Always ensure that ethical guidelines and legal considerations are followed when dealing with system programming and security-related topics.

