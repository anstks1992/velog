<h2 id="24-클로저">24. 클로저</h2>
<hr />
<h3 id="241-렉시컬-스코프">24.1 렉시컬 스코프</h3>
<blockquote>
<p>자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프롤 결정한다. 이를 렉시컬 스코프(정적 스코프)라 한다.</p>
</blockquote>
<pre><code class="language-js">const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1</code></pre>
<h5 id="foo와-bar의-상위-스코프는-전역이다-함수를-어디서-호출했는지는-상위-스코프-결정에-어떠한-영향도-주지-못한다-함수의-상위-스코프는-함수를-정의한-위치에-의해-정적으로-결정되고-변하지-않는다">foo와 bar의 상위 스코프는 전역이다. 함수를 어디서 호출했는지는 상위 스코프 결정에 어떠한 영향도 주지 못한다. 함수의 상위 스코프는 함수를 정의한 위치에 의해 정적으로 결정되고 변하지 않는다.</h5>
<h5 id="스코프의-실체는-실행-컨텍스트의-렉시컬-환경이다-이-렉시컬-환경은-자신의-외부-렉시컬-환경에-대한-참조를-통해-상위-렉시컬-환경과-연결된다-이것이-바로-스코프-체인이다">스코프의 실체는 실행 컨텍스트의 렉시컬 환경이다. 이 렉시컬 환경은 자신의 &quot;외부 렉시컬 환경에 대한 참조&quot;를 통해 상위 렉시컬 환경과 연결된다. 이것이 바로 스코프 체인이다.</h5>
<h5 id="따라서-함수의-상위-스코프를-결정한다는-것은-렉시컬-환경의-외부-렉시컬-환경에-대한-참조에-저장할-참조값을-결정한다는-것과-같다">따라서 &quot;함수의 상위 스코프를 결정한다&quot;는 것은 &quot;렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값을 결정한다&quot;는 것과 같다</h5>
<blockquote>
<p>위 개념을 반영해서 렉시컬 스코프를 정의하면 렉시컬 환경의 &quot;외부 렉시컬 환경에 대한 참조&quot;에 저장할 참조값, 즉 상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 '함수가 정의된 위치'에 의해 결정된다. 이것이 바로 렉시컬 스코프다.</p>
</blockquote>
<h3 id="242-함수-객체의-내부-슬롯enviroment">24.2 함수 객체의 내부 슬롯[[Enviroment]]</h3>
<blockquote>
<p>함수는 자신의 내부 슬롯[[Enviroment]]에 자신이 정의 된 환경, 즉 상위 스코프의 참조를 저장한다.</p>
</blockquote>
<h5 id="함수-객체를-생성할-때-자신이-정의된-위치에-의해-결정된-상위-스코프의-참조를-함수-객체-자신의-내부-슬롯enviroment에-저장한다-이때-저장된-상위-스코프의-참조는-현재-실행-중인-실행-컨텍스트의-렉시컬-환경을-가리킨다">함수 객체를 생성할 때 자신이 정의된 위치에 의해 결정된 상위 스코프의 참조를 함수 객체 자신의 내부 슬롯[[Enviroment]]에 저장한다. 이때 저장된 상위 스코프의 참조는 현재 실행 중인 실행 컨텍스트의 렉시컬 환경을 가리킨다.</h5>
<blockquote>
<p>따라서 함수 객체의 내부 슬롯[[Enviroment]]에 저장된 현재 실행 중인 실행 컨텍스트의 렉시컬 환경의 참조가 바로 상위 스코프다. 또한 자신이 호출되었을때 생성될 함수 렉시컬 환경의 &quot;외부 렉시컬 환경에 대한 참조&quot;에 저장될 참조값이다. 함수 객체는 내부 슬롯[[Enviroment]]에 저장한 렉시컬 환경의 참조, 즉 상위 스코프를 자신이 존재하는 한 기억한다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/0f622165-33d6-43df-9bc2-c50c051dd225/image.png" /></p>
<h5 id="외부-렉시컬-환경에-대한-참조에는-함수-객체의-내부-슬롯enviroment에-저장된-렉시컬-환경의-참조가-할당된다위-그림에서-2와3">외부 렉시컬 환경에 대한 참조에는 함수 객체의 내부 슬롯[[Enviroment]]에 저장된 렉시컬 환경의 참조가 할당된다.(위 그림에서 2와3)</h5>
<h3 id="243-클로저와-렉시컬-환경">24.3 클로저와 렉시컬 환경</h3>
<pre><code class="language-js">const x = 1;

