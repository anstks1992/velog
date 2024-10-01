<h2 id="201-strict-mode">20.1 strict mode</h2>
<hr />
<h3 id="201-strict-mode란">20.1 strict mode란?</h3>
<pre><code class="language-js">function foo() {
  x = 10;
}
foo();

console.log(x); // 10</code></pre>
<h5 id="위-예제에서-foo-함수의-스코프에는-x의-선언이-없으므로-검색에-실패하고-자바스크립트-엔진은-상위스코프위-같은-경우는-전역-스코프에서-x-변수의-선언을-검색한다">위 예제에서 foo 함수의 스코프에는 x의 선언이 없으므로 검색에 실패하고 자바스크립트 엔진은 상위스코프(위 같은 경우는 전역 스코프)에서 x 변수의 선언을 검색한다.</h5>
<h5 id="전역스코프에서-x변수의-선언이-없어-error가-발생할-것-같지만-자바스크립트는-엔진은-암묵적으로-전역-객체에-x프로퍼티를-동적으로-생성한다">전역스코프에서 x변수의 선언이 없어 error가 발생할 것 같지만 자바스크립트는 엔진은 암묵적으로 전역 객체에 x프로퍼티를 동적으로 생성한다.</h5>
<blockquote>
<p>전역 객체의 x프로퍼티는 마치 전역 변수처럼 사용할 수 있는데 이러한 현상을 암묵적 전역이라 한다.</p>
</blockquote>
<h5 id="이러한-암묵적-전역은-개발자의-의도와-상관없이-오류를-발생-시킬-수-있기-때문에-이를-지원하기-위해-es5부터-strict-mode엄격-모드가-추가-되었다">이러한 암묵적 전역은 개발자의 의도와 상관없이 오류를 발생 시킬 수 있기 때문에 이를 지원하기 위해 ES5부터 strict mode(엄격 모드)가 추가 되었다.</h5>
<h3 id="202-strict-mode의-적용">20.2 strict mode의 적용</h3>
<h5 id="strict-mode를-적용하려면-전역의-선두-또는-함수-몸체의-선두에-use-strict를-추가한다">strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에 'use strict;'를 추가한다.</h5>
<pre><code class="language-js">'use strict';

