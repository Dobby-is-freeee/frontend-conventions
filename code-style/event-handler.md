# event-handler

DOM과의 상호작용을 하면서 event-handler(이하 핸들러)는 필수적인 요소이다. 그만큼 많이 다룬다.

그런데 생각보다 핸들러에 대하여 일괄되고 규칙적인 개념을 잡은 사람은 많지 않다.

때로는 유지 보수를 하기 위해 내가 아닌 다른 누군가가 작성한 핸들러 함수를 수정해야할 때가 있다.

이때 규칙 없이 무지성으로 작성되어 있다면 필히 어지러움을 느낄 것이다.

이 문서는 이러한 사항을 미연에 방지하고자 한다.

## `on-`, `handle-` prefix

핸들러는 일반적인 함수와는 다른 규칙을 적용한다. `on-` 또는 `handle-`로 시작하는 prefix를 갇도록 하자.

이벤트 핸들러와 일반 함수의 구분은 추후 유지보수면에서, 가독성면에서도 훨씬 효과적이다. 명시적으로 구분되기 때문이다.

일반적인 자바스크립트에서 둘 중 어느것을 쓰던 자유이지만, props로 관리하는 React의 경우 `handle-` prefix를 권장한다.

리액트는 다음과 같이 이벤트를 붙이게 되는데,

`onClick={onClick}`

중복되는 prefix가 이유이다.

#### Bad
```js
const deleteNotification = () => {
	// ...
}

<button type="button" onClick={deleteNotification}></button>
```

#### Good
```js
const handleNotificationDelete = () => {
	// ...	
}

<button type="button" onClick={handleNotificationDelete}></button>
```

마지막으로 이벤트 핸들러의 단어 순서는 명사(Notification)-동사(Delete)순으로 진행한다.

## 커링 활용

가끔씩 핸들러를 커링으로 활용할 경우가 생긴다. 가령 id를 넘겨줘야 하는 경우이다.

이때는 몇 가지 방법이 있겠지만, 대표적으로 두 가지가 있다.

첫째는 핸들러가 연결된 엘리먼트에 속성을 선언하여, 그 값을 핸들러 내에서 가져오는 것이다.

```js
const handleClick = (e) => {
	console.log(e.target.id);
	console.log(e.currentTarget.dataset.id);
}
```

이 방법도 좋은 방법이다. 또한 많이 사용하는 방식이므로 언급하지 않고 넘어가도록 한다.

두번째는 커링으로 인자를 넘겨주는 것이다.

```js
const handleClick = (id) => (e) => {
	console.log(id);
}
```

둘 중 어느 방법이 더 낫다고 할 수는 없겠으나, 이러한 방법도 있음을 숙지하자.

3. 인라인 핸들러는 작성 하지 않는다.

인라인 함수가 성능적으로 나쁘지 않을 수 있다는 글도 종종 보이나, 성능은 별개로 `인라인 함수`는 관심사 분리가 되어 있지 않은 설계임으로 지양한다.

인라인 핸들러를 작성하면 마크업 단계에 핸들러 함수가 들어가 있어 보기 싫을 뿐더러 수정하기 위해서는 마크업을 드려다 봐야 하는 불상사가 생긴다.


#### Bad

```js
<button id={id} onClick={(e) => {
	const { id } = e.target;

	// ...
	}}>
	클릭
</button>
```

#### Good

```js

const handleClick = () => {
	// ...
}

<button id={id} onClick={handleClick}>클릭</button>
```

4. Props로 넘기는 React handler

리액트에서는 자식 컴포넌트에게 handler를 넘길 수 있다.

이때 handler를 받은 자식 컴포넌트는 부모가 내려준 함수를 한 번 감싸준다.

```js
const Parent = () => {
	const handleClick = (id) => {
		console.log(id);
	}

	return <Child onClick={handleClick} />
}

const Child = ({onClick}) => {
	const handleClick = (e) => {
		const id = e.target.id;
		onClick(id);
	}

	return <button id={id} onClick={handleClick}>클릭</button>
}
```

굳이 한번 더 감싼 이유는

1. 부모가 핸들러로 활용하고자 하는 데이터 값만을 전달해 주기 위함이며
2. 이벤트를 발생시키는 쪽과 그것을 처리하는 곳을 명확히 구분하기 위함이다.

이때 추가로 기억해야 할 점은, 컴포넌트로 핸들러를 내릴 때에도 `on-` prefix를 통해 내린다는 점이다.
