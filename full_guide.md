
# 🚀 Complete Guide to Full-Stack Application Cloud Deployment (GCP + Docker)

## 1. Architecture Overview

- Dual-container, dual-port:
  - Frontend on port 9191
  - Backend on port 9090

### Why this approach?
✅ Decoupled frontend/backend  
✅ Independent deployment  
✅ Scalable and maintainable  
❌ Requires more config (e.g., firewall rules)

---

## 2. Key Concepts

- **Containerization**: Package apps + environments
- **Port Mapping**: Frontend (9191), Backend (9090)
- **Firewall Rules**: Control network access

---

## 3. GCP Instance Setup

### Step 1: Create a VM
- Go to: https://console.cloud.google.com
- Region: `us-central1`, Type: `e2-micro`
- OS: Debian 11 or 12
- Allow HTTP/HTTPS traffic

### Step 2: SSH into VM
```bash
ssh -i ~/.ssh/google_compute_engine -o StrictHostKeyChecking=no your-user@<IP>
```

---

## 4. Install Environment

### Docker
```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Git
```bash
sudo apt install git-all
```

---

## 5. Clone Project from GitHub

```bash
git clone https://github.com/your-username/logoinResgister.git
cd logoinResgister
```

---

## 6. Project Structure

```
logoinResgister/
├── frontend/
├── backend/
└── docker-compose.yml
```

---

## 7. docker-compose Configuration

```yaml
services:
  frontend:
    build: ./frontend
    ports:
      - "9191:9191"
    environment:
      - VITE_BACKEND_PATH=http://<VM-IP>:9090
  backend:
    build: ./backend
    ports:
      - "9090:9090"
```

---

## 8. Firewall Rules

### Port 9191 (Frontend):
- Name: `allow-9191`
- Source: `0.0.0.0/0`

### Port 9090 (Backend):
- Name: `allow-9090`
- Source: `0.0.0.0/0`

---

## 9. Start Services

```bash
sudo docker compose up --build -d
```

Verify with:
```bash
sudo docker ps
sudo docker logs <container-name>
```

---

## 10. System Diagram

```
User Browser
     ↓
  Internet
     ↓
GCP Firewall
 ┌────────────────────┐
 │    GCP Instance    │
 │ ┌───────────────┐  │
 │ │ Frontend (9191)│ │
 │ └────┬──────────┘  │
 │      ↓             │
 │ ┌───────────────┐  │
 │ │ Backend (9090)│  │
 │ └───────────────┘  │
 └────────────────────┘
```

---

## 11. Access Links

- Frontend: `http://<your-ip>:9191`
- Backend: `http://<your-ip>:9090`

---

## 12. Best Practices

- HTTPS & Authentication (JWT)
- Restart policies & logs
- Use environment variables
- Load balancing or GKE for scalability