function foo() {
  x = 10; // ReferenceError: x is not defined
}
foo();</code></pre>
<pre><code class="language-js">function foo() {
  'use strict';

  x = 10; // ReferenceError: x is not defined
}
foo();</code></pre>
<h3 id="203-전역에-strict-mode를-적용하는-것은-피하자">20.3 전역에 strict mode를 적용하는 것은 피하자</h3>
<h5 id="스크립트-단위로-적용된-strict-mode는-다른-스크립트에-영향을-주지-않고-해당-스크립트에-한정되어-적용된다">스크립트 단위로 적용된 strict mode는 다른 스크립트에 영향을 주지 않고 해당 스크립트에 한정되어 적용된다.</h5>
<pre><code class="language-js">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  &lt;script&gt;
    'use strict';
  &lt;/script&gt;
  &lt;script&gt;
    x = 1; // 에러가 발생하지 않는다.
    console.log(x); // 1
  &lt;/script&gt;
  &lt;script&gt;
    'use strict';

    y = 1; // ReferenceError: y is not defined
    console.log(y);
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<h5 id="하지만-strict-mode-스크립트와-non-strict-mode-스크립트를-오류-발생-가능성이-있어-옳지-않다">하지만 strict mode 스크립트와 non-strict mode 스크립트를 오류 발생 가능성이 있어 옳지 않다.</h5>
<h5 id="이러한-경우-즉시-실행-함수로-스크립트-전체를-감싸서-스코프를-구분하고-즉시-실행-함수의-선두에-strict-mode를-적용하면-된다">이러한 경우 즉시 실행 함수로 스크립트 전체를 감싸서 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용하면 된다.</h5>
<pre><code class="language-js">// 즉시 실행 함수의 선두에 strict mode 적용
(function () {
  'use strict';

  // Do something...
}());</code></pre>
<h3 id="204-함수-단위로-strict-mode를-적용하는-것도-피하자">20.4 함수 단위로 strict mode를 적용하는 것도 피하자</h3>
<h5 id="함수-단위로도-strict-mode를-적용할-수-있지만-일일이-적용하는-것도-번거롭고-strict-mode가-적용된-함수가-참조할-함수-외부의-컨텍스트에-strict-mode를-적용하지-않으면-이-또한-문제가-발생할-수-있어-권장되지-않는다">함수 단위로도 strict mode를 적용할 수 있지만 일일이 적용하는 것도 번거롭고 strict mode가 적용된 함수가 참조할 함수 외부의 컨텍스트에 strict mode를 적용하지 않으면 이 또한 문제가 발생할 수 있어 권장되지 않는다.</h5>
<pre><code class="language-js">(function () {
  // non-strict mode
  var lеt = 10; // 에러가 발생하지 않는다.

  function foo() {
    'use strict';

    let = 20; // SyntaxError: Unexpected strict mode reserved word
  }
  foo();
}());</code></pre>
<h5 id="따라서-strict-mode는-즉시-실행-함수로-감싼-스크립트-단위로-적용하는-것이-바람직하다">따라서 strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.</h5>
<h3 id="205-strict-mode가-발생시키는-에러">20.5 strict mode가 발생시키는 에러</h3>
<h5 id="다음은-strict-mode를-적용했을-때-에러가-발생하는-대표적인-사례다">다음은 strict mode를 적용했을 때 에러가 발생하는 대표적인 사례다.</h5>
<h4 id="2051-암묵적-전역">20.5.1 암묵적 전역</h4>
<h5 id="선언하지-않은-변수를-참조하면-referenceerror가-발생한다">선언하지 않은 변수를 참조하면 ReferenceError가 발생한다.</h5>
<pre><code class="language-js">(function () {
  'use strict';

  x = 1;
  console.log(x); // ReferenceError: x is not defined
}());</code></pre>
<h4 id="2052-변수함수매개변수의-삭제">20.5.2 변수,함수,매개변수의 삭제</h4>
<h5 id="delete-연산자로-변수함수매개변수를-삭제하면-syntanerror가-발생한다">delete 연산자로 변수,함수,매개변수를 삭제하면 SyntanError가 발생한다.</h5>
<pre><code class="language-js">(function () {
  'use strict';

  var x = 1;
  delete x;
  // SyntaxError: Delete of an unqualified identifier in strict mode.

  function foo(a) {
    delete a;
    // SyntaxError: Delete of an unqualified identifier in strict mode.
  }
  delete foo;
  // SyntaxError: Delete of an unqualified identifier in strict mode.
}());</code></pre>
<h4 id="2053-매개변수-이름의-중복">20.5.3 매개변수 이름의 중복</h4>
<h5 id="중복된-매개변수-이름을-사용하면-syntaxerror가-발생한다">중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.</h5>
<pre><code class="language-js">(function () {
  'use strict';

  //SyntaxError: Duplicate parameter name not allowed in this context
  function foo(x, x) {
    return x + x;
  }
  console.log(foo(1, 2));
}());</code></pre>
<h3 id="2054--with문의-사용">20.5.4  with문의 사용</h3>
<h5 id="with문은-동일한-객체의-프로퍼티를-반복해서-사용할-때-객체-이름을-생락할-수-있어서-코드가-간단해지는-효과가-있지만-성능과-가독성이-나빠지는-문제가-있다-따라서-사용이-권장되지-않는다">with문은 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생락할 수 있어서 코드가 간단해지는 효과가 있지만 성능과 가독성이 나빠지는 문제가 있다. 따라서 사용이 권장되지 않는다.</h5>
<pre><code class="language-js">(function () {
  'use strict';

  // SyntaxError: Strict mode code may not include a with statement
  with({ x: 1 }) {
    console.log(x);
  }
}());</code></pre>
<h3 id="206-strict-mode-적용에-의한-변화">20.6 strict mode 적용에 의한 변화</h3>
<h4 id="2061-일반-함수의-this">20.6.1 일반 함수의 this</h4>
<h5 id="strict-mode에서-함수를-일반-함수로서-호출하면-this에-undefined가-바인딩된다-생성자-함수가-아닌-일반-함수-내부에서는-this를-사용할-필요가-없기-때문이다">strict mode에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다. 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문이다.</h5>
<pre><code class="language-js">(function () {
  'use strict';

  function foo() {
    console.log(this); // undefined
  }
  foo();

  function Foo() {
    console.log(this); // Foo
  }
  new Foo();
}());</code></pre>
<h4 id="2062-arguments-객체">20.6.2 arguments 객체</h4>
<h5 id="strict-mode에서는-매개변수에-전달된-인수를-재할당하여-변경해도-arguments-객체에-반영되지-않는다">strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.</h5>
<pre><code class="language-js">(function (a) {
  'use strict';
  // 매개변수에 전달된 인수를 재할당하여 변경
  a = 2;

  // 변경된 인수가 arguments 객체에 반영되지 않는다.
  console.log(arguments); // { 0: 1, length: 1 }
}(1));</code></pre>
<h3 id="😲-느낀점">😲 느낀점</h3>
<p>책에도 쓰여있었지만 ESLint가 그 역할을 완벽하게 대체해서 지금에서는 굳이 strict mode를 사용할 필요는 없을것 같다. </p>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/20.md">wikibooks</a></p>