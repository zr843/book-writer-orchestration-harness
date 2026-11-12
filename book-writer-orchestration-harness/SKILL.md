# SKILL: book-writer
## Description
본 스킬은 다중 에이전트 오케스트레이션 하네스를 활용해 책 집필, 챕터 작성, 원고 통합, 사실 검증, 기술 리뷰, 구조 점검, 문체 교정, 초고 수정, 최종 빌드, 샘플 검토, 단락 순회 점검, 참고문헌 정리, 목차 생성, 장 분할, 원고 병합, 피드백 반영, 코드 예시 삽입, 메타데이터 주석 삽입, 분량 조절, 용어 통일, 인용 검증, 논리 흐름 보완, 오류 트래킹, 리뷰 의견 취합, 충돌 조율, 워크플로 재시작, 원고 분할 제출, 에이전트 팀 구성·해체 요청을 감지한다. 사용자 요청이 책 집필 관련일 경우 우선 실행하며, 컨텍스트 예산 절약을 위해 필요한 워크플로만 지연 로딩한다. 오케스트레이터는 단순 작업 배분자이며 에이전트 간 직접 메시지 교환을 허용한다.

## Progressive Disclosure: 7종 작업 모드 테이블
| 모드 이름 | 역할 | 로딩 대상 워크플로 파일 |
|---|---|---|
| writing | 챕터 초고 작성 | workflows/01-writing.md |
| revision | 리뷰 피드백 반영 수정 | workflows/02-revision.md |
| compile | 전체 챕터 통합 빌드 | workflows/03-compile.md |
| sampling-review | 일부 샘플 단락 검토 | workflows/04-sampling-review.md |
| consolidation | 다수 리뷰 주석 취합 | workflows/05-consolidation.md |
| supervised-review | 최종 종합 검수 | workflows/06-supervised-review.md |
| paragraph-walkthrough | 단락 단위 순회 점검 | workflows/07-paragraph-walkthrough.md |

## 분기 규칙
오케스트레이터는 요청에 맞는 모드만 선택하고, 해당 workflows 파일만 조건부로 로드한다. 모든 세부 절차는 워크플로 파일에 위임하며 SKILL.md에는 상세 절차를 기재하지 않는다. 오케스트레이터는 에이전트 팀 생성, 작업 라우팅, 팀 해체만 관리하고 내부 피드백은 SendMessage로 에이전트끼리 직접 교환한다.