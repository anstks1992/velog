<h2 id="21-빌트인-객체">21. 빌트인 객체</h2>
<hr />
<h3 id="211-자바스크립트-객체의-분류">21.1 .자바스크립트 객체의 분류</h3>
<h5 id="자바스립트-객체는-크게-3개의-객체로-분류할-수-있다">자바스립트 객체는 크게 3개의 객체로 분류할 수 있다</h5>
<ul style="font-size: 17px;">
<li> 표준 빌트인 객체 : <br />
 1)  ECMAScript 사양에 정의된 객체를 말하며, 애플리 케이션 전역의 공동 기능을 제공한다.<br />
 2) 실행 환경에 상관없이 사용 가능하다. <br />
  3) 표준 빌트인 전역 객체의 프로퍼티로서 제공된다. 따라서 별도의 선언 없이 전역 변수처럼 언제나 참조할 수 있다.
<li>  호스트 객체 : <br />
  1) ECMAScript 사양에 정의되어 있지 않지만 자바스크립트 실행 환경에서 추가로 제공하는 객체
  2) 브라우저 환경에서는 클라이언트 사이드 web api를 node 환경에서는 고유의 api를 호스트 객체로 제공한다
<li> 사용자 정의 객체 : <br />
  1) 사용자가 직접 정의한 객체
</ul>

<h3 id="212-표준-빌트인-객체">21.2 표준 빌트인 객체</h3>
<h5 id="자바스크립트는--object-string-number-boolean-symbol-date-math-regexp-array-mapset-weakmap-weakset-function-promise-reflect-proxy-json-error-등-40여-개의-표준-빌트인-객체를-제공한다">자바스크립트는  Object, String, Number, Boolean, Symbol, Date, Math, RegExp, Array, Map/Set, WeakMap/ WeakSet, Function, Promise, Reflect, Proxy, JSON, Error 등 40여 개의 표준 빌트인 객체를 제공한다.</h5>
<h5 id="math-reflect-json을-제외한-표준-빌트인-객체는-모두-인스턴스를-생성할-수-있는-생성자-함수-객체이다">Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체이다.</h5>
<h5 id="생성자-함수-객체인-표준-빌트인-객체는-프로토타입-메서드와-정적-메서드를-제공하고-생성자-함수-객체가-아닌-표준-빌트인-객체는-정적-메서드만-제공한다">생성자 함수 객체인 표준 빌트인 객체는 프로토타입 메서드와 정적 메서드를 제공하고 생성자 함수 객체가 아닌 표준 빌트인 객체는 정적 메서드만 제공한다.</h5>
<pre><code class="language-js">// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee'); // String {&quot;Lee&quot;}
console.log(typeof strObj);       // object

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123); // Number {123}
console.log(typeof numObj);     // object

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj= new Boolean(true); // Boolean {true}
console.log(typeof boolObj);      // object

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x'); // ƒ anonymous(x )
console.log(typeof func);                       // function

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3); // (3) [1, 2, 3]
console.log(typeof arr);        // object

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RegExp(/ab+c/i); // /ab+c/i
console.log(typeof regExp);         // object

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();  // Fri May 08 2020 10:43:25 GMT+0900 (대한민국 표준시)
console.log(typeof date); // object</code></pre>
<h5 id="생성자-함수인-표준-빌트인-객체가-생성한-인스턴스의-프로토타입은-표준-빌트인-객체의-prototype-프로퍼티에-바인딩된-객체다">생성자 함수인 표준 빌트인 객체가 생성한 인스턴스의 프로토타입은 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체다.</h5>
<pre><code class="language-js">// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee'); // String {&quot;Lee&quot;}

// String 생성자 함수를 통해 생성한 strObj 객체의 프로토타입은 String.prototype이다.
console.log(Object.getPrototypeOf(strObj) === String.prototype); // true</code></pre>
<h5 id="표준-빌트은-객체의-prototype-프로퍼티에-바인딩된-객체는-다양한-기능의-빌트인-프로토타입-메서드를-제공한다-그리고-표준-빌트인-객체는-인스턴스-없이도-호출-가능한-빌트인-정적-메서드를-제공한다">표준 빌트은 객체의 prototype 프로퍼티에 바인딩된 객체는 다양한 기능의 빌트인 프로토타입 메서드를 제공한다. 그리고 표준 빌트인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메서드를 제공한다.</h5>
<pre><code class="language-js">// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(1.5); // Number {1.5}

// toFixed는 Number.prototype의 프로토타입 메서드다.
// Number.prototype.toFixed는 소수점 자리를 반올림하여 문자열로 반환한다.
console.log(numObj.toFixed()); // 2

