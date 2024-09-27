<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3688ffea-a398-4aee-a0a6-6f166ea75fab/image.png" /></p>
<h2 id="12-함수">12. 함수</h2>
<hr />
<h3 id="121-함수란">12.1 함수란</h3>
<blockquote>
<p>일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것 이다</p>
</blockquote>
<pre><code class="language-js">// f(x, y) = x + y
function add(x, y) {
  return x + y;
}

// f(2, 5) = 7
add(2, 5); // 7</code></pre>
<blockquote>
<p>함수의 구성은 크게 함수 내부터 입력을 전달 받는 변수를 매개변수(parameter), 입력을 인수(argument),출력을 반환값(return value)이라 한다</p>
</blockquote>
<p>그림 12-2</p>
<blockquote>
<p>함수는 함수 정의를 통해 생성한다.</p>
</blockquote>
<pre><code class="language-js">function add(x,y) {
 return x+y 
} </code></pre>
<blockquote>
<p>함수는 함수 호출로 인수와 매개변수를 통해 함수의 실행을 지시한다</p>
</blockquote>
<pre><code class="language-js">var result = add(2, 5);

// 함수 add에 인수 2, 5를 전달하면서 호출하면 반환값 7을 반환한다.
console.log(result); // 7</code></pre>
<h3 id="122-함수를-사용하는-이유">12.2 함수를 사용하는 이유</h3>
<blockquote>
<ul>
  <li> 코드의 재사용 : 여러번 사용이 가능
  <li> 유지보수의 편의성 : 코드의 중복을 억제한다
  <li> 코드의 신뢰성 : 실수를 줄여준다
  <li> 코드의 가독성 : 네이밍으로 함수의 역할을 파악 할 수 있음
  </ul>
</blockquote>
<h3 id="123-함수-리터럴">12.3 함수 리터럴</h3>
<blockquote>
<p>함수는 객체 타입의 값이다. 따라서 함수를 함수 리터럴로 생성할 수 있다.</p>
</blockquote>
<pre><code class="language-js">// 변수에 함수 리터럴을 할당
var f = function add(x, y) {
  return x + y;
};</code></pre>
<blockquote>
<p>함수 이름</p>
</blockquote>
<ul>
  <li> 함수 이름은 식별자다. 네이밍 규칙을 준수해야 한다.
    <li>함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다.
      <li>함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명함수, 없는 함수를 무명/익명 함수라 한다
        </ul><br />
  매개변수 목록
  <ul>
  <li> 0개 이상의 매겨변수를 소괄호로 깜싸고 쉼표로 구분한다.
    <li> 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당된다.
      <li> 매개변수는 함수 몸체 내에서 변수와 동일하게 취급된다.
        </ul> <br />
        함수 몸체
    <ul>
  <li> 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의
    <li> 함수 몸체는 함수 호출에 의해 실행된다
  </li>
  </ul>

<blockquote>
<p>함수는 객체다. 따라서 일반 객체와 달리 호출할 수 있다 </p>
</blockquote>
<h3 id="124-함수-정의">12.4 함수 정의</h3>
<blockquote>
<p>함수 정의란 함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행한 문들, 그리고 반환할 값을 지정하는 것을 말한다</p>
</blockquote>
<pre><code class="language-js">// 함수 선언문
function add(x, y) {
  return x + y;
}
//함수 표현식
var add = function(x,y) {
 return x + y; 
}
//function 생성자 함수
var add = new Function('x','y','return x+y')
//화살표 함수
var add = (x,y) =&gt; x+y;</code></pre>
<h4 id="1241-함수-선언문">12.4.1 함수 선언문</h4>
<h5 id="함수-선언문의-정의-방식은-다음과-같다">함수 선언문의 정의 방식은 다음과 같다</h5>
<pre><code class="language-js">// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티까지 출력한다.
// 단, Node.js 환경에서는 console.log와 같은 결과가 출력된다.
console.dir(add); // ƒ add(x, y)

