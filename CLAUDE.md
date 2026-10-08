# anipang — Orca Orchestration

## 프로젝트 구조

이 프로젝트는 **Claude(기획/조정)** + **Codex(구현)** 이중 에이전트 Orca orchestration으로 운영된다.

| worktree | 경로 | 브랜치 | 역할 |
|----------|------|--------|------|
| main | `projects/anipang` | `master` | 공통 기반 |
| shearwater | `workspaces/anipang/shearwater` | `jjinzxx/anipang-git-sync-baseline` | Claude — 기획·조정 |
| weakfish | `workspaces/anipang/weakfish` | `weakfish` | Codex — 구현 |

## 기준 브랜치

`master` → `origin/main` (GitHub: https://github.com/jjinzxx/anipang.git)

## Orchestration 규칙

1. **Claude** 가 기능 단위 태스크를 정의하고 Codex에게 할당한다.
2. **Codex** 가 구현한다. 사용자 코드 검수·승인 대기는 없다.
3. Codex가 애매한 결정을 만나면 **grilling** 방식으로 질문을 정리한 뒤 `orca ask`로 Claude에게 질문한다.
4. Claude가 답변하면 Codex는 즉시 구현을 재개한다.
5. 강제 푸시(`--force`) 및 기존 작업 삭제 금지.
