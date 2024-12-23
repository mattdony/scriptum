> Flexbox보다 행과 열을 더 정교하게 배치할 수 있으며, 레이아웃을 구축하는데 있어 CSS의 핵심이다.

### Columns and Rows
- 원하는 크기를 선언하는 것만으로 기본 레이아웃(행과 열)을 설정할 수 있다.
	- `grid-template-columns`: 열의 갯수와 크기를 설정
	- `grid-template-rows`: 행의 갯수와 크기를 설정
- 예시 (2 x 3 크기의 레이아웃 설정)
	```css
	/* style.css */
	.parents {
		display: grid;
		grid-template-columns: 100px 200px 50px;
		grid-template-rows: 200px 100px;
		gap: 10px;
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
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
	![[CSS Layout Masterclass/assets/grid_fig01.png]]
	- Grid 경우 사용자가 선언한 행과 열을 구분하기 위한 구분선이 생기며, 구분선에는 번호가 부여된다.
		- 열(column) 라인: ➡️ (왼쪽 > 오른쪽) 방향으로 1부터 시작해 1씩 증가하는 오름차순의 라인번호를 갖게됨
		- 행(row) 라인: ⬇️ (위 > 아래) 방향으로 1부터 시작해 1씩 증가하는 오름차순의 라인번호를 갖게됨
		- 열(column) 라인 역방향: ⬅️ (오른쪽 > 왼쪽) 방향으로 -1부터 시작해 1씩 감소하는 내림차순의 라인번호를 갖게됨
		- 행(row) 라인 역방향: ⬆️ (아래 > 위) 방향으로 -1부터 시작해 1씩 감소하는 내림차순의 라인번호를 갖게됨

<br>

### Grid Lines
- Grid를 통해 그려지는 요소들은 기본적으로 (1 x 1)의 크기로 순서대로 배치되지만 grid line을 활용해 속성을 활용해 손쉽게 원하는 크기와 위치에 배치시킬 수 있다.
- 다음의 속성을 자식 요소에 선언해 배치를 설정한다.
	- `gird-column-start`: 해당 요소의 열 시작 번호 입력
	- `gird-column-end`: 해당 요소의 열 끝 번호 입력
	- `grid-column`: 해당 요소의 열 시작, 끝 번호 입력
	- `gird-row-start`: 헤당 요소의 행 시작 번호 입력
	- `gird-row-end`: 해당 요소의 행 끝 번호 입력
	- `grid-row`: 해당 요소의 행 시작, 끝 번호 입력
- 번호는 방향에 따라 음수와 양수 두 개의 번호를 갖는다.
	```css
	/* style.css */
	.parents {
		display: grid;
		grid-template-columns: 100px 200px 50px;
		grid-template-rows: 200px 100px;
		gap: 10px;
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}

	.child:first-child {
		grid-row-start: 1;
		grid-row-end: -1;
		/* grid-row: 1 / -1; 위의 두 줄과 같은 기능 */
	}

	.child:last-child {
		grid-column-start: 2;
		grid-column-end: 4;
		/* grid-column: 2 / 4; 위의 두 줄과 같은 기능 */
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
	![[CSS Layout Masterclass/assets/grid_fig02.png]]

<br>

### Line Names
- Grid 라인은 기본적으로 라인 번호를 갖지만 특정 이름을 지정해 줄 수 도 있다.
	```css
	/* style.css */
	.parents {
		display: grid;
		grid-template-columns: [apple] 100px [banana] 200px [grape] 50px [melon];
		grid-template-rows: [kor] 200px [jap] 100px [chn];
		gap: 10px;
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}

	.child:first-child {
		grid-row: kor / chn;
	}

	.child:last-child {
		grid-column: banana / melon;
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
	![[CSS Layout Masterclass/assets/grid_fig03.png]]

<br>

### Grid Template
- `grid-template-columns`, `grid-template-rows`를 통해 전체 레아웃을 구성한 후 `grid-template-areas` 로 공간에 대한 이름을 설정하고, `grid-area`를 통해 공간을 바인딩 할 수 있다.
- `gird-template` = `gird-template-columns` + `grid-template-rows` + `grid-template-areas`
	```css
	/* style.css */
	body {
		margin: 0;
		padding: 0;
	
		display: grid;
		/* 넓이는 뷰포트를 기본값으로 갖는다. */
		grid-template-columns: 1fr 2fr 1fr 1fr;
		/* 높이는 기본값이 0이므로 크기를 설정해줘야 한다. */
		height: 100vh;
		grid-template-rows: 1fr 1fr 1fr 1fr;
		grid-template-areas:
			"header header header header"
			"content content content menu"
			"content content content menu"
			"footer footer footer footer";
		/* 아래와 같이 grid-template 속성을 사용해 columns, rows, areas 를 한번에 설정할 수 있다. */
		/* grid-template:
			"header header header header" 1fr
			"content content content menu" 1fr
			"content content content menu" 1fr
			"footer footer footer footer" 1fr / 1fr 2fr 1fr 1fr; */
	}
	

	header {
		background-color: aqua;
		grid-area: header;
	}
	
	section {
		background-color: coral;
		grid-area: content;
	}
	
	aside {
		background-color: forestgreen;
		grid-area: menu;
	}
	
	footer {
		background-color: deeppink;
		grid-area: footer;
	}
	```

	```html
	<!-- index.html -->
	<body>
		<header></header>
		<section></section>
		<aside></aside>
		<footer></footer>
	</body>
	```
	![[CSS Layout Masterclass/assets/grid_fig04.png]]

<br>

### Span Keyword
- Gird 라인 넘버나 이름으로 크기를 정하지 않고, 단순히 n개의 칸을 차지하게 싶을 때 `span` 키워드를 사용해 설정할 수 있다.
	```css
	/* style.css */
	.parents {
		display: grid;
		grid-template-columns: 100px 200px 50px ;
		grid-template-rows: 200px 100px;
		gap: 10px;
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}

	.child:first-child {
		background-color: khaki;
		grid-row: span 2;
	}

	.child:last-child {
		grid-column: span 2;
		/* 아래와 같이 시작라인과 함께 사용할 수도 있음 */
		/* grid-column: 2 / span 2; */
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
	![[CSS Layout Masterclass/assets/grid_fig05.png]]

<br>

### Auto Columns and Rows
- 예상한 Grid 레이아웃의 크기를 벗어나는 요소에 대해 설정하는 속성이다.
- Gird 레이아웃의 예상되는 크기를 벗어나는 속성에 대해서는 기본적으로 행(row)으로 추가되며 이는 `gird-auto-flow`의 기본값이 `row`임을 의미한다.
	- `gird-auto-rows` 속성을 통해 새롭게 추가되는 요소들의 행의 크기를 조절할 수 있다.
	- `gird-auto-columns` 속성을 통해 새롭게 추가되는 요소들의 열의 크기를 조절할 수 있다.
	```css
	/* style.css */
	.parents {
		display: grid;
		/* "repeat(2, 1fr)" -> "1fr 1fr" 과 같은 의미 */
		grid-template-columns: repeat(2, 1fr);
		grid-template-rows: repeat(2, 1fr);
		gap: 10px;
		grid-auto-flow: column;
		grid-auto-columns: 0.5fr;
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
		<div class="child">4</div>
		<div class="child">5</div>
		<div class="child">6</div>
		<div class="child">7</div>
		<div class="child">8</div>
		<div class="child">9</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/grid_fig06.png]]
	- (2 x 2) 를 예상하고 만들었지만, 더 늘어나는 속성에 대해 컬럼으로 채워지면서 0.5fr의 크기를 갖도록 설정

<br>

### Align and Justify Items
> - [*] 부모 요소에서 설정하는 row, column 의 크기가 자식 요소의 크기와 항상 같지는 않다.(다만, 자식 요소의 높이와 넓이를 별로도 지정해주지 않으면, 자식요소의 크기는 부모요소에서 선언한 셀의 크기와 같은 기본값을 갖는다.)
- 설계한 개별의 공간(셀) 안에 요소를 배치하기 위한 속성이다.
- 부모에서 요소를 설정해 자식 요소 전체가 배치되게 하는 속성이다.
	- `justify-items`: 가로 방향으로 자식 요소의 위치를 특정한다.
	- `align-items`: 세로 방향으로 자식 요소의 위치를 특정한다.
	- `place-items`: `align-items` + `justify-items`
- 자식 요소 개별로 선언해 해당 요소의 위치만 특정한다.
	- `justify-self`: 가로 방향의 자신의 위치를 특정한다.
	- `align-self`: 세로 방향으로 자신의 위치를 특정한다.
	- `place-self`: `align-self` + `justify-self`
	```css
	/* style.css */
	.parents {
		display: grid;
		/* "repeat(2, 1fr)" -> "1fr 1fr" 과 같은 의미 */
		grid-template-columns: repeat(2, 1fr);
		grid-template-rows: repeat(2, 1fr);
		gap: 10px;
		grid-auto-flow: column;
		grid-auto-columns: 1fr;
		align-items: end;
		justify-items: start;
		/* 위의 두 줄과 같은 기능 */
		/* place-items: end start; */
	}

	.child {
		width: 50px;
		height: 50px;
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}

	.child:nth-child(6) {
		background-color: forestgreen;
		grid-column: span 2;
		/* align-self: center;
		justify-self: center; */
		/* 위의 두 줄과 같은 기능 */
		place-self: center;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
		<div class="child">4</div>
		<div class="child">5</div>
		<div class="child">6</div>
		<div class="child">7</div>
		<div class="child">8</div>
		<div class="child">9</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/grid_fig07.png]]

<br>

### Align and Justify Content
- 셀 자체를 배치하기 위한 속성이다.
	- `justify-content`: 가로 방향으로 셀 배치를 설정한다.
	- `align-content`: 세로 방향으로 셀 배치를 설정한다.
	- `place-content`: `align-content` + `justify-content`
- 셀 배치를 위해서는 여분의 공간을 필요로 한다.
	```css
	/* style.css */
	.parents {
		display: grid;
		height: 100vh;
		grid-template-columns: repeat(3, 100px);
		grid-template-rows: repeat(2, 100px);
		gap: 10px;
		grid-auto-flow: column;
		grid-auto-columns: 1fr;
		align-content: center;
		justify-content: space-between;
		/* 위의 두 줄과 같은 기능 */
		/* place-content: center space-between; */
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
		<div class="child">4</div>
		<div class="child">5</div>
		<div class="child">6</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/grid_fig08.png]]

<br>

### Auto Sizing and Minmax
- 내용물의 크기에 따라 자동으로 크기를 설정해주는 키워드이다.
	- `max-content`: 해당 셀의 자식요소 길이 만큼을 셀의 넓이로 한다. 
	- `min-content`: 해당 셀의 자식요소가 가질 수 있는 최소한의 넓이 만큼을 셀의 넓이로 한다.
	- `minmax([min], [max])`: 해당 셀이 가질 수 있는 최소, 최대의 크기를 설정한다.
	```css
	/* style.css */
	.parents {
		display: grid;
		height: 100vh;
		gap: 10px;
		grid-template-columns: max-content min-content minmax(300px, 1fr);
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">-=- maxcontent -=-</div>
		<div class="child">-=- mincontent -=-</div>
		<div class="child">1fr</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/grid_fig09.png]]

<br>

### Auto Fill and Auto Fit
- 반응형 그리드로 만들어주는 속성이다.
	- `auto-fill`: 사용자 설정에 따라 셀을 최대한 많이 생성해 자동으로 배치하는 키워드이다.
	- `auto-fit`: 사용자 설정에 따라 셀을 최대한 많이 생성해 자동으로 배치하되, 비어 있는 셀은 병합시키는 키워드이다.
	```css
	/* style.css */
	.parents {
		display: grid;
		height: 100vh;
		gap: 10px;
		grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
		/* grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); */
	}

	.child {
		background-color: tomato;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		font-size: 30px;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1fr</div>
		<div class="child">1fr</div>
		<div class="child">1fr</div>
	</div>
	```
	![[CSS Layout Masterclass/assets/grid_fig10.png]]

<br>

> [!TIP] Grid 연습 게임
> - Grid Garden ([https://cssgridgarden.com/#ko](https://cssgridgarden.com/#ko))

