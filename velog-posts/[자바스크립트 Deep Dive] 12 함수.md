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