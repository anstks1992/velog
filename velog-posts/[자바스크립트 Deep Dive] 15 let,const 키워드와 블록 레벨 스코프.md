<h2 id="15-letconst-키워드와-블록-레벨-스코프">15. let,const 키워드와 블록 레벨 스코프</h2>
<hr />
<h3 id="151-var-키워드로-선언한-변수의-문제점">15.1 var 키워드로 선언한 변수의 문제점</h3>
<h4 id="1511-변수-중복-선언-허용">15.1.1 변수 중복 선언 허용</h4>
<h5 id="var-변수는-중복-선언이-허용되는데-이-경우-먼저-선언된-변수값이-의도치-않게-변경되는-부작용이-발생-할-수-있다">var 변수는 중복 선언이 허용되는데 이 경우 먼저 선언된 변수값이 의도치 않게 변경되는 부작용이 발생 할 수 있다.</h5>
<pre><code class="language-js">var x = 1;
var y = 1;

// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var x = 100;
// 초기화문이 없는 변수 선언문은 무시된다.
var y;

console.log(x); // 100
console.log(y); // 1</code></pre>
<h4 id="1512-함수-레벨-스코프">15.1.2 함수 레벨 스코프</h4>
<h5 id="var-변수는-오로지-함수의-코드-블록만을-지역-스코프로-인정한다-따라서-함수-외부에서-var-선언한-변수는-코드-블록-내에서-선언해도-모두-전역-변수가-된다">var 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 따라서 함수 외부에서 var 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다.</h5>
<pre><code class="language-js">var x = 1;

