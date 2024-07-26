# Docker Compose Setup for Kafka and Zookeeper

This document provides guidance on setting up Apache Kafka and Zookeeper using Docker Compose. It outlines the configuration necessary to run these services together in a development environment.

## Overview

Apache Kafka is a distributed streaming platform that lets you publish and subscribe to streams of records, store streams of records in a fault-tolerant way, and process streams of records as they occur. Zookeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services.

This setup uses Docker Compose to simplify the deployment and management of Kafka and Zookeeper containers. It leverages the Bitnami images for both Kafka and Zookeeper, ensuring compatibility and ease of use.

## Prerequisites

- Docker installed on your machine.
- Docker Compose installed on your machine.

## Configuration

The `docker-compose.yml` file defines the services, networks, and volumes for the Kafka and Zookeeper setup. Below is a breakdown of the configuration:

### Services

#### Zookeeper

- **Image**: Uses the latest Bitnami Zookeeper image.
- **Ports**: Maps port 2181 on the host to port 2181 in the container, which is the default port for Zookeeper.
- **Environment Variables**: Enables anonymous login for simplicity in development environments.

#### Kafka

- **Image**: Uses the latest Bitnami Kafka image.
- **User**: Runs as the root user inside the container.
- **Ports**: Maps port 9092 on the host to port 9092 in the container, which is the default port for Kafka brokers.
- **Environment Variables**:
  - Sets the broker ID to 1.
  - Configures listeners to use plaintext communication on port 9092.
  - Advertises listeners on localhost (127.0.0.1) for simplicity in development environments.
  - Connects to Zookeeper at `zookeeper:2181`.
  - Allows plaintext listener for ease of connection without SSL/TLS encryption.
- **Volumes**: Maps a local directory (`./Kafka`) to `/bitnami/kafka` inside the container for persistent storage.
- **Dependencies**: Ensures Kafka starts only after Zookeeper is up and running.

## Usage

1. Ensure Docker and Docker Compose are installed on your machine.
2. Clone this repository or copy the `docker-compose.yml` file to your project directory.
3. Open a terminal and navigate to the directory containing the `docker-compose.yml` file.
4. Run `docker-compose up -d` to start the services in detached mode.
5. Verify the services are running by executing `docker-compose ps`.

## Stopping the Services

To stop the Kafka and Zookeeper containers, execute the following command in the terminal:

```bash
docker-compose down
```

This command stops and removes the containers, networks, and volumes defined in your `docker-compose.yml` file.

## Conclusion

This setup provides a simple and effective way to run Kafka and Zookeeper locally using Docker Compose. It's suitable for development and testing purposes. For production environments, consider adjusting configurations such as security settings, persistence options, and scaling parameters.