// isInteger는 Number의 정적 메서드다.
// Number.isInteger는 인수가 정수(integer)인지 검사하여 그 결과를 Boolean으로 반환한다.
console.log(Number.isInteger(0.5)); // false</code></pre>
<h3 id="213-원시값과-래퍼-객체">21.3 원시값과 래퍼 객체</h3>
<h5 id="원시값인-문자열숫자불리언-값의-경우-이들-원시값에-대해-마치-객체처럼-마침표-표기법으로-접근하면-자바스크립트-엔진이-일시적으로-원시-값을-연관된-객체로-변화해-준다">원시값인 문자열,숫자,불리언 값의 경우 이들 원시값에 대해 마치 객체처럼 마침표 표기법으로 접근하면 자바스크립트 엔진이 일시적으로 원시 값을 연관된 객체로 변화해 준다.</h5>
<pre><code class="language-js">const str = 'hello';

// 원시 타입인 문자열이 프로퍼티와 메서드를 갖고 있는 객체처럼 동작한다.
console.log(str.length); // 5
console.log(str.toUpperCase()); // HELLO</code></pre>
<h5 id="원시값을-객체처럼-사용하면-자바스크립트-엔진은-암묵적으로-연관된-객체를-생성하여-생성된-객체로-프로퍼티에-접근하거나-메서드를-호출하고-다시-원시값으로-되돌린다">원시값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하여 생성된 객체로 프로퍼티에 접근하거나 메서드를 호출하고 다시 원시값으로 되돌린다.</h5>
<blockquote>
<p>이처럼 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 '래퍼 객체'라 한다.</p>
</blockquote>
<h5 id="문자열에-대해-마침표-표기법으로-접근하면-그-순간-래퍼-객체인-string-생성자-함수의-인스턴스가-생성되고-문자열은-래퍼-객체의-stringdata-내부-슬롯에-할당된다">문자열에 대해 마침표 표기법으로 접근하면 그 순간 래퍼 객체인 String 생성자 함수의 인스턴스가 생성되고 문자열은 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된다.</h5>
<pre><code class="language-js">const str = 'hi';

// 원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 변환된다.
console.log(str.length); // 2
console.log(str.toUpperCase()); // HI

// 래퍼 객체로 프로퍼티에 접근하거나 메서드를 호출한 후, 다시 원시값으로 되돌린다.
console.log(typeof str); // string</code></pre>
<h5 id="이때-문자열-래퍼-객체인-string-생성자-함수의-인스턴스는-stringprototype의-메서드를-상속받아-사용할-수-있다">이때 문자열 래퍼 객체인 String 생성자 함수의 인스턴스는 String.prototype의 메서드를 상속받아 사용할 수 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3c4faefc-8c71-4726-96bf-daeae0d91393/image.png" /></p>
<h5 id="그-후-래퍼-객체의-처리가-종료되면-래퍼-객체의-stringdata-내부-슬롯에-할당된-원시값으로-원래의-상태-즉-식별자가-원시값을-갖도록-되돌리고-래퍼-객체는-가비지-컬렉션의-대상이-된다">그 후 래퍼 객체의 처리가 종료되면 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된 원시값으로 원래의 상태, 즉 식별자가 원시값을 갖도록 되돌리고 래퍼 객체는 가비지 컬렉션의 대상이 된다.</h5>
<pre><code class="language-js">// ① 식별자 str은 문자열을 값으로 가지고 있다.
const str = 'hello';

// ② 식별자 str은 암묵적으로 생성된 래퍼 객체를 가리킨다.
// 식별자 str의 값 'hello'는 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된다.
// 래퍼 객체에 name 프로퍼티가 동적 추가된다.
str.name = 'Lee';

// ③ 식별자 str은 다시 원래의 문자열, 즉 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된 원시값을 갖는다.
// 이때 ②에서 생성된 래퍼 객체는 아무도 참조하지 않는 상태이므로 가비지 컬렉션의 대상이 된다.

// ④ 식별자 str은 새롭게 암묵적으로 생성된(②에서 생성된 래퍼 객체와는 다른) 래퍼 객체를 가리킨다.
// 새롭게 생성된 래퍼 객체에는 name 프로퍼티가 존재하지 않는다.
console.log(str.name); // undefined

