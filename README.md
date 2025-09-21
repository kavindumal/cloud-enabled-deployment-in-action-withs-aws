# Cloud Enabled Deployment In Action with AWS

This monorepo demonstrates a simple cloud‑ready microservices + frontend stack used for a practical assignment. It contains:

- **course-service** (Spring Boot + MySQL)
- **student-service** (Spring Boot + MongoDB)
- **media-service** (Spring Boot + local file storage → extendable to S3/MinIO)
- **frontend-app** (React + TypeScript + Vite + Axios + MUI)

---
## 👤 Student / Author
| Name | Registration No. | Programme | Email |
|------|------------------|-----------|-------|
| Kavindu Malshan Jayasinghe | 2301682069 | GDSE 68 | kavindu11250403@gmail.com |

---
## 🎬 Demonstration Video (≤ 3 min)

Google Drive link (ensure you are signed in to view):

https://drive.google.com/file/d/1zZkN0FAhGQtnM1uJ3lD-ksbkG5E4gGlB/view?usp=sharing

If the above link is not accessible, please request access via email. Marks may be deducted if the video cannot be viewed.

> (Optional YouTube embed placeholder – not used in this submission.)

---
## ✅ Assignment Submission Checklist

- [x] Meaningful commit history (no reused foreign commits apart from ECA materials)
- [x] README with usage + author + license + video link
- [x] Separate backend services + frontend
- [x] Demonstration video uploaded and accessible

> Note: Only the GitHub repository link needs to be submitted in Google Classroom. Late submissions are not accepted (Deadline: Sept 14, 11:59 PM).

---
## 🧩 Architecture Overview

Simple microservices communicating independently (no direct service-to-service dependencies represented here yet). Each service can be containerized and deployed separately to cloud platforms (AWS/GCP) with environment‑driven configuration.

```
┌────────────────┐   ┌──────────────────┐   ┌────────────────┐
│ course-service │   │ student-service  │   │ media-service  │
│ 8081 (MySQL)   │   │ 8082 (MongoDB)   │   │ 8083 (Disk/S3) │
└───────┬────────┘   └────────┬─────────┘   └────────┬───────┘
        │                      │                      │
        └─────────── REST API consumed by ────────────┘
                         frontend-app
```

---
## 🗄️ Backend Services

### 1. course-service
Entity: `Course(id, name, duration)`

Endpoints:
- `GET /courses`
- `GET /courses/{id}`
- `POST /courses`
- `DELETE /courses/{id}`

Defaults:
- Port: `8081`
- Requires MySQL (configure credentials via `application.properties` or environment variables)

### 2. student-service
Document: `Student(registrationNumber, fullName, address, contact, email)`

Endpoints:
- `GET /students`
- `GET /students/{id}`
- `POST /students`
- `DELETE /students/{id}`

Defaults:
- Port: `8082`
- Requires MongoDB instance (connection string configurable)

### 3. media-service
Resource: Uploaded files

Endpoints:
- `POST /files` (multipart field: `file`)
- `GET /files` (list)
- `GET /files/{id}` (download / fetch)
- `DELETE /files/{id}`

Defaults:
- Port: `8083`
- Storage: local path `./data/media` (override with env var `MEDIA_STORAGE_DIR`)

---
## 🖥️ Frontend (`frontend-app`)
React + TypeScript + Vite application providing UI sections for Courses, Students, and Media management.

Scripts:
- `npm install` – install dependencies
- `npm run dev` – start Vite dev server
- `npm run build` – production build
- `npm run preview` – preview build output

Environment variables (optional) can point to backend base URLs (e.g. create `.env` with `VITE_API_BASE=http://localhost:8081`).

---
## 🚀 Running Locally

Prerequisites:
- Java 17+
- Maven 3.9+
- Node.js 18+
- MySQL & MongoDB running (or adjust configs)

Backend build (skips tests for speed):
```
mvn -DskipTests package
```

Run each service (examples):
```
cd course-service
mvn spring-boot:run

cd ../student-service
mvn spring-boot:run

cd ../media-service
mvn spring-boot:run
```

Frontend:
```
cd frontend-app
npm install
npm run dev
```

Open the printed local URL (default: http://localhost:5173).

---
## 🔧 Configuration Notes

You can externalize configurations via Spring profiles (`application-dev.properties`, `application-aws.properties`, `application-gcp.properties`). Activate using:
```
mvn spring-boot:run -Dspring-boot.run.profiles=aws
```

Or with environment variable:
```
SPRING_PROFILES_ACTIVE=aws
```

Media storage override example (PowerShell):
```
$Env:MEDIA_STORAGE_DIR="D:/temp/media"
mvn spring-boot:run
```

---
## 🧪 Future Improvements (Roadmap)
- Add API gateway / single aggregated endpoint layer
- Containerize with Docker + compose file
- CI workflow (GitHub Actions) for build/test
- Add integration tests & contract tests
- Replace local file storage with AWS S3 bucket

---
## 📄 License

This project is released under the MIT License. See `LICENSE` file for details.

---
## 📬 Contact
For clarifications reach out via Slack or email: `kavindu11250403@gmail.com`.

---
## ✅ Academic Integrity
All work here is original for the assignment. No external unauthorized contributions were merged.