// 함수 호출
console.log(add(2, 5)); // 7</code></pre>
<blockquote>
<p>함수 리터럴과 형태과 동일하다. 하지만 함수 리터럴은 함수 이름을 생략할 수 있으나 함수 선언문은 함수 이름을 생략할 수 없다.</p>
</blockquote>
<pre><code class="language-js">// 함수 선언문은 함수 이름을 생략할 수 없다.
function (x, y) {
  return x + y;
}
// SyntaxError: Function statements require a function name</code></pre>
<blockquote>
<p>자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당한다.</p>
</blockquote>
<pre><code class="language-js">// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() { console.log('foo'); }
foo(); // foo</code></pre>
<p>그림 126</p>
<blockquote>
<p>함수는 함수 이름으로 호출하는 것이 아니나 함수 객체를 가리키는 식별자로 호출한다.</p>
</blockquote>
<pre><code class="language-js">var add = function add(x, y) {
  return x + y;
};

console.log(add(2, 5)); 
//function add를 제외한 나머지 add는 식별자이다</code></pre>
<h4 id="1242-함수-표현식">12.4.2 함수 표현식</h4>
<blockquote>
<p>자바스크립트의 함수는 객체 타입의 값이다. 값처럼 변수에 할당 할 수 있고 프로퍼티 값이 될 수도 있고 배열의 요소도 될 수도 있다. 이처럼 값의 성질을 갖는 객체를 일급 객체라 한다</p>
</blockquote>
<pre><code class="language-js">// 함수 표현식
var add = function (x, y) {
  return x + y;
};

console.log(add(2, 5)); // 7</code></pre>
<blockquote>
<p>함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다.</p>
</blockquote>
<pre><code class="language-js">// 기명 함수 표현식
var add = function foo (x, y) {
  return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); // 7

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined</code></pre>
<h4 id="1243-함수-생성-시점과-함수-호이스팅">12.4.3 함수 생성 시점과 함수 호이스팅</h4>
<h5 id="함수-선언문은-표현식이-아닌-문이고-함수-표현식은-표현식인-문이다-미묘하지만-중요한-차이가-있다">함수 선언문은 '표현식이 아닌 문'이고 함수 표현식은 '표현식인 문'이다. 미묘하지만 중요한 차이가 있다</h5>
<pre><code class="language-js">// 함수 참조
console.dir(add); // ƒ add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};</code></pre>
<blockquote>
<p>함수 선언문은 함수 표현식과 달리 선언문 이전에 호출이 가능한데 이는 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문이다</p>
</blockquote>
<blockquote>
<p>함수 선언문 실행 순서</p>
</blockquote>
<ol>
<li>런타임 이전에 자바스크립트 엔진에 의해 실행 </li>
<li>함수 선언문으로 함수를 정의하면 런타임 이전에 함수 객체 생성</li>
<li>자바스크팁트는 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고 생성된 함수 객체를 할당</li>
<li>이미 함수 객체가 생성되어 있고 함수 이름과 동일하 식별자에 할당 완료</li>
<li>따라서 함수 선언문 이전에 함수를 참조하고 호출도 가능<blockquote>
<blockquote>
<p>이처럼 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라 한다.</p>
</blockquote>
</blockquote>
</li>
</ol>
<blockquote>
<p>함수 표현식으로 함수를 정의 하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다. 따라서 함수 표현식으로 정의한 함수는 반드시 함수 표현식 이후에 참조 또는 호출 해야한다.</p>
</blockquote>
<h4 id="1244-function-생성자-함수">12.4.4 Function 생성자 함수</h4>
<h5 id="function-생성자-함수는-빌트인-함수인-function-생성자-함수를-이용한-함수인데-일반적이지-않으며-바람직하지도-않으므로-가볍게-예시만-보자">Function 생성자 함수는 빌트인 함수인 Function 생성자 함수를 이용한 함수인데 일반적이지 않으며 바람직하지도 않으므로 가볍게 예시만 보자</h5>
<pre><code class="language-js">var add = new Function('x', 'y', 'return x + y');

console.log(add(2, 5)); // 7</code></pre>
<pre><code class="language-js">var add1 = (function () {
  var a = 10;
  return function (x, y) {
    return x + y + a;
  };
}());

console.log(add1(1, 2)); // 13

var add2 = (function () {
  var a = 10;
  return new Function('x', 'y', 'return x + y + a;');
}());

