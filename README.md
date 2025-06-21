# RabbitMQ101

This repository is a simple introduction to RabbitMQ using .NET, featuring a basic **Producer** and **Consumer** application. It is designed for learning and experimenting with message queues.

---

## Table of Contents
- [Overview](#overview)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Cloning the Repository](#cloning-the-repository)
  - [Prerequisites](#prerequisites)
  - [Running RabbitMQ with Docker](#running-rabbitmq-with-docker)
  - [Accessing RabbitMQ Management Portal](#accessing-rabbitmq-management-portal)
  - [Running the Producer](#running-the-producer)
  - [Running the Consumer](#running-the-consumer)
- [How It Works](#how-it-works)
- [License](#license)

---

## Overview
This playground demonstrates the basics of message queuing with RabbitMQ. The **Producer** sends messages to a queue, and the **Consumer** receives and processes them. Both are implemented in C# using the [RabbitMQ.Client](https://www.nuget.org/packages/RabbitMQ.Client/) library.

## Project Structure
```
RabbitMQ101/
├── Producer/         # Producer app (sends messages)
│   └── Program.cs
├── Consumer/         # Consumer app (receives messages)
│   └── Program.cs
├── README.md         # This file
└── ...
```

## Getting Started

### Cloning the Repository
Clone this repository to your local machine:

```sh
git clone https://github.com/fkucukkara/rabbitMQ101.git
cd RabbitMQ101
```

### Prerequisites
- [.NET 9 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/9.0)
- [Docker](https://www.docker.com/get-started) (for running RabbitMQ)

### Running RabbitMQ with Docker
To quickly start a RabbitMQ server with the management UI, run the following command:

```sh
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management
```
- **5672**: RabbitMQ main protocol port (used by the apps)
- **15672**: RabbitMQ Management Portal (web UI)

#### Stopping and Removing the Container
To stop and remove the container when done:
```sh
docker stop rabbitmq && docker rm rabbitmq
```

### Accessing RabbitMQ Management Portal
Once the container is running, open your browser and go to:

[http://localhost:15672/](http://localhost:15672/)

- **Default credentials:**
  - Username: `guest`
  - Password: `guest`

This portal allows you to monitor queues, exchanges, and messages.

### Running the Producer
1. Open a terminal in the `Producer` directory.
2. Run:
   ```bash
   dotnet run
   ```
3. The producer will send 5 messages to the `message` queue.

### Running the Consumer
1. Open a terminal in the `Consumer` directory.
2. Run:
   ```bash
   dotnet run
   ```
3. The consumer will listen for messages and print them as they arrive.

## How It Works
- **Producer**: Connects to RabbitMQ, declares a durable queue named `message`, and publishes 5 persistent messages with a 1-second delay between each.
- **Consumer**: Connects to RabbitMQ, declares the same queue, and listens for messages. When a message arrives, it prints the content and acknowledges it.

Both apps use `localhost` as the RabbitMQ host, so they expect RabbitMQ to be running locally (e.g., via Docker as shown above).

## License
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

This project is licensed under the MIT License. See the [`LICENSE`](LICENSE) file for details.