// ①
function outer() {
  const x = 10;
  const inner = function () { console.log(x); }; // ②
  return inner;
}

// outer 함수를 호출하면 중첩 함수 inner를 반환한다.
// 그리고 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝되어 제거된다.
const innerFunc = outer(); // ③
innerFunc(); // ④ 10</code></pre>
<h5 id="outer-함수를-호출하면-outer-함수는-중첩-함수-inner를-반화하고-생명주기를-마감한다-이때-outer함수의-실행-컨택스트가-제거되었으므로-x변수에-접근할-수-있는-방법은-달리-없어-보이지만-outer-지역변수-x가-다시-부활-한-듯이-동작한다">outer 함수를 호출하면 outer 함수는 중첩 함수 inner를 반화하고 생명주기를 마감한다. 이때 outer함수의 실행 컨택스트가 제거되었으므로 x변수에 접근할 수 있는 방법은 달리 없어 보이지만 outer 지역변수 x가 다시 부활 한 듯이 동작한다.</h5>
<blockquote>
<p>이처럼 외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다. 이것을 클로저라 부른다</p>
</blockquote>
<h5 id="위-예제에서-outer-함수가-평가되어-함수-객체를-생성할-때1-현재-실행-중인-실행-컨택스트의-렉시컬-환경-즉-전역-렉시컬-환경을-outer-함수-객체의-environment-내부-슷롯에-상위-스코프로서-저장한다">위 예제에서 outer 함수가 평가되어 함수 객체를 생성할 때(1) 현재 실행 중인 실행 컨택스트의 렉시컬 환경, 즉 전역 렉시컬 환경을 outer 함수 객체의 [[Environment]] 내부 슷롯에 상위 스코프로서 저장한다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/624ef545-c5ed-4f37-b4c8-ca6ad066c0d5/image.png" /></p>
<h5 id="outer-함수를-호출하면-outer-함수의-렉시컬-환경이-생성되고-outer-함수-객체의-environment-렉시컬-환경을-outer-함수-렉시컬-환경의-외부-렉시컬-환경에-대한-참조에-할당-한다">outer 함수를 호출하면 outer 함수의 렉시컬 환경이 생성되고 outer 함수 객체의 [[Environment]] 렉시컬 환경을 outer 함수 렉시컬 환경의 &quot;외부 렉시컬 환경에 대한 참조&quot;에 할당 한다.</h5>
<h5 id="그리고-중첩함수-inner가-평가되고-이때-inner는-자신의-environment-내부-슬롯에-현재-실행-중인-outer-함수의-렉시컬-환경을-상위-스코프로서-저장한다">그리고 중첩함수 inner가 평가되고 이때 inner는 자신의 [[Environment]] 내부 슬롯에 현재 실행 중인 outer 함수의 렉시컬 환경을 상위 스코프로서 저장한다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/f473a476-d87e-4f88-b0d9-0ce16d1200c7/image.png" /></p>
<h5 id="outer-함수의-실행이-종료하면-inner-함수를-반환하면서-outer-함수의-생명-주기가-종료되지만-이때-outer-함수의-실행-컨택스트는-실행-컨택스택에서-제거되지만-outer-함수의-렉시컬-환경까지-소멸하는-것은-아니다">outer 함수의 실행이 종료하면 inner 함수를 반환하면서 outer 함수의 생명 주기가 종료되지만 이때 outer 함수의 실행 컨택스트는 실행 컨택스택에서 제거되지만 outer 함수의 렉시컬 환경까지 소멸하는 것은 아니다.</h5>
<h5 id="outer-함수의-렉시컬-환경은-inner-함수의-environment-내부-슬롯에서-참조되고-있는데-가비지-컬렉터는-누군가가-참조하고-있는-메모리-공간을-해체하지-않기-때문이다">outer 함수의 렉시컬 환경은 inner 함수의 [[Environment]] 내부 슬롯에서 참조되고 있는데 가비지 컬렉터는 누군가가 참조하고 있는 메모리 공간을 해체하지 않기 때문이다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/5bc6a78e-2a0f-4a7e-be44-9a2799d61c37/image.png" /></p>
<h5 id="outer-함수가-반환한-inner-함수를-호출4하면-inner-함수의-실행-컨텍스트가-생성되고-실행-컨텍스트-스택에-푸시된다-그리고-렉시컬-환경의-외부-렉시컬-환경에-대한-참조에는-inner-함수-객체의-environment-내부-슬롯에-저장되어-있는-참조값이-할당된다">outer 함수가 반환한 inner 함수를 호출(4)하면 inner 함수의 실행 컨텍스트가 생성되고 실행 컨텍스트 스택에 푸시된다. 그리고 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에는 inner 함수 객체의 [[Environment]] 내부 슬롯에 저장되어 있는 참조값이 할당된다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3214d837-b26a-458b-95f1-fbdf0dacaef0/image.png" /></p>
<h5 id="외부-함수outer-보다-더-오래-생존할-중첩-함수inner는-외부-함수의-생존-여부와-상관없이-자신이-정의된-위치에-의해-결정된-상위-스코프를-기억한다">외부 함수(outer) 보다 더 오래 생존할 중첩 함수(inner)는 외부 함수의 생존 여부와 상관없이 자신이 정의된 위치에 의해 결정된 상위 스코프를 기억한다.</h5>
<h5 id="자바스크립트의-모든-함수는-상위-스코프를-기억하므로-모든-함수는-클로저라고-볼-수-있지만-일반적으로-모든-함수를-클로저하고-하지는-않는다-몇가지-예를-보자">자바스크립트의 모든 함수는 상위 스코프를 기억하므로 모든 함수는 클로저라고 볼 수 있지만 일반적으로 모든 함수를 클로저하고 하지는 않는다 몇가지 예를 보자</h5>
<h5 id="상위-스코프의-어떤-식별자도-참조하지-않는-함수는-클로저가-아니다">상위 스코프의 어떤 식별자도 참조하지 않는 함수는 클로저가 아니다.</h5>
<pre><code class="language-js">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  &lt;script&gt;
    function foo() {
      const x = 1;
      const y = 2;

      // 일반적으로 클로저라고 하지 않는다.
      function bar() {
        const z = 3;

        debugger;
        // 상위 스코프의 식별자를 참조하지 않는다.
        console.log(z);
      }

      return bar;
    }

    const bar = foo();
    bar();
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<h5 id="외부함수보다-중첩함수의-생명주기가-더-짧을-경우-클로저가-아니다">외부함수보다 중첩함수의 생명주기가 더 짧을 경우 클로저가 아니다.</h5>
<pre><code class="language-js">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  &lt;script&gt;
    function foo() {
      const x = 1;

      // 일반적으로 클로저라고 하지 않는다.
      // bar 함수는 클로저였지만 곧바로 소멸한다.
      function bar() {
        debugger;
        // 상위 스코프의 식별자를 참조한다.
        console.log(x);
      }
      bar();
    }

    foo();
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<blockquote>
<p>클로저는 중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 더 오래 유지되는 경우에 한정하는 것이 일반적이다.</p>
</blockquote>
<h3 id="244-클로저의-활용">24.4 클로저의 활용</h3>
<blockquote>
<p>클로저는 상태를 완전하게 변경하고 유지하기 위해 사용한다. 즉 상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하기 위해 사용한다.</p>
</blockquote>
<h5 id="아래-코드는-잘-작동하지만-카운트-상태는-전역-변수를-통해-관리되고-있기-때문에-언제든지-누구나-접근할-수-있고-변수-num의-값이-변경될-수-있는-오류-가능성이-있다">아래 코드는 잘 작동하지만 카운트 상태는 전역 변수를 통해 관리되고 있기 때문에 언제든지 누구나 접근할 수 있고 변수 num의 값이 변경될 수 있는 오류 가능성이 있다.</h5>
<pre><code class="language-js">// 카운트 상태 변수
let num = 0;