console.log(add2(1, 2)); // ReferenceError: a is not defined</code></pre>
<h4 id="1245-화살표-함수">12.4.5 화살표 함수</h4>
<h5 id="화살표-함수는-항상-익명-함수로-정의하며-선행학습-되어야-할것들이-많아-자세한-것은-263파트에서-알아보자">화살표 함수는 항상 익명 함수로 정의하며 선행학습 되어야 할것들이 많아 자세한 것은 26.3파트에서 알아보자</h5>
<pre><code class="language-js">// 화살표 함수
const add = (x, y) =&gt; x + y;
console.log(add(2, 5)); // 7</code></pre>
<h3 id="125-함수-호출">12.5 함수 호출</h3>
<h4 id="1251-매개변수와-인수">12.5.1 매개변수와 인수</h4>
<blockquote>
<p>함수를 실행하기 위해 필요한 값을 함수 외부에서 내부로 전달한 필요가 있는 경우, 매개변수(인자,parameter)를 통해 인수(argument)를 전달한다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/941187e5-b5cb-4a77-99bb-bdac69bc627c/image.png" /></p>
<pre><code class="language-js">// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2는 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2);</code></pre>
<h5 id="매개변수는-함수-몸체-내에서만-참조할-수-있다">매개변수는 함수 몸체 내에서만 참조할 수 있다.</h5>
<pre><code class="language-js">function add(x, y) {
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// add 함수의 매개변수 x, y는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined</code></pre>
<h5 id="함수는-매개변수의-개수와-인수의-개수가-일치하는지-체크하지-않고-에러가-발생하지-않는다-인수가-부족해-인수가-할당되지-않은-매개변수는-undefined다">함수는 매개변수의 개수와 인수의 개수가 일치하는지 체크하지 않고 에러가 발생하지 않는다. 인수가 부족해 인수가 할당되지 않은 매개변수는 undefined다.</h5>
<pre><code class="language-js">function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN
// x에 2가 전달되지만 y는 undefined이다. 따라서 리턴값은 2+undefined와 같으므로 NaN가 출력된다 </code></pre>
<h5 id="매개변수보다-인수가-더-많은-경우-초과된-인수는-무시한다">매개변수보다 인수가 더 많은 경우 초과된 인수는 무시한다</h5>
<pre><code class="language-js">function add(x, y) {
  return x + y;
}

console.log(add(2, 5, 10)); // 7</code></pre>
<h4 id="1252-인수-확인">12.5.2 인수 확인</h4>
<h5 id="자바스크립트-함수는-매개변수와-인수의-개수가-일하는지-확인하지-않는다-따라서-적절한-인수가-전달되었는지-확인할-필요가-있다">자바스크립트 함수는 매개변수와 인수의 개수가 일하는지 확인하지 않는다. 따라서 적절한 인수가 전달되었는지 확인할 필요가 있다.</h5>
<pre><code class="language-js">function add(x, y) {
  if (typeof x !== 'number' || typeof y !== 'number') {
    // 매개변수를 통해 전달된 인수의 타입이 부적절한 경우 에러를 발생시킨다.
    throw new TypeError('인수는 모두 숫자 값이어야 합니다.');
  }

  return x + y;
}

console.log(add(2));        // TypeError: 인수는 모두 숫자 값이어야 합니다.
console.log(add('a', 'b')); // TypeError: 인수는 모두 숫자 값이어야 합니다.</code></pre>
<h4 id="1253-매개변수의-최대-개수">12.5.3 매개변수의 최대 개수</h4>
<blockquote>
<p>매개변수의 최대 개수에 대해 명시적으로 제한하고 있지 않지만 이상적인 함수는 한가지 일만 해야 되는게 이상적이며 최대 3개 이상을 넘지 않는 것을 권장한다.</p>
</blockquote>
<h4 id="1254-반환문">12.5.4 반환문</h4>
<h5 id="함수-호출은-표현식을-사용하며-return-키워드를-이용한다">함수 호출은 표현식을 사용하며 return 키워드를 이용한다.</h5>
<pre><code class="language-js">function multiply(x, y) {
  return x * y; // 반환문
}

// 함수 호출은 반환값으로 평가된다.
var result = multiply(3, 5);
console.log(result); // 15</code></pre>
<h5 id="반환문은-반환문-이후의-다른-문이-존재하면-함수의-실행을-중단하고-함수-몸체를-빠져나간다">반환문은 반환문 이후의 다른 문이 존재하면 함수의 실행을 중단하고 함수 몸체를 빠져나간다.</h5>
<pre><code class="language-js">function multiply(x, y) {
  return x * y; // 반환문
  // 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
  console.log('실행되지 않는다.'); //실행 안됨
}

console.log(multiply(3, 5)); // 15</code></pre>
<h5 id="return-뒤에-오는-표현식을-평가해-반환한다-없으면-undefined가-반환된다">return 뒤에 오는 표현식을 평가해 반환한다. 없으면 undefined가 반환된다.</h5>
<pre><code class="language-js">function foo () {
  return;
}

console.log(foo()); // undefined</code></pre>
<h5 id="반환문은-생략할-수-있다-생략시-undefined를-반환한다">반환문은 생략할 수 있다. 생략시 undefined를 반환한다.</h5>
<pre><code class="language-js">function foo () {
  return;
}

console.log(foo()); // undefined</code></pre>
<h5 id="반환문은-함수-몸체-내부에서만-사용할-수-있다">반환문은 함수 몸체 내부에서만 사용할 수 있다.</h5>
<h3 id="126-참조에-의한-전달과-외부-상태의-변경">12.6 참조에 의한 전달과 외부 상태의 변경</h3>
<h5 id="원시타입은-변경-불가능이기-때문에-재할당을-통해-원본의-훼손없이-교체되었고-객체는-변경-가능하기-때문에-재할당-대신-직접-교체를-해-원본의-훼손이-발생한다">원시타입은 변경 불가능이기 때문에 재할당을 통해 원본의 훼손없이 교체되었고 객체는 변경 가능하기 때문에 재할당 대신 직접 교체를 해 원본의 훼손이 발생한다.</h5>
<pre><code class="language-js">// 매개변수 primitive는 원시 값을 전달받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = 'Kim';
}

