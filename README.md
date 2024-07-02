# MTServer
Designed and implemented a multithreaded HTTP web server in C++ using socket programming, proficient in concurrent connection handling, processing HTTP requests, file operations, POSIX threads for multithreading, networking functions, and system programming.

# Project Overview
1. Socket Initialization and Binding: Created a TCP socket (`server_socket`) using
`socket(AF_INET, SOCK_STREAM, 0)`. The server binds to a random port within a range around
8080 (`randomPORT`) using `bind()`. `listen()` is used to set up the socket to accept incoming
connections with a backlog of 10 connections.
2. Handling Connections: In an infinite loop (`while(1)`), the server waits for and accepts incoming
connections using `accept()`. For each incoming connection, a new thread (`pthread_create()`) is
created to handle the connection independently. The `connection_handler` function is passed to
manage each client connection.
3. Thread Management: A semaphore (`sem_t mutex`) is used to control access to shared resources,
particularly `thread_count`, which tracks the number of active threads. The `connection_handler`
function manages the lifecycle of each connection:
• Reads the incoming HTTP request using `read()`.
• Parses the request type (`GET`, `POST`) and requested file.
• Handles `multipart/form-data` requests separately by parsing and saving uploaded files to a
specified directory (`./public/downloads/`).
• Manages normal `GET` and `POST` requests by sending appropriate HTTP headers and file
contents back to the client using `send_message()`.
4. File Sending: The `send_message()` function constructs HTTP headers and sends files back to
clients using `sendfile()` for efficient file transmission.
5. Data Handling: Data from `POST` requests is parsed and stored in `serverData`, allowing the
server to handle form submissions and potentially process data further.
6. Error Handling: The server handles errors such as failed socket creation, binding, listening, and
thread creation using `perror()` to log error messages.
# Project Functionality
1. Concurrency: The server handles multiple client connections concurrently using POSIX threads
(`pthread`).
2. File Serving: It can serve static files (`html`, `css`, `js`, etc.) and process `POST` requests with
file uploads.
3. Dynamic Behavior: It handles dynamic content through PHP files (although currently set to do
nothing).
4. Error Tolerance: Basic error handling for socket operations and thread creation ensures the
server remains stable under typical conditions.
# Conclusion
My project demonstrates a solid foundation for a multithreaded HTTP server capable of handling
basic HTTP requests and file uploads. With further refinement and additional features, it could
serve as a robust platform for web applications or content delivery. Ensure to test thoroughly and
address any edge cases or performance bottlenecks encountered during development.


