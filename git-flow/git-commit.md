# git commit

커밋은 작업의 최소 단위로 어떤 히스토리로 작업을 진행하는 지 추척할 수 있다.

커밋의 컨벤션을 꼭 지킬 필요는 없으나, 지킨다면 자신이 작업한 히스토리를 쉽게 파악하여 `Rebase`나 `Reset`이 필요할 때 용이하게 사용 가능하다.

또한 리뷰 시 커밋 단위로 작업 이력을 볼 수 있기 때문에 리뷰할 때 역시 용이할 수 있다.

## 커밋명

일반적으로 `{카테고리}: {커밋명}`과 같이 커밋 한다.

본문, 푸터를 사용하는 경우는 극히 드물기 때문에 컨벤션으로 지정하지 않는다.


| type | description |
| :--- | :---------- |
| feat | 기능 추가 및 변경 |
| fix | 버그 수정 |
| refactor | 기존 기능 리팩터링 |
| test | 각종 테스트. unit/visual/e2e 에 해당됨.<br />테스트에 사용된 fixture 나 mocking 포함. |
| style | eslint 나 convention 에 따른 코딩 스타일 변경<br />(css 변경건을 말하는게 아님!) |
| docs | README.md 나 라이브러리 및 코드 문서화.<br/>기타 현재 프로젝트에 대한 각종 문서화에 해당. |
| chore | 기타 잡다한 변경<br />ex: 버전업, 패키지 추가/변경, 환경설정 변경, ci 수정, snippets 추가 등 |

### Examples

```
feat: 로그인 화면에 email 유효성 검증 기능 추가

fix: 회원 가입 시 발생된 토큰 오류 수정

refactor: 상품 검색 목록의 중복된 코드 제거

docs: README.md 의 빌드 내용 보완

test: 주문서에 cypress 를 이용한 e2e 테스트 코드 추가

chore: package.json 내 버전업

chore: tsconfig 및 eslint 내용 업데이트
```
