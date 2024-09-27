<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/eca42fe7-df1a-46ef-b3ee-38f43d9ee6a1/image.png" /></p>
<h2 id="10-객체-리터럴">10. 객체 리터럴</h2>
<hr />
<h3 id="101-객체란">10.1 객체란?</h3>
<blockquote>
<p>변경 불가능 한 값인 원시 타입과 달리 객체는 변경 가능한 값이다.</p>
</blockquote>
<blockquote>
<ul>
  <li> 프로퍼티: 객체의 상태를 나타내는 값
  <li>메서드: 프로퍼티를 참조하고 조작할 수 있는 동작 = 객체안에 함수
  </ul>
</blockquote>
<pre><code class="language-js">var person = {
 name: 'kim',//프로퍼티
 age:20//프로퍼티
 //name,age: key
 //kim,20 : value
 increase: function (){//메서드
 this.num++
 }
} </code></pre>
<h3 id="102-객체-리터럴에-의한-객체-생성">10.2 객체 리터럴에 의한 객체 생성</h3>
<blockquote>
<p>자바스크립트는 프로토타입 기반 객체지향 언어로서 다양한 객체 생성 방법을 지원한다</p>
</blockquote>
<blockquote>
<ul>
  <li> 객체 리터럴
  <li> object 생성자 함수
  <li> 생성자 함수
  <li> Object.crate 메서드
  <li> 클래스
 </ul>
</blockquote>
<h5 id="객체-생성-방법-중에서-가장-일반적이고-간단한-방법은-객체-리터럴이다">객체 생성 방법 중에서 가장 일반적이고 간단한 방법은 객체 리터럴이다</h5>
<pre><code class="language-js">var person = {
  name: 'Lee',
  sayHello: function () {
    console.log(`Hello! My name is ${this.name}.`);
  }
};
console.log(typeof person); // object
console.log(person); // {name: &quot;Lee&quot;, sayHello: ƒ}   

var empty = {};// 빈객체
console.log(type of empty) //object</code></pre>
<h3 id="103-프로퍼티">10.3 프로퍼티</h3>
<blockquote>
<p>객체는 프로퍼티의 집합이며 프로퍼티는 키와 값으로 구성된다.</p>
<ul>
  <li> 키(key) : 빈 문자열은 포함하는 모든 문자열 또는 심벌 값
  <li> 값(value) : 자바스크립트에서 사용할 수 있는 모든 값
  </ul>
</blockquote>
<pre><code class="language-js">   var person = {
  // 프로퍼티 키는 name, 프로퍼티 값은 'Lee'
  name: 'Lee',
  // 프로퍼티 키는 age, 프로퍼티 값은 20
  age: 20
};</code></pre>
<h5 id="문자열-또는-문자열로-평가할-수-있는-표현식을-사용해-프로퍼티-키를-동적으로-생성-가능하다">문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성 가능하다.</h5>
<pre><code class="language-js">var obj = {};
var key = 'hello';

// ES5: 프로퍼티 키 동적 생성
obj[key] = 'world';
// ES6: 계산된 프로퍼티 이름
// var obj = { [key]: 'world' };

console.log(obj); // {hello: &quot;world&quot;}</code></pre>
<h5 id="프로퍼티-키에-문자열이나-심벌-값-외의-값을-사용하면-암묵적-타입-변환을-통해-문자열이-된다">프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.</h5>
<pre><code class="language-js">var foo = {
  0: 1,
  1: 2,
  2: 3
};

console.log(foo); // {0: 1, 1: 2, 2: 3}</code></pre>
<h5 id="이미-존재하는-프로퍼티-키를-중복-선언하면-나중에-선언한-프로퍼티가-먼저-선언한-프로퍼티를-덮어쓴다">이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.</h5>
<pre><code class="language-js">var foo = {
  name: 'Lee',
  name: 'Kim'
};

console.log(foo); // {name: &quot;Kim&quot;}</code></pre>
<h3 id="104-메서드">10.4 메서드</h3>
<blockquote>
<p>자바스크립트의 함수는 객체이다. 함수는 값으로 취급될수 있기 때문에 프로퍼티 값으로 사용할 수 있다. 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다. <br />
즉, 메서드는 객체에 묶여있는 함수를 의미한다</p>
</blockquote>
<pre><code class="language-js">var circle = {
  radius: 5, // ← 프로퍼티

  // 원의 지름
  getDiameter: function () { // ← 메서드
    return 2 * this.radius; // this는 circle을 가리킨다.
  }
};

