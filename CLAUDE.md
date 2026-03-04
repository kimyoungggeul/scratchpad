# CLAUDE.md - Scratchpad Repository Guide

## 이 레포는 무엇인가

이 레포는 **스크래치패드(scratchpad)** 레포입니다.
아이디어를 빠르게 프로토타이핑하고, 괜찮으면 독립 레포로 분리하는 용도입니다.

## 디렉토리 구조

```
/
├── CLAUDE.md          # 이 파일 (Claude Code 작업 가이드)
├── README.md          # 프로젝트 목록 & 상태 요약
├── projects/          # 활성 프로젝트
│   ├── project-a/     # 각 아이디어별 독립 폴더
│   │   ├── README.md  # 프로젝트 설명, 상태, 메모
│   │   └── ...
│   ├── project-b/
│   └── ...
└── archives/          # 분리/폐기된 프로젝트 보관
    ├── project-c/     # 📦 분리됨 또는 🗑️ 폐기된 프로젝트
    │   ├── README.md  # 상태, 분리 레포 링크 등 기록
    │   └── ...
    └── ...
```

## 작업 규칙

### 새 프로젝트 시작 시
1. `projects/<project-name>/` 폴더를 생성한다
2. 해당 폴더 안에 `README.md`를 만들고 아래 내용을 포함한다:
   - 프로젝트 한 줄 설명
   - 사용 기술 스택
   - 상태: `🧪 실험중` | `🚧 개발중` | `✅ 완성` | `📦 분리됨` | `🗑️ 폐기`
   - 시작일
3. 루트 `README.md`의 프로젝트 목록 테이블에 항목을 추가한다

### 작업 이어갈 때
1. 해당 프로젝트 폴더의 `README.md`를 먼저 읽고 맥락을 파악한다
2. 작업 후 변경사항을 `README.md`에 간단히 기록한다
3. 커밋 메시지 형식: `[project-name] 변경 내용 요약`

### 새 레포로 분리할 때

해당 프로젝트 폴더 관련 커밋 히스토리를 새 레포로 가져간다.

1. 스크래치패드 레포를 임시 디렉토리에 클론한다
2. `git filter-repo --subdirectory-filter projects/<project-name>`으로 해당 폴더의 히스토리만 추출한다
3. 새 GitHub 레포를 생성한다 (`gh repo create`)
4. 추출된 히스토리를 새 레포에 push한다
5. 새 레포에 적절한 `.gitignore`, `LICENSE`를 세팅한다
6. 임시 디렉토리를 정리한다
7. 이 스크래치패드 레포에서:
   - 원본 프로젝트 폴더를 `projects/`에서 `archives/`로 이동한다
   - 프로젝트 상태를 `📦 분리됨`으로 변경하고, 새 레포 링크를 기록한다
8. 루트 `README.md`의 프로젝트 테이블에서 링크를 `archives/`로 변경하고 분리 레포 링크를 추가한다

> 참고: `git-filter-repo`가 설치되어 있지 않으면 `pip install git-filter-repo`로 설치한다.

### 프로젝트 폐기 시
1. 프로젝트 상태를 `🗑️ 폐기`로 변경한다
2. `projects/`에서 `archives/`로 폴더를 이동한다 (나중에 참고할 수 있도록 보존)
3. 루트 `README.md`의 링크를 `archives/`로 업데이트한다

## 커밋 컨벤션

```
[project-name] 작업 내용 요약

예시:
[todo-app] 초기 프로토타입 생성
[todo-app] 다크모드 기능 추가
[todo-app] 새 레포로 분리 완료
[chat-bot] 프로젝트 폐기 처리
```

## 코드 스타일 기본 규칙

- 각 프로젝트는 독립적으로 실행 가능해야 한다
- 프로젝트 간 의존성을 만들지 않는다
- 각 프로젝트 폴더 안에 해당 프로젝트의 `.gitignore`를 둔다
- 가능하면 `package.json` 또는 `requirements.txt` 등 의존성 파일을 포함한다

## 루트 README.md 템플릿

루트 README.md는 아래 형식의 테이블을 유지한다:

```markdown
# 🧪 Scratchpad

| 프로젝트 | 설명 | 기술 스택 | 상태 | 분리 레포 |
|---------|------|----------|------|----------|
| [chat-bot](./projects/chat-bot) | AI 챗봇 실험 | Python, FastAPI | 🧪 실험중 | - |
| [todo-app](./archives/todo-app) | 간단한 투두앱 | React, TS | 📦 분리됨 | [링크](https://github.com/...) |
```

> 참고: 활성 프로젝트는 `projects/`에, 분리/폐기된 프로젝트는 `archives/`에 위치한다.
