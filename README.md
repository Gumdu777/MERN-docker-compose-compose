# Containerizing a MERN Stack Application and Deploying with Docker Compose

This project demonstrates how to containerize a simple MERN (MongoDB, Express, React, Node.js) stack application using Docker and Docker Compose. By leveraging Docker's containerization, the application is seamlessly deployed with isolated and interlinked services.

---

## Features

- **Full MERN Stack Application**: A simple application built with MongoDB, Express.js, React.js, and Node.js.
- **Docker Containerization**: Each component is containerized for easy deployment and scalability.
- **Docker Networking**: Containers communicate with each other using a Docker network.
- **Persistent Storage**: MongoDB data is stored persistently using Docker volumes.
- **Docker Compose Integration**: Simplifies multi-container orchestration.

---

## Prerequisites

- [Docker](https://www.docker.com/) installed on your system.
- [Docker Compose](https://docs.docker.com/compose/) installed.
- Basic understanding of Docker and containerization.

---

## Steps to Containerize the MERN Stack Application

### 1. Create a Docker Network

```bash
docker network create demo
```
This network allows the containers (frontend, backend, and MongoDB) to communicate with each other.

---

### 2. Build and Run the Frontend (React.js)

#### Build the Frontend
Navigate to the `mern/frontend` directory and build the Docker image:

```bash
cd mern/frontend
docker build -t mern-frontend .
```

#### Run the Frontend Container

```bash
docker run --name=frontend --network=demo -d -p 5173:5173 mern-frontend
```

#### Verify the Frontend
Open your browser and navigate to:

```
http://localhost:5173
```

---

### 3. Run the MongoDB Container

Run a MongoDB container with persistent storage:

```bash
docker run --network=demo --name mongodb -d -p 27017:27017 -v ~/opt/data:/data/db mongo:latest
```

This maps the container’s data directory to `~/opt/data` on your host machine.

---

### 4. Build and Run the Backend (Node.js + Express.js)

#### Build the Backend
Navigate to the `mern/backend` directory and build the Docker image:

```bash
cd mern/backend
docker build -t mern-backend .
```

#### Run the Backend Container

```bash
docker run --name=backend --network=demo -d -p 5050:5050 mern-backend
```

---

### 5. Using Docker Compose

Docker Compose simplifies the process of running multi-container applications. Instead of manually managing each container, you can use the `docker-compose.yml` file provided in this project.

#### Start the Application with Docker Compose

```bash
docker compose up -d
```
This command builds and starts all the containers defined in the `docker-compose.yml` file.

---

## Verify the Application

1. **Frontend**: Open your browser and navigate to:
   ```
   http://localhost:5173
   ```

2. **Backend**: The backend API is running on:
   ```
   http://localhost:5050
   ```

3. **MongoDB**: MongoDB is accessible on port 27017.

---

## Benefits of Docker Containerization

- **Isolation**: Each service runs in its own container, ensuring no conflicts between dependencies.
- **Portability**: The application can be deployed on any system with Docker installed.
- **Scalability**: Easily scale services by running additional containers.
- **Simplified Networking**: Docker handles container communication via a dedicated network.
- **Persistent Data**: MongoDB data persists even if the container is stopped or removed.

---

## Conclusion

This project highlights the power of Docker containerization and Docker Compose to simplify the deployment of a MERN stack application. By breaking the application into containers, it ensures modularity, portability, and scalability, making it production-ready.

Feel free to contribute or use this repository as a template for your own projects!
   
