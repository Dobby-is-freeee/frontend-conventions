# git branch strategy

git flow란 `master`, `develop`, `release`, `feature`, `hotfix`로 이뤄진 브랜치 전략으로 현재 가장 유명하다.

만약 git flow를 모른다면. 다음 사이트를 참조하자.

[git flow 알아보기](https://uxgjs.tistory.com/183)

본 문서는 git flow의 규칙을 따르되, 약간의 각색이 있으므로 git flow의 개념을 알고 있는 편이 좋다.

## Master
**운영 서버**에 배포 되는 브랜치이다.

운영 서버에 배포되므로 기본적으로 **안정적**이고 **build와 test에 오류가 없어야 한다.**

## Develop
**개발 서버**에 배포 되는 브랜치이다.

해당 브랜치는 개발이 끝난 기능(feature)들이 포함되어 있다.

실제 유저가 만나는 운영 서버에 배포 되기 전, 테스트를 위하여 사용하는 브랜치이다.

## Feature
배포 되지는 않고, 기능 개발을 진행하는 브랜치이다.

다음과 같은 규칙으로 브랜치를 생성한다.

- `feat/{원하는이름}`

해당 브랜치는 기본적으로 `develop`을 기반으로 생성되며, 생성된 브랜치의 PR 역시 `develop` 브랜치를 향한다.

- PR : `feat/{원하는이름}` -> `develop`

## Base Feature

만약 어떠한 기능을 위해 페이지 마크업과 스타일링을 진행해야 하고, 스크립트를 적용시켜야 한다면 하나의 PR로 부족할 수 있다.

이처럼 기능 개발 단위가 클때는 `Base Feature` 브랜치를 생성해 진행한다.

- `feat/{원하는이름}_base`
  - ex) `develop` -> `feat/something_base` 생성

이제 `feat/something_base`를 기반으로 브랜치를 생성해 작업을 진행하고, PR을 보낸다.

이때 **base 브랜치**에서 파생된 브랜치를 **서브 브랜치**라고 하며 다음과 같은 규칙을 지켜 생성하도록 한다.

- `feat/something_{yyMMdd[a~b]}`
  - ex) `feat/something_220504a`

**서브 브랜치는 항상 베이스 브랜치를 향하여 PR을 보내야하며, 그 순서도 지켜야 한다.**

- PR : `feat/something_220504a` -> `feat/something_base`

순서를 파악하기 위해 가장 마지막 단에는 알파벳을 순서로 지키는 걸 권장한다.

## HotFix
운영 중인 서버에 문제가 생긴다면 hotfix 브랜치를 생성한다.

- `hotfix/{원하는이름}`

hotfix 브랜치는 `master` 브랜치를 향하여 PR한다.

- PR : `hotfix/{원하는이름}` -> `master`

hotfix 브랜치가 master 브랜치에 병합되었다면 master 브랜치를 다시 develop 브랜치에 머지하는 작업을 또 한 번 수행해야 한다.

이를 **백머지(Back Merge)**라고 하며, `master` -> `develop` 로 PR을 진행한다.