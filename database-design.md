# 데이터베이스 설계

BandMate는 **MongoDB**를 주 데이터베이스로 사용합니다. 데이터는 5개의 컬렉션으로 구성되며, 컬렉션 간의 관계는 ObjectId 참조(임베딩이 아닌 참조 방식)로 관리합니다. 이를 통해 도큐먼트를 가볍게 유지하고 독립적인 쿼리가 가능합니다.

---

## 컬렉션 관계도

```
users
  └── 참조됨: bands.members, practice_sessions, songs, practice_materials

bands
  └── 참조됨: practice_sessions, songs, practice_materials

practice_sessions
  └── 소속: bands

songs
  └── 소속: bands

practice_materials
  └── 소속: bands
  └── 선택적 연결: practice_sessions, songs
```

---

## 컬렉션: `users` (사용자)

각 사용자 계정의 인증 정보 및 기본 프로필을 저장합니다.

| 필드           | 타입     | 필수 여부 | 설명                                      |
|----------------|----------|-----------|-------------------------------------------|
| `_id`          | ObjectId | 자동 생성 | 고유 식별자                               |
| `name`         | String   | 필수      | 사용자 표시 이름                          |
| `email`        | String   | 필수      | 고유 이메일 주소 (로그인에 사용)          |
| `password`     | String   | 필수      | 해시된 비밀번호 (bcrypt 처리)             |
| `instrument`   | String   | 선택      | 주 담당 악기 (예: "기타", "드럼")         |
| `profileImage` | String   | 선택      | 프로필 사진의 경로 또는 URL               |
| `createdAt`    | Date     | 자동 생성 | 계정 생성 시각                            |
| `updatedAt`    | Date     | 자동 생성 | 마지막 수정 시각                          |

---

## 컬렉션: `bands` (밴드)

밴드 메타데이터 및 멤버 목록을 저장합니다.

| 필드          | 타입              | 필수 여부 | 설명                                          |
|---------------|-------------------|-----------|-----------------------------------------------|
| `_id`         | ObjectId          | 자동 생성 | 고유 식별자                                   |
| `name`        | String            | 필수      | 밴드 이름                                     |
| `description` | String            | 선택      | 밴드 소개 또는 설명                           |
| `genre`       | String            | 선택      | 음악 장르 (예: "록", "재즈")                  |
| `coverImage`  | String            | 선택      | 밴드 커버 이미지의 경로 또는 URL              |
| `members`     | Array of Object   | 필수      | 멤버 목록 (하위 필드 참조)                    |
| `createdBy`   | ObjectId (→ User) | 필수      | 밴드를 생성한 사용자 (밴드 리더)              |
| `createdAt`   | Date              | 자동 생성 | 생성 시각                                     |
| `updatedAt`   | Date              | 자동 생성 | 마지막 수정 시각                              |

**`members` 서브도큐먼트:**

| 필드       | 타입              | 설명                                     |
|------------|-------------------|------------------------------------------|
| `userId`   | ObjectId (→ User) | 해당 사용자에 대한 참조                  |
| `role`     | String (enum)     | `"leader"` (리더) 또는 `"member"` (멤버) |
| `joinedAt` | Date              | 밴드에 합류한 시각                       |

---

## 컬렉션: `practice_sessions` (합주 세션)

예정된 또는 완료된 합주 세션 하나하나를 나타냅니다.

| 필드        | 타입              | 필수 여부 | 설명                                                    |
|-------------|-------------------|-----------|---------------------------------------------------------|
| `_id`       | ObjectId          | 자동 생성 | 고유 식별자                                             |
| `bandId`    | ObjectId (→ Band) | 필수      | 이 세션이 속한 밴드                                     |
| `title`     | String            | 필수      | 세션 제목 (예: "주간 합주 #5")                          |
| `date`      | Date              | 필수      | 예정된 날짜 및 시간                                     |
| `location`  | String            | 선택      | 연습 장소 또는 스튜디오 이름                            |
| `status`    | String (enum)     | 필수      | `"scheduled"` (예정), `"completed"` (완료), `"cancelled"` (취소) |
| `agenda`    | String            | 선택      | 해당 세션에서 연습할 내용                               |
| `notes`     | Array of Object   | 선택      | 세션 이후 남기는 메모 목록 (하위 필드 참조)             |
| `createdBy` | ObjectId (→ User) | 필수      | 세션을 생성한 멤버                                      |
| `createdAt` | Date              | 자동 생성 | 생성 시각                                               |
| `updatedAt` | Date              | 자동 생성 | 마지막 수정 시각                                        |

