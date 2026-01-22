# UDP/TCP Discussion Forum

A command-line discussion forum built using a custom client--server
protocol. Users can authenticate, create threads, post/edit/delete
messages, and upload/download files over the network.

## Overview

-   Client--server architecture\
-   **UDP** used for authentication and forum commands\
-   **TCP** used strictly for file transfers\
-   Supports multiple concurrent clients\
-   Fully terminal-based interface

## Features

### Authentication

-   Login using a `credentials.txt` file on the server\
-   New users can register automatically\
-   Prevents duplicate logins with the same username

### Commands

  Command                   Description
  ------------------------- --------------------------------
  `CRT thread`              Create a new thread
  `LST`                     List all threads
  `MSG thread message`      Post a message
  `RDT thread`              Read a thread
  `EDT thread id message`   Edit your own message
  `DLT thread id`           Delete your own message
  `RMV thread`              Delete a thread (creator only)
  `UPD thread filename`     Upload a file (TCP transfer)
  `DWN thread filename`     Download a file (TCP transfer)
  `XIT`                     Logout

## Data Model

-   Each thread is stored as a file on the server\
-   First line = thread creator\
-   Messages stored as:

```{=html}
<!-- -->
```
    1 username: message
    2 username: message

-   File uploads recorded as:

```{=html}
<!-- -->
```
    username uploaded filename

-   Files stored on server as:

```{=html}
<!-- -->
```
    threadname-filename

## Networking Design

-   **UDP**
    -   Authentication\
    -   Thread management\
    -   Message operations\
    -   Listing and reading threads
-   **TCP**
    -   File upload (UPD)\
    -   File download (DWN)

## Running the Application

Start the server:

    python server.py <port>

Start a client:

    python client.py <port>

Clients connect via `localhost` and interact through the terminal.

## Summary

This project demonstrates low-level socket programming, protocol design,
concurrency handling, and persistent state management in a practical
networked application.
