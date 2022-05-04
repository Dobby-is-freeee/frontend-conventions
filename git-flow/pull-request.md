# Pull Request

Pull Request(이하 PR)이란, 브랜치 하나를 다른 브랜치에 병합(merge)시키기 위해 요청하는 작업을 뜻한다.

PR은 협업에 있어 필수적인 과정으로, 코드 리뷰를 통해 각자의 코드 스타일을 파악하고 개선점을 같이 찾아 볼 수 있으며 서로 알고 있는 지식을 교류해 긍정적인 효과를 가질 수 있다.

이전 문서인 [git-branch-strategy](./git-branch-strategy.md)를 읽지 않았다면 이해하지 못할 수 있다.

## 일반적 PR

일반적으로 PR 이름은 생성된 브랜치의 suffix + 콜론(:)과 어떤 것을 위한 PR인지 요약해 작성한다. 

예컨데, `feat/something`이라면 PR 제목은 다음처럼 작성하면 된다.

- `Feat: {PR제목}`

첫 문자는 대문자로 시작한다.

일반적인 규칙이므로 모든 PR시 통용된다.

만약 이슈(깃헙, 지라 ..etc) 관리를 사용한다면. 제목 뒤에 이슈 번호를 붙인다. 이 사항은 모든 부분 공통으로 따로 언급하지 않겠다.

- ex) `Feat: {PR제목} [#1]`

## Base PR

이전 문서에서 보았듯, `base branch`와 `sub branch`가 있다. 

`sub branch` 브랜치나 `base branch`라도 각각의 브랜치명은 `feat`로 시작할 것이다.

그러나 `sub branch`에서 `base branch`로 PR을 보낼 때는 `Feat: {PR제목}`이 아니라, Sub + 콜론(:)을 붙인다.

- `Sub: something 개발`

굳이 `sub`를 붙이는 이유는 이 PR이 `develop`을 향하는 PR인지 `base branch`를 향하는 PR인지 손쉽게 체크하는 점에 있다.

## Release PR

`develop` 브랜치를 `master` 브랜치를 향해 PR을 보내야 할 때면 다른 규칙을 이용한다.

이때, develop으로 배포된 개발 서버에서 오류가 없는지 꼭 확인한다.

`master` 브랜치로 보낸다는 건, 운영 서버로의 배포를 의미 하므로 Release + 콜론(:)을 붙인다.

또한 `package.json`의 버전업을 진행하여 해당하는 Release 버전을 명시한다.

- `Release: v1.8.0`

> 버전 관리에 대한 설명은 [version-management]("./version-management.md) 참조.


## BackMerge PR

`master` 브랜치로 바로 병합하는 `hotfix`의 경우, 다시 `develop`을 향하여 PR을 보낼 필요가 있다.

이를 **백머지**라고 한다. 백머지 PR은 다음처럼 작성한다.

- `BackMerge: v1.8.0`

## Try PR

가끔 서버에 배포하여 확인해야만 하는 상황이 생긴다.

이때는 Try PR을 보내 병합하여 실험적으로 서버 배포를 진행할 수 있다.

- `Try: {PR제목}`

Try를 명시하면 코드를 보는 리뷰어는 이 PR이 배포 후 테스트를 위한 PR임을 알 수 있다. 하여 즉각 `approve`를 할 수 있다.

Try PR을 시도하고 성공했다면 해당 PR을 다시 올리기 때문에 상관없다.

Try PR을 성공했다면 작성자는 해당 하는 코드를 다시 PR로 올린다.

- ex) `Feat: {PR제목}`

이후 올려진 PR가 리뷰 끝에 approve 된다면 PR을 close하면 된다. (이미 Try PR로 병합되었기 때문)

## Refactor PR

기능은 변함 없으나 파일명 변경, 파일 위치 변경, 함수 추출, 함수명 변경 등 수정 사항이 생겼을때 올린다.

- `Refactor: {PR제목}`

## Chore PR

문서 작성 PR이다.

- `Chore: {PR제목}`


## PR 양식

규칙적인 PR을 위해 양식을 통일한다.

현재 근무 중인 직장에서 활용 중인 템플릿으로 간단하지만 꽤 효과 있는 양식이다.

```
## Updates <!-- 추가 되거나 바뀐 내용 -->

- blah
- blah

## Fixes <!-- 고쳐진 오류들 -->

## Others <!-- 기타 변경점들 (기능에 직접적인 연관이 없는 chore, style 등) -->

## Notes <!-- 리뷰어에게 알려줄 내용이나 PR에 히스토리로 남기고 싶은 내용들 -->

## Captures <!-- 캡쳐된 스크린샷이나 영상들 -->

## Refs <!-- 연관된 이슈나 PR 주소들 -->

```

모두 적을 필요는 없다.

```
## Updates <!-- 추가 되거나 바뀐 내용 -->

- 유저 로그인 기능을 추가합니다.
	- React-google-login 라이브러리 설치


## Notes <!-- 리뷰어에게 알려줄 내용이나 PR에 히스토리로 남기고 싶은 내용들 -->

- 로그인 관련 리덕스를 작성했는데 관심사 분리나.. 변수명?들 잘 작성했는지 의견 한번만 부탁드립니다 ㅎㅎ
```