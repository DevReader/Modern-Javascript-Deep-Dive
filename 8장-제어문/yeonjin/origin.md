## [8장 - 제어문]

제어문은 코드의 흐름을 이해하기 어렵게 만들어 `가독성을 해치는 단점이 있다.`

`forEach, map, filter, reduce 같은 고차 함수`를 사용한 함수형 프로그래밍 기법에서는 제어문의 사용을 억제하여 복잡성을 해결하려고 노력한다.

### 8.1 블록문

0개 이상의 문을 중괄호로 묶은 것, 코드 블록 또는 블록이라고 부름.

자바스크립트는 블록문을 하나의 실행 단위로 취급함.

```jsx
// 블록문
{
  var foo = 10;
}

// 제어문
var x = 1;
if (x < 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}
```

### 8.2 조건문

주어진 조건식의 평가 결과에 따라 코드 블록의 실행을 결정

1. if else문 `(if, else if, else)`
2. switch문
   1. 폴스루

```jsx
switch (표현식) {
  case 표현식1:
    switch문의 표현식과 표현식1이 일치하면 실행될 문;
	  **break;**
  case 표현식2:
    switch문의 표현식과 표현식2가 일치하면 실행될 문;
	  break;
  default:
	  switch문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

### 8.3 반복문

1. for문

```jsx
for (var i = 0; i < 2; i++) {
  console.log(i);
}
```

1. while 문

```jsx
var count = 0;

while (count < 3) {
  console.log(count);
  count++;
}
```

1. do while 문

```jsx
var count = 0;

do {
  console.log(count);
  count++;
} while (count < 3);
```

### 8.4 break 문

레이블 문, 반복문, switch 문의 코드 블록을 탈출한다.

이 블록 외에서 break 문을 사용하면 SyntaxError가 발생한다.

### 8.5 continue 문

반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