if (true) {
  // x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
  // 이는 의도치 않게 변수값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10</code></pre>
<pre><code class="language-js">var i = 10;

// for문에서 선언한 i는 전역 변수이다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i &lt; 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 i 변수의 값이 변경되었다.
console.log(i); // 5</code></pre>
<h4 id="1513-변수-호이스팅">15.1.3 변수 호이스팅</h4>
<h5 id="var-키워드로-변수를-선언하면-변수-호이스팅에-의해-변수-선언문이-스코프의-선두로-끌어-올려진-것처럼-동작한다">var 키워드로 변수를 선언하면 변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어 올려진 것처럼 동작한다.</h5>
<pre><code class="language-js">// 이 시점에는 변수 호이스팅에 의해 이미 foo 변수가 선언되었다(1. 선언 단계)
// 변수 foo는 undefined로 초기화된다. (2. 초기화 단계)
console.log(foo); // undefined

// 변수에 값을 할당(3. 할당 단계)
foo = 123;

console.log(foo); // 123

// 변수 선언은 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 실행된다.
var foo;</code></pre>
<h3 id="152-let-키워드">15.2 let 키워드</h3>
<h4 id="1521-변수-중복-선언-금지">15.2.1 변수 중복 선언 금지</h4>
<h5 id="var와-달리-let은-같은-이름으로-변수를-중복-선언하면-문법에러가-발생한다">var와 달리 let은 같은 이름으로 변수를 중복 선언하면 문법에러가 발생한다.</h5>
<pre><code class="language-js">var foo = 123;
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var foo = 456;

let bar = 123;
// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared</code></pre>
<h4 id="1522-블록-레벨-스코프">15.2.2 블록 레벨 스코프</h4>
<h5 id="함수의-코드-블록만을-지역-스코프로-인정하던-var와-달리-let은-모든-코드-블록을-지역-스코프로-인정하는-블록-레벨-스코프를-가진다">함수의 코드 블록만을 지역 스코프로 인정하던 var와 달리 let은 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 가진다.</h5>
<pre><code class="language-js">let foo = 1; // 전역 변수

{
  let foo = 2; // 지역 변수
  let bar = 3; // 지역 변수
}

console.log(foo); // 1
console.log(bar); // ReferenceError: bar is not defined</code></pre>
<h4 id="1523-변수-호이스팅">15.2.3 변수 호이스팅</h4>
<h5 id="let은-변수-호이스팅이-발생하지-않는-것처럼-동작한다">let은 변수 호이스팅이 발생하지 않는 것처럼 동작한다.</h5>
<pre><code class="language-js">console.log(foo); // ReferenceError: foo is not defined
let foo;</code></pre>
<h5 id="var는-런타임-이전에-선언-단계와-초기화-단계가-한번에-진행된다-초기화-단계에-undefined로-변수를-초기화-하기-때문에-선언문-이전에-변수에-접근해도-에러가-발생하지-않는다">var는 런타임 이전에 '선언 단계'와 '초기화 단계'가 한번에 진행된다. 초기화 단계에 undefined로 변수를 초기화 하기 때문에 선언문 이전에 변수에 접근해도 에러가 발생하지 않는다.</h5>
<pre><code class="language-js">// var 키워드로 선언한 변수는 런타임 이전에 선언 단계와 초기화 단계가 실행된다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 있다.
console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1</code></pre>
<blockquote>
<h5 id="var-생명주기br">var 생명주기<br /></h5>
<p>선언단계 + 초기화단계(foo===undefined) 
⬇ 
런타임
⬇
할당 단계(foo ===1)</p>
</blockquote>
<blockquote>
<p>let 키워드는 var와 달리 '선언 단계'와 '초기화 단계'가 분리되어 진행된다.</p>
</blockquote>
<pre><code class="language-js">// 런타임 이전에 선언 단계가 실행된다. 아직 변수가 초기화되지 않았다.
// 초기화 이전의 일시적 사각 지대에서는 변수를 참조할 수 없다.
console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1</code></pre>
<blockquote>
<h5 id="let-생명주기">let 생명주기</h5>
<p>선언단계
⬇
일시적 사각지대(TDZ) : 스코프의 시작부터 초기화 단계 시작까지 변수 참조 불가
⬇ 
초기화단계(foo === undefined)(선언문 단계에서)
⬇
할당 단계(foo === 1)</p>
</blockquote>
<h4 id="1524-전역-객체와-let">15.2.4 전역 객체와 let</h4>
<h5 id="var키워드와-달리-let-키워드로-선언한-변수는-전역-객체의-프로퍼티가-아니다">var키워드와 달리 let 키워드로 선언한 변수는 전역 객체의 프로퍼티가 아니다.</h5>
<pre><code class="language-js">// 이 예제는 브라우저 환경에서 실행해야 한다.

// 전역 변수
var x = 1;
// 암묵적 전역
y = 2;
// 전역 함수
function foo() {}

// var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티다.
console.log(window.x); // 1
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(x); // 1

// 암묵적 전역은 전역 객체 window의 프로퍼티다.
console.log(window.y); // 2
console.log(y); // 2

// 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티다.
console.log(window.foo); // ƒ foo() {}
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(foo); // ƒ foo() {}</code></pre>
<pre><code class="language-js">// 이 예제는 브라우저 환경에서 실행해야 한다.
let x = 1;

// let, const 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아니다.
console.log(window.x); // undefined
console.log(x); // 1</code></pre>
<h3 id="153-const-키워드">15.3 const 키워드</h3>
<h4 id="1531-선언과-초기화">15.3.1 선언과 초기화</h4>
<blockquote>
<p>const 변수는 반드시 선언과 동시에 초기화해야 한다.</p>
</blockquote>
<pre><code class="language-js">const foo; // SyntaxError: Missing initializer in const declaration</code></pre>
<h4 id="1532-재할당-금지">15.3.2 재할당 금지</h4>
<blockquote>
<p>var, let과 달리 const 변수는 재할당이 금지된다.</p>
</blockquote>
<pre><code class="language-js">const foo =1;
foo =2;</code></pre>
<h4 id="1533-상수">15.3.3 상수</h4>
<blockquote>
<p>const 변수에 원시 값을 할당한 경우 원시 값은 변경할 수 없는 값이고 const 키워드에 의해 재할당이 금지되므로 할당된 값을 변경할 수 있는 방법은 없다.</p>
</blockquote>
<h4 id="1534-const-키워드와-객체">15.3.4 const 키워드와 객체</h4>
<blockquote>
<p>const 변수에 객체를 할당한 경우 값을 변경할 수 있다.</p>
</blockquote>
<pre><code class="language-js">const person = {
  name: 'Lee'
};

// 객체는 변경 가능한 값이다. 따라서 재할당없이 변경이 가능하다.
person.name = 'Kim';

console.log(person); // {name: &quot;Kim&quot;}</code></pre>
<h4 id="1534-var-vs-let-vs-const">15.3.4 var vs let vs const</h4>
<table>
<thead>
<tr>
<th></th>
<th>var</th>
<th>let</th>
<th>const</th>
</tr>
</thead>
<tbody><tr>
<td>재할당</td>
<td>o</td>
<td>o</td>
<td>x</td>
</tr>
<tr>
<td>재선언</td>
<td>o</td>
<td>x</td>
<td>x</td>
</tr>
<tr>
<td>초기화 필요 여부</td>
<td>x</td>
<td>x</td>
<td>o</td>
</tr>
<tr>
<td>호이스팅</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐</td>
</tr>
<tr>
<td>초기화</td>
<td>선언과동시에</td>
<td>선언-&gt;TDZ(일시적 사각지대)-&gt;초기화</td>
<td>선언-&gt;TDZ(일시적 사각지대)-&gt;초기화</td>
</tr>
<tr>
<td>스코프</td>
<td>함수</td>
<td>블록</td>
<td>블록</td>
</tr>
</tbody></table>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 deep dive
<a href="https://github.com/wikibook/mjs/blob/master/15.md">wikibooks</a></p>