## [9장 - 타입 변환과 단축 평가]

### 9.1 타입 변환이란?

개발자가 의도적으로 값의 타입을 변환하는 것을 명시적 타입 변환 또는 타입 캐스팅이라 한다.

개발자 의도와 상관없이 표현식을 평가하는 도중에 암묵적으로 타입이 자동변환되는 것을 암묵적 타입 변환 또는 타입 강제 변환이라 한다.

### 9.2 암묵적 타입 변환

암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환함.

1. 문자열 타입으로 변환
   1. 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작 `1 + “2” → “12”`
2. 숫자 타입으로 변환
   1. 산술 연산자 표현식을 평가하기 위해 산술 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환. 숫자로 변환할 수 없는 경우 NaN 반환 `+”1” → 1`
3. 불리언 타입으로 변환
   1. if 문, for문, 제어문, 삼항 조건 연산자 조건식
   2. false로 평가되는 Falsy 값 - false, undefined, null, 0, -0, NaN, “”(빈문자열)

### 9.3 명시적 타입 변환

생성자 함수(String, Number, Boolean)을 new 연산자 없이 호출하는 방법, 빌트인 메서드를 사용하는 방법, 암묵적 변환 사용

1. 문자열 타입으로 변환
   1. String 생성자 함수를 new 연산자 없이 호출
   2. Object.prototype.toString 메서드 사용
   3. 문자열 연결 연산자를 사용하는 방법
2. 숫자 타입으로 변환
   1. Number 생성자 함수를 new 연산자 없이 호출
   2. parseInt, parseFloat 함수를 사용
   3. +단항 산술 연산자를 이용
   4. \*산술 연산자를 이용
3. 불리언 타입으로 변환
   1. Boolean 생성자 함수를 new 연산자 없이 호출
   2. !부정 논리 연산자를 두번 사용하는 방법
      1. ! 반대
      2. !! → 반대가 아니면서, true or false 값을 가질 수 있다.

### 9.4 단축 평가

단축평가: `표현식을 평가하는 도중에 평가 결과가 확정된 경우, 나머지 평가 과정을 생략하는 것을 말한다.`

1. 논리 연산자를 사용한 단축 평가
   1. 논리합 또는 논리곱 연산자의 표현식 평가 결과는 불리언 값이 아닐 수 있다.
   2. 2개의 피연산자 중 어느 한쪽으로 평가된다.
   3. true || anything ⇒ true
   4. false || anything ⇒ anything
   5. true && anything ⇒ anything
   6. false && anything ⇒ false

```jsx
message = done && "완료"; // done 이 true라면 message에 '완료'를 할당
```

- 객체를 가리키기를 기대하는 변수가 null or undefined가 아닌지 확인하고 프로퍼티를 참조할 때

```jsx
var elem = null;
var value = elem && elem.value;
```

- 함수 매개변수에 기본값을 설정할 때

```jsx
function getStringLength() {
  str = str || "";
  return str.length;
}
```

1. 옵셔널 체이닝 연산자

옵셔널 체이닝 연산자(?.)는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어감.

```jsx
var str = "";

var length = str?.length;

console.log(length); // 0
```

1. null 병합 연산자

null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.

변수에 기본값을 설정할 때 유용하다.

```jsx
var foo = null ?? "default string";
console.log(foo); // "default string"
```

++ 타입 변환도 기존의 원시값을 변경하는 게 아니라 새로운 타입의 원시값을 생성하는 것