// 카운트 상태 변경 함수
const increase = function () {
  // 카운트 상태를 1만큼 증가 시킨다.
  return ++num;
};

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3</code></pre>
<h5 id="이전-코드에서-카운트-상태를-안전하게-변겨하고-유지하기-위한-전역-변수-num을-increase-함수의-지역-변수로-변경하여-의토치-않은-상태-변경은-방지했다">이전 코드에서 카운트 상태를 안전하게 변겨하고 유지하기 위한 전역 변수 num을 increase 함수의 지역 변수로 변경하여 의토치 않은 상태 변경은 방지했다.</h5>
<h5 id="하지만-increase-함수가-호출될-때마다-지역-변수-num은-다시-선언되고-0으로-초기화되고-결과는-항상-1이기때문에-옳지-못하다">하지만 increase 함수가 호출될 때마다 지역 변수 num은 다시 선언되고 0으로 초기화되고 결과는 항상 1이기때문에 옳지 못하다.</h5>
<pre><code class="language-js">// 카운트 상태 변경 함수
const increase = function () {
  // 카운트 상태 변수
  let num = 0;

  // 카운트 상태를 1만큼 증가 시킨다.
  return ++num;
};

// 이전 상태를 유지하지 못한다.
console.log(increase()); // 1
console.log(increase()); // 1
console.log(increase()); // 1</code></pre>
<h5 id="클로저를-사용시-즉시-실행-함수는-호출된-이후-소멸되지만-즉시-실행-함수가-반환한-클로저는-increase-변수에-할당되어-호출된다">클로저를 사용시 즉시 실행 함수는 호출된 이후 소멸되지만 즉시 실행 함수가 반환한 클로저는 increase 변수에 할당되어 호출된다.</h5>
<h5 id="이때-즉시-실행-함수가-반환한-클로저는-자신이-정의된-위치에-의해-결정된-상위-스코프인-즉시-실행-함수의-렉시컬-환경을-기억하고-있다">이때, 즉시 실행 함수가 반환한 클로저는 자신이 정의된 위치에 의해 결정된 상위 스코프인 즉시 실행 함수의 렉시컬 환경을 기억하고 있다.</h5>
<h5 id="따라서-즉시-실행-함수가-반환한-클로저는-카운트-상태를-유지하기-위한-자유-변수-num을-언제-어디서-호출하든지-참조하고-변경할-수-있다">따라서 즉시 실행 함수가 반환한 클로저는 카운트 상태를 유지하기 위한 자유 변수 num을 언제 어디서 호출하든지 참조하고 변경할 수 있다.</h5>
<pre><code class="language-js">// 카운트 상태 변경 함수
const increase = (function () {
  // 카운트 상태 변수
  let num = 0;

  // 클로저
  return function () {
    // 카운트 상태를 1만큼 증가 시킨다.
    return ++num;
  };
}());

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3</code></pre>
<blockquote>
<p>이처럼 클로저는 상태가 의도치 않게 변경되지 않도록 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하여 상태를 안전하게 변경하고 유지하기 위해 사용한다.</p>
</blockquote>
<pre><code class="language-js">// 함수를 인수로 전달받고 함수를 반환하는 고차 함수
// 이 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저를 반환한다.
function makeCounter(aux) {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;

  // 클로저를 반환
  return function () {
    // 인수로 전달 받은 보조 함수에 상태 변경을 위임한다.
    counter = aux(counter);
    return counter;
  };
}

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 함수로 함수를 생성한다.
// makeCounter 함수는 보조 함수를 인수로 전달받아 함수를 반환한다
const increaser = makeCounter(increase); // ①
console.log(increaser()); // 1
console.log(increaser()); // 2