// ⑤ 식별자 str은 다시 원래의 문자열, 즉 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된 원시값을 갖는다.
// 이때 ④에서 생성된 래퍼 객체는 아무도 참조하지 않는 상태이므로 가비지 컬렉션의 대상이 된다.
console.log(typeof str, str);</code></pre>
<h5 id="문자열-뿐만-아니라-숫자불리언심벌-역시-암묵적으로-생성되는-래퍼객체에-의해-마치-객체처럼-사용할-수-있으며-표준-빌트인-객체인-string-number-boolean-symbol의-프로토타입-메서드-또는-프로퍼티는-참조할-수-있다">문자열 뿐만 아니라 숫자,불리언,심벌 역시 암묵적으로 생성되는 래퍼객체에 의해 마치 객체처럼 사용할 수 있으며 표준 빌트인 객체인 String, Number, Boolean, Symbol의 프로토타입 메서드 또는 프로퍼티는 참조할 수 있다.</h5>
<h5 id="따라서-string-number-boolean-생성자-함수를-new-연산자와-함께-호출하여-문자열-숫자-불리언-인스턴스를-생성할-필요가-없으며-권장하지도-않는다">따라서 String, Number, Boolean 생성자 함수를 new 연산자와 함께 호출하여 문자열, 숫자, 불리언 인스턴스를 생성할 필요가 없으며 권장하지도 않는다.</h5>
<h3 id="214-전역-객체">21.4 전역 객체</h3>
<h5 id="전역-객체는-코드가-실행되기-이전-단계에-자바스크립트-엔진에-의해-어떤-객체보다도-먼저-생성되는-특수-객체이며-어떤-객체에도-속하지-않은-최상위-객체다">전역 객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수 객체이며 어떤 객체에도 속하지 않은 최상위 객체다</h5>
<h5 id="전역-객체는-계층적-구조상-어떤-객체에도-속하지-않은-모든-빌트인-객체의-최상위-객체다">전역 객체는 계층적 구조상 어떤 객체에도 속하지 않은 모든 빌트인 객체의 최상위 객체다.</h5>
<h5 id="전역-객체-자신은-어떤-객체의-프로퍼티도-아니며-객체의-계층적-구조상-표준-빌트인-객체와-호스트-객체를-프로퍼티로-소유한다">전역 객체 자신은 어떤 객체의 프로퍼티도 아니며 객체의 계층적 구조상 표준 빌트인 객체와 호스트 객체를 프로퍼티로 소유한다.</h5>
<h5 id="전역-객체의-특징은-다음과-같다">전역 객체의 특징은 다음과 같다.</h5>
<ul style="font-size: 17px;">
<li> 개발자가 의도적으로 생성할 수 없다. 즉, 전역 객체를 생성할 수 있는 생성자 함수가 제공되지 않는다.
  <li> 전역 객체의 프로퍼티를 참조할 때 window를 생략 가능하다.


<pre><code class="language-js">// 문자열 'F'를 16진수로 해석하여 10진수로 변환하여 반환한다.
window.parseInt('F', 16); // -&gt; 15
// window.parseInt는 parseInt로 호출할 수 있다.
parseInt('F', 16); // -&gt; 15

window.parseInt === parseInt; // -&gt; true</code></pre>
<li>전역 객체는 Object, String, Number, Boolean, Function, Array, RegExp, Math, Promise 같은 모든 표준 빌트인 객체를 프로퍼티로 가지고 있다.
<li>브라우저 환경에서는DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Component, Web Worker 같은 클라이언트 사이드 Web API를 Node.js 환경에서는 Node.js 고유의 API를 호스트 객체로 제공한다. 
<li> var 키워드로 선언한 전역 변수와 선언하지 않은 변수에 값을 할당한 암묵적 전역과 전역 함수는 전역 객체의 프로퍼티가 된다.


<pre><code class="language-js">  // var 키워드로 선언한 전역 변수
var foo = 1;
console.log(window.foo); // 1

// 선언하지 않은 변수에 값을 암묵적 전역. bar는 전역 변수가 아니라 전역 객체의 프로퍼티다.
bar = 2; // window.bar = 2
console.log(window.bar); // 2

// 전역 함수
function baz() { return 3; }
console.log(window.baz()); // 3</code></pre>
<li>let이나 const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니라 window.foo와 같이 접근 불가하다.
let이나 const 키워드로 선언한 전역 변수는 보이지 않는 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드) 내에 존재하게 된다.

<pre><code class="language-js"> let foo = 123;
console.log(window.foo); // undefined </code></pre>
<li>브라우저 환경의 모든 자바스크립트 코드는 script 태그를 통해 분리되어 있어도 하나의 전역 객체 window를 공유한다.
</ul>

<h5 id="전역객체의-프로퍼티와-메서드는-전역-객체를-가리키는-식별자-즉-window나-global을-생략하여-참조호출할-수-있으므로-전역-변수와-전역-함수처럼-사용할-수-있다">전역객체의 프로퍼티와 메서드는 전역 객체를 가리키는 식별자 즉, window나 global을 생략하여 참조/호출할 수 있으므로 전역 변수와 전역 함수처럼 사용할 수 있다.</h5>
<h4 id="2141-빌트인-전역-프로퍼티">21.4.1 빌트인 전역 프로퍼티</h4>
<h5 id="빌트인-전역-프로퍼티는-전역-객체의-프로퍼티를-의미한다">빌트인 전역 프로퍼티는 전역 객체의 프로퍼티를 의미한다.</h5>
<h5 id="1-infinity">1) Infinity</h5>
<h5 id="infinity-프로퍼티는-무한대를-나타내는-숫자값-infinity를-갖는다">Infinity 프로퍼티는 무한대를 나타내는 숫자값 Infinity를 갖는다.</h5>
<pre><code class="language-js">// 전역 프로퍼티는 window를 생략하고 참조할 수 있다.
console.log(window.Infinity === Infinity); // true

