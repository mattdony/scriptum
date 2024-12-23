> CSS의 display 속성의 `inline`, `block`, `inline-block` 에 대한 사전지식이 있을 경우 이해가 수월할 수 있음
### Flexbox를 사용하는 이유
- 레이아웃을 구성하는데 있어 flexbox를 사용하지 않고 요소들을 특정 위치에 배치하기 위해선, 각각의 요소에 대해 브라우저의 크기를 고려해 위치값들을 직접 계산해서 입력해줘야 하며, 브라우저의 크기가 바뀔 때마다 새롭게 계산하고 수정해줘야 한다.
- Flexbox는 레이아웃을 구성하는 요소들 각각에 하나하나 값을 지정하는 방식인 **명령형**의 불편함을 해소하기 위해, **선언형**으로 요소들이 위치해야할 곳을 기술함으로서 요소들의 위치 값을 브라우저가 크기에 따라 동적으로 계산한다.

<br>

### Flexbox의 사용하기
- 일반적으로 표현할 요소의 부모요소에 표현방식(속성)을 선언한다. 
	- 자식요소들에 사용하는 속성도 있음(`order`, `align-self`, 등등등)
	```css
	/* style.css */
	.parents {
		display: flex; /* flexbox 설정 */
		gap: 10px; /* 자식요소들 간의 간격을 부모요소에 설정*/
	}

	.child {
		width: 100px;
		height: 100px;
		background-color: orange;
	}
	```

	```html
	<!-- index.html -->
	<head>
		<link rel="stylesheet" href="style.css" />
	</head>

	<body>
		<div class="parents">
			<div class="child"></div>
			<div class="child"></div>
			<div class="child"></div>
		</div>
	</body>
	```

<br>

### flex-direction
>- [*] Flexbox의 축(axis) 개념 (매우 중요한 개념 반드시 암기)
- Flexbox에는 주축(main axis)과 교차축(cross axis) 두 가지 축이 있으며, 축의 방향에 따라 요소들이 배치된다.

- **주축(Main Axis)**
	- `flex-direction` 으로 **주축의 방향을 설정**할 수 있으며 기본값은 `row` 이다.
		```css
		.parents {
			display: flex;
			/* flex-direction: row; 기본값 */
		}
		```
	- `flex-direction` 값에 따라 주축은 네 가지 방향을 갖는다.
		- `row`: ➡️ (왼쪽 > 오른쪽)
		- `row-reverse`: ⬅️ (오른쪽 > 왼쪽)
		- `column`: ⬇️ (위 > 아래)
		- `column-reverse`: ⬆️ (아래 > 위)
	- `justify-content` 속성을 통해 주축방향으로 요소들이 어떻게 배치될 것인지 설정 할 수 있다.

- **교차축(Cross Axis)**
	- 주축과 수직을 이루며 `flex-direction` 을 통해 주축을 설정하면 수직방향으로 별도의 선언 없이 자동으로 교차축이 설정된다.
	- `flex-direction` 에 따라 교차축은 두 가지 방향을 갖는다.
		- `row`, `row-reverse` : ⬇️ (위 > 아래)
		- `column`, `column-reverse`: ➡️ (왼쪽 > 오른쪽)
	- `align-items` 속성을 통해 교차축방향으로 요소들이 어떻게 배치될 것인지 설정 할 수 있다.
