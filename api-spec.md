# API 명세

모든 엔드포인트는 `/api` 접두사를 사용합니다. 요청 및 응답은 별도 명시가 없는 한 `application/json` 형식을 사용합니다.  
보호된 라우트는 `Authorization: Bearer <token>` 헤더(또는 HTTP-only 쿠키)에 유효한 JWT가 필요합니다.

---

## 인증 (Auth)

| 메서드 | 엔드포인트         | 설명                              | 인증 필요 |
|--------|--------------------|-----------------------------------|-----------|
| POST   | `/auth/register`   | 새 사용자 계정 등록               | 아니오    |
| POST   | `/auth/login`      | 로그인 후 JWT 발급                | 아니오    |
| POST   | `/auth/logout`     | 현재 세션 종료                    | 예        |
| GET    | `/auth/me`         | 현재 로그인한 사용자 정보 조회    | 예        |

---

## 사용자 (Users)

| 메서드 | 엔드포인트      | 설명                              | 인증 필요 |
|--------|-----------------|-----------------------------------|-----------|
| GET    | `/users/:id`    | 사용자 공개 프로필 조회           | 예        |
| PUT    | `/users/:id`    | 현재 사용자 프로필 수정           | 예        |
| DELETE | `/users/:id`    | 현재 사용자 계정 삭제             | 예        |

---

## 밴드 (Bands)

| 메서드 | 엔드포인트                          | 설명                                   | 인증 필요        |
|--------|-------------------------------------|----------------------------------------|------------------|
| POST   | `/bands`                            | 새 밴드 생성                           | 예               |
| GET    | `/bands`                            | 현재 사용자가 속한 밴드 목록 조회      | 예               |
| GET    | `/bands/:bandId`                    | 밴드 상세 정보 조회                    | 예               |
| PUT    | `/bands/:bandId`                    | 밴드 정보 수정                         | 예 (리더만)      |
| DELETE | `/bands/:bandId`                    | 밴드 삭제 (해체)                       | 예 (리더만)      |
| POST   | `/bands/:bandId/members`            | 사용자 ID 또는 이메일로 멤버 초대      | 예 (리더만)      |
| DELETE | `/bands/:bandId/members/:userId`    | 밴드에서 멤버 제거                     | 예 (리더만)      |

---

## 합주 일정 (Practice Sessions)

| 메서드 | 엔드포인트                                    | 설명                                    | 인증 필요 |
|--------|-----------------------------------------------|-----------------------------------------|-----------|
| POST   | `/bands/:bandId/sessions`                     | 새 합주 세션 생성                       | 예        |
| GET    | `/bands/:bandId/sessions`                     | 밴드의 모든 세션 목록 조회              | 예        |
| GET    | `/bands/:bandId/sessions/:sessionId`          | 특정 세션 상세 조회                     | 예        |
| PUT    | `/bands/:bandId/sessions/:sessionId`          | 세션 정보 수정 (날짜, 장소 등)          | 예        |
| DELETE | `/bands/:bandId/sessions/:sessionId`          | 세션 취소 / 삭제                        | 예        |
| POST   | `/bands/:bandId/sessions/:sessionId/notes`    | 세션에 메모 추가                        | 예        |

---

## 곡 목록 (Songs)

| 메서드 | 엔드포인트                          | 설명                                   | 인증 필요 |
|--------|-------------------------------------|----------------------------------------|-----------|
| POST   | `/bands/:bandId/songs`              | 밴드 곡 목록에 곡 추가                 | 예        |
| GET    | `/bands/:bandId/songs`              | 밴드의 전체 곡 목록 조회               | 예        |
| GET    | `/bands/:bandId/songs/:songId`      | 특정 곡 상세 조회                      | 예        |
| PUT    | `/bands/:bandId/songs/:songId`      | 곡 정보 또는 연습 상태 수정            | 예        |
| DELETE | `/bands/:bandId/songs/:songId`      | 곡 목록에서 곡 삭제                    | 예        |

---

## 연습 자료 / 파일 업로드 (Practice Materials)

| 메서드 | 엔드포인트                                    | 설명                                       | 인증 필요 |
|--------|-----------------------------------------------|--------------------------------------------|-----------|
| POST   | `/bands/:bandId/materials`                    | 파일 업로드 (악보, 탭, 녹음 등)            | 예        |
| GET    | `/bands/:bandId/materials`                    | 밴드에 업로드된 전체 자료 목록 조회        | 예        |
| GET    | `/bands/:bandId/materials/:materialId`        | 특정 파일 메타데이터 조회                  | 예        |
| DELETE | `/bands/:bandId/materials/:materialId`        | 업로드된 파일 삭제                         | 예        |

> **참고:** 파일 업로드 엔드포인트는 `multipart/form-data` 인코딩을 사용합니다.  
> 지원 파일 형식: `.pdf`, `.png`, `.jpg`, `.mp3`, `.wav`, `.m4a`, `.gp`, `.gp5`  
> 최대 파일 크기: 업로드당 **50MB**

---

## 응답 형식

모든 응답은 아래 구조를 따릅니다.

**성공 응답**
```json
{
  "success": true,
  "data": { ... }
}
```

**오류 응답**
```json
{
  "success": false,
  "message": "사람이 읽을 수 있는 오류 메시지",
  "code": "ERROR_CODE"
}
```

---

## HTTP 상태 코드

| 코드 | 의미                              |
|------|-----------------------------------|
| 200  | OK — 요청 성공                    |
| 201  | Created — 리소스 생성 성공        |
| 400  | Bad Request — 잘못된 입력         |
| 401  | Unauthorized — 로그인 필요        |
| 403  | Forbidden — 권한 없음             |
| 404  | Not Found — 리소스를 찾을 수 없음 |
| 500  | Internal Server Error — 서버 오류 |