// 양의 무한대
console.log(3/0);  // Infinity
// 음의 무한대
console.log(-3/0); // -Infinity
// Infinity는 숫자값이다.
console.log(typeof Infinity); // number</code></pre>
<h5 id="2-nan">2) NaN</h5>
<h5 id="nan-프로퍼티는-숫자가-아님not-a-number을-나타내는-숫자값-nan을-갖는다">NaN 프로퍼티는 숫자가 아님(not-a-number)을 나타내는 숫자값 NaN을 갖는다.</h5>
<pre><code class="language-js">console.log(window.NaN); // NaN

console.log(Number('xyz')); // NaN
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number</code></pre>
<h5 id="3-undefined">3) undefined</h5>
<h5 id="undefined-프로퍼티는-원시타입-undefined를-값으로-갖는다">undefined 프로퍼티는 원시타입 undefined를 값으로 갖는다.</h5>
<pre><code class="language-js">console.log(window.undefined); // undefined

var foo;
console.log(foo); // undefined
console.log(typeof undefined); // undefined</code></pre>
<h4 id="2142-빌트인-전역-함수">21.4.2 빌트인 전역 함수</h4>
<h5 id="빌트인-전역-함수는-애플리케이션-전역에서-호출할-수-있는-빌트인-함수로서-전역-객체의-메서드다">빌트인 전역 함수는 애플리케이션 전역에서 호출할 수 있는 빌트인 함수로서 전역 객체의 메서드다.</h5>
<h5 id="1-eval">1) eval</h5>
<h5 id="eval-함수는-자바스크립트-코드를-나타내는-문자열을-인수로-전달받는다">eval 함수는 자바스크립트 코드를 나타내는 문자열을 인수로 전달받는다.</h5>
<pre><code class="language-js">/**
 * 주어진 문자열 코드를 런타임에 평가 또는 실행한다.
 * @param {string} code - 코드를 나타내는 문자열
 * @returns {*} 문자열 코드를 평가/실행한 결과값
 */
eval(code)</code></pre>
<pre><code class="language-js">// 표현식인 문
eval('1 + 2;'); // -&gt; 3
// 표현식이 아닌 문
eval('var x = 5;'); // -&gt; undefined

// eval 함수에 의해 런타임에 변수 선언문이 실행되어 x 변수가 선언되었다.
console.log(x); // 5

// 객체 리터럴은 반드시 괄호로 둘러싼다.
const o = eval('({ a: 1 })');
console.log(o); // {a: 1}

// 함수 리터럴은 반드시 괄호로 둘러싼다.
const f = eval('(function() { return 1; })');
console.log(f()); // 1</code></pre>
<h5 id="전달받은-문자열-코드가-여러개의-문이면-마지막-결과값을-반환한다">전달받은 문자열 코드가 여러개의 문이면 마지막 결과값을 반환한다.</h5>
<pre><code class="language-js">eval('1+2; 3+4'); //7</code></pre>
<blockquote>
<p>eval 함수는 자신이 호출된 위치에 해당하는 기존의 스코프를 런타임에 동적으로 수정한다.</p>
</blockquote>
<pre><code class="language-js">const x = 1;

function foo() {
  // eval 함수는 런타임에 foo 함수의 스코프를 동적으로 수정한다.
  eval('var x = 2;');
  console.log(x); // 2
}

foo();
console.log(x); // 1</code></pre>
<h5 id="인수로-전달받은-문자열-코드가-let-const-키워드를-사용한-변수-선언문이라면-암묵적으로-strict-mode가-적용된다">인수로 전달받은 문자열 코드가 let, const 키워드를 사용한 변수 선언문이라면 암묵적으로 strict mode가 적용된다.</h5>
<pre><code class="language-js">const x = 1;

function foo() {
  eval('var x = 2; console.log(x);'); // 2
  // let, const 키워드를 사용한 변수 선언문은 strict mode가 적용된다.
  eval('const x = 3; console.log(x);'); // 3
  console.log(x); // 2
}

foo();
console.log(x); // 1</code></pre>
<blockquote>
<p>eval 함수는 보안에 매우 취약하고 코드 실행에 비해 처리 속도가 느리다. 따라서 eval 함수의 사용은 권장되지 않는다.</p>
</blockquote>
<h5 id="1-isfinite">1) isFinite</h5>
<h5 id="전달받은-인수가-유한수이며-true르-무한수이면-false를-반환하고-숫자-타입이-아니면-숫자로-타입을-변경하고-nan이면-false를-반환한다">전달받은 인수가 유한수이며 true르 무한수이면 false를 반환하고 숫자 타입이 아니면 숫자로 타입을 변경하고 NaN이면 false를 반환한다</h5>
<pre><code class="language-js">/**
 * 전달받은 인수가 유한수인지 확인하고 그 결과를 반환한다.
 * @param {number} testvalue - 검사 대상 값
 * @returns {boolean} 유한수 여부 확인 결과
 */
