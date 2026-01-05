## 타입 변환이란?

- 명시적 타입 변환(타입 캐스팅): 개발자가 의도적으로 타입을 변환
- 암묵적 타입 변환: 자바스크립트 엔진에 의해 표현식을 평가하는 도중에 암묵적으로 값의 타입이 자동 변환
- 타입 변환은 기존 원시 값을 직접 변경하는 것이 아닌 다른 타입의 새로운 원시 값을 생성하는 것

## 암묵적 타입 변환

### 문자열 타입으로 변환

- - 연산자는 피연산자 중 하나 이상이 문자열이면 문자열로 암묵적 타입 변환함

    ```jsx
    1 + "2"; // -> "12"
    ```
- ES6 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환함
  ```jsx
  `1 + 1 = ${1 + 1}`; // "1 + 1 = 2"
  ```

### 숫자 타입으로 변환

- 산술 연산자의 역할은 숫자 값을 만드는 것으로, 모든 피연산자는 코드 문맥상 모두 숫자타입이어야 함
  ```jsx
  1 - "1"; // -> 0
  1 * 10; // -> 10
  1 / "one"; // NaN
  ```
- 비교 연산자의 역할은 불리언 값을 만드는 것으로, 피연산자를 비교하므로 코드의 문맥상 모두 숫자 타입이어야 함
  ```jsx
  "1" > 0; // -> true
  ```
- 숫자 타입이어야 하는데 숫자 타입으로 변환할 수 없는 경우는 평과 결과가 NaN 이 됨

### 불리언 타입으로 변환

- 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환함
- 자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy값(참으로 평가되는 값) 또는 Falsy(거짓으로 평가되는 값)값으로 구분함
- 다음의 falsy 값 외의 모든 값은 모두 true로 평가되는 Truthy값이다.
  - false
  - undefined
  - null
  - 0, -0
  - NaN
  - ''(빈 문자열)

## 명시적 타입 변환

- 표준 빌트인 생성자 함수를 new 연산자 없이 호출
- 빌트인 메서드 사용
- 암묵적 타입 변환 사용

### 문자열 타입으로 변환

1. String 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototypee.toString 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

### 숫자 타입으로 변환

1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. `parseInt`, `parseFloat` 함수를 사용하는 방법
3. - 단항 산술 연산자를 이용하는 방법
4. - 산술 연산자를 이용하는 방법

### 불리언 타입으로 변환

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. !부정 논리 연산자를 두 번 사용(`!!`)하는 방법

## 단축 평가

### 논리연산자를 사용한 단축 평가

- 논리합 또는 논리곱 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가되는데, 논리 연산자 표현식의 평가 결과는 불리언 값이 아닐 수 있음
- 논리곱 (`&&`) 연산자
  ```jsx
  "cat" && "dog"; // -> "dog"
  ```
  논리곱 연산자는 두 개의 피연산자가 모두 true 평가될 때만 true를 반환
  좌항에서 우항으로 평가가 진행됨 → 두 번째 피연산자가 위 논리곱 연산자 표현식의 평가 결과를 결정
- 논리합 (`||`) 연산자
  ```jsx
  "cat" || "dog"; // -> "cat"
  ```
  논리합 연산자 역시 좌항에서 우항으로 평가가 진행
  → 논리합 연산자는 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환하여, 두 번째 피연산자까지 평가해 보지 않아도 표현식을 평가할 수 있음
  → 'cat'을 반환한다.
- 단축 평가: 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는 것
- 단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략함
- If 문을 대체 하는 방법
  ```jsx
  var done = true;
  ver message = '';

  //if (done) message = '완료';
  message = done && '완료'
  //if (!done) message = '미완료';
  message = done || '미완료'
  ```
  1. 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

     ```jsx
     var elem = null;
     var value = elem.value; // TypeError: Cannot read property 'value' of null
     ```

     객체를 기대하는 변수 값이 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입에러가 발생.

  2. 함수 매개변수에 기본값을 설정할 때
  ```jsx
  // 단축 평가를 사용한 매개변수의 기본값 설정
  function getStringLength(str) {
    str = str || "";
    return str.length;
  }

  getStringLength(); // -> 0
  getStringLength("hi"); // -> 2

  // ES6의 매개변수의 기본값 설정

  function getStringLength(str = "") {
    return str.length;
  }

  getStringLength(); // -> 0
  getStringlength("hi"); // -> 2
  ```
  함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당 → 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있음

### 옵셔널 체이닝 연산자

- ES11(ECMAScript2020)에서 도입된 옵셔널 체이닝 연산자 `?.`는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어감
  이는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용
  ```jsx
  var elem = null;

  var value = elem?.value;
  console.log(value); // undefined
  ```
- 옵셔널 체이닝 연산자는 좌항 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN, ‘’)이라도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어감
  ```jsx
  .var str = '';

  var length = str?.length;
  console.log(length); // 0
  ```

### null 병합 연산자

- ES11(ECMAScript2020)에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환
- null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용
  ```jsx
  var foo = null ?? "default string";
  console.log(foo); // default string
  ```
  null 병합 연산자는 좌항의 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN, ‘’)이라도 null 또는 undefined가 아니면 좌항의 피연산자를 그대로 반환
