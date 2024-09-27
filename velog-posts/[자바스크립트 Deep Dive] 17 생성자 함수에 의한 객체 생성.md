<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/6693728d-57d3-4afe-bb4a-a23b56f5dc9b/image.png" /></p>
<h2 id="17-생성자-함수에-의한-객체-생성">17. 생성자 함수에 의한 객체 생성</h2>
<hr />
<h3 id="171-object-성성자-함수">17.1 Object 성성자 함수</h3>
<h5 id="new-연산자와-함께-object-생성자-함수를-호출하면-빈-객체를-생성하여-반환한다">new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.</h5>
<pre><code class="language-js">// 빈 객체의 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(person); // {name: &quot;Lee&quot;, sayHello: ƒ}
person.sayHello(); // Hi! My name is Lee</code></pre>
<h5 id="생성자-함수란-new-연산자와-함께-호출하여-객체를-생성하는-함수를-말한다">생성자 함수란 new 연산자와 함께 호출하여 객체를 생성하는 함수를 말한다.</h5>
<pre><code class="language-js">// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee');
console.log(typeof strObj); // object
console.log(strObj);        // String {&quot;Lee&quot;}

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123);
console.log(typeof numObj); // object
console.log(numObj);        // Number {123}

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj= new Boolean(true);
console.log(typeof boolObj); // object
console.log(boolObj);        // Boolean {true}

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func); // function
console.dir(func);        // ƒ anonymous(x)

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3);
console.log(typeof arr); // object
console.log(arr);        // [1, 2, 3]

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RegExp(/ab+c/i);
console.log(typeof regExp); // object
console.log(regExp);        // /ab+c/i

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();
console.log(typeof date); // object
console.log(date);        // Mon May 04 2020 08:36:33 GMT+0900 (대한민국 표준시)</code></pre>
<h3 id="172-생성자-함수">17.2 생성자 함수</h3>
<h4 id="1721-객체-리터럴에-의한-객체-생성-방식의-문제점">17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점</h4>
<h5 id="객체-리터럴에-의한-객체-생성-방식은-하나의-객체만-생성해서-동일한-프로퍼티를-가진-객체를-여러-개-생성해야-하는-경우-비효율-적이다">객체 리터럴에 의한 객체 생성 방식은 하나의 객체만 생성해서 동일한 프로퍼티를 가진 객체를 여러 개 생성해야 하는 경우 비효율 적이다</h5>
<pre><code class="language-js">const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle1.getDiameter()); // 10

const circle2 = {
  radius: 10,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle2.getDiameter()); // 20</code></pre>
<h4 id="1722-생성자-함수에-의한-객체-생성-방식의-장점">17.2.2 생성자 함수에 의한 객체 생성 방식의 장점</h4>
<h5 id="생성자-함수에-의한-객체-생성-방식은-마치-객체를-생성하기-위한-템플릿class처럼-생성자-함수를-사용하여-프로퍼티-구조가-동일한-객체-여러-개를-간편하게-생성할-수-있다">생성자 함수에 의한 객체 생성 방식은 마치 객체를 생성하기 위한 템플릿(class)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.</h5>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20</code></pre>
<blockquote>
<p>new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.</p>
</blockquote>
<pre><code class="language-js">// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다.
// 즉, 일반 함수로서 호출된다.
const circle3 = Circle(15);

// 일반 함수로서 호출된 Circle은 반환문이 없으므로 암묵적으로 undefined를 반환한다.
console.log(circle3); // undefined

// 일반 함수로서 호출된 Circle내의 this는 전역 객체를 가리킨다.
console.log(radius); // 15</code></pre>
<h4 id="1723-생성자-함수의-인스턴스-생성-과정">17.2.3 생성자 함수의 인스턴스 생성 과정</h4>
<blockquote>
<p>생성자 함수의 역할은 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것이다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  // 인스턴스 초기화
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스 생성
const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성</code></pre>
<h5 id="1-인스턴스-생성과-this-바인딩">1. 인스턴스 생성과 this 바인딩</h5>
<blockquote>
</blockquote>
<h5 id="암묵적으로-빈-객체가-생성된다-이-객체가-생성자-함수가-생성한-인스턴스인데-이-인스턴스는-this에-바인딩된다">암묵적으로 빈 객체가 생성된다. 이 객체가 생성자 함수가 생성한 인스턴스인데 이 인스턴스는 this에 바인딩된다.</h5>
<pre><code class="language-js">function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Circle {}

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}</code></pre>
<h5 id="2-인스턴스-초기화">2. 인스턴스 초기화</h5>
<blockquote>
</blockquote>
<h5 id="생성자-함수에-기술되어-있는-코드가-한-줄씩-실행되어-this에-바인딩되어-있는-인스턴스-초기화한다-즉-this에-바인딩되어-있는-인스턴스에-프로퍼티나-메서드를-추가하고-생성자-함수가-인수로-전달받은-초기-값을-인스턴스-프로퍼티에-할당하여-초기화하거나-고정값을-할당한다">생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this에 바인딩되어 있는 인스턴스 초기화한다. 즉 this에 바인딩되어 있는 인스턴스에 프로퍼티나 메서드를 추가하고 생성자 함수가 인수로 전달받은 초기 값을 인스턴스 프로퍼티에 할당하여 초기화하거나 고정값을 할당한다.</h5>
<pre><code class="language-js">function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}</code></pre>
<h5 id="3인스턴스-반환">3.인스턴스 반환</h5>
<blockquote>
</blockquote>
<h5 id="생성자-함수-내부에서-모든-처리가-끝나면-완성된-인스턴스가-바인딩된-this를-암묵적으로-반환한다">생성자 함수 내부에서 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환한다.</h5>
<pre><code class="language-js">function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };

  // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다
}