isFinite (testvalue)</code></pre>
<pre><code class="language-js">// 인수가 유한수이면 true를 반환한다.
isFinite(0);    // -&gt; true
isFinite(2e64); // -&gt; true
isFinite('10'); // -&gt; true: '10' → 10
isFinite(null); // -&gt; true: null → 0

// 인수가 무한수 또는 NaN으로 평가되는 값이라면 false를 반환한다.
isFinite(Infinity);  // -&gt; false
isFinite(-Infinity); // -&gt; false

// 인수가 NaN으로 평가되는 값이라면 false를 반환한다.
isFinite(NaN);     // -&gt; false
isFinite('Hello'); // -&gt; false
isFinite('2005/12/12'); // -&gt; false</code></pre>
<h5 id="2-isnan">2) isNaN</h5>
<h5 id="전달받은-인수가-nan인지-검사하여-그-결과를-불리언-타입으로-반화한다-숫자타입이-아닐경우-숫자로-타입을-변화한-후-검사를-수행한다">전달받은 인수가 NaN인지 검사하여 그 결과를 불리언 타입으로 반화한다. 숫자타입이 아닐경우 숫자로 타입을 변화한 후 검사를 수행한다.</h5>
<pre><code class="language-js">/**
 * 전달받은 숫자가 NaN인지 확인하고 그 결과를 반환한다.
 * @param {number} testvalue - 검사 대상 값
 * @returns {boolean} NaN 여부 확인 결과
 */
isNaN (testvalue)</code></pre>
<pre><code class="language-js">// 숫자
isNaN(NaN); // -&gt; true
isNaN(10);  // -&gt; false

// 문자열
isNaN('blabla'); // -&gt; true: 'blabla' =&gt; NaN
isNaN('10');     // -&gt; false: '10' =&gt; 10
isNaN('10.12');  // -&gt; false: '10.12' =&gt; 10.12
isNaN('');       // -&gt; false: '' =&gt; 0
isNaN(' ');      // -&gt; false: ' ' =&gt; 0

// 불리언
isNaN(true); // -&gt; false: true → 1
isNaN(null); // -&gt; false: null → 0

// undefined
isNaN(undefined); // -&gt; true: undefined =&gt; NaN

// 객체
isNaN({}); // -&gt; true: {} =&gt; NaN

// date
isNaN(new Date());            // -&gt; false: new Date() =&gt; Number
isNaN(new Date().toString()); // -&gt; true:  String =&gt; NaN</code></pre>
<h5 id="3-parsefloat">3) parseFloat</h5>
<h5 id="전달받은-문자열-인수를-부동-소수점-숫자-즉-실수로-해석하여-반환한다">전달받은 문자열 인수를 부동 소수점 숫자, 즉 실수로 해석하여 반환한다.</h5>
<pre><code class="language-js">/**
 * 전달받은 문자열 인수를 실수로 해석하여 반환한다.
 * @param {string} String - 검사 대상 값
 * @returns {number} 변환 결과
 */
parseFloat (string)</code></pre>
<pre><code class="language-js">// 문자열을 실수로 해석하여 반환한다.
parseFloat('3.14');  // -&gt; 3.14
parseFloat('10.00'); // -&gt; 10

// 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
parseFloat('34 45 66'); // -&gt; 34
parseFloat('40 years'); // -&gt; 40

// 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
parseFloat('He was 40'); // -&gt; NaN

// 앞뒤 공백은 무시된다.
parseFloat(' 60 '); // -&gt; 60</code></pre>
<h5 id="4-parseint">4) parseInt</h5>
<h5 id="전달받은-문자열-인수를-정수로-해석하여-반환한다">전달받은 문자열 인수를 정수로 해석하여 반환한다.</h5>
<pre><code class="language-js">/**
 * 전달받은 문자열 인수를 정수로 해석하여 반환한다.
 * @param {string} String - 변환 대상 값
 * @param {number} [radix] - 진법을 나타내는 기수(2 ~ 36, 기본값 10)
 * @returns {number} 변환 결과
 */