console.log(circle.getDiameter()); // 10</code></pre>
<h3 id="105-프로퍼티-접근">10.5 프로퍼티 접근</h3>
<blockquote>
<ul>
  <li>마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법
  <li>대괄호 프로퍼티 접근 연산자([...])를 사용하는 대괄호 표기법
  </ul>
</blockquote>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // Lee

// 대괄호 표기법에 의한 프로퍼티 접근
console.log(person['name']); // Lee
                             // 대괄호 안은 반드시 따옴표로 감싸야한다</code></pre>
<blockquote>
<p>객체에 존재하지 않은 프로퍼티에 접근하면 undefined를 반환한다.</p>
</blockquote>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

console.log(person.age); // undefined</code></pre>
<h3 id="106-프로퍼티-값-갱신">10.6 프로퍼티 값 갱신</h3>
<h5 id="이미-존재하는-프로퍼티에-값을-할당하면-프로퍼티-값이-갱신된다">이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.</h5>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.
person.name = 'Kim';

console.log(person);  // {name: &quot;Kim&quot;}</code></pre>
<h3 id="107-프로퍼티-동적-생성">10.7 프로퍼티 동적 생성</h3>
<h5 id="존재하지-않는-프로퍼티에-값을-할당하면-프로퍼티가-동적으로-생성되어-추가되고-프로퍼티-값이-할당된다">존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.</h5>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// person 객체에는 age 프로퍼티가 존재하지 않는다.
// 따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.
person.age = 20;

console.log(person); // {name: &quot;Lee&quot;, age: 20}</code></pre>
<h3 id="108-프로퍼티-삭제">10.8 프로퍼티 삭제</h3>
<h5 id="delete-연산자는-객체의-프로퍼티를-삭제한다-이때-존재하지-않는-프로퍼티를-삭제하면-아무런-에러-없이-무시된다">delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 존재하지 않는 프로퍼티를 삭제하면 아무런 에러 없이 무시된다.</h5>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

// person 객체에 age 프로퍼티가 존재한다.
// 따라서 delete 연산자로 age 프로퍼티를 삭제할 수 있다.
delete person.age;

// person 객체에 address 프로퍼티가 존재하지 않는다.
// 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
delete person.address;

console.log(person); // {name: &quot;Lee&quot;}</code></pre>
<h3 id="109-es6에서-추가된-객체-리터럴의-확장-기능">10.9 ES6에서 추가된 객체 리터럴의 확장 기능</h3>
<h4 id="1091-프로퍼티-축약-표현">10.9.1 프로퍼티 축약 표현</h4>
<h5 id="객체-리터럴의-프로퍼티는-프로퍼티-키와-프로퍼티-값으로-구성된다">객체 리터럴의 프로퍼티는 프로퍼티 키와 프로퍼티 값으로 구성된다.</h5>
<pre><code class="language-js">var x = 1, y = 2;

var obj = {
  x: x,
  y: y
};

console.log(obj); // {x: 1, y: 2}</code></pre>
<h5 id="es6에서는-프로퍼티-값으로-변수를-사용하는-경우-변수-이름과-프로퍼티-키가-동일한-이름일-때-키를-생략-할-수-있다">ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 키를 생략 할 수 있다.</h5>
<pre><code class="language-js">// ES6
let x = 1, y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}</code></pre>
<h4 id="1092-계산된-프로퍼티-이름">10.9.2 계산된 프로퍼티 이름</h4>
<h5 id="문자열-또는-문자열로-타입-변환할-수-있는-값으로-평가되는-표현식을-사용해-프로퍼티-키를-동적으로-생성할-수-있는데-표현식을-대괄호로-묶어야-하며-이를-계산된-프로퍼티-이름이라고-한다">문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있는데 표현식을 대괄호([...])로 묶어야 하며 이를 계산된 프로퍼티 이름이라고 한다.</h5>
<pre><code class="language-js">// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

// 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}</code></pre>
<h5 id="es6에서는-객체-리터럴-내부에서도-계산된-프로퍼티-이름으로-프로퍼티-키를-동적-생성할-수-있다">ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.</h5>
<pre><code class="language-js">// ES6
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}</code></pre>
<h4 id="1093">10.9.3</h4>
<h5 id="es6에서는-메서드를-정의할-대-function-키워드를-생략할-수-있다">ES6에서는 메서드를 정의할 대 function 키워드를 생략할 수 있다</h5>
<pre><code class="language-js">// ES6
const obj = {
  name: 'Lee',
  // 메서드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="인스턴스">인스턴스</h5>
<blockquote>
<p>인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함 한 개념이다. 클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 한다. 
인스턴스는 객체가 메모리에 저장되어 실제로 존재하는 것에 초점을 맞춘 용어다.</p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/10.md">wikibooks</a></h4>