- 예시
	```css
	/* sytle.css */
	.parents {
		height: 300px;
		display: flex;
		flex-direction: row-reverse;
		justify-content: space-around;
		align-items: center;
	}
	
	.child {
		width: 100px;
		height: 100px;
		background-color: purple;

		/* 숫자를 가운데 표시하기 위한 속성 */
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 50px;
		color: whitesmoke;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
		<div class="child">4</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/flexbox_fig01.png]]

<br>

### flex-wrap
> Flexbox 안의 자식요소들에 대해 다중라인 여부를 결정
- **한 줄로 표시(Single Line)**
	- `flex-wrap`의 기본값은 `nowrap` 으로, 자식 요소들을 한 줄로 표현한다.
	- 자식 요소들의 총 넓이(width)가 부모인 flexbox의 넓이보다 큰 경우, 자식요소의 넓이가 축소된다.
	- 예시
		```css
		/* sytle.css */
		.parents {
			display: flex;
			/* flex-wrap: nowrap; 기본값*/
			gap: 10px;
		}
		
		.child {
			width: 100px;
			height: 100px;
			background-color: purple;
	
			/* 숫자를 가운데 표시하기 위한 속성 */
			display: flex;
			justify-content: center;
			align-items: center;
			font-size: 50px;
			color: whitesmoke;
		}
		```

		```html
		<!-- index.html -->
		<div class="parents">
			<div class="child">1</div>
			<div class="child">2</div>
			...
			<div class="child">14</div>
			<div class="child">15</div>
		</div>
		```
		![[CSS Layout Masterclass/assets/flexbox_fig02.png]]

- **여러 줄로 표시(Multi Line)**
	- `felx-wrap`의 속성을 `wrap`으로 할 경우 자식 요소들의 길이에 맞춰 여러줄로 나타낸다.
	- 예시
		```css
		/* sytle.css */
		.parents {
			display: flex;
			felx-wrap: wrap;
			gap: 10px;
		}
		```

		```html
		<!-- index.html -->
		<div class="parents">
			<div class="child">1</div>
			<div class="child">2</div>
			...
			<div class="child">14</div>
			<div class="child">15</div>
		</div>
		```
		![[CSS Layout Masterclass/assets/flexbox_fig03.png]]
	- `wrap-reverse`의 경우 마지막줄부터 표시된다.
		![[CSS Layout Masterclass/assets/flexbox_fig04.png]]

<br>

### align-content
> Flexbox로 자식요소를 여러 줄로 나타낼 때 자식 요소들 간의 배치 형태를 결정
- `align-content`는 자식요소가 여러 줄인 경우에만 동작한다.
- `align-content`는 교차축을 기준으로 자식 요소들을 배치하며, 주축을 기준으로 자식 요소를 배치하는 `justify-content`의 유사하다.
- align-items 와 align-content 비교 예시
	- `align-items: flex-end` vs `align-content: flex-end`
	![[CSS Layout Masterclass/assets/flexbox_fig05.png]]
	- 양쪽 모두 `flex-direction: row;`이며, 같은 `height`와 `gap` 을 적용
	- `align-items`의 경우 자식요소 전체를 교차축의 끝방향으로 배치시키지만, `height`값으로 줄 간격을 자동으로 계산해 지정한 `gap` 보다 더 많이 벌어진다. (부모 flexbox의 높이 값이 클수록 줄 간격도 커진다.)
	- `align-content`의 경우 지정한 `gap`을 유지하며 자식 요소 전체를 교차축의 끝방향으로 배치시킨다. (부모 flexbox의 높이 값에 상관없이 자식요소들의 줄간격이 유지된다.)

<br>

### flex-flow
> `flex-direction`과 `flex-wrap`을 한 번에 사용할 수 있는 속성
- `flex-direction` 속성의 값(`row`, `row-reverse`, `column`, `column-reverse`)과 `flex-wrap` 속성의 값(`nowrap`, `wrap`, `wrap-reverse`)들을 모두 사용할 수 있다.
- `flex-direction`과 `flex-wrap`의 속성 중 하나 또는 두 속성을 한번에 정해줄 수 있다. (속성 값의 순서는 상관없음)
- 예시
	```css
	/* style.css */
	.parents {
		display: felx;
		
		/* flex-direction: column; 과 같은 기능*/
		flex-flow: column;
	}
	```

	```css
	/* style.css */
	.parents {
		display: flex;
		
		/* flex-direction: column; */
		/* flex-wrap: wrap; */
		flex-flow: column wrap; /* 위의 두 줄과 같은 기능 */
	}
	```

<br>

### 자식요소에 적용하는 속성
#### order
> Flexbox 안의 자식요소들의 순서를 결정
- 모든 자식 요소는 기본적으로 `order: 0;`을 기본값으로 갖는다.
- `order`에 정수(음수, 0, 양수)를 입력하면 오름차순으로 자식 요소들이 정렬된다.
- 예시
	```css
	/* style.css */
	.parents {
		display: flex;
		gap: 10px;
	}
	
	.child {
		width: 100px;
		height: 100px;
		background-color: purple;		
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 50px;
		color: whitesmoke;
	}
		
	.child:nth-child(2) {
		background-color: skyblue;
		order: 3;
	}
		
	.child:nth-child(4) {
		background-color: tomato;
		order: -8;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>  <!-- order: 0 -->
		<div class="child">2</div>  <!-- order: 3 -->
		<div class="child">3</div>  <!-- order: 0 -->
		<div class="child">4</div>  <!-- order: -8 -->
		<div class="child">5</div>  <!-- order: 0 -->
	</div>
	```
	![[CSS Layout Masterclass/assets/flexbox_fig06.png]]
	- `order` 값의 오름차순(-8, 0, 0, 0, 3)으로 요소가 정렬된다.


<Br>

#### align-self
> 교차축으로 방향으로 자식요소 개별의 위치를 결정
- 예시
	```css
	/* style.css */
	.parents {
		display: felx;
		gap: 10px;
		height: 300px;
	}

	.child {
		width: 100px;
		height: 100px;
		background-color: purple;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 50px;
		color: whitesmoke;
	}
	
	.child:first-child {
		align-self: flex-start;
	}
	
	.child:last-child {
		align-self: flex-end;
	}

	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/flexbox_fig07.png]]