// 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환한다.
const circle = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: ƒ}</code></pre>
<h4 id="1724-내부-메서드-call과construct">17.2.4 내부 메서드 [[call]]과[[construct]]</h4>
<h5 id="함수-선언문-또는-함수-표현식으로-정의한-함수는-일반적인-함수로서-호출할-수-있는-것은-물론-생성자-함수로서-호출할-수-있다-생성자-함수로서-호출한다는-것은-new-연산자와-함께-호출하여-객체를-생성하는-것을-의미한다">함수 선언문 또는 함수 표현식으로 정의한 함수는 일반적인 함수로서 호출할 수 있는 것은 물론 생성자 함수로서 호출할 수 있다. 생성자 함수로서 호출한다는 것은 new 연산자와 함께 호출하여 객체를 생성하는 것을 의미한다.</h5>
<pre><code class="language-js">// 함수는 객체다.
function foo() {}

// 함수는 객체이므로 프로퍼티를 소유할 수 있다.
foo.prop = 10;

// 함수는 객체이므로 메서드를 소유할 수 있다.
foo.method = function () {
  console.log(this.prop);
};

foo.method(); // 10</code></pre>
<blockquote>
<p>함수는 객체이지만 일반 객체와는 다르다. 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.</p>
</blockquote>
<h5 id="함수가-일반-함수로서-호출되면-함수-객체의-내부-메서드call이-호출되고-new-연산자와-함께-생성자-함수로서-호출되면-내부-메서드-construct가-호출된다">함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드[[call]]이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 [[construct]]가 호출된다.</h5>
<pre><code class="language-js">function foo() {}

// 일반적인 함수로서 호출: [[Call]]이 호출된다.

foo();

// 생성자 함수로서 호출: [[Construct]]가 호출된다.
new foo();</code></pre>
<h5 id="내부-메서드-call을-갖는-함수-객체를-callable이라-하며-callable은-호출할-수-있는-객체이며-함수-객체는-반드시-callable이어야-한다">내부 메서드 [[call]]을 갖는 함수 객체를 callable이라 하며 callable은 호출할 수 있는 객체이며 함수 객체는 반드시 callable이어야 한다.</h5>
<h5 id="이와-반대로-모든-함수-객체가-construct를-갖는-것은-아니다-다시말해-모든-함수-객체는-callable이면서-construct-이나-non-construct이다">이와 반대로 모든 함수 객체가 [[Construct]]를 갖는 것은 아니다. 다시말해 모든 함수 객체는 callable이면서 Construct 이나 non-Construct이다.</h5>
<h4 id="1725-constructor와-non-constructor의-구분">17.2.5 constructor와 non-constructor의 구분</h4>
<h5 id="constructor를-갖지-않는-함수-객체를-non-constructor이라-한고-갖는-객체를-constructor이라-한다">[[constructor]]를 갖지 않는 함수 객체를 non-constructor이라 한고 갖는 객체를 constructor이라 한다.</h5>
<blockquote>
<ul>
  <li> constructor : 함수 선언문,함수 표현식, 클래스
    <li>non-constructor : 메서드,화살표 함수
      </ul>
</blockquote>
<pre><code class="language-js">// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function () {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수다. 이는 메서드로 인정하지 않는다.
const baz = {
  x: function () {}
};

// 일반 함수로 정의된 함수만이 constructor이다.
new foo();   // -&gt; foo {}
new bar();   // -&gt; bar {}
new baz.x(); // -&gt; x {}

// 화살표 함수 정의
const arrow = () =&gt; {};

