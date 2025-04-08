
# 🧠 Technical Notes: Docker, GCP, CI/CD, Image Hosting, and Webhook

## 🐳 Docker Basics

### Docker Image
A Docker Image is a read-only template containing everything needed to run an application:
- OS (e.g., Debian, Alpine)
- App code
- Dependencies
- Environment variables
- Configuration files

**Features:**
- Read-only
- Portable (cross-platform)

**Analogy:** Like a recipe — you can’t “eat” it, but you can use it to cook.

### Docker Container
A Docker Container is a running instance of an image, providing an isolated, lightweight environment.

**Features:**
- Writable
- Isolated
- Fast boot

**Analogy:** Like a cooked meal based on the recipe (image).

---

## ☁ Google Cloud Platform (GCP)

**Essence:** Move your local dev environment to the cloud.

| Component      | Role                         |
|----------------|------------------------------|
| Compute Engine | Virtual machines for apps    |
| Cloud APIs     | Service integrations         |
| IAM            | Access control               |
| Cloud Storage  | Static file hosting          |
| GKE            | Kubernetes container orchestration |

---

## 🔁 CI/CD Workflow

- **CI (Continuous Integration):** Automatically build and test on every code push
- **CD (Continuous Delivery/Deployment):** Auto-deploy code to production

**Analogy:** Like a factory line — code gets pushed in, tested, and deployed automatically.

---

## 🖼 Image Hosting (图床)

**Purpose:** Upload and serve images via URL.

### Platforms:
- GitHub (easy)
- Alibaba Cloud OSS (professional)

### Notes:
- Base64: self-contained but large
- Recommended: use `.png`, `.jpg`, `.webp` and reference via URLs

---

## 🔔 Webhooks

Webhooks automatically trigger actions based on events.

### Examples:
- GitHub push triggers CI/CD
- Order placed triggers a notification or payment API

**Analogy:** Like a tripwire that starts a machine when stepped on.
