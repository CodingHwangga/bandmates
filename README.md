# BandMate 형상관리 프로젝트

> 소프트웨어공학 과제 - BandMate 프로젝트 형상관리

---

## 📦 프로젝트 구조

```
bandmate-config-mgmt/
├── docs/
│   ├── requirements/     # 요구사항 관련 문서
│   ├── design/           # 설계 문서
│   ├── plan/             # 프로젝트 관리 문서
│   │   └── 과제2.프로젝트관리계획서.md
│   └── test/             # 테스트 문서
├── src/                  # 소스코드 (향후 추가)
├── .gitignore
├── CHANGELOG.md
├── 형상관리계획서.md
└── README.md
```

---

## 🚀 시작하기

### 1. 프로젝트 압축 해제
```bash
tar -xzf bandmate-config-mgmt.tar.gz
cd bandmate-config-mgmt
```

### 2. Git 상태 확인
```bash
git log --oneline --decorate
git tag
```

### 3. 현재 커밋 내역
```
a22723f (tag: v1.0.0) [FEAT] 과제2 프로젝트관리계획서 작성 완료
f43e40f [DOCS] 초기 프로젝트 구조 생성 및 형상관리 계획서 작성
```

---

## 📝 이번 주 완료 사항 (Week 1: 4/6-4/13)

- ✅ Git 저장소 초기화
- ✅ 형상관리 계획서 작성
- ✅ 프로젝트 관리 계획서 작성 (과제2)
- ✅ 디렉토리 구조 생성
- ✅ v1.0.0 태그 생성

---

## 🔄 다음 주 할 일 (Week 2: 4/14-4/20)

### 과제 3: 요구사항 정의서 작성
```bash
# draft 브랜치에서 작업
git checkout -b draft
# ... 요구사항 정의서 작성 ...
git add docs/requirements/과제3.요구사항정의서.md
git commit -m "[FEAT] 요구사항정의서 초안 작성"

# 검토 후 main 브랜치 병합
git checkout main
git merge draft
git tag requirements_freeze
```

---

## 📌 주간 Commit 체크리스트

- [ ] Week 2 (4/14-4/20): 과제3 요구사항정의서
- [ ] Week 3 (4/21-4/27): 과제4 요구사항분석서
- [ ] Week 4 (4/28-5/4): 과제5 소프트웨어설계서
- [ ] Week 5 이후: 개발 및 테스트

---

## 🔗 GitHub 연동 방법

### 1. GitHub에 새 저장소 생성
1. https://github.com 접속
2. "New repository" 클릭
3. 저장소 이름: `bandmate` 입력
4. Public/Private 선택 후 생성

### 2. 로컬 저장소와 연결
```bash
git remote add origin https://github.com/your-username/bandmate.git
git branch -M main
git push -u origin main --tags
```

### 3. 주 1회 Push
```bash
git push origin main --tags
```

---

## 📖 참고 문서

- `형상관리계획서.md`: 전체 형상관리 방침
- `docs/plan/과제2.프로젝트관리계획서.md`: 프로젝트 일정 및 관리 계획
- `CHANGELOG.md`: 변경 이력

---

**작성자**: 황주원  
**프로젝트**: BandMate  
**과목**: 소프트웨어공학  
**제출일**: 2026년 4월 13일