<br>

#### flex-grow
> 화면의 비율에 따라 너비가 얼마나 커져야 할지 정해주는 속성
- Flexbox의 자식요소들에 대해 넓이 값을 정해주지 않으면 기본적으로 자식요소가 가지고 있는 컨텐츠의 넓이를 기본 크기로 한다.
- 각각의 자식요소는 `flex-grow` 속성을 통해 형제 속성들과 비교해 얼마만큼의 너비를 차지할지 비율로 설정하며, 기본값은 0이다.
- 예시
	```css
	/* style.css */
	.parents {
		height: 300px;
		display: felx;
	}

	.child {
		height: 200px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 50px;
		color: whitesmoke;
	}
	
	.child:first-child {
		background-color: tomaot;
		flex-grow: 1.5;
	}
	
	.child:last-child {
		background-color: teal;
		flex-grow: 1;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/flexbox_fig08.png]]

<br>

#### flex-shrink
> 화면의 비율에 따라 너비가 얼마나 작아져야 할지 정해주는 속성

- `flex-shrink`는 flexbox의 자식요소들이 화면의 넓이에 따라 얼마만큼 줄어들지를 결정하는 속성으로, `flex-grow`와 반대된다.
- `flex-shrink`의 기본값은 1이며 값이 커질수로 더 빠르게 줄어든다. 0으로 설정한 경우 자식 요소의 기본 넓이 이하로 줄어들지 않는다. (기본 크기를 특별히 설정하지 않은 경우 자식요소의 컨텐츠의 넓이를 기본 크기로 갖는다.)
- `flex-shrink` 값에 상관 없이 먼저 각각의 자식요소가 가지고 있는 기본 크기 이상의 값들을 먼저 축소하며, 모든 자식 요소가 기본 크기만 남겨둔 상태에서 더 축소돼야 할 때 `flex-shrink` 값의 비율로 줄어든다.
- 예시
	```css
	/* style.css */
	.parents {
		height: 300px;
		display: felx;
	}

	.child {
		height: 200px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 30px;
		color: whitesmoke;
	}
	
	.child:first-child {
		backgroud-color: tomaot;
		flex-grow: 1;
		flex-shrink: 3;
	}

	.child:nth-child(2) {
		backgroud-color: orange;
		flex-grow: 3;
		flex-shrink: 0;
	}

	.child:last-child {
		backgroud-color: teal;
		flex-grow: 2;
		flex-shrink: 1;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">Flex-Shrink Test Box</div>
		<div class="child">Flex-Shrink Test Box</div>
		<div class="child">Flex-Shrink Test Box</div>
	</div>
	```

	![[CSS Layout Masterclass/assets/flexbox_fig09.png]]
	- 결과 화면의 너비: 1388px
	- 화면의 크기가 충분히 큰 경우 `flex-grow`의 비율(1:3:2)에 따라 자식요소가 너비를 갖는다.

	![[CSS Layout Masterclass/assets/flexbox_fig10.png]]
	- 결과 화면의 너비: 796px
	- 화면의 크기가 줄어듬에 따라 자식 요소들에서 컨텐츠의 여백이 먼저 줄어든다.

	![[CSS Layout Masterclass/assets/flexbox_fig11.png]]
	- 결과 화면의 너비: 556px
	- 모든 여백이 사라진 이후에도 화면이 계속해서 줄어들 경우 `flex-shrink`의 비율(3:0:1)에 따라 화면의 크기가 줄어든다.
	  (숫자가 클수록 빨리 축소되며, 0 인 경우 기본 크기 이하로 줄어들지 않는다.)

<br>

#### flex-basis
> 해당 요소의 시작 크기를 설정하는 속성
- Flexbox의 자식 요소들은 기본적으로 컨텐츠의 너비를 기본 크기로 갖지만, flex-basis를 통해 원하는 값으로 지정해 줄 수 있다.
- `flex-basis` 주축(main-axsis)에 따라 너비가 아닌 높이의 기본 크기를 지정할 수도 있다. (부모의 `flex-direction: column;` 인 경우)
- 예시
	```css
	/* style.css */
	.parents {
		height: 250px;
		display: felx;
	}

	.child {
		height: 200px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 30px;
		color: whitesmoke;
	}
	
	.group1:first-child {
		background-color: tomaot;
		flex-grow: 1;
	}

	.group1:last-child {
		background-color: teal;
		flex-grow: 1;
	}

	.group2:first-child {
		background-color: tomaot;
		flex-grow: 1;
		flex-basis: 500px;
	}

	.group2:last-child {
		background-color: teal;
		flex-grow: 1;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child group1">Flex-Basis Test Box</div>
		<div class="child group1">Flex-Basis Test Box</div>
	</div>
	<div class="parents">
		<div class="child group2">Flex-Basis Test Box</div>
		<div class="child group2">Flex-Basis Test Box</div>
	</div>
	```

	![[CSS Layout Masterclass/assets/flexbox_fig12.png]]
	- 첫번째 flexbox의 자식 요소들은 같은 컨텐츠와 `flex-grow`값을 가지며 기본 크기를 조정하지 않았기에 차지하는 너비가 같다.
		- `group1`의 기본 넓이(컨텐츠 크기)
			- (tomato, teal) = (244.46px, 244.46px)
		- `group1`의 커진 이후 넓이
			- (tomato, teal) = (686px, 686px)
		- `group1`의 늘어난 크기
			- (tomato, teal) = (441.54px, 441.54px)
	- 두번째 flexbox의 자식 요소들은 같은 컨텐츠와 `flex-grow`값을 갖지만, 첫번째 자식 요소는 본인의 컨텐츠 너비보다 더 큰 기본 크기(500px)를 지정해 주었기 때문에, 첫번째 자식이 차지하는 너비가 더 크다.
		- `group2`의 기본 넓이
			- (tomato, teal) = (500px, 244.46px)
		- `group2`의 커진 이후 넓이
			- (tomato, teal) = (813.77px, 558.23px)
		- `group2`의 늘어난 크기
			- (tomato, teal) = (313.77px, 313.77px)

> [!INFO] `flex-grow`, `flex-shrink`, `flex-basis` 속성 응용
> - 'min-width' or 'min-height' 구현
> 	- `flex-grow` > 0
> 	- `flex-shrink` = 0
> 	- `flex-basis` = (원하는 최소 크기)
> - 'max-width' or 'max-height' 구현
> 	- `flex-grow` = 0
> 	- `flex-shrink` > 0
> 	- `flex-basis` = (원하는 최대 크기)

<br>

#### flex
> `flex-grow`, `flex-shrink`, `flex-basis` 속성을 한 번에 사용할 수 있는 속성
- `flex`의 값으로 `flex-grow`, `flex-shrink`, `flex-basis` 순서대로 입력하셔 세 가지 속성을 한 번에 정의 할 수 있다.
- 예시
	```css
	/* style.css */
	.parents {
		height: 250px;
		display: felx;
	}

	.child {
		/* flex-grow: 1; */
		/* flex-shrink: 0; */
		/* flex-basis: 500px; */
		flex: 1 0 500px; /* 위의 세 줄과 같은 기능 */
	}
	```

<br>

> [!TIP] Flexbox 연습 게임
> - Flexbox Froggy ([https://flexboxfroggy.com/#ko](https://flexboxfroggy.com/#ko))

---
### 마무리
> [!SUMMARY] **Flexbox 요약**
> - 개념
> 	- Flexbox와 관련된 대부분의 속성은 부모요소에 선언형으로 작성한다. 
> 	- Flexbox는 주축(main-axsis)과 교차축(cross-axsis)이 있다.
> - 관련속성
> 	- `display: flex;` 해당요소를 flexbox로 선언
> 	- 부모요소에 선언하는 속성
> 		- `flex-direction`: 주축을 설정
> 		- `flex-wrap`:  자식요소를 한 줄 또는 여러 줄로 나타낼지 설정
> 		- `flex-flow`: `flex-direction` + `flex-wrap`
> 		- `justify-content`: 주축 빙향으로 자식요소들의 배치 설정
> 		- `align-items`: 줄 안에서 교차축 방향으로 자식요소들의 배치 설정(자식요소가 여러 줄인 경우 부모 요소의 교차축 크기를 고려해 한 줄의크기(=아이템)가 자동으로 결정)
> 		- `align-content`: 교차축 방향으로 자식요소들의 배치 설정(`flex-wrap: wrap;` 인 경우에만 적용됨)
> 	- 자식요소에 선언하는 속성
> 		- `order`: 해당 자식요소의 순서를 설정
> 		- `align-self`: 해당 자식요소의 교차축 방향에서의 위치를 설정
> 		- `flex-grow`: 해당 자식 요소의 주축으로 늘어나는 비율 설정
> 		- `flex-shrink`: 해당 자식 요소의 주축으로 줄어드는 비율 설정
> 		- `flex-basis`: 해당 자식요소의 기본 크기를 설정
> 		- `flex`: `flex-grow` + `flex-shrink` + `flex-basis`