parseInt (string, radix);</code></pre>
<pre><code class="language-js">// 문자열을 정수로 해석하여 반환한다.
parseInt('10');     // -&gt; 10
parseInt('10.123'); // -&gt; 10</code></pre>
<h5 id="문자열이-아니면-문자열로-반환한-다음-정수로-해석하여-반환한다">문자열이 아니면 문자열로 반환한 다음 정수로 해석하여 반환한다.</h5>
<pre><code class="language-js">parseInt(10);     // -&gt; 10
parseInt(10.123); // -&gt; 10</code></pre>
<h5 id="두-번째-인수로-진법을-나타내는-기수를-전달할-수-있다-첫-번째-인수로-전달된-문자열을-해당-기수의-숫자로-해석하여-반환하며-이때-반환값은-언제나-10진수이다">두 번째 인수로 진법을 나타내는 기수를 전달할 수 있다. 첫 번째 인수로 전달된 문자열을 해당 기수의 숫자로 해석하여 반환하며 이때 반환값은 언제나 10진수이다.</h5>
<pre><code class="language-js">// 10'을 10진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10'); // -&gt; 10
// '10'을 2진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 2); // -&gt; 2
// '10'을 8진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 8); // -&gt; 8
// '10'을 16진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 16); // -&gt; 16</code></pre>
<h5 id="기수를-지정하여-10진수-숫자를-해당-기수의-문자열로-반환하여-반환하고-싶을-때는-numberprototypetostring-메서드를-사용한다">기수를 지정하여 10진수 숫자를 해당 기수의 문자열로 반환하여 반환하고 싶을 때는 Number.prototype.toString 메서드를 사용한다.</h5>
<pre><code class="language-js">const x = 15;

// 10진수 15를 2진수로 변환하여 그 결과를 문자열로 반환한다.
x.toString(2); // -&gt; '1111'
// 문자열 '1111'을 2진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt(x.toString(2), 2); // -&gt; 15

// 10진수 15를 8진수로 변환하여 그 결과를 문자열로 반환한다.
x.toString(8); // -&gt; '17'
// 문자열 '17'을 8진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt(x.toString(8), 8); // -&gt; 15

// 10진수 15를 16진수로 변환하여 그 결과를 문자열로 반환한다.
x.toString(16); // -&gt; 'f'
// 문자열 'f'를 16진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt(x.toString(8), 8); // -&gt; 15

// 숫자값을 문자열로 변환한다.
x.toString(); // -&gt; '15'
// 문자열 '15'를 10진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt(x.toString()); // -&gt; 15</code></pre>
<h5 id="두-번째-인수로-진법을-나타내는-기수를-지정하지-않더라도-첫-번째-인수가-0x-또는-0x로-시작하는-16진수-리터럴이면-16진수로-해석하여-10진수-정수로-반환한다">두 번째 인수로 진법을 나타내는 기수를 지정하지 않더라도 첫 번째 인수가 '0x' 또는 '0X'로 시작하는 16진수 리터럴이면 16진수로 해석하여 10진수 정수로 반환한다.</h5>
<pre><code class="language-js">// 16진수 리터럴 '0xf'를 16진수로 해석하고 10진수 정수로 그 결과를 반환한다.
parseInt('0xf'); // -&gt; 15
// 위 코드와 같다.
parseInt('f', 16); // -&gt; 15</code></pre>
<h5 id="2진수-리터럴과-8진수-리터럴은-제대로-해석하지-못한다">2진수 리터럴과 8진수 리터럴은 제대로 해석하지 못한다.</h5>
<pre><code class="language-js">// 2진수 리터럴(0b로 시작)은 제대로 해석하지 못한다. 0 이후가 무시된다.
parseInt('0b10'); // -&gt; 0
// 8진수 리터럴(ES6에서 도입. 0o로 시작)은 제대로 해석하지 못한다. 0 이후가 무시된다.
parseInt('0o10'); // -&gt; 0</code></pre>
<h5 id="문자열을-8진수로-해석하려면-지수를-반드시-지정해야-한다">문자열을 8진수로 해석하려면 지수를 반드시 지정해야 한다.</h5>
<pre><code class="language-js">// 문자열 '10'을 2진수로 해석한다.
parseInt('10', 2); // -&gt; 2
// 문자열 '10'을 8진수로 해석한다.
parseInt('10', 8); // -&gt; 8</code></pre>
<h5 id="첫-번째-인수로-전달한-문자열의-첫-번째-문자가-해당-지수의-숫자로-반환될-수-없다면-nan을-반환한다">첫 번째 인수로 전달한 문자열의 첫 번째 문자가 해당 지수의 숫자로 반환될 수 없다면 NaN을 반환한다.</h5>
<pre><code class="language-js">// 'A'는 10진수로 해석할 수 없다.
parseInt('A0'); // -&gt; NaN
// '2'는 2진수로 해석할 수 없다.
parseInt('20', 2); // -&gt; NaN</code></pre>
<h5 id="첫-번째-인수로-전달한-문자열의-두-번째-문자부터-해당-진수를-나타내는-숫자가-아닌-문자ex-2진수의-경우-2와-마주치면-이-문자와-계속되는-문자들은-전부-무시되며-해석된-정수값만-반환한다">첫 번째 인수로 전달한 문자열의 두 번째 문자부터 해당 진수를 나타내는 숫자가 아닌 문자(ex 2진수의 경우 2)와 마주치면 이 문자와 계속되는 문자들은 전부 무시되며 해석된 정수값만 반환한다.</h5>
<pre><code class="language-js">// 10진수로 해석할 수 없는 'A' 이후의 문자는 모두 무시된다.
parseInt('1A0'); // -&gt; 1
// 2진수로 해석할 수 없는 '2' 이후의 문자는 모두 무시된다.
parseInt('102', 2); // -&gt; 2
// 8진수로 해석할 수 없는 '8' 이후의 문자는 모두 무시된다.
parseInt('58', 8); // -&gt; 5
// 16진수로 해석할 수 없는 'G' 이후의 문자는 모두 무시된다.
parseInt('FG', 16); // -&gt; 15</code></pre>
<h5 id="첫-번째-인수-문자열에-공백이-있다면-첫-번째-문자열만-해석하여-반환한다">첫 번째 인수 문자열에 공백이 있다면 첫 번째 문자열만 해석하여 반환한다.</h5>
<pre><code class="language-js">// 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
parseInt('34 45 66'); // -&gt; 34
parseInt('40 years'); // -&gt; 40
// 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
parseInt('He was 40'); // -&gt; NaN
// 앞뒤 공백은 무시된다.
parseInt(' 60 '); // -&gt; 60</code></pre>
<h5 id="5-encodeuri--decodeuri">5) encodeURI / decodeURI</h5>
<h5 id="완전한-uri를-문자열로-전달받아-이스케이프-처리를-위해-인코딩한다">완전한 URI를 문자열로 전달받아 이스케이프 처리를 위해 인코딩한다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/d8f8e233-5218-415d-bcf6-9aa4a61bda31/image.png" /></p>
<pre><code class="language-js">/**
 * 완전한 URI를 문자열로 전달받아 이스케이프 처리를 위해 인코딩한다.
 * @param {string} uri - 완전한 URI
 * @returns {string} 인코딩된 URI
 */
