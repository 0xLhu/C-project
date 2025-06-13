Client-Server Keylogger C2 in C (Educational Project)
🧠 Introduction

This project is an educational exercise designed to reinforce C programming skills, with a focus on system-level development, socket programming, and multithreading. It implements a simple Command & Control (C2) architecture where:

    A client daemon acts as a keylogger and command executor.

    A server collects keystrokes and sends shell commands to the client.

    ⚠️ Disclaimer: This project is strictly for educational and ethical purposes. Unauthorized deployment of such techniques is illegal.

 Features
Client

    🖥️ Daemonization – Detaches from terminal and runs in the background.

    ⌨️ Keylogger – Captures keystrokes from /dev/input/event0 and sends them to the server.

    🧠 Command Listener – Receives commands from the server and executes them on the client system.

    🧵 Multithreading – Separates keylogging and command-handling in concurrent threads.

    🌐 TCP Communication – Maintains a persistent connection to the remote server.

Server

    📥 Keystroke Logging – Receives and writes keystrokes to a local file (keylogger.txt).

    💬 Command Sender – Sends shell commands to the client and displays the execution result.

    ⚙️ Multiclient Support (WIP) – Can be extended to handle multiple clients via threading.

🗂️ Project Structure
Client

client/
│── src/
│   ├── main.c          # Initializes the daemon and starts threads
│   ├── demon.c         # Converts the process into a daemon
│   ├── keylogger.c     # Captures and sends keystrokes
│   ├── c2_listener.c   # Listens for commands from the server
│   ├── commands.c      # Executes commands and sends results
│   ├── network.c       # TCP connection management
│── include/
│   ├── demon.h
│   ├── keylogger.h
│   ├── c2_listener.h
│   ├── commands.h
│   ├── network.h
│── Makefile

Server

server/
│── src/
│   ├── main.c          # Accepts client connections
│   ├── server.c        # Handles incoming client data and command processing
│   ├── log.c           # Writes keystrokes to a file and prints command results
│── include/
│   ├── server.h
│   ├── log.h
│── Makefile
│── keylogger.txt       # Keystrokes log (auto-created)

⚙️ Installation
Requirements

    Linux-based OS

    GCC compiler

    Root privileges (for client to access /dev/input/event0)

    Open port (default 8080)

Build

# Build the client
cd client
make

# Build the server
cd ../server
make

Usage
1. Start the Server

./server

It will listen on port 8080 and write logs to keylogger.txt.
2. Start the Client (as root)

./client

The client runs in the background and begins:

    Sending keystrokes

    Listening for commands

3. Interacting with the Client

On the server console, you can enter shell commands (e.g., whoami, ls, uname -a).
The output will be sent back by the client and displayed on the server terminal.
 Communication Flow

CLIENT                            SERVER
-------                          --------
| keylogger thread | ——— keystrokes ———> | log to file |
|                  |                      |
| command thread   | <—— commands ————   | stdin input |
|     exec result  | ——— result ————> | print output |

All communication occurs via a single TCP socket connection using a simple protocol:

    Commands and keystrokes are sent as char buffers.

    Server distinguishes between log data and command results.

 Learning Objectives

    Daemon and process control (fork, setsid, umask)

    Multithreaded C programming with pthread

    Low-level keyboard event reading (/dev/input/eventX)

    TCP sockets: connect, bind, listen, accept

    Modular C architecture: .c/.h separation and Makefiles

❗ Legal Disclaimer

This project is strictly for educational use only.
Do not deploy, distribute, or use this code on any device or network without explicit consent.
Improper use may lead to criminal charges.
