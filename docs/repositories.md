# 저장소 적용 현황

## 관리 대상

| 저장소 | 기본 브랜치 | 라벨 프로필 | 자동 배정 | Pages 배포 |
|---|---|---|---|---|
| `.github` | `main` | `governance` | 적용 | 해당 없음 |
| `hadevyi` | `main` | `profile` | 적용 | 해당 없음 |
| `hadevyi.github.io` | `main` | `branding` | 적용 | 적용 |
| `blog` | `main` | `branding` | 적용 | 적용 |
| `experience` | `main` | `branding` | 적용 | 적용 |
| `portfolio` | `main` | `branding-document` | 적용 | 적용 |
| `resume` | `main` | `branding-document` | 적용 | 적용 |
| `Algorithms-Problem-Solving` | `main` | `algorithm` | 적용 | 해당 없음 |
| `Learn-New-Thing` | `main` | `learning` | 적용 | 해당 없음 |

라벨 동기화는 모든 관리 대상 저장소에서 매월 13일 오전 9시 8분에 실행하며 수동 실행도 지원합니다.

## 제외 대상

| 저장소 | 제외 사유 | 중앙 기본 템플릿 |
|---|---|---|
| `ETRI_Intern` | 비공개 과거 프로젝트 | 자동 상속 안 됨 |
| `English-Word-Study` | 아카이브 보관용 대학 프로젝트 | 공개 저장소지만 중앙화 대상 제외 |
| `O-to-I` | 아카이브 보관용 대학 프로젝트 | 공개 저장소지만 중앙화 대상 제외 |
| `ZB-BE-DS-ALGO` | 향후 학습 저장소로 통합 예정 | 공개 저장소이므로 자체 템플릿 제거 후 상속 가능 |
| `Project-With-AI` | 삭제 예정 | 반영하지 않음 |
| `productive-box` | Fork | 반영하지 않음 |
| `github-stats-box` | Fork | 반영하지 않음 |

제외 대상에는 라벨 동기화, 자동 배정과 배포 호출 워크플로를 추가하지 않습니다.

## 적용 경계

- 중앙 기본 이슈·PR 템플릿은 자체 템플릿이 없는 공개 저장소에서 상속됩니다.
- 라벨, 자동 배정과 배포는 호출 워크플로가 있는 저장소에서만 실행됩니다.
- 저장소 전용 빌드 설정, 변수, Secret과 라벨은 각 저장소에서 관리합니다.
- 브랜딩 사이트의 콘텐츠와 UI 변경은 중앙 설정 반영 범위에 포함하지 않습니다.