// increaser 함수와는 별개의 독립된 렉시컬 환경을 갖기 때문에 카운터 상태가 연동하지 않는다.
const decreaser = makeCounter(decrease); // ②
console.log(decreaser()); // -1
console.log(decreaser()); // -2</code></pre>
<blockquote>
<p>makeCounter 함수를 호출해 함수를 반환할 때 반환된 함수는 자신만의 독립된 렉시컬 환경을 갖는다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/f892a2ef-e939-4a94-9581-cb1088ddabd8/image.png" /></p>
<h5 id="2에서-makecounter-함수를-호출하면-함수-객체를-생성하여-반환한-후-실행-컨텍스트는-소멸되지만-makecounter-함수-실행-컨택스트의-렉시컬-환경은-makecounter-함수가-반환한-함수의-environment-내부-슬롯에-의해-참조되고-있기-때문에-소멸되지-않는다">(2)에서 makeCounter 함수를 호출하면 함수 객체를 생성하여 반환한 후 실행 컨텍스트는 소멸되지만 makeCounter 함수 실행 컨택스트의 렉시컬 환경은 makeCounter 함수가 반환한 함수의 [[Environment]] 내부 슬롯에 의해 참조되고 있기 때문에 소멸되지 않는다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/e46b7714-68fa-49fc-8780-0a03d5703f83/image.png" /></p>
<h5 id="전역-변수-increase와-decreaser에-할당된-함수는-각각-자신만의-독립된-렉시컬-환경을-갖기-때문에-counter를-공유하지-않고-이로인해-카운트의-증감이-연동이-안된다">전역 변수 increase와 decreaser에 할당된 함수는 각각 자신만의 독립된 렉시컬 환경을 갖기 때문에 counter를 공유하지 않고 이로인해 카운트의 증감이 연동이 안된다.</h5>
<h5 id="따라서-연동하여-증감이-가능한-카운터를-만들려면-렉시컬-환경을-공유하는-클로저를-만들어야-한다-이를-위해서-makecounter-함수를-두-번-호출하지-말아야-한다">따라서 연동하여 증감이 가능한 카운터를 만들려면 렉시컬 환경을 공유하는 클로저를 만들어야 한다. 이를 위해서 makeCounter 함수를 두 번 호출하지 말아야 한다.</h5>
<pre><code class="language-js">// 함수를 반환하는 고차 함수
// 이 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저를 반환한다.
const counter = (function () {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;

  // 함수를 인수로 전달받는 클로저를 반환
  return function (aux) {
    // 인수로 전달 받은 보조 함수에 상태 변경을 위임한다.
    counter = aux(counter);
    return counter;
  };
}());

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 보조 함수를 전달하여 호출
console.log(counter(increase)); // 1
console.log(counter(increase)); // 2

