<h2 id="181-함수와-일급-객체">18.1 함수와 일급 객체</h2>
<hr />
<h5 id="다음과-같은-조건을-만족하는-객체를-일급-객체라-한다">다음과 같은 조건을 만족하는 객체를 '일급 객체'라 한다.</h5>
<blockquote>
<ul>
  <li> 무명의 리터럴로 생성할 수 있다. 즉,런타임에 생성이 가능하다.
    <li>변수나 자료구조에 저장할 수 있다.
      <li>함수의 매개변수에 전달할 수 있다.
        <li> 함수의 반환값으로 사용할 수 있다.
          </ul>
</blockquote>
<pre><code class="language-js">// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

// 2. 함수는 객체에 저장할 수 있다.
const auxs = { increase, decrease };

// 3. 함수의 매개변수에게 전달할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(aux) {
  let num = 0;

  return function () {
    num = aux(num);
    return num;
  };
}

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(auxs.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const decreaser = makeCounter(auxs.decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2</code></pre>
<h3 id="182-함수-객체의-프로퍼티">18.2 함수 객체의 프로퍼티</h3>
<h5 id="함수도-객체이므로-프로퍼티를-가질수-있다">함수도 객체이므로 프로퍼티를 가질수 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/97383c42-4e1b-435e-976e-49dbe804b225/image.png" /></p>
<h5 id="함수의-모든-프로퍼티의-프로퍼티-어트리뷰트를-objectgetownpropertydescriptors-메서드로-확인-가능하다">함수의 모든 프로퍼티의 프로퍼티 어트리뷰트를 Object.getOwnPropertyDescriptors 메서드로 확인 가능하다.</h5>
<pre><code class="language-js">function square(number) {
  return number * number;
}

console.log(Object.getOwnPropertyDescriptors(square));
/*
{
  length: {value: 1, writable: false, enumerable: false, configurable: true},
  name: {value: &quot;square&quot;, writable: false, enumerable: false, configurable: true},
  arguments: {value: null, writable: false, enumerable: false, configurable: false},
  caller: {value: null, writable: false, enumerable: false, configurable: false},
  prototype: {value: {...}, writable: true, enumerable: false, configurable: false}
}
*/

// __proto__는 square 함수의 프로퍼티가 아니다.
console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefined

// __proto__는 Object.prototype 객체의 접근자 프로퍼티다.
// square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받는다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get: ƒ, set: ƒ, enumerable: false, configurable: true}</code></pre>
<h4 id="1821-arguments-프로퍼티">18.2.1 arguments 프로퍼티</h4>
<h5 id="함수-객체의-arguments-프로퍼티-값은-arguments-객체다">함수 객체의 arguments 프로퍼티 값은 arguments 객체다.</h5>
<h5 id="arguments-객체는-인수를-프로퍼티-값으로-소유하며-프로퍼티-키는-인수의-순서를-나타낸다">arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/340d0fd8-10d1-43a7-a5df-1abf3d505efb/image.png" /></p>
<h4 id="1822-caller-프로퍼티">18.2.2 caller 프로퍼티</h4>
<h5 id="현재는-비표준-프로퍼티이므로-굳이-알지-않아도-된다">현재는 비표준 프로퍼티이므로 굳이 알지 않아도 된다.</h5>
<h4 id="1823-length-프로퍼티">18.2.3 length 프로퍼티</h4>
<h5 id="length-프로퍼티는-함수를-정희할-때-선언한-매개변수의-개수를-가리킨다-arguments-length-프로퍼티는-인자의-개수를-가리키고-함수-객체의-length프로퍼티는-매개변수의-개수를-가리킨다">length 프로퍼티는 함수를 정희할 때 선언한 매개변수의 개수를 가리킨다. arguments length 프로퍼티는 인자의 개수를 가리키고, 함수 객체의 length프로퍼티는 매개변수의 개수를 가리킨다.</h5>
<pre><code class="language-js">function foo() {}
console.log(foo.length); // 0

function bar(x) {
  return x;
}
console.log(bar.length); // 1

function baz(x, y) {
  return x * y;
}
console.log(baz.length); // 2</code></pre>
<h4 id="1824-name-프로퍼티">18.2.4 name 프로퍼티</h4>
<h5 id="함수객체의-name-프로퍼티는-함수-이름을-나타낸다">함수객체의 name 프로퍼티는 함수 이름을 나타낸다.</h5>
<pre><code class="language-js">// 기명 함수 표현식
var namedFunc = function foo() {};
console.log(namedFunc.name); // foo

// 익명 함수 표현식
var anonymousFunc = function() {};
// ES5: name 프로퍼티는 빈 문자열을 값으로 갖는다.
// ES6: name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문(Function declaration)
function bar() {}
console.log(bar.name); // bar</code></pre>
<h4 id="1825-proto-접근자-프로퍼티">18.2.5 <strong>Proto</strong> 접근자 프로퍼티</h4>
<h5 id="proto프로퍼티는-prototype-내부-슬롯이-가리키는-프로토타입-객체에-접근하기-위해-사용하는-접근자-프로퍼티다"><strong>proto</strong>프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티다.</h5>
<h5 id="prototype-내부-슬롯에도-직접-접근할-수-없으며-proto접근자-프로퍼티를-통해-간접적으로-프로토타입-객체에-접근할-수-있다">[[Prototype]] 내부 슬롯에도 직접 접근할 수 없으며 <strong>proto</strong>접근자 프로퍼티를 통해 간접적으로 프로토타입 객체에 접근할 수 있다.</h5>
<pre><code class="language-js">const obj = { a: 1 };

// 객체 리터럴 방식으로 생성한 객체의 프로토타입 객체는 Object.prototype이다.
console.log(obj.__proto__ === Object.prototype); // true

// 객체 리터럴 방식으로 생성한 객체는 프로토타입 객체인 Object.prototype의 프로퍼티를 상속받는다.
// hasOwnProperty 메서드는 Object.prototype의 메서드다.
console.log(obj.hasOwnProperty('a'));         // true
console.log(obj.hasOwnProperty('__proto__')); // false</code></pre>
<h4 id="1826-prototype-프로퍼티">18.2.6 prototype 프로퍼티</h4>
<h5 id="prototype-프로퍼티는-생성자-함수로-호출할-수-있는-객체-즉-constructor만이-소유하는-프로퍼티다">prototype 프로퍼티는 생성자 함수로 호출할 수 있는 객체, 즉 constructor만이 소유하는 프로퍼티다.</h5>
<pre><code class="language-js">// 함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}).hasOwnProperty('prototype'); // -&gt; true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty('prototype'); // -&gt; false</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="arguments-객체의-symboliterator-프로퍼티">arguments 객체의 (Symbol.iterator) 프로퍼티</h5>
<blockquote>
<p>arguments 객체의 (Symbol.iterator) 프로퍼티는 arguments 객체를 순회 가능한 자료구조인 이터러블로 만들기 위한 프로퍼티다. <br />Symbol.iterator를 프로퍼티 키로 사용한 메서드를 구현하는 것에 의해 이터러블이 된다.</p>
</blockquote>
<pre><code class="language-js">function multiply(x, y) {
  // 이터레이터
  const iterator = arguments[Symbol.iterator]();

  // 이터레이터의 next 메서드를 호출하여 이터러블 객체 arguments를 순회
  console.log(iterator.next()); // {value: 1, done: false}
  console.log(iterator.next()); // {value: 2, done: false}
  console.log(iterator.next()); // {value: 3, done: false}
  console.log(iterator.next()); // {value: undefined, done: true}

  return x * y;
}

multiply(1, 2, 3);</code></pre>
<h5 id="유사-배열-객체와-이터러블">유사 배열 객체와 이터러블</h5>
<blockquote>
<p>ES6에서 도입된 이터레이션 프로토콜을 준수하면 순회 가능한 자료구조인 이터러블이 된다. 이터러블의 개념이 없었던 ES6에서 arguments 객체는 유사 배열 객체로 구분되었다. 하지만 이터러블이 도입된 ES6부터 arguments 객체는 유사 배열 객체이면서 동시에 이터러블이다.</p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/18.md">wikibooks</a></p>