# Day 21 - Docker Networking, Volumes, and Compose


[![](https://img.youtube.com/vi/nMbGQ9my7TY/0.jpg)](https://www.youtube.com/watch?v=nMbGQ9my7TY)

[Watch the video](https://www.youtube.com/watch?v=nMbGQ9my7TY)

1. Docker Networking

---

### Summary

Docker networking enables containers to communicate with each other and with external networks. Docker provides several network drivers tailored to specific use cases.

| Network Mode | Description                                         | Use Case                                 |
| ------------ | --------------------------------------------------- | ---------------------------------------- |
| bridge       | Default internal network with NAT and IP assignment | Local isolated containers                |
| host         | Shares host network stack (no isolation)            | High-performance apps                    |
| none         | Disables networking completely                      | Secure or offline containers             |
| overlay      | Enables cross-host networking                       | Distributed microservices in Swarm       |
| macvlan      | Assigns MAC address from physical NIC               | Legacy apps requiring Layer 2 visibility |
| ipvlan       | Similar to macvlan with Layer 3 separation          | High-scale apps                          |

### Internals

* Uses Linux namespaces for isolation
* Virtual Ethernet pairs (veth) connect containers to host bridge (docker0)
* iptables/NAT handles external access
* Internal DNS at 127.0.0.11

### Lab Examples

**Bridge Network:**

```sh
docker network create my_bridge_net
docker run -dit --name app1 --network my_bridge_net alpine sh
docker run -dit --name app2 --network my_bridge_net alpine sh
docker exec app1 ping app2
```

**Host Network:**

```sh
docker run --rm -d --network host nginx
curl http://localhost:80
```

**None Network:**

```sh
docker run -dit --name isolated --network none alpine
```

**Overlay Network (Docker Swarm):**

```sh
docker swarm init
docker network create --driver overlay my_overlay_net
docker service create --replicas 2 --network my_overlay_net --name web nginx
```

**Macvlan Network:**

```sh
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 \
  macvlan_net
docker run -dit --name mac_container --network macvlan_net alpine
```

2. Docker Storage

---

### Storage Options

| Type        | Description                                             | Use Case                  |
| ----------- | ------------------------------------------------------- | ------------------------- |
| Volumes     | Managed by Docker, stored under /var/lib/docker/volumes | Recommended for most apps |
| Bind Mounts | Maps host path to container                             | Dev or advanced use       |
| tmpfs       | RAM-only storage, non-persistent                        | Temporary secrets/logs    |

### Volumes

```sh
docker volume create mydata
docker run -dit --name volume-container -v mydata:/app/data alpine sh
docker exec -it volume-container sh -c "echo 'persistent log' > /app/data/log.txt"
docker rm -f volume-container
docker run --rm -v mydata:/app/data alpine cat /app/data/log.txt
```

### Bind Mount

```sh
mkdir -p /tmp/logs
echo "Hello from host" > /tmp/logs/hello.txt
docker run --rm -v /tmp/logs:/data alpine cat /data/hello.txt
```

### tmpfs Mount

```sh
docker run --rm \
  --tmpfs /app/temp \
  alpine sh -c "echo secret > /app/temp/secret && cat /app/temp/secret"
```

3. Docker Compose

---

### Overview

Tool for defining and running multi-container Docker apps using YAML.

### Benefits

* Declarative configuration
* Simplified orchestration
* Built-in networking
* Portable across environments

### Example File

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis
    networks:
      - appnet

  redis:
    image: redis
    networks:
      - appnet

networks:
  appnet:
```

### Flask + Redis Lab Example

**Directory Structure:**

```
docker-compose-demo/
├── app.py
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

**app.py**

```python
from flask import Flask
import redis
app = Flask(__name__)
r = redis.Redis(host='redis', port=6379)

@app.route('/')
def count():
    r.incr('hits')
    return f"Viewed {r.get('hits').decode('utf-8')} times."

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

**requirements.txt**

```
flask
redis
```

**Dockerfile**

```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

**docker-compose.yml**

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis
    networks:
      - appnet

  redis:
    image: redis
    networks:
      - appnet

networks:
  appnet:
```

**Commands:**

```sh
docker-compose up --build
docker-compose down -v
```