// 자유 변수를 공유한다.
console.log(counter(decrease)); // 1
console.log(counter(decrease)); // 0</code></pre>
<h3 id="245-캡슐화와-정보-은닉">24.5 캡슐화와 정보 은닉</h3>
<h5 id="캡슐화는-객체의-상태를-나타내는-프로퍼티와-프로퍼티를-참조하고-조작할-수-있는-동작인-메서드를-하나로-묶는-것을-말한다">캡슐화는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다.</h5>
<h5 id="캡슐화는-특정-프로퍼티나-메서드를-감출-목적으로-사용하기도-하는데-이를-정보-은닉이라-한다">캡슐화는 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라 한다</h5>
<pre><code class="language-js">function Person(name, age) {
  this.name = name; // public
  let _age = age;   // private

  // 인스턴스 메서드
  this.sayHi = function () {
    console.log(`Hi! My name is ${this.name}. I am ${_age}.`);
  };
}

const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 30.
console.log(you.name); // Kim
console.log(you._age); // undefined</code></pre>
<h5 id="위-예제에서-name은-public이지만-_age는-private이다-sayhi-메서드는-person-객체가-생성될-때-마다-중복-생성된다">위 예제에서 name은 public이지만 _age는 private이다. sayHi 메서드는 Person 객체가 생성될 때 마다 중복 생성된다.</h5>
<pre><code class="language-js">const Person = (function () {
  let _age = 0; // private

  // 생성자 함수
  function Person(name, age) {
    this.name = name; // public
    _age = age;
  }

  // 프로토타입 메서드
  Person.prototype.sayHi = function () {
    console.log(`Hi! My name is ${this.name}. I am ${_age}.`);
  };

  // 생성자 함수를 반환
  return Person;
}());

