Multithreaded Socket WebServer in Java

Overview

This project is a Java-based concurrent client–server system built from scratch to understand low-level networking, multithreading, and controlled concurrency using core Java APIs.

The server is designed to handle multiple simultaneous client connections efficiently by using a thread pool (ExecutorService), avoiding the scalability and stability issues of single-threaded or thread-per-client models.

The project is fully implemented, executed, and performance-tested, with validation done using Apache JMeter.

Problem Statement:

A single threaded server processes client requests sequentially, causing blocking and poor responsiveness under concurrent load.
A naive multi threaded approach (one thread per client) improves concurrency but:

Creates unbounded threads

Risks memory exhaustion

Degrades performance under high load

Objective:
Design and validate a server that supports safe, efficient concurrency with controlled resource usage.

Solution Approach:

Use ServerSocket to accept TCP connections

Submit each client connection to a fixed-size thread pool

Process client requests independently inside pooled worker threads

Ensure proper socket and stream lifecycle management

Architecture:
Multiple Clients
       |
       |  TCP Connections
       v
  ServerSocket
       |
       v
 ExecutorService (Thread Pool)
       |
       v
 Worker Threads → Request Processing → Response


Key Design Choice:
Concurrency is handled internally by the server, while clients remain simple and unaware of the threading model.

Technologies & Concepts Used
Technologies

Java (Core Java)

TCP Sockets (ServerSocket, Socket)

Multithreading (Runnable)

Thread Pool (ExecutorService)

Apache JMeter (Performance Testing)

Concepts

Client–Server Architecture

Blocking I/O

Thread Pooling & Resource Control

Concurrent Request Handling

Performance & Throughput Analysis

Performance Testing & Validation

This project was tested using Apache JMeter to compare single-threaded vs multi-threaded (thread pool) server behavior under concurrent load.

Tooling

Apache JMeter (TCP Sampler)

Localhost environment

Identical test configuration for fair comparison

Single-Threaded Server Results
Test Setup

Multiple concurrent JMeter threads

TCP Sampler sending requests

Server running in single-threaded mode

Observations

Requests handled sequentially

Increased response time under load

Lower throughput

Evidence
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/9b9c9864-977f-495c-8258-15cd3ccaff8b" />
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/37d70a25-3569-4202-91a4-136d5baa5eed" />
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/ccbc5436-9deb-4f4f-8649-e8a56f83e9e8" />




Conclusion:
Single-threaded architecture becomes a bottleneck when handling concurrent clients.

Multi-Threaded / Thread Pool Server Results
Test Setup

Same JMeter configuration

Server running with a fixed-size thread pool

Each request handled by a pooled worker thread

Observations

Concurrent request processing

Stable latency

Significantly improved throughput

Evidence:
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/ef5c5ede-89fe-4868-a59d-bbac38d1b0fe" />
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/2305dbc1-d05d-4f4d-93ed-244256e60d61" />
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/45f67e3f-ee61-4232-b773-c25743179542" />

<img width="1920" height="1080" alt="Screenshot 2026-01-06 115329" src="https://github.com/user-attachments/assets/a97b9741-4589-426f-b7a4-14f9ebaba250" />
<img width="1920" height="1080" alt="Screenshot 2026-01-06 115353" src="https://github.com/user-attachments/assets/3b7b1324-82aa-47b4-abab-f63a075c41c4" />
<img width="1920" height="1080" alt="Screenshot 2026-01-06 115403" src="https://github.com/user-attachments/assets/9d3ef31a-baaf-4e9d-85b7-030b8fe35cd2" />


Conclusion:
Using a thread pool enables controlled concurrency and consistent performance under load.

Server-Side Execution Proof

The server console logs confirm real, parallel client connections, not simulated behavior.

<img width="1574" height="912" alt="image" src="https://github.com/user-attachments/assets/40d6a2de-fc5b-4702-ac3a-171b5cb3bc35" />

This proves:

Active socket connections

Concurrent handling

Thread pool execution

How to Run the Project
Compile & Run Server
javac Server.java
java Server

Compile & Run Client
javac Client.java
java Client


Run multiple clients simultaneously or use Apache JMeter to observe concurrency.

Project Structure
├── Server.java
├── Client.java
├── screenshots/
│   ├── jmeter-single-thread-results.png
│   ├── jmeter-single-thread-graph.png
│   ├── jmeter-multi-thread-results.png
│   ├── jmeter-multi-thread-graph.png
│   └── server-console-connections.png
└── README.md

Limitations:

Uses blocking I/O (not Java NIO)

Not a full HTTP server

No authentication or encryption

Intended for learning and demonstration, not production deployment

Future Enhancements:

Add HTTP/1.1 request parsing

Serve static files

Switch to Java NIO for non-blocking I/O

Add request logging and metrics

Graceful shutdown handling

What This Project Demonstrates:

Strong understanding of Java concurrency fundamentals

Practical use of thread pools

Ability to measure and analyze performance

Ownership of design decisions backed by data
