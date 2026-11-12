# Book Writer Orchestration Harness
7개의 AI 에이전트 협업 기반 책 집필 오케스트레이션 하네스 (Claude Code 기반 과제)

## 과제 목표
단순 프롬프트 엔지니어링을 넘어, 독립적인 역할을 가진 7개의 AI 에이전트가 협업하여 책을 집필하는 오케스트레이션 하네스를 구현한다.
- 에이전트 역할 분리
- 최소 권한 원칙 기반 도구 할당
- 컨텍스트 예산 절약을 위한 단계적 정보 공개(Progressive Disclosure)
- Opus / Sonnet 모델 라우팅으로 비용 최적화
- 우체국 안티패턴 회피: 에이전트 간 직접 SendMessage 통신

## 에이전트 구성
| 에이전트 | 모델 | 권한 | 역할 |
|---|---|---|---|
| researcher | Opus | Read, Write, Edit, Grep | 주제 조사, 참고문헌 브리프 생성 |
| chapter-writer | Opus | Read, Write, Edit, Grep | 챕터 초고 작성 |
| tech-reviewer | Opus | Read, Write, Edit, Grep | 코드, 기술 로직 검토 |
| consolidation-agent | Opus | Read, Write, Edit, Grep | 리뷰 의견 취합, 최종 원고 병합 |
| fact-checker | Sonnet | Read, Grep (읽기전용) | 사실, 수치, 인용 검증 |
| structure-reviewer | Sonnet | Read, Grep (읽기전용) | 목차, 논리 흐름 검토 |
| copy-editor | Sonnet | Read, Grep (읽기전용) | 문법, 용어 통일, 문체 교정 |

## 워크플로우 파이프라인
`researcher → chapter-writer → [fact-checker, tech-reviewer, structure-reviewer 병렬 검토] → copy-editor → consolidation-agent → supervised-review`

## 작업 모드 (Progressive Disclosure Lazy Loading)
- writing
- revision
- compile
- sampling-review
- consolidation
- supervised-review
- paragraph-walkthrough

## 사용 방법
1. Claude Code 환경에서 이 프로젝트 폴더를 열기
2. SKILL.md 기반 book-writer 스킬 활성화
3. 트리거 키워드: 책 집필, 챕터 작성, 원고 통합, 사실 검증 등
4. 에이전트 팀이 자동 구성되어 협업 진행

## 설계 원칙
- 최소 권한：리뷰 에이전트는 원고 직접 수정 불가
- Why-First：강제 규칙 대신 근거와 함께 지시
- 컨텍스트 절약：필요한 workflow만 지연 로딩
- 안티패턴 회피：오케스트레이터가 모든 메시지를 중계하지 않음