const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 30.
console.log(you.name); // Kim
console.log(you._age); // undefined</code></pre>
<h5 id="위-예제에서는-publicprivateprotected-같은-접근-제한자를-제공하지-않는-자바스크립트에서도-정보-은닉이-가능한-것처럼-보인다">위 예제에서는 public,private,protected 같은 접근 제한자를 제공하지 않는 자바스크립트에서도 정보 은닉이 가능한 것처럼 보인다.</h5>
<pre><code class="language-js">const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 30.

// _age 변수 값이 변경된다!
me.sayHi(); // Hi! My name is Lee. I am 30.</code></pre>
<h5 id="하지만-위-코드처럼-person-생성자-함수가-여러개의-인스턴스를-생성할-경우-_age-변수의-상태가-유지되지-않는다">하지만 위 코드처럼 Person 생성자 함수가 여러개의 인스턴스를 생성할 경우 _age 변수의 상태가 유지되지 않는다.</h5>
<h5 id="이처럼-자바스크립트는-정보-은닉을-완전하게-지원하지-않는다">이처럼 자바스크립트는 정보 은닉을 완전하게 지원하지 않는다.</h5>
<h3 id="246-자주-발생하는-실수">24.6 자주 발생하는 실수</h3>
<h5 id="다음-예제는-클로저를-사용할때-자주-발생할-수-있는-실수를-보여주는-예제다">다음 예제는 클로저를 사용할때 자주 발생할 수 있는 실수를 보여주는 예제다.</h5>
<pre><code class="language-js">var funcs = [];

for (var i = 0; i &lt; 3; i++) {
  funcs[i] = function () { return i; }; // ①
}

for (var j = 0; j &lt; funcs.length; j++) {
  console.log(funcs[j]()); // ②
}</code></pre>
<h5 id="for문의-변수-선언문에서-var-키워드로-선언한-i-변수는-블록-레벨-스코프가-아닌-함수-레벨-스코프를-갖기-때문에-전역-변수다-전역-변수-i에는-012가-순차적으로-할당된다-따라서-funcs-배열의-요소로-추가한-함수를-호출하면-전역-변수-i를-참조하여-i의-값-3이-출력된다">for문의 변수 선언문에서 var 키워드로 선언한 i 변수는 블록 레벨 스코프가 아닌 함수 레벨 스코프를 갖기 때문에 전역 변수다. 전역 변수 i에는 0,1,2가 순차적으로 할당된다. 따라서 funcs 배열의 요소로 추가한 함수를 호출하면 전역 변수 i를 참조하여 i의 값 3이 출력된다.</h5>
<h5 id="다음은-클로저를-이용한-올바른-예제이다">다음은 클로저를 이용한 올바른 예제이다</h5>
<pre><code class="language-js">var funcs = [];

for (var i = 0; i &lt; 3; i++){
  funcs[i] = (function (id) { // ①
    return function () {
      return id;
    };
  }(i));
}

for (var j = 0; j &lt; funcs.length; j++) {
  console.log(funcs[j]());
}</code></pre>
<h5 id="위-예제는-자바스크립트의-함수-레벨-스코프-특성으로-인해-for문의-변수-선언문에서-var-키워드로-선언한-변수가-전역-변수가-되기-때문에-발생하는-현상이다">위 예제는 자바스크립트의 함수 레벨 스코프 특성으로 인해 for문의 변수 선언문에서 var 키워드로 선언한 변수가 전역 변수가 되기 때문에 발생하는 현상이다.</h5>
<h5 id="따라서-let-키워드를-사용하면-이런-번거로움이-사라진다">따라서 let 키워드를 사용하면 이런 번거로움이 사라진다.</h5>
<pre><code class="language-js">const funcs = [];

for (let i = 0; i &lt; 3; i++) {
  funcs[i] = function () { return i; };
}

for (let i = 0; i &lt; funcs.length; i++) {
  console.log(funcs[i]()); // 0 1 2
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/96460e91-3993-4c82-97de-b5ebde330c62/image.png" /></p>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/24.md">wikibooks</a></p>