encodeURI (uri)</code></pre>
<h5 id="인코딩이란-uri의-문자들을-이스케이프-처리하는-것을-의미한다">인코딩이란 URI의 문자들을 이스케이프 처리하는 것을 의미한다.</h5>
<h5 id="아스키-문자-셋에-정의되지-않은-특수-문자들을-이스케이프-처리하여-야기될-수-있는-문제를-예방하기-위해-이스케이프-처리가-필요하다">아스키 문자 셋에 정의되지 않은 특수 문자들을 이스케이프 처리하여 야기될 수 있는 문제를 예방하기 위해 이스케이프 처리가 필요하다.</h5>
<h5 id="단-알파벳-09의-숫자----_--------문자는-이스케이프-처리에서-제외된다">단, 알파벳, 0~9의 숫자,  - _ . ! ~ * ' ( ) 문자는 이스케이프 처리에서 제외된다.</h5>
<pre><code class="language-js">// 완전한 URI
const uri = 'http://example.com?name=이웅모&amp;job=programmer&amp;teacher';

// encodeURI 함수는 완전한 URI를 전달받아 이스케이프 처리를 위해 인코딩한다.
const enc = encodeURI(uri);
console.log(enc);
// http://example.com?name=%EC%9D%B4%EC%9B%85%EB%AA%A8&amp;job=programmer&amp;teacher</code></pre>
<h5 id="decodeuri-함수는-인코딩된-uri를-인수로-전달받아-이스케이프-처리-이전으로-디코딩한다">decodeURI 함수는 인코딩된 URI를 인수로 전달받아 이스케이프 처리 이전으로 디코딩한다.</h5>
<pre><code class="language-js">/**
* 인코딩된 URI를 전달받아 이스케이프 처리 이전으로 디코딩한다 
* @param {string} encodedURI - 인코딩된 URI
* @returns {string} 디코딩된 URI
*/
decodeURI(encodedURI)</code></pre>
<pre><code class="language-js">const uri = 'http://example.com?name=이웅모&amp;job=programmer&amp;teacher';

// encodeURI 함수는 완전한 URI를 전달받아 이스케이프 처리를 위해 인코딩한다.
const enc = encodeURI(uri);
console.log(enc);
// http://example.com?name=%EC%9D%B4%EC%9B%85%EB%AA%A8&amp;job=programmer&amp;teacher

// decodeURI 함수는 인코딩된 완전한 URI를 전달받아 이스케이프 처리 이전으로 디코딩한다.
const dec = decodeURI(enc);
console.log(dec);
// http://example.com?name=이웅모&amp;job=programmer&amp;teacher</code></pre>
<h5 id="6-encodeuricomponent--decodeuricomponent">6) encodeURIComponent / decodeURIComponent</h5>
<h5 id="encodeuricomponent-함수는-uri-구성-요소를-인수로-전달받아-인코딩한다">encodeURIComponent 함수는 URI 구성 요소를 인수로 전달받아 인코딩한다.</h5>
<pre><code class="language-js">/**
 * URI의 구성요소를 전달받아 이스케이프 처리를 위해 인코딩한다.
 * @param {string} uriComponent - URI의 구성요소
 * @returns {string} 인코딩된 URI의 구성요소
 */