new arrow(); // TypeError: arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만을 메서드로 인정한다.
const obj = {
  x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor</code></pre>
<h4 id="1726-new연산자">17.2.6 new연산자</h4>
<h5 id="일반함수와-생성자-함수의-형식에-차이점은-new연산자를-함께-호출하면-해당-함수는-생성자-함수로-동작한다">일반함수와 생성자 함수의 형식에 차이점은 new연산자를 함께 호출하면 해당 함수는 생성자 함수로 동작한다.</h5>
<pre><code class="language-js">// 생성자 함수로서 정의하지 않은 일반 함수
function add(x, y) {
  return x + y;
}

// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
let inst = new add();

// 함수가 객체를 반환하지 않았으므로 반환문이 무시된다. 따라서 빈 객체가 생성되어 반환된다.
console.log(inst); // {}

// 객체를 반환하는 일반 함수
function createUser(name, role) {
  return { name, role };
}

// 일반 함수를 new 연산자와 함께 호출
inst = new createUser('Lee', 'admin');
// 함수가 생성한 객체를 반환한다.
console.log(inst); // {name: &quot;Lee&quot;, role: &quot;admin&quot;}</code></pre>
<h4 id="1727-newtarget">17.2.7 new.target</h4>
<h5 id="함수-내부에서-newtarget을-사용하면-new연산자와-함께-생성자-함수로서-호출되었는지-알수-있다">함수 내부에서 new.target을 사용하면 new연산자와 함께 생성자 함수로서 호출되었는지 알수 있다.</h5>
<blockquote>
<p>new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다. new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined이다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
  if (!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter());  // 10</code></pre>
<h5 id="대부분의-빌트인-생성자-함수-objectstringnumberbooleanfunctionarraydataregexppromise는-new연산자와-함께-호출되었는지를-확인한-후-값을-반환한다">대부분의 빌트인 생성자 함수 (Object,String,Number,Boolean,Function,Array,Data,RegExp,Promise)는 new연산자와 함께 호출되었는지를 확인한 후 값을 반환한다.</h5>
<pre><code class="language-js">let obj = new Object();
console.log(obj); // {}

obj = Object();
console.log(obj); // {}

let f = new Function('x', 'return x ** x');
console.log(f); // ƒ anonymous(x) { return x ** x }

f = Function('x', 'return x ** x');
console.log(f); // ƒ anonymous(x) { return x ** x }</code></pre>
<h5 id="하지만-stringnumberboolean-생성자-함수는-new-연산자-없이-호출하면-문자열숫자불리언값을-반환한다">하지만 string,Number,Boolean 생성자 함수는 new 연산자 없이 호출하면 문자열,숫자,불리언값을 반환한다.</h5>
<pre><code class="language-js">const str = String(123);
console.log(str, typeof str); // 123 string

const num = Number('123');
console.log(num, typeof num); // 123 number

const bool = Boolean('true');
console.log(bool, typeof bool); // true boolean</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="this">this</h5>
<blockquote>
<p>this는 객체 자신이 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. this가 가리키는 값, 즉 this바인딩은 함수 호출 방식에 따라 동적으로 결정된다.</p>
</blockquote>
<table>
<thead>
<tr>
<th>함수 호출 방식</th>
<th>this가 가리키는 값(this 바인딩)</th>
</tr>
</thead>
<tbody><tr>
<td>일반 함수로서 호출</td>
<td>전역 객체</td>
</tr>
<tr>
<td>메서드로서 호출</td>
<td>메서드를 호출한 객체(마침표 앞의 객체)</td>
</tr>
<tr>
<td>생성자 함수로서 호출</td>
<td>생성자 함수가 생성할 인스턴스</td>
</tr>
<tr>
<td>##### 바인딩</td>
<td></td>
</tr>
</tbody></table>
<blockquote>
<p>바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 예를들어 선수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩하는 것이다. this 바인딩은 this(키워드로 분류되지만 식별자 역할을 하는)와 this가 가리킬 객체를 바인딩하는 것이다.</p>
</blockquote>
<h5 id="스코프-세이프-생성자-패턴">스코프 세이프 생성자 패턴</h5>
<blockquote>
<p>ES6에서는 new.target 지원이 안되는 스코프 세이프 생성자 패턴을 사용해야 한다.</p>
</blockquote>
<pre><code class="language-js">// Scope-Safe Constructor Pattern
function Circle(radius) {
  // 생성자 함수가 new 연산자와 함께 호출되면 함수의 선두에서 빈 객체를 생성하고
  // this에 바인딩한다. 이때 this와 Circle은 프로토타입에 의해 연결된다.

  // 이 함수가 new 연산자와 함께 호출되지 않았다면 이 시점의 this는 전역 객체 window를 가리킨다.
  // 즉, this와 Circle은 프로토타입에 의해 연결되지 않는다.
  if (!(this instanceof Circle)) {
    // new 연산자와 함께 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter()); // 10</code></pre>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/17.md">wikibooks
</a></p>