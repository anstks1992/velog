<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/44ec9529-0073-4e60-9fee-8c4a51965b1d/image.png" /></p>
<h2 id="14-전역-변수의-문제점">14. 전역 변수의 문제점</h2>
<hr />
<h3 id="141-변수의-생명-주기">14.1 변수의 생명 주기</h3>
<h4 id="1411-지역-변수의-생명-주기">14.1.1 지역 변수의 생명 주기</h4>
<blockquote>
<p>지역 변수의 생명 주기는 함수의 생명 주기와 일치한다</p>
</blockquote>
<pre><code class="language-js">function foo() {
  var x = 'local';
  console.log(x); // local
  return x;
}

foo();
console.log(x); // ReferenceError: x is not defined</code></pre>
<blockquote>
<p>변수 선언이 스코프의 선두로 끌어 올려진 것처럼 동작하는 호이스팅은 스코프를 단위로 작동한다</p>
</blockquote>
<pre><code class="language-js">var x = 'global';

function foo() {
  console.log(x); // undefined
  var x = 'local';
}

foo();
console.log(x); // global</code></pre>
<h4 id="1412-전역-변수의-생명-주기">14.1.2 전역 변수의 생명 주기</h4>
<blockquote>
<p>var 키워드로 선언한 전역 변수의 생명 주기는 전역 객체의 생명주기와 일치한다</p>
</blockquote>
<pre><code class="language-js">var x = 'global';

function foo() {
  console.log(x); 
  var x = 'local';
}

foo();
console.log(x); </code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/e6a8dbd2-5797-4b0f-914d-096aad86a08a/image.png" /></p>
<h3 id="142-전역-변수의-문제점">14.2 전역 변수의 문제점</h3>
<blockquote>
<ul> 
  <li> 암묵적 결함 : 모든 코드가 전역 변수를 참조하고 변경할 수 있음
    <li> 긴 생명 주기 : 긴 생명 주기로 인해 의도치 않은 상태 변화와 메모리 리소스를 오랜 기간 소비한다.
      <li> 스코프 체인 상에서 종점에 존재 : 전역 변수는 종점에 위치해 가장 마지막에 검색된다. 즉 전역 변수의 검색 속도가 가장 느리다. 
        <li>네임 스페이스 오염 : 다른 파일 내에서 동일한 이름으로 명명된 전역 변수나 전역 함수가 같은 스코프 내에 존재시 오류 발생 가능성
          </ul>
</blockquote>
<h3 id="143-전역-변수의-사용을-억제하는-방법">14.3 전역 변수의 사용을 억제하는 방법</h3>
<blockquote>
<p>전역 변수를 반드시 사용해야 할 이유가 아니면 지역 변수를 사용해야 한다. 변수의 스코프는 좁을수록 좋다.</p>
</blockquote>
<h4 id="1431-즉시-실행-함수">14.3.1 즉시 실행 함수</h4>
<blockquote>
<p>모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 변수가 된다.</p>
</blockquote>
<pre><code class="language-js">(function () {
  var foo = 10; // 즉시 실행 함수의 지역 변수
  // ...
}());

console.log(foo); // ReferenceError: foo is not defined</code></pre>
<h4 id="1432-네임스페이스-객체">14.3.2 네임스페이스 객체</h4>
<h5 id="전역에-네임스페이스-역할을-담당할-객체를-생성하고-전역-변수처럼-사용하고-싶은-변수를-프로퍼티로-추가">전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가</h5>
<pre><code class="language-js">var MYAPP = {}; // 전역 네임스페이스 객체

MYAPP.name = 'Lee';

console.log(MYAPP.name); // Lee</code></pre>
<h4 id="1433-모듈-패턴">14.3.3 모듈 패턴</h4>
<h5 id="모듈-패턴은-변수와-함수를-모아-즉시-실행-함수로-감싸-하나의-모듈을-만든다">모듈 패턴은 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈을 만든다.</h5>
<h5 id="캡슐화는-객체의-상태를-나타내는-프로퍼티와-프로퍼티를-참조하고-조작할-수-있는-동작인-메서드를-하나로-묶는-것을-말한다">캡슐화는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다.</h5>
<pre><code class="language-js">var Counter = (function () {
  // private 변수
  var num = 0;

  // 외부로 공개할 데이터나 메서드를 프로퍼티로 추가한 객체를 반환한다.
  return {
    increase() {
      return ++num;
    },
    decrease() {
      return --num;
    }
  };
}());

// private 변수는 외부로 노출되지 않는다.
console.log(Counter.num); // undefined

console.log(Counter.increase()); // 1
console.log(Counter.increase()); // 2
console.log(Counter.decrease()); // 1
console.log(Counter.decrease()); // 0</code></pre>
<h4 id="1434-es6-모듈">14.3.4 ES6 모듈</h4>
<blockquote>
<p>ES6 모듈은 파일 자체의 독자적인 스코프를 제공한다</p>
</blockquote>
<h5 id="es6-모듈을-사용하더라도-번들링-필요하기-때문에-아직까지는-webpack이라-babel등의-모듈-번들화는-사용하는-것이-일반적이다">ES6 모듈을 사용하더라도 번들링 필요하기 때문에 아직까지는 Webpack이라 babel등의 모듈 번들화는 사용하는 것이 일반적이다.</h5>
<pre><code class="language-js">&lt;script type=&quot;module&quot; src=&quot;lib.mjs&quot;&gt;&lt;/script&gt;
&lt;script type=&quot;module&quot; src=&quot;app.mjs&quot;&gt;&lt;/script&gt;</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="전역-객체">전역 객체</h5>
<blockquote>
<p>전역 객체는 코드가 실행되기 이전에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체다. CSR환경에서는 window, SSR환경에서는 global 객체를 의미한다.</p>
</blockquote>
<h5 id="네임스페이스">네임스페이스</h5>
<blockquote>
<p>이름공간 또는 네임스페이스는 개체를 구분할 수 있는 범위를 나타내는 말로 일반적으로 하나의 이름 공간에서는 하나의 이름이 단 하나의 개체만을 가리키게 된다.<br />
<a href="https://ko.wikipedia.org/wiki/%EC%9D%B4%EB%A6%84%EA%B3%B5%EA%B0%84">위키북스 이름공간</a></p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 deep dive
<a href="https://github.com/wikibook/mjs/blob/master/14.md">wikibooks</a></p>