encodeURIComponent (uriComponent)

/**
 * 인코딩된 URI의 구성요소를 전달받아 이스케이프 처리 이전으로 디코딩한다.
 * @param {string} encodeURIComponent - 인코딩된 URI의 구성요소
 * @returns {string} 디코딩된 URI의 구성요소
 */
decodeURIComponent (encodeURIComponent)</code></pre>
<h5 id="encodeuricomponent는-쿼리스트링-구분자로-사용되는-까지-인코딩-하지만-encodeuri는-쿼리스트링-구분자는-인코딩-하지-않는다">encodeURIComponent는 쿼리스트링 구분자로 사용되는 =,?,&amp;까지 인코딩 하지만 encodeURI는 쿼리스트링 구분자는 인코딩 하지 않는다.</h5>
<pre><code class="language-js">// URI의 쿼리 스트링
const uriComp = 'name=이웅모&amp;job=programmer&amp;teacher';

// encodeURIComponent 함수는 인수로 전달받은 문자열을 URI의 구성요소인 쿼리 스트링의 일부로 간주한다.
// 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &amp;까지 인코딩한다.
let enc = encodeURIComponent(uriComp);
console.log(enc);
// name%3D%EC%9D%B4%EC%9B%85%EB%AA%A8%26job%3Dprogrammer%26teacher

let dec = decodeURIComponent(enc);
console.log(dec);
// 이웅모&amp;job=programmer&amp;teacher

// encodeURI 함수는 인수로 전달받은 문자열을 완전한 URI로 간주한다.
// 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &amp;를 인코딩하지 않는다.
enc = encodeURI(uriComp);
console.log(enc);
// name=%EC%9D%B4%EC%9B%85%EB%AA%A8&amp;job=programmer&amp;teacher

dec = decodeURI(enc);
console.log(dec);
// name=이웅모&amp;job=programmer&amp;teacher</code></pre>
<h4 id="2143-암묵적-전역">21.4.3 암묵적 전역</h4>
<pre><code class="language-js">var x = 10; // 전역 변수

function foo () {
  // 선언하지 않은 식별자에 값을 할당
  y = 20; // window.y = 20;
}
foo();

// 선언하지 않은 식별자 y를 전역에서 참조할 수 있다.
console.log(x + y); // 30</code></pre>
<h5 id="선언하지-않은-식별자-y는-마치-선언된-전역-변수처럼-동작한다-이는-선언하지-않은-식별자에-값을-할당하면-전역-객체의-프로퍼티가-되기-때문이다">선언하지 않은 식별자 y는 마치 선언된 전역 변수처럼 동작한다. 이는 선언하지 않은 식별자에 값을 할당하면 전역 객체의 프로퍼티가 되기 때문이다.</h5>
<h5 id="자바스크립트-엔진은-y20을-windowy20으로-해석하여-전역-객체에-프로퍼티를-동적으로-생성한다-결국">자바스크립트 엔진은 y=20을 window.y=20으로 해석하여 전역 객체에 프로퍼티를 동적으로 생성한다. 결국</h5>
<blockquote>
<p>y는 전역 객체의 프로퍼티가 되어 마치 전역 변수처럼 동작하는데 이러한 현상을 암묵적 전역이라 한다.</p>
</blockquote>
<h5 id="y는-변수-선언-없이-단지-전역-객체의-프로퍼티로-추가되었을-뿐이기-때문에-변수가-아니고-그로인해-호이스팅이-발생하지-않는다">y는 변수 선언 없이 단지 전역 객체의 프로퍼티로 추가되었을 뿐이기 때문에 변수가 아니고 그로인해 호이스팅이 발생하지 않는다.</h5>
<pre><code class="language-js">// 전역 변수 x는 호이스팅이 발생한다.
console.log(x); // undefined
// 전역 변수가 아니라 단지 전역 객체의 프로퍼티인 y는 호이스팅이 발생하지 않는다.
console.log(y); // ReferenceError: y is not defined

var x = 10; // 전역 변수

function foo () {
  // 선언하지 않은 식별자에 값을 할당
  y = 20; // window.y = 20;
}
foo();

// 선언하지 않은 식별자 y를 전역에서 참조할 수 있다.
console.log(x + y); // 30</code></pre>
<h5 id="또한-변수가-아니라서-delete-연산자로-삭제할-수-있다">또한 변수가 아니라서 delete 연산자로 삭제할 수 있다</h5>
<pre><code class="language-js">var x = 10; // 전역 변수

function foo () {
  // 선언하지 않은 식별자에 값을 할당
  y = 20; // window.y = 20;
  console.log(x + y);
}

foo(); // 30

console.log(window.x); // 10
console.log(window.y); // 20

delete x; // 전역 변수는 삭제되지 않는다.
delete y; // 프로퍼티는 삭제된다.

console.log(window.x); // 10
console.log(window.y); // undefined</code></pre>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/21.md">wikibooks</a></p>