<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3f8d9dfc-2d72-4d2d-ab8c-6f9b27ef0c35/image.png" /></p>
<h2 id="13-스코프">13. 스코프</h2>
<hr />
<h3 id="131-스코프란">13.1 스코프란?</h3>
<blockquote>
<p>모든 식별자(변수 이름, 함수 이름, 클래스 이름등)는 자신이 선언한 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정되는데 이를 스코프라 한다.</p>
</blockquote>
<pre><code class="language-js">function add(x, y) {
  // 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
  // 즉, 매개변수의 스코프(유효범위)는 함수 몸체 내부다.
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined</code></pre>
<blockquote>
<p>스코프란 식별자를 검색할 때 사용하는 규칙이다. 어떤 값을 구별할 수 있어야 하므로 변수 이름은 중복 될 수 없고 유일해야 한다.</p>
</blockquote>
<pre><code class="language-js">var x = 'global';

function foo() {
  var x = 'local';
  console.log(x); // local : 함수 내에서만 사용 가능
}

foo();

console.log(x); // global : 어디서든 참조 가능</code></pre>
<h3 id="132-스코프의-종류">13.2 스코프의 종류</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th>설명</th>
<th>스코프</th>
<th>변수</th>
</tr>
</thead>
<tbody><tr>
<td>전역</td>
<td>코드의 가장 바깥 영역</td>
<td>전역 스코프</td>
<td>전역 변수</td>
</tr>
<tr>
<td>지역</td>
<td>함수 몸체 내부</td>
<td>지역 스코프</td>
<td>지역 변수</td>
</tr>
</tbody></table>
<h4 id="1321-전역과-전역-스코프">13.2.1 전역과 전역 스코프</h4>
<blockquote>
<p>전역이란 코드의 가장 바깥 영역이다. 전역 변수는 어디서든지 참조 가능 하다.</p>
</blockquote>
<h4 id="1322-지역과-지역-스코프">13.2.2 지역과 지역 스코프</h4>
<blockquote>
<p>지역이란 함수 몸체 내부를 말한다. 지역변수는 자신이 선언된 지역과 하위 지역(중첩 함수)에서만 참조 할 수 있다. 따라서 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서만 유효하다</p>
</blockquote>
<h3 id="133-스코프-체인">13.3 스코프 체인</h3>
<blockquote>
<p>함수는 중첩 될 수 있는데 이는 스코프가 함수의 중첩에 의해 계층적 구조를 갖는다는 점이다.</p>
</blockquote>
<pre><code class="language-js">var x = &quot;global x&quot;
var y = &quot;global y&quot;

function outer (){ //지역
  var z = &quot;outer local z&quot;;
  console.log(x); // global x
  console.log(y); // global y
  console.log(z); // outer local z

  function inner (){ //지역
    var x = &quot;inner local x&quot;

    console.log(x) // inner local x
    console.log(y) // global y
    console.log(z) // outer local z
  }

  inner()
}

outer()

console.log(x) // global x
console.log(y) // ReferenceError: z is not defined</code></pre>
<blockquote>
<p>전역 스코프 : var x = &quot;global x&quot; | var y = &quot;global y&quot; | function outer
⬆
outer 지역 스코프 :  var z = &quot;outer local z&quot; | function inner
⬆
inner 지역 스코프 :   var x = &quot;inner local x&quot; <br />
모든 스코프는 이처럼 하나의 계층적 구조로 연결되어 있는데 이를 스코프 체인이라 한다</p>
</blockquote>
<blockquote>
<p>변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.</p>
</blockquote>
<h4 id="1331-스코프-체인에-의한-변수-검색">13.3.1 스코프 체인에 의한 변수 검색</h4>
<blockquote>
<p>자바스크립트는 상위 스코프 방향으로 이동하며 선언된 변수를 검색하며 절대 하위 스코프로 내려가면 서 식별자를 검색하는 일은 없다.<br /> 
이는 상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참조할수 있지만 하위 스코프에서 유효한 변수를 상위 스코프에서 참조할 수 없다는 의미다.</p>
</blockquote>
<h3 id="134-함수-레벨-스코프">13.4 함수 레벨 스코프</h3>
<blockquote>
<p>지역은 함수 몸체 내부를 말하고 지역은 지역 스코프를 만드는데 이는 코드 블록 아닌 함숭에 의해서만 지역 스코프가 생성된다는 의미다</p>
</blockquote>
<blockquote>
<ul>
</blockquote>
<li>블록 레벨 스코프 : 모든 코드 블록에서 지역 스코프를 만듦
<li>함수 레벨 스코프 : var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수몸체)만은 지역 스코프로 인정
</ul>

<pre><code class="language-js">var x = 1;

if (true) {
  // var 키워드로 선언된 변수는 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다.
  // 함수 밖에서 var 키워드로 선언된 변수는 코드 블록 내에서 선언되었다 할지라도 모두 전역 변수다.
  // 따라서 x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
  // 이는 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10</code></pre>
<pre><code class="language-js">var i = 10;

// for 문에서 선언한 i는 전역 변수다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i &lt; 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5</code></pre>
<h3 id="135-렉시컬-스코프">13.5 렉시컬 스코프</h3>
<blockquote>
<ul>
  <li> 동적 스코프 : 함수를 어디서 호출했는지에 따라 함수의 상위 스코프 결정
  <li> 렉시컬 스코프 : 함수를 어디서 정의했는지에 따라 함수의 상위 스코프 결정
  </ul>
</blockquote>
<pre><code class="language-js">var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1

// 1. bar 함수는 전역에서 정의된 함수이다.
// 2. bar 함수는 전역 코드가 실행되기 전에 먼저 평가되어 함수 객체를 생성한다
// 3. 이때 생성된 bar 함수 객체는 전역 스코프(x=1)를 기억한다
// 4. bar 함수가 어디서 호출되든 자신이 기억하는 전역 스코프를 상위 스코프로 사용한다.
// 5. 따라서 x의 값 1을 두 번 출력한다</code></pre>
<blockquote>
<p>자바스크립트는 기본적으로 렉시컬 스코프를 따르므로 함수를 어디에서 정의 했는지에 따라 상위 스코프를 결정한다. 함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향도 주지 않는다. 즉, 함수의 상위 스코프는 언제나 자신이 정의된 스코프다.</p>
</blockquote>
<blockquote>
<p>함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정한다. 함수 정의가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다. 함수가 호출될 때마다 함수의 상위 스코프를 참조할 필요가 있기 때문이다</p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/13.md">wikibooks</a></h4>