// 외부 상태
var num = 100;
var person = { name: 'Lee' };

console.log(num); // 100
console.log(person); // {name: &quot;Lee&quot;}

// 원시 값은 값 자체가 복사되어 전달되고 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // {name: &quot;Kim&quot;}</code></pre>
<h5 id="함수가-외부상태를-변경하면-변화를-추적하기-어렵고-코드의-복잡성-증가와-가독성을-해치는-원인이-된다-이러한-문제의-해결-방법중-하나는-객체를-불변-객체로-만들어-사용하는-것이다">함수가 외부상태를 변경하면 변화를 추적하기 어렵고 코드의 복잡성 증가와 가독성을 해치는 원인이 된다. 이러한 문제의 해결 방법중 하나는 객체를 불변 객체로 만들어 사용하는 것이다.</h5>
<h3 id="127-다양한-함수의-형태">12.7 다양한 함수의 형태</h3>
<h4 id="1271-즉시-실행-함수">12.7.1 즉시 실행 함수</h4>
<h5 id="함수-정의와-동시에-단-한번만-호출되는-함수를-즉시-실행-함수라고-한다">함수 정의와 동시에 단 한번만 호출되는 함수를 즉시 실행 함수라고 한다.</h5>
<pre><code class="language-js">// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
}());

console.log(res); // 15

// 즉시 실행 함수에도 일반 함수처럼 인수를 전달할 수 있다.
res = (function (a, b) {
  return a * b;
}(3, 5));

console.log(res); // 15</code></pre>
<h4 id="1772-재귀함수">17.7.2 재귀함수</h4>
<h5 id="함수가-자기-자신을-호출하는-것을-재귀-호출이라-한다-주로-반복되는-처리를-위해-사용한다">함수가 자기 자신을 호출하는 것을 재귀 호출이라 한다. 주로 반복되는 처리를 위해 사용한다.</h5>
<pre><code class="language-js">//반복문
function countdown(n) {
  for (var i = n; i &gt;= 0; i--) console.log(i);
}

countdown(10);