**`notes` 서브도큐먼트:**

| 필드        | 타입              | 설명                         |
|-------------|-------------------|------------------------------|
| `authorId`  | ObjectId (→ User) | 메모를 작성한 멤버           |
| `content`   | String            | 메모 내용                    |
| `createdAt` | Date              | 메모 작성 시각               |

---

## 컬렉션: `songs` (곡 목록)

밴드의 셋리스트 또는 연습 곡 목록의 각 항목을 나타냅니다.

| 필드       | 타입              | 필수 여부 | 설명                                                          |
|------------|-------------------|-----------|---------------------------------------------------------------|
| `_id`      | ObjectId          | 자동 생성 | 고유 식별자                                                   |
| `bandId`   | ObjectId (→ Band) | 필수      | 이 곡이 속한 밴드                                             |
| `title`    | String            | 필수      | 곡 제목                                                       |
| `artist`   | String            | 선택      | 원곡 아티스트 또는 작곡가                                     |
| `key`      | String            | 선택      | 음악 키 (예: "C 장조", "A 단조")                              |
| `bpm`      | Number            | 선택      | 분당 비트 수 (템포)                                           |
| `status`   | String (enum)     | 필수      | `"learning"` (배우는 중), `"in-progress"` (연습 중), `"performance-ready"` (완성) |
| `notes`    | String            | 선택      | 곡에 대한 전반적인 메모                                       |
| `addedBy`  | ObjectId (→ User) | 필수      | 곡을 추가한 멤버                                              |
| `createdAt`| Date              | 자동 생성 | 생성 시각                                                     |
| `updatedAt`| Date              | 자동 생성 | 마지막 수정 시각                                              |

---

## 컬렉션: `practice_materials` (연습 자료)

업로드된 파일의 메타데이터를 저장합니다. 실제 파일 바이너리는 파일 시스템 또는 오브젝트 스토리지에 저장되며, 경로 또는 URL만 이 컬렉션에 기록됩니다.

| 필드             | 타입                          | 필수 여부 | 설명                                                                       |
|------------------|-------------------------------|-----------|----------------------------------------------------------------------------|
| `_id`            | ObjectId                      | 자동 생성 | 고유 식별자                                                                |
| `bandId`         | ObjectId (→ Band)             | 필수      | 이 자료가 속한 밴드                                                        |
| `uploadedBy`     | ObjectId (→ User)             | 필수      | 파일을 업로드한 멤버                                                       |
| `fileName`       | String                        | 필수      | 원본 파일 이름                                                             |
| `fileType`       | String (enum)                 | 필수      | `"sheet-music"` (악보), `"tab"` (탭), `"mr"` (MR), `"recording"` (녹음), `"other"` (기타) |
| `mimeType`       | String                        | 필수      | MIME 타입 (예: `audio/mpeg`, `application/pdf`)                            |
| `filePath`       | String                        | 필수      | 서버 경로 또는 클라우드 스토리지 URL                                       |
| `fileSize`       | Number                        | 필수      | 파일 크기 (바이트 단위)                                                    |
| `linkedSong`     | ObjectId (→ Song)             | 선택      | 이 자료와 연결된 곡 (선택 사항)                                            |
| `linkedSession`  | ObjectId (→ PracticeSession)  | 선택      | 이 자료와 연결된 합주 세션 (선택 사항)                                     |
| `description`    | String                        | 선택      | 파일에 대한 설명 또는 라벨                                                 |
| `createdAt`      | Date                          | 자동 생성 | 업로드 시각                                                                |

---

## 설계 유의사항

- **비밀번호**는 평문으로 저장하지 않습니다. 데이터베이스 저장 전 애플리케이션 계층에서 bcrypt로 해시 처리합니다.
- **파일 바이너리**는 MongoDB에 저장하지 않습니다. `practice_materials` 컬렉션에는 메타데이터와 파일 경로만 저장합니다.
- **인덱스**는 자주 쿼리되는 필드에 생성해야 합니다: `users.email`, `bands.members.userId`, `practice_sessions.bandId`, `songs.bandId`, `practice_materials.bandId`
