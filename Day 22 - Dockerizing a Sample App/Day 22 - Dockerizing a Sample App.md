# Day 22 - Dockerizing a Sample App


[![](https://img.youtube.com/vi/rKm-_VdjTsU/0.jpg)](https://www.youtube.com/watch?v=rKm-_VdjTsU)

[Watch the video](https://www.youtube.com/watch?v=rKm-_VdjTsU)

## 🎯 Objective

Learn how to Dockerize a full-stack application (Frontend + Backend) using Docker and run both services using Docker Compose. You’ll also use environment variables to configure the application.

---

## 🧠 Concepts Covered

- Dockerizing frontend and backend apps  
- Creating multi-container apps with Docker Compose  
- Using `.env` files for configuration  
- Building custom Dockerfiles for each service  
- Container-to-container networking in Docker

---

## 🧩 Project Structure

```

dockerized-app/
├── backend/
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
├── frontend/
│   ├── index.html
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
├── .env
├── docker-compose.yml
└── README.md

````

---

## 🧪 Lab Steps

### Step 1: Backend Setup (Node.js + Express)

**backend/server.js**
```js
const express = require('express');
const app = express();
const PORT = process.env.BACKEND_PORT || 4000;

app.get('/api', (req, res) => {
  res.json({ message: 'Hello from Backend API!' });
});

app.listen(PORT, () => {
  console.log(`Backend server running on port ${PORT}`);
});
````

**backend/package.json**

```json
{
  "name": "backend",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

**backend/Dockerfile**

```Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 4000

CMD ["npm", "start"]
```

---

### 🌐 Step 2: Frontend Setup (Express Static Server)

**frontend/index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Frontend</title>
  </head>
  <body>
    <h1>Hello from Frontend!</h1>
    <script>
      fetch('/api')
        .then(res => res.json())
        .then(data => {
          document.body.innerHTML += `<p>${data.message}</p>`;
        });
    </script>
  </body>
</html>
```

**frontend/server.js**

```js
const express = require('express');
const fetch = require('node-fetch');
const app = express();
const PORT = process.env.FRONTEND_PORT || 3000;

app.use(express.static(__dirname));

app.get('/api', async (req, res) => {
  const backendUrl = process.env.BACKEND_URL || 'http://localhost:4000/api';
  try {
    const response = await fetch(backendUrl);
    const data = await response.json();
    res.json(data);
  } catch (err) {
    res.status(500).json({ error: 'Failed to connect to backend' });
  }
});

app.listen(PORT, () => {
  console.log(`Frontend running on port ${PORT}`);
});
```

**frontend/package.json**

```json
{
  "name": "frontend",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "node-fetch": "^2.6.7"
  }
}
```

**frontend/Dockerfile**

```Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

### ⚙️ Step 3: Docker Compose Setup

**docker-compose.yml**

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "${BACKEND_PORT}:4000"
    environment:
      - BACKEND_PORT=${BACKEND_PORT}

  frontend:
    build: ./frontend
    ports:
      - "${FRONTEND_PORT}:3000"
    environment:
      - FRONTEND_PORT=${FRONTEND_PORT}
      - BACKEND_URL=http://backend:4000/api
    depends_on:
      - backend
```

---

### 🔐 Step 4: .env File

**.env**

```
BACKEND_PORT=4000
FRONTEND_PORT=3000
```

---

### ▶️ Step 5: Run the App

```bash
docker compose up -d --build
```

Visit the frontend:

```
http://localhost:3000
```

You should see a message from the backend displayed on the page.

---

### Step 6: Stop and Clean Up

```bash
docker compose down
docker image prune -f
```

---

## Extra Useful Docker Commands

```bash
docker logs <container_id>           # Show logs
docker inspect <container_id>        # View container metadata
docker exec -it <container_id> bash  # Access container shell
docker stats                         # Real-time container metrics
```

---

## Summary

✅ Built a full-stack app with backend and frontend
✅ Wrote Dockerfiles for both services
✅ Used Docker Compose for orchestration
✅ Configured with .env file
✅ Connected services using internal Docker networking