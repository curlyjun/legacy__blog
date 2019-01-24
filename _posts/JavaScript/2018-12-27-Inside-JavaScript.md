---
layout: post
title: (계속 업데이트)인사이드 자바스크립트 정리
category: JavaScript
tags: Inside_JavaScript
comments: true
---


* TOC
{:toc}

# 자바 스크립트

> [인사이드 자바스크립트](http://book.interpark.com/product/BookDisplay.do?_method=detail&sc.saNo=001&sc.prdNo=213715769&gclid=Cj0KCQiA6ozhBRC8ARIsAIh_VC2Y0zlBJjuz4SEnsyPKgxpMh4eCzQ-SJ0KCv5-3NIakgSRXylRGsvAaAoYiEALw_wcB&product2017=true) 를 보며 몰랐거나 어려웠던 부분만 따로 정리한 문서입니다. 해당 문서의 코드들은 대부분 인사이드 자바스크립트 책 내의 예제들을 토대로 작성하였습니다.
>

## 소개

- 스크립트 언어
- 초창기에는 웹 페이지 제작을 위한 보조적인 기능 수행을 위한 용도였음.
- [github](http://github.com) 에 가장 많이 사용되고 있는 언어가 자바스크립트이다.
- Node.js가 등장해서 서버 쪽에서도 자바스크립트를 사용할 수 있게 되었다.

## 자바스크립트 활용 범위

- 웹 개발
- 서버 개발
- 애플리케이션 개발

## 데이터 타입

### 1. 기본 타입

#### 1-1. 숫자(Number)

- 숫자 타입이 하나임..(자바스크립트에서는 모든 숫자를 64비트 부동 소수점 형태로 저장함.) (c언어 double타입과 유사함)

- > 자바스크립트는 **느슨한 타입 체크 언어** 이다. 따라서 var 라는 변수에 어떤 값을 넣던지 간에 그에 따라서 타입이 결정된다

  ```js
  var a = 1.5;
  console.log(typeof(a));  //출력 값 : number
  var b = "abc";
  console.log(typeof(b)); //출력 값: string
  ```

  ------

  자바스크립트에서 나눗셈 연산을 조심해야함. 나 같은 경우는 기존에 c# 언어를 사용해와서 정수의 나눗셈에서 소숫점을 버린다고 알고있지만 예를들어 

  ```js
  var num = 5/2 ;
  console.log(num);	//출력 값 : 2.5
  //정수 부분만 출력하고 싶을 때
  var num1 = Math.floor(num);
  console.log(num1); //출력 값: 2
  ```

  이와 같이 2가 아닌 2.5가 출력이 된다. 

  > Why? 정수가 아닌 실수 취급을 하기 때문이다.
  >
  > 기존 언어처럼 소수 부분을 제외한 값을 원할 때: Math.floor() 메서드를 사용.

#### 1-2. 문자열(String)

- 문자열은 문자 배열처럼 인덱스를 이용해서 접근이 가능하다. 인덱스를 이용한 수정은 불가능

  ```js
  var str = 'abcd';
  console.log(str[0]);	//출력값: a
  str[0] = 'k'
  console.log(str);	//출력값: abcd
  //인덱스를 이용해서 문자열의 값을 바꿀 수 없음.
  ```

#### 1-3. 불린값(Boolean)

#### 1-4. undefined & null

-  둘 다 값이 비어있음을 나타냄.

  ```js
  var foo
  console.log(typeof(foo));	//출력 값: undefinded
  var moo = null;
  console.log(typeof(foo));	//출력 값: object   타입은 null이 아님.
  console.log(moo === null);		//출력 값: true
  ```

### 2. 참조 타입

#### 2-1. 객체(Object)

> 단순히 '이름(key):값(value)' 형태의 프로퍼티들을 저장하는 컨테이너. 해시(hash)와 유사함.

자신의 부모 역할을 하는 객체를 **프로토타입 객체** 라고한다.

+ 생성 방법

  + Object() 생성자 이용

    ```js
    var foo = new Object();
    // 프로퍼티 설정
    foo.name = 'foo';
    foo.age = 25;
    foo.gender = 'male';
    
    console.log()	//출력 값: {name: "foo", age: 25, gender: "male"}
    ```

  + 객체 리터럴 방식 이용

    ```js
    var foo = {
        name : 'foo',
        age : 25,
        gener : 'male'
    };
    
    console.log(foo)	//출력 값: {name: "foo", age: 25, gender: "male"}
    ```

  + 객체 프로퍼티 삭제는 delete를 이용하면 된다.

    ```js
    delete foo.name;
    console.log(foo.name);	//출력 값: undefinded
    
    delete foo;		//객체는 delete를 통해 삭제할 수 없으므로 지워지지 않는다.
    console.log(foo.age);	//출력 값: 25
    ```

#### 2-2. 배열(Array)

+ 배열 리터럴을 이용한 생성방법

  ```js
  var arr = ['apple','orange','melon'];
  
  //동적으로 배열 원소 추가
  arr[3] = 'grape';
  ```

> 객체의 프로토타입은 Object 지만 배열의 프로토타입은 Array이다.

- 배열에 프로퍼티를 추가할 수 있다. 하지만 인덱스를 통해서 배열의 원소를 추가하는 것이 아니라면 length는 증가하지 않는다. 

  ```js
  var arr = ['a','b','c'];
  arr.name = 'alphabet';
  
  console.log(arr.length);	//출력 값: 3
  console.log(arr);
  ```

- 배열도 delete를 통해 배열 요소를 삭제할 수 있다. 

  ```js
  var arr = [0,1,2,3,4];
  delete arr[2];
  console.log(arr);	//출력 값: [0,1,empty,3,4]
  ```

- Array() 생성자를 이용한 배열 생성

  ```js
  /// 길이가 3인 빈 배열 생성
  var foo = new Array(3);
  /// 길이가 3인 요소가 있는 배열 생성
  var woo = new Array(1,2,3);
  ```

- 유사 배열 객체에서도 배열의 메서드를 사용하고 싶을 때가 있을지는 모르겠지만 사용이 가능하다. **apply()**라는 메서드를 사용하면 됨


#### 2-3. 함수(Function)

#### 2-4. 정규표현식





## 함수

함수는 세 가지 방법으로 생성이 가능하다.

1. 함수 선언문
2. 함수 표현식
3. Funtion() 생성자 함수

### 1. 함수 선언문

자바스크립트에서는 함수도 일반 객체처럼 값으로 취급한다. 따라서 **함수 리터럴**을 이용해서 생성할 수 있다.

```js
//함수 리터럴, 함수 선언문 방식
function add(x,y){
    return x+y
}
console.log(add(3,4));	//출력값: 7
```

1-1. 함수 선언문 방식도 함수 리터럴 방식과 동일하다. 

<!--3 Dec 2018-->

### 2. 함수 표현식

2-1. 함수 표현식 방식으로 생성하는 법

> 함수 표현식 방식은 함수 정의 후 세미콜론을 붙이는 것을 권장한다. 

   ```js
//함수 표현식 방식
var add = function (x,y){	//보통 함수 이름을 선언하지 않는다. **익명 함수**
    return x+y;
};
var plus = add;		//이와 같이 다른 변수에 대입 가능

console.log(plus(10+5));		//출력값: 15
console.log(add(1+2));			//출력값: 3

   ```



```js
//함수 표현식 방식으로 함수를 선언할 때 함수 이름을 주면(기명 함수 표현식) 생길 수 있는 문제
var add = function sum(x,y){
    return x+y;
};

console.log(add(3,4));	//출력값 : 7
console.log(sum(3,4));	//출력값: sum은 정의되어있지 않았다고 나옴.
```

이와 같은 오류가 나오는 이유는 sum은 외부 코드에서 접근할 수 없음. (디폴트로 private로 만들어지나봄)

- 위에서 말한 세미콜론을 붙이는 것을 권장하는 이유

  ```js
  var fun = function(num){
      return num;
  }		//여기서 세미콜론은 붙이지 않는다면 함수가 끝났다고 판단하지않고 즉시 실행 함수로 이해하게 된다.
  		//따라서 아래의 즉시 실행 함수가 실행된 값이 num에 들어오게 되고
  (function(x,y){
      return x+y;
  })(5,4);
  
  console.log(fun);		//이처럼 fun을 출력해 보게 되면 9가 나온다.
  
  ```

  인사이드 자바스크립트 p.77 참고.

### 3. Function() 생성자

3-1. Function() 생성자 함수를 통해 생성하기

이 방식은 자주 사용되지 않음.

```js
var add = new Function('x','y','return x+y');
console.log(add(1,2));		//출력값: 3
```



위의 세가지 방식으로 함수를 생성할 수 있다. 하지만 권장하는 방식은 함수 표현식 방식이다. 왜냐하면 함수 선언문 방식으로 선언을 하게 되면 **함수 호이스팅**이 발생하기 때문이다. 

```js
add(3,5);		//출력값: 8
				//함수를 밑에 정의했지만 오류가 발생하지 않고 8이 출력된다. (함수가 호이스팅 되었기 때문)
function add(x,y){
    return x+y;
}

add(1,2);		//출력값: 3
```

이러한 문제는 규칙을 무시하므로 구조를 망칠 수 있다. 따라서 함수 표현식 형태로 함수를 선언하자.

### 4. 함수도 객체다

자바스크립트에서는 함수도 객체다. 따라서 함수도 프로퍼티를 가질 수 있다. 또한 함수도 일반 객체처럼 취급이 가능하여 이와 같은 동작이 가능하다.

- 리터럴에 의해 생성
- 변수나 배열의 요소,객체의 프로퍼티 등에 할당 가능
- 함수의 인자로 전달 가능
- 함수의 리턴값으로 리턴 가능
- 동적으로 프로퍼티를 생성 및 할당 가능

이러한 특징 덕에 자바스크립트에서는 함수를 **일급 객체(First Class)**라고 부른다.

#### 함수 객체의 기본 프로퍼티

함수 객체에는 표준 프로퍼티가 정의되어있다. (arguments, caller, length 등) 이것들은 함수를 생성하면 기본적으로 생성이 된다. 모든 객체들이 프로토타입을 갖고 있듯이 함수 객체 또한 [[Prototype]]을 가지고 있다. 함수 객체의 프로토타입은 **Function.prototype** 객체이다. 이 객체를 또 살펴보면 이와 같은 프로퍼티와 메서드를 갖고 있다.

- constructor 프로퍼티
- toString() 메서드
- **apply(thisArg, argArray)** 메서드
- **call(thisArg, [, arg1 [,arg2, ]])** 메서드
- bind(thisArg, [, arg1 [,arg2,]]) 메서드

apply와 call은 실제로 자주 사용된다고 한다.



#### length 프로퍼티

length 프로퍼티는 모든 함수가 가져야 하는 표준 프로퍼티이다. 함수가 정상적으로 실행될 때 기대되는 인자의 개수를 나타낸다.



#### prototype 프로퍼티

부모를 나타내는 내부 프로퍼티인 **[[Prototype]]**과 혼동하면 안된다. 이 프로퍼티는 함수가 생성될 때 만들어지며 constructor 프로퍼티 하나만 있는 객체를 가리킨다. 이 constructor은 함수 객체를 가리킨다(서로를 가리키는 셈). 함수 객체와 프로토타입 객체는 서로 밀접하게 연결돼 있다.



### 5. 함수의 다양한 형태

#### 콜백 함수

코드에서 명시적으로 호출하는 함수가 아닌 이벤트에 의해 호출되는 함수를 말한다. 보통 익명 함수를 콜백 함수에 사용하는 경우가 많다. (개발자가 명시적으로 호출할 일이 없고 이벤트가 발생했을 때 실행되면 되기 때문)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
        //페이지 로드시 알림 창
        window.onload = function(){		//익명 함수
            window.alert("show me");
        }    
    </script>
</body>
</html>
```



#### 즉시 실행 함수

즉시 실행 함수를 만드는 방법은 간단하다. 함수 리터럴을 괄호로 둘러싼 후, 함수가 바로 호출될 수 있게 괄호를 추가해준다. 인자가 필요하다면 괄호 안에 인자를 넣어주면 된다.

```js
(function (x,y){
    console.log(x+y);
})(3,5);		//출력값: 8
```

이와 같은 즉시 실행 함수는 함수를 다시 호출할 수 없다. 따라서 주로 **최초 한 번의 실행만을 필요로 하는 초기화 코드 부분**에 쓰인다.

<!--27 Dec 2018-->

#### 내부 함수

함수 내부에 있는 함수를 내부 함수라고 한다. 특징으로는

- 부모 함수 밖에서 사용할 수가 없다.
- 내부 함수에서는 부모 함수의 변수에 접근이 가능하다.

### 6. 함수 호출과 this

#### arguments 객체

함수 내에서 인자로 들어온 arguments의 정보를 얻을 수 있다.  arguments 객체는 \_\_proto\_\_ 를 제외하고 다음과 같이 구성되어 있다.

- 함수를 호출할 때 넘겨진 인자 (배열 형태)
- length 프로퍼티: 인자의 개수
- callee 프로퍼티: 실행 중인 함수의 참조값

**arguments는 배열이 아닌 객체이다. (length 프로퍼티가 있어서 배열로 착각할 수 있음.)**

다음과 같이 활용 가능

```js
function sum(){
    var result = 0;
    for(var i = 0 ; i < arguments.length; i++){
        result += arguments[i];
    }
    return result;
}

console.log(sum(1,2,3));	//6
console.log(sum(1,2,3,4,5,6,)) //21 
```

#### this

`this` 는 고급 자바스크립트 개발자로 거듭나려면 확실하게 이해해야 한다. **함수가 호출되는 방식(호출 패턴)에 따라 this가 다른 객체를 참조**(<u>this 바인딩</u>)한다.

- 객체의 메서드 호출 시 **해당 메서드를 호출한 객체로 바인딩** 된다.

- 함수를 호출 할 때의 **this는 전역 객체(window 객체)에 바인딩** 된다.

- 내부 함수 호출 시에도 this의 바인딩 특성이 적용된다. 여기서 주의 해야할 점이 있다.

  ```js
  //전역 변수 
  var value = 100;
  
  //객체 생성
  var myObj = {
      value: 1,
      func1: function(){
          this.value += 1;
          console.log('func1() called. this.value :' + this.value);
          
          //func2() 내부 함수
          func2 = function(){
              this.value += 1;
              console.log('func2() called. this.value :' + this.value);
              
              //func3() 내부 함수
              func3 = function(){
                  this.value += 1;
              	console.log('func3() called. this.value :' + this.value);
              }
              func3();
          }
          func2();
      }
  };
  myObj.func1();
  ```

  해당 코드를 실행했을 때 func1() => func2() => func3() 이 순차적으로 실행되는데 기대했던 값은 myObj객체 내의 value 값이 증가해서 

  ```js
  //예상 출력 값
  func1() called. this.value : 2
  func2() called. this.value : 3
  func3() called. this.value : 4
  ```

  를 예상 했지만 결과는 

  ```js
  //실제 출력 값
  func1() called. this.value :2
  func2() called. this.value :101
  func3() called. this.value :102
  ```

  위와 같이 나왔다. 이유는 자바스크립트에서는 **내부 함수 호출 패턴을 정의해 놓지 않기 때문**이라고 한다. 따라서 func2() 함수 부터는 전역 변수인 value의 값을 증가시킨 것이다. 내부 함수를 사용할 때 주의해야 할 것같다.