//반목문 없이 재귀함수
function countdown(n) {
  if (n &lt; 0) return;
  console.log(n);
  countdown(n - 1); // 재귀 호출
}

countdown(10);</code></pre>
<h5 id="재귀함수는-재귀호출을-멈출-수-없는-탈출-조건이-없으면-무한-반복에-빠질-위험이-있고-스택-오버플로-에러가-발생할-수있다-따라서-반복문을-사용하는-것을-권장한다">재귀함수는 재귀호출을 멈출 수 없는 탈출 조건이 없으면 무한 반복에 빠질 위험이 있고 스택 오버플로 에러가 발생할 수있다. 따라서 반복문을 사용하는 것을 권장한다.</h5>
<h4 id="1273-중첩-함수">12.7.3 중첩 함수</h4>
<h5 id="함수-내부에-정의된-함수를-중첩함수-또는-내부함수라-한다일반적으로-중첩-함수는-자신을-포함하는-외부-함수를-돕는-헬퍼-함수의-역할만-한다">함수 내부에 정의된 함수를 중첩함수 또는 내부함수라 한다.일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수의 역할만 한다.</h5>
<pre><code class="language-js">function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }

  inner();
}

outer();</code></pre>
<h4 id="1274-콜백-함수">12.7.4 콜백 함수</h4>
<blockquote>
<p>함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백함수라 하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수라고 한다.</p>
</blockquote>
<pre><code class="language-js">// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) { //고차함수
  for (var i = 0; i &lt; n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) { //콜백함수
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) { //콜백함수
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3</code></pre>
<blockquote>
<p>고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다. 다시 말해 콜백 함수는 고차 함수에 의해 호출되며 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다.</p>
</blockquote>
<pre><code class="language-js">// 익명 함수 리터럴을 콜백 함수로 고차 함수에 전달한다.
// 익명 함수 리터럴은 repeat 함수를 호출할 때마다 평가되어 함수 객체를 생성한다.
repeat(5, function (i) {
  if (i % 2) console.log(i);
}); // 1 3</code></pre>
<h5 id="이-외에도-콜백-함수는-비동기처리-고차함수등에서-사용된다">이 외에도 콜백 함수는 비동기처리, 고차함수등에서 사용된다.</h5>
<pre><code class="language-js">// 콜백 함수를 사용한 이벤트 처리
// myButton 버튼을 클릭하면 콜백 함수를 실행한다.
document.getElementById('myButton').addEventListener('click', function () {
  console.log('button clicked!');
});

// 콜백 함수를 사용한 비동기 처리
// 1초 후에 메시지를 출력한다.
setTimeout(function () {
  console.log('1초 경과');
}, 1000);</code></pre>
<pre><code class="language-js">// 콜백 함수를 사용하는 고차 함수 map
var res = [1, 2, 3].map(function (item) {
  return item * 2;
});

console.log(res); // [2, 4, 6]

// 콜백 함수를 사용하는 고차 함수 filter
res = [1, 2, 3].filter(function (item) {
  return item % 2;
});

console.log(res); // [1, 3]

// 콜백 함수를 사용하는 고차 함수 reduce
res = [1, 2, 3].reduce(function (acc, cur) {
  return acc + cur;
}, 0);

console.log(res); // 6</code></pre>
<h4 id="1275-순수-함수와-비순수-함수">12.7.5 순수 함수와 비순수 함수</h4>
<h5 id="순수-함수는-어떤-외부-상태에-의존하지도-않고-변경되는도-않는-최소-하나-이상의-인수를-전달-받아-언제나-동일한-값을-반환하는-함수다">순수 함수는 어떤 외부 상태에 의존하지도 않고 변경되는도 않는 최소 하나 이상의 인수를 전달 받아 언제나 동일한 값을 반환하는 함수다.</h5>
<pre><code class="language-js">var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2</code></pre>
<h5 id="비순수-함수는-외부-상태에-의존하거나-외부-상태를-변경하는-함수다">비순수 함수는 외부 상태에 의존하거나 외부 상태를 변경하는 함수다.</h5>
<pre><code class="language-js">var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2</code></pre>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/12.md">wikibooks</a></p>