# SKILL: book-writer
## Description
본 스킬은 다중 에이전트 오케스트레이션 프레임워크를 활용하여 책 집필 관련 작업을 수행합니다. 책 작성, 챕터 작성, 원고 통합, 사실 검증, 기술 리뷰, 구조 점검, 문체 교정, 초고 수정, 최종 빌드, 샘플 검토, 문단 단위 검사, 참고문헌 정리, 목차 생성, 장 분할, 원고 병합, 피드백 반영, 코드 예시 삽입, 메타 주석 추가, 분량 조절, 용어 통일, 인용 검증, 논리 보완, 오류 추적, 리뷰 의견 취합, 충돌 조율, 워크플로 재시작, 분할 제출, 에이전트 팀 생성 및 해체 요청을 감지합니다. 사용자 요청이 책 집필과 관련된 경우 우선 실행하며, 컨텍스트 토큰을 절약하기 위해 필요한 워크플로 파일만 조건부로 로드합니다. 오케스트레이터는 작업 분배, 팀 생성 및 해체만 관리하고 에이전트 간 직접 통신을 허용합니다.

## Progressive Disclosure: 7종 작업 모드 테이블
| 모드 이름 | 역할 | 로드 대상 워크플로 파일 |
|---|---|---|
| writing | 챕터 초고 작성 | workflows/01-writing.md |
| revision | 리뷰 피드백 기반 원고 수정 | workflows/02-revision.md |
| compile | 여러 챕터를 하나의 완성된 원고로 통합 | workflows/03-compile.md |
| sampling-review | 일부 샘플 문단 빠른 검토 | workflows/04-sampling-review.md |
| consolidation | 여러 리뷰 의견 취합 | workflows/05-consolidation.md |
| supervised-review | 최종 종합 검수 | workflows/06-supervised-review.md |
| paragraph-walkthrough | 문단 단위 흐름 검사 | workflows/07-paragraph-walkthrough.md |

## 분기 규칙
오케스트레이터는 사용자 요청에 맞는 모드만 선택하고 해당 워크플로 파일만 조건부로 로드합니다. 모든 상세 실행 로직은 워크플로 파일에 위임하며, 본 SKILL에 과도한 세부 내용을 기입하지 않습니다.
> 근거：Progressive Disclosure(점진적 정보 공개) 설계로 컨텍스트 토큰 사용량을 줄이고, 전체 워크플로를 한 번에 불러오는 것을 방지하기 위함입니다.

오케스트레이터는 에이전트 팀 생성, 작업 라우팅, 팀 해체만 담당하며 내부 피드백은 에이전트끼리 SendMessage로 직접 통신합니다.
> 근거：우체국 안티패턴을 회피하여 오케스트레이터가 단일 메시지 전달 병목 지점이 되는 것을 막기 위함입니다.

## References
1. https://github.com/revfactory/harness-engineering-with-cc/tree/main/ex-05-12-antipatterns
2. Claude Code 공식 문서
3. 본 과제 지침 문서
fix: https://wikidocs.net/363235,https://github.com/aiiiiiiiden/harness_engineering_8_priciples
