# 🚀 TalleMalle Docker Deployment Guide

이 문서는 TalleMalle 프로젝트를 리눅스 서버에서 Docker Compose를 사용해 쉽고 안전하게 배포하기 위한 안내서입니다.

---

## 📂 프로젝트 구조
```text
TalleMalle/
├── backend/            # Spring Boot / API 서버
├── frontend/           # React (Vite) / 클라이언트
└── docker/             # Docker 설정 파일 및 실행 디렉토리
    └── docker-compose.yml
```

---

## 🛠️ 사전 준비 (Prerequisites)
1. **Docker & Docker Compose** 설치 완료
2. **Git** 설치 완료

---

## ⚙️ 환경 설정 (.env 세팅)

프로젝트 실행을 위해 `backend`, `frontend`, `docker` 폴더 각각에 `.env` 파일을 생성해야 합니다.

### 1️⃣ 백엔드 설정 (`backend/.env`)
`backend` 폴더 내에 `.env` 파일을 생성하고 아래 내용을 입력하세요.
```bash
# Database (데이터베이스)
DB_URL=jdbc:mariadb://db:3306/tallemalle (DB 접속 URL)
DB_USER=root (DB 사용자명)
DB_PASS=your_secure_password (DB 비밀번호)

# Security (보안)
JWT_SECRET=your_jwt_secret_key (JWT 서명용 비밀키)
JWT_EXPIRE=86400 (JWT 만료 시간)
AES_KEY=your_aes_encryption_key (AES 암호화 키)

# App Settings (앱 주소 및 경로)
UPLOAD_PATH=./uploads (파일 업로드 경로)
COOKIE_DOMAIN=localhost (쿠키 도메인)
FRONT_URL=http://localhost (프론트엔드 접속 주소)
API_URL=http://localhost:8080 (백엔드 API 접속 주소)
SSL_KEY_PASS=your_ssl_password (SSL 키스토어 비밀번호)

# OAuth2 (소셜 로그인)
GOOGLE_CLIENT_ID=your_google_id (구글 클라이언트 ID)
GOOGLE_CLIENT_SECRET=your_google_secret (구글 클라이언트 시크릿)
GOOGLE_REDIRECT_URI=http://localhost:8080/login/oauth2/code/google (구글 리다이렉트 URI)
KAKAO_CLIENT_ID=your_kakao_id (카카오 클라이언트 ID)
KAKAO_CLIENT_SECRET=your_kakao_secret (카카오 클라이언트 시크릿)
KAKAO_REDIRECT_URI=http://localhost:8080/login/oauth2/code/kakao (카카오 리다이렉트 URI)

# External Services (외부 서비스)
MAIL_ADDR=your_email@gmail.com (관리자 메일 주소)
MAIL_PASS=your_email_password (메일 앱 비밀번호)
AWS_ACCESS_KEY=your_aws_access (AWS 액세스 키)
AWS_SECRET_KEY=your_aws_secret (AWS 시크릿 키)
TOSS_SECRET_KEY=your_toss_key (토스페이먼츠 시크릿 키)
KAKAO_API_KEY=your_kakao_api_key (카카오 REST API 키)
PORTONE_SECRET_API=your_portone_api (포트원 시크릿 API 키)

# Push Notification (푸시 알림)
VAPID_PUBLIC_KEY=your_vapid_public (VAPID 공개키)
VAPID_PRIVATE_KEY=your_vapid_private (VAPID 개인키)
```

### 2️⃣ 프론트엔드 설정 (`frontend/.env`)
`frontend` 폴더 내에 `.env` 파일을 생성하세요. (빌드 시 정적 파일에 포함됩니다.)
```bash
VITE_API_BASE_URL=http://<SERVER_IP>:8080 (백엔드 API 서버 주소)
VITE_WS_URL=ws://<SERVER_IP>:8080/ws (웹소켓 접속 주소)
VITE_KAKAO_MAP_KEY=your_kakao_map_key (카카오맵 자바스크립트 키)
VITE_PORTONE_STORE_ID=your_store_id (포트원 가맹점 식별코드)
VITE_PORTONE_CHANNEL_KEY=your_channel_key (포트원 채널 키)
VITE_VAPID_PUBLIC_KEY=your_vapid_public_key (VAPID 공개키)
```

### 3️⃣ Docker 실행 설정 (`docker/.env`)
`docker` 폴더 내에 `.env` 파일을 생성하세요. (컨테이너 오케스트레이션 및 빌드 인자)
```bash
# DB 초기 설정
DB_ROOT_PASSWORD=your_secure_password (DB 루트 비밀번호)
DB_NAME=tallemalle (생성할 DB 이름)

# Frontend 빌드 인자 (위 frontend/.env 설정과 동일하게 작성)
VITE_API_BASE_URL=http://<SERVER_IP>:8080 (백엔드 API 서버 주소)
VITE_WS_URL=ws://<SERVER_IP>:8080/ws (웹소켓 접속 주소)
```

---

## 🚀 실행 방법 (How to Run)

1. **프로젝트 클론**
   ```bash
   git clone <REPO_URL>
   cd TalleMalle
   ```

2. **환경 변수 파일 생성**
   - 위 안내에 따라 `backend/.env`, `frontend/.env`, `docker/.env` 세 파일을 작성합니다.

3. **컨테이너 빌드 및 실행**
   ```bash
   cd docker
   docker compose up -d --build
   ```

4. **상태 확인**
   ```bash
   docker compose ps
   ```

---

## ⚠️ 주의 사항
- `.env` 파일은 민감한 정보를 포함하고 있으므로 **절대로 Git에 커밋하지 마세요.**
- 서버 배포 시 80(Front), 8080(Back), 3306(DB) 포트가 방화벽에서 열려있는지 확인하세요.
"# TalleMalle_DevOps" 
