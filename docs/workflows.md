# 재사용 워크플로

재사용 워크플로는 자동 상속되지 않습니다. 사용할 저장소에 이벤트, 권한과 중앙 워크플로를 호출하는 파일이 있어야 합니다.

## 구성

| 워크플로 | 중앙 파일 | 용도 |
|---|---|---|
| Astro Pages 배포 | `reusable-astro-pages.yml` | Astro 빌드와 GitHub Pages 배포 |
| 신규 이슈 자동 배정 | `reusable-auto-assign.yml` | 새 이슈를 `hadevyi`에게 자동 배정 |
| 공통 라벨 동기화 | `reusable-sync-labels.yml` | 공통·프로필별 라벨 생성·갱신·정리 |

중앙 파일은 [`.github/workflows`](../.github/workflows)에서 관리합니다.

## Astro Pages 배포

호출 저장소에서 배포 이벤트, Pages 권한과 저장소 변수를 전달합니다.

```yaml
name: Deploy Astro site to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    uses: hadevyi/.github/.github/workflows/reusable-astro-pages.yml@main
    with:
      public-ga-id: ${{ vars.PUBLIC_GA_ID }}
      public-google-site-verification: ${{ vars.PUBLIC_GOOGLE_SITE_VERIFICATION }}
```

저장소별 변수와 Secret은 호출 저장소에서 관리합니다.

## 신규 이슈 자동 배정

Issue Form 이외의 경로로 생성된 이슈도 기본 담당자에게 배정합니다.

```yaml
name: Auto assign issues

on:
  issues:
    types: [opened]

permissions:
  issues: write

jobs:
  assign:
    uses: hadevyi/.github/.github/workflows/reusable-auto-assign.yml@main
```

## 공통 라벨 동기화

각 저장소는 매월 13일 오전 9시 8분에 동기화하며 필요할 때 수동 실행할 수 있습니다.

```yaml
name: Sync shared labels

on:
  workflow_dispatch:
  schedule:
    - cron: "8 9 13 * *"
      timezone: "Asia/Seoul"

permissions:
  issues: write

jobs:
  sync:
    uses: hadevyi/.github/.github/workflows/reusable-sync-labels.yml@main
    with:
      profile: branding
```

사용 가능한 `profile` 값과 대상 저장소는 [라벨 체계](labels.md#프로필-적용-대상)에서 관리합니다. 중앙 `.github` 저장소도 별도 호출 파일에서 `governance` 프로필을 사용합니다.

- 예약 실행은 기본 브랜치의 최신 커밋을 기준으로 동작합니다.
- 공개 저장소에 60일 동안 활동이 없으면 GitHub가 예약 워크플로를 비활성화할 수 있습니다.
- 비활성화되거나 즉시 반영이 필요할 때는 `workflow_dispatch`로 수동 실행합니다.

## 적용 순서

1. 중앙 `.github` 저장소의 재사용 워크플로를 `main`에 반영합니다.
2. 호출 저장소에 이벤트와 권한을 선언한 워크플로를 반영합니다.
3. 라벨 동기화를 수동 실행해 기존 라벨을 중앙 체계로 정리합니다.
4. 기존 이슈에서 삭제된 라벨이 제거된 결과를 확인합니다.

중앙 라벨 동기화는 프로필에 선언되지 않은 라벨을 삭제합니다. 보존할 라벨이 있다면 먼저 프로필 정의에 추가해야 합니다.
