# 🎸 BandMate

> 밴드의 합주 일정, 곡 목록, 연습 자료를 한 곳에서 관리하는 웹 플랫폼입니다.

BandMate는 밴드 멤버들이 합주 일정 조율부터 악보 공유, 녹음 파일 보관까지 음악 활동에 필요한 모든 것을 효율적으로 관리할 수 있도록 도와줍니다.

---

## ✨ 주요 기능

- **밴드 관리** — 밴드를 생성하고 멤버를 초대하여 역할을 관리
- **합주 일정 관리** — 캘린더 형태로 연습 세션을 계획하고 기록
- **곡 목록 관리** — 셋리스트를 공유하고 곡별 연습 진행 상태 추적
- **연습 자료 공유** — 기타 탭, 악보, MR 파일 등 자료를 팀원과 공유
- **합주 녹음 저장** — 연습 녹음 파일을 업로드하고 세션별 메모 기록

---

## 🛠 기술 스택

| 구분         | 기술                              |
|--------------|-----------------------------------|
| 프론트엔드   | Next.js + React                   |
| 백엔드       | Node.js + Express                 |
| 데이터베이스 | MongoDB                           |
| 파일 저장    | 로컬 스토리지 / 클라우드 스토리지 |

---

## 📁 레포지토리 구조

```
bandmate/
├── client/                      # Next.js 프론트엔드
│   ├── components/              # 재사용 가능한 React 컴포넌트
│   ├── pages/                   # Next.js 페이지 라우트
│   ├── styles/                  # 전역 및 모듈 CSS
│   └── public/                  # 정적 파일 (이미지, 폰트 등)
│
├── server/                      # Node.js + Express 백엔드
│   ├── controllers/             # 라우트 핸들러 로직
│   ├── models/                  # Mongoose 데이터 모델
│   ├── routes/                  # API 라우트 정의
│   └── middleware/              # 인증 및 에러 처리 미들웨어
│
├── docs/                        # 프로젝트 설계 문서
│   ├── system-architecture.md  # 시스템 아키텍처 설계
│   ├── api-spec.md              # REST API 명세
│   ├── database-design.md      # 데이터베이스 설계
│   └── wireframe.md            # UI 와이어프레임
│
├── .env.example                 # 환경 변수 템플릿
├── .gitignore
└── README.md
```

---

## 🚀 시작하기

### 사전 요구 사항

- Node.js v18 이상
- MongoDB (로컬 설치 또는 MongoDB Atlas)

### 설치

```bash
# 레포지토리 클론
git clone https://github.com/your-username/bandmate.git
cd bandmate

# 서버 의존성 설치
cd server && npm install

# 클라이언트 의존성 설치
cd ../client && npm install
```

### 실행

```bash
# 백엔드 서버 실행
cd server && npm run dev

# 프론트엔드 실행 (새 터미널에서)
cd client && npm run dev
```

앱은 `http://localhost:3000`에서 실행됩니다.

---

## 👥 팀 소개

본 프로젝트는 대학교 소프트웨어공학 과목의 팀 프로젝트로 개발되었습니다.

---

## 📄 라이선스

MIT
