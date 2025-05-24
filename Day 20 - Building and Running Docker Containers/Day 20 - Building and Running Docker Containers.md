# Day 20 - Building and Running Docker Containers

## Objective:
Understand how to create your own Docker images using Dockerfiles, build them, run containers, and manage images effectively.

[![](https://img.youtube.com/vi/97Hdg4V4EPA/0.jpg)](https://www.youtube.com/watch?v=97Hdg4V4EPA)

[Watch the video](https://www.youtube.com/watch?v=97Hdg4V4EPA)
---

## What is a Dockerfile?

A `Dockerfile` is a script that contains a set of instructions to assemble a Docker image. It's the blueprint for your Docker image and defines what goes inside your container.

### Common Dockerfile Instructions:

- `FROM`: Specifies the base image.
- `RUN`: Executes commands in the container during build.
- `COPY` or `ADD`: Copies files into the image.
- `WORKDIR`: Sets the working directory inside the container.
- `CMD`: Specifies the command to run when the container starts.
- `EXPOSE`: Documents the port the container listens on.

---

## Docker Image & Container Commands

| Command | Description |
|--------|-------------|
| `docker build` | Builds a Docker image from a Dockerfile |
| `docker run` | Runs a Docker container from an image |
| `docker images` | Lists all local Docker images |
| `docker ps` | Lists running containers |
| `docker ps -a` | Lists all containers (including stopped) |
| `docker stop <container>` | Stops a running container |
| `docker rm <container>` | Removes a container |
| `docker rmi <image>` | Removes a Docker image |
| `docker tag` | Tags a Docker image |
| `docker push` | Pushes an image to Docker Hub |
| `docker pull` | Pulls an image from Docker Hub |
| `docker commit` | Creates an image from container changes |

---

## Lab: Build and Run Your First Docker Container

### Step 1: Create a Simple Python Flask App

```bash
mkdir docker-python-app
cd docker-python-app
````

**app.py**

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

**requirements.txt**

```
flask
```

---

### Step 2: Create a Dockerfile

```Dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]
```

---

### Step 3: Build Docker Image

```bash
docker build -t flask-docker-app .
```

---

### Step 4: Run Docker Container

```bash
docker run -d -p 5000:5000 flask-docker-app
```

Visit: `http://localhost:5000` (or your EC2 public IP if deployed remotely)

---

## Docker Hub Operations

### Tag Your Image

```bash
docker tag flask-docker-app your_dockerhub_username/flask-docker-app:v1
```

### Login to Docker Hub

```bash
docker login
```

### Push Image to Docker Hub

```bash
docker push your_dockerhub_username/flask-docker-app:v1
```

### Pull Image from Docker Hub

```bash
docker pull nginx
```

### Commit Container to Image

```bash
docker ps
docker commit <container_id> custom-nginx:v1
```

---

### Cleanup Commands

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
docker rmi flask-docker-app
```

---

## Summary

* You learned how to write a Dockerfile
* Built and ran a custom Docker container
* Tagged, pushed, pulled images with Docker Hub
* Used `docker commit` to save container changes

---