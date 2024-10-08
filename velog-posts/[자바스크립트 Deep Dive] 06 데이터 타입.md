<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3abc6f22-d65d-4143-a10d-9555588b1fa7/image.png" /></p>
<h2 id="06-데이터-타입">06. 데이터 타입</h2>
<hr />
<blockquote>
<p>데이터 타입</p>
</blockquote>
<li>원시 타입</li>
<ul>
  <ul>
    <li>숫자 타입 : 숫자,정수와 실수 구분 없이 하나의 숫자 타입만 존재</li>
      <li>문자열 타입: 문자열</li>
      <li>불리언 타입: true,false</li>
      <li>undefined 타입: var 키워드로 선언된 변수에 암묵적으로 할당되는 값</li>
      <li>null 타입: 값이 없다는 것을 의도적으로 명시할때 사용하는 값</li>
      <li>심벌 타입: ES6에서 추가된 7번째 타입</li>
   </ul>
</ul> 
<li>객체 타입</li>
<ul><ul><li>객체,함수,배열</li></ul></ul>

<h3 id="61-숫자타입">6.1 숫자타입</h3>
<blockquote>
<h5 id="자바스크립트는-모든-수를-실수로-처리하며-정수만-표현하기-위한-데이터는-존재하지-않는다">자바스크립트는 모든 수를 실수로 처리하며, 정수만 표현하기 위한 데이터는 존재하지 않는다.</h5>
</blockquote>
<pre><code>var integer = 10;    // 정수
var double = 10.12;  // 실수
var negative = -20;  // 음의 정수</code></pre><h5 id="자바스크립트는-2진수8진수16진수를-표현하기-위한-데이터-타입을-제공하지-않기-때문에-이들-값을-참조하면-모두-10진수로-해석된다">자바스크립트는 2진수,8진수,16진수를 표현하기 위한 데이터 타입을 제공하지 않기 때문에 이들 값을 참조하면 모두 10진수로 해석된다.</h5>
<pre><code>var binary = 0b01000001; // 2진수
var octal = 0o101;       // 8진수
var hex = 0x41;          // 16진수

// 표기법만 다를 뿐 모두 같은 값이다.
console.log(binary); // 65
console.log(octal);  // 65
console.log(hex);    // 65
console.log(binary === octal); // true
console.log(octal === hex);    // true</code></pre><h5 id="자바스크립트는-정수로-표시되는-수끼리-나누더라도-실수가-나올-수-있다">자바스크립트는 정수로 표시되는 수끼리 나누더라도 실수가 나올 수 있다.</h5>
<pre><code>// 숫자 타입은 모두 실수로 처리된다.
console.log(1 === 1.0); // true
console.log(4 / 2);     // 2
console.log(3 / 2);     // 1.5</code></pre><h5 id="숫자-타입은-추가적으로-세가지-특별한-값을-표현할-수-있다">숫자 타입은 추가적으로 세가지 특별한 값을 표현할 수 있다.</h5>
<pre><code>// 숫자 타입의 세 가지 특별한 값
console.log(10 / 0);       // Infinity:양의무한대
console.log(10 / -0);      // -Infinity:음의무한대
console.log(1 * 'String'); // NaN:산술 연산 불가</code></pre><h5 id="자바스크립트는-대소문자를-구별하므로-nannannan-에러가-발생하고-이들을-값이-아닌-식별자로-해석한다">자바스크립트는 대소문자를 구별하므로 NaN,Nan,nan 에러가 발생하고 이들을 값이 아닌 식별자로 해석한다</h5>
<pre><code>// 자바스크립트는 대소문자를 구별한다.
var x = nan; // ReferenceError: nan is not defined</code></pre><h3 id="62-문자열-타입">6.2 문자열 타입</h3>
<blockquote>
<h5 id="문자열은--으로-텍스트를-감싸며-자바스크립트에서-가장-일반-적인-표기법은-작은따옴표이다">문자열은 &quot;&quot;,'',`` 으로 텍스트를 감싸며 자바스크립트에서 가장 일반 적인 표기법은 작은따옴표('')이다.</h5>
</blockquote>
<pre><code>// 문자열 타입
var string;
string = '문자열'; // 작은따옴표
string = &quot;문자열&quot;; // 큰따옴표
string = `문자열`; // 백틱 (ES6)

string = '작은따옴표로 감싼 문자열 내의 &quot;큰따옴표&quot;는 문자열로 인식된다.';
string = &quot;큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.&quot;;</code></pre><h5 id="문자열을-따옴표로-감싸는-이유는-키워드나-식별자-같은-토큰과-구분하기-위해서다-또한-따옴표로-감싸지-않으면-스페이스와-같은-공백문자도-포함시킬-수-없다">문자열을 따옴표로 감싸는 이유는 키워드나 식별자 같은 토큰과 구분하기 위해서다. 또한 따옴표로 감싸지 않으면 스페이스와 같은 공백문자도 포함시킬 수 없다</h5>
<pre><code>// 따옴표로 감싸지 않은 hello를 식별자로 인식한다.
var string = hello; // ReferenceError: hello is not defined</code></pre><h5 id="자바스크립트의-문자열을-생성되면-그-문자열이-변경될수-없는-변경-불가능한-값이며-원시타입이다">자바스크립트의 문자열을 생성되면 그 문자열이 변경될수 없는 변경 불가능한 값이며 원시타입이다.</h5>
<h3 id="63-템플릿-리터럴">6.3 템플릿 리터럴</h3>
<blockquote>
<h5 id="es6부터-멀티라인-문자열-표현식-삽입-태그드-템플릿등-편리한-문자열-처리-기능을-제공하는-템플릿-리터럴이-도입되었으며-주로-일반적인-따옴표-대시-백틱을-사용한다">ES6부터 멀티라인 문자열, 표현식 삽입, 태그드 템플릿등 편리한 문자열 처리 기능을 제공하는 템플릿 리터럴이 도입되었으며 주로 일반적인 따옴표 대시 백틱(``)을 사용한다.</h5>
</blockquote>
<pre><code>var template = `Template literal`;
console.log(template); // Template literal</code></pre><h4 id="631-멀티라인-문자열">6.3.1 멀티라인 문자열</h4>
<h5 id="일반-문자열-내에서는-줄바꿈이-허용되지-않는다-따라서-일반-문자열에서-줄바꿈들의-공백을-표현하려면-백슬레시로-시작하는-이스케이프-시퀸스를-사용해야-한다">일반 문자열 내에서는 줄바꿈이 허용되지 않는다. 따라서 일반 문자열에서 줄바꿈들의 공백을 표현하려면 백슬레시()로 시작하는 이스케이프 시퀸스를 사용해야 한다.</h5>
<pre><code>var str = 'Hello
world.';
// SyntaxError: Invalid or unexpected token</code></pre><p><a href="https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%8A%A4%EC%BC%80%EC%9D%B4%ED%94%84_%EB%AC%B8%EC%9E%90">위키백과 이스케이프 문자 참고</a></p>
<h5 id="이스케이프-시퀸스가-적용된-예제">이스케이프 시퀸스가 적용된 예제</h5>
<pre><code>var template = '&lt;ul&gt;\n\t&lt;li&gt;&lt;a href=&quot;#&quot;&gt;Home&lt;/a&gt;&lt;/li&gt;\n&lt;/ul&gt;';

console.log(template);
/* 결과 
&lt;ul&gt;
  &lt;li&gt;&lt;a href=&quot;#&quot;&gt;Home&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
*/</code></pre><h5 id="이스테이프-시퀀스가-적용되지-않은-예제">이스테이프 시퀀스가 적용되지 않은 예제</h5>
<pre><code>var template = `&lt;ul&gt;
  &lt;li&gt;&lt;a href=&quot;#&quot;&gt;Home&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;`;

console.log(template);
/*
&lt;ul&gt;
  &lt;li&gt;&lt;a href=&quot;#&quot;&gt;Home&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
*/</code></pre><h4 id="632-표현식-삽입">6.3.2 표현식 삽입</h4>
<h5 id="템플릿-리터럴-내에서는-연사자-를-통해-간단히-문자열을-삽입할-수-있다">템플릿 리터럴 내에서는 연사자 +를 통해 간단히 문자열을 삽입할 수 있다.</h5>
<pre><code>var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.'); // My name is Ung-mo Lee.</code></pre><h5 id="표현식을-삽입-할려면-으로-표현식을-감싼다">표현식을 삽입 할려면 ${}으로 표현식을 감싼다.</h5>
<pre><code>var first = 'Ung-mo';
var last = 'Lee';

// ES6: 표현식 삽입
console.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.</code></pre><h5 id="표현식-삽입은-일반식이-아닌-반드시-템플릿-리터럴-사용해야-한다">표현식 삽입은 일반식이 아닌 반드시 템플릿 리터럴 사용해야 한다</h5>
<pre><code>//템플릿 리터럴
console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3
//일반식 
console.log('1 + 2 = ${1 + 2}'); // 1 + 2 = ${1 + 2}</code></pre><h3 id="64-boolean-타입">6.4 boolean 타입</h3>
<blockquote>
<h5 id="주로-참거짓을-가리는-조건문에서-자주-쓰인다">주로 참/거짓을 가리는 조건문에서 자주 쓰인다.</h5>
</blockquote>
<pre><code>var foo = true;
console.log(foo); // true

foo = false;
console.log(foo); // false</code></pre><h3 id="65-undefined-타입">6.5 undefined 타입</h3>
<blockquote>
<h5 id="자바스크립트-var-키워드-변수선언에-의해-확보된-처음-메모리공간을-빈-상태로-두지-않고-undefined를-할당한다">자바스크립트 var 키워드 변수선언에 의해 확보된 처음 메모리공간을 빈 상태로 두지 않고 undefined를 할당한다.</h5>
</blockquote>
<pre><code>var foo;
console.log(foo); // undefined</code></pre><h5 id="이처럼-undefined는-의도적으로-할당한-값이-아닌-자바스크립트-엔진이-변수를-초기화-할-때-사용하는-값이다-즉-변수를-참조했을때-undefined가-변환된다면-참조한-변수가-선언-이후-값이-할당된적-없는-초기화되지-않은-변수라는-것을-알-수-있다">이처럼 undefined는 의도적으로 할당한 값이 아닌 자바스크립트 엔진이 변수를 초기화 할 때 사용하는 값이다. 즉 변수를 참조했을때 undefined가 변환된다면 참조한 변수가 선언 이후 값이 할당된적 없는 초기화되지 않은 변수라는 것을 알 수 있다.</h5>
<h3 id="66-null-타입">6.6 null 타입</h3>
<blockquote>
<h5 id="null은-변수에-값이-없다는-것을-의도적으로-명시-할-때사용한다-변수가-이전에-참조하던-값을-더-이상-참조하지-않겠다는-의미이며-이전에-할당되어-있던-값에-대한-참조를-명시적으로-제거하는-것을-의미한다">null은 변수에 값이 없다는 것을 의도적으로 명시 할 때사용한다. 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미이며 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거하는 것을 의미한다.</h5>
</blockquote>
<pre><code>var foo = 'Lee';

// 이전에 할당되어 있던 값에 대한 참조를 제거. foo 변수는 더 이상 'Lee'를 참조하지 않는다.
// 유용해 보이지는 않는다. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시키는 편이 낫다.
foo = null;
console.log(foo) //null</code></pre><h5 id="함수가-유효한-값을-반환할-수-없을-경우-명시적으로-null을-반환하기도-한다">함수가 유효한 값을 반환할 수 없을 경우 명시적으로 null을 반환하기도 한다.</h5>
<pre><code>  &lt;script&gt;
    var element = document.querySelector('.myClass');
    // HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null을 반환한다.
    console.log(element); // null
  &lt;/script&gt;</code></pre><h3 id="67-symbol-타입">6.7 symbol 타입</h3>
<blockquote>
<h5 id="심벌-값은-다른-값과-중복-되지-않는-유일무이한-값이다-따라서-주로-이름이-충돌할-위험이-없는-객체의-유일한-프로퍼티-키를-만들기-위해-사용된다">심벌 값은 다른 값과 중복 되지 않는 유일무이한 값이다. 따라서 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용된다.</h5>
</blockquote>
<h5 id="심벌-이외의-원시-값은-리터럴을-통해-생성하지만-심벌은-symbol-함수를-호출해-생성한다-이때-생성된-심벌값은-외부에-노출되지-않으며-다른-값과-절대-중보되지-않는-유일무이한-값이다">심벌 이외의 원시 값은 리터럴을 통해 생성하지만 심벌은 symbol 함수를 호출해 생성한다. 이때 생성된 심벌값은 외부에 노출되지 않으며 다른 값과 절대 중보되지 않는 유일무이한 값이다.</h5>
<pre><code>var key = Symbol('key');
console.log(typeof key); // symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value</code></pre><h3 id="68-객체타입">6.8 객체타입</h3>
<h5 id="자바스크립트를-이루고-있는-거의-모든-것이-객체다-자세한것은-33장에서-살펴보자">자바스크립트를 이루고 있는 거의 모든 것이 객체다. 자세한것은 33장에서 살펴보자</h5>
<h3 id="69-데이터-타입의-필요성">6.9 데이터 타입의 필요성</h3>
<h4 id="691-데이터-타입에-의한-메모리-공간의-확보와-참조">6.9.1 데이터 타입에 의한 메모리 공간의 확보와 참조</h4>
<h5 id="메모리에-값을-저장하려면-먼저-확보해야-할-메모리-공간의-크기를-결정해야-한다">메모리에 값을 저장하려면 먼저 확보해야 할 메모리 공간의 크기를 결정해야 한다.</h5>
<pre><code>var score = 100;</code></pre><h5 id="자바스크립트-엔진은-데이터-타입-즉-값의-종류에-따라-정해진-크기의-메모리-공간을-확보하는데-변수에-할당되는-값의-데이터-타입에-따라-확보해야-할-메모리-공간의-크기가-결정된다-위-경우-리터럴-100을-숫자타입의-값으로-해석하고-숫자-타입의-값-100을-저장하기-위해-8바이트의-메모리-공간을-확보한다-그리고-100을-2진수로-저장한다">자바스크립트 엔진은 데이터 타입, 즉 값의 종류에 따라 정해진 크기의 메모리 공간을 확보하는데 변수에 할당되는 값의 데이터 타입에 따라 확보해야 할 메모리 공간의 크기가 결정된다. 위 경우 리터럴 100을 숫자타입의 값으로 해석하고 숫자 타입의 값 100을 저장하기 위해 8바이트의 메모리 공간을 확보한다. 그리고 100을 2진수로 저장한다</h5>
<h5 id="값을-참조하려면-한-번에-읽어-들여야-할-메모리-공간의-크기-즉-메모리-셀의-개수바이트-수를-알아야-한다-위-경우-변수에는-숫자-타입의-값이-할당되어-있으므로-자바스크립트는-score변수를-숫자-타입으로-인식한다-숫자-타입은-8바이트-단위로-저장되므로-score-변수를-참조하면-8바이트-단위로-메모리-공간에-저장된-값을-읽어-들인다">값을 참조하려면 한 번에 읽어 들여야 할 메모리 공간의 크기, 즉 메모리 셀의 개수(바이트 수)를 알아야 한다. 위 경우 변수에는 숫자 타입의 값이 할당되어 있으므로 자바스크립트는 score변수를 숫자 타입으로 인식한다. 숫자 타입은 8바이트 단위로 저장되므로 score 변수를 참조하면 8바이트 단위로 메모리 공간에 저장된 값을 읽어 들인다.</h5>
<h4 id="692-데이터-타입에-의한-값의-해석">6.9.2 데이터 타입에 의한 값의 해석</h4>
<h5 id="그렇다면-메모리에서-읽은-2진수를-어떻게-해석해야-할까-메모리에-저장된-값은-데어티-타입에-따라-다르게-해석된다-예를-들어-메모리에-저장된-값-0100-0001을-숫자로-해석하면-65지만-문자열로-해석하면-a다-따라서-숫자-타입인-score-변수를-참조하면-메모리-주소에서-읽어-들인-2진수를-숫자로-해석한다">그렇다면 메모리에서 읽은 2진수를 어떻게 해석해야 할까? 메모리에 저장된 값은 데어티 타입에 따라 다르게 해석된다. 예를 들어, 메모리에 저장된 값 0100 0001을 숫자로 해석하면 65지만 문자열로 해석하면 'A'다. 따라서 숫자 타입인 score 변수를 참조하면 메모리 주소에서 읽어 들인 2진수를 숫자로 해석한다.</h5>
<h5 id="요약하면-데이터-타입이-필요한-이유는-다음과-같다">요약하면 데이터 타입이 필요한 이유는 다음과 같다.</h5>
<blockquote>
<li>값을 저장할 때 확보해야 하는 <b>메모리 공간의 크기</b>를 결정하기 위해</li>
</blockquote>
<li>값을 참조할 때 한 번에 읽어야 할<b> 메모리 공간의 크기</b>를 결정하기 위해</li>
<li>메모리에서 읽어 들인 <b>2진수를 어떻게 해석</b>할지 결정하기 위해</li>

<h3 id="610-동적-타이핑">6.10 동적 타이핑</h3>
<h4 id="6101-동적-타입-언어와-정적-타입-언어">6.10.1 동적 타입 언어와 정적 타입 언어</h4>
<h5 id="c언어나-자바같은-정적타입-언어는-변수를-선언할-때-변수의-타입을-변경할-수-없는-데이터-타입을-사전에-선언해야-한다">c언어나 자바같은 정적타입 언어는 변수를 선언할 때 변수의 타입을 변경할 수 없는 데이터 타입을 사전에 선언해야 한다.</h5>
<pre><code>// c 변수에는 1바이트 정수 타입의 값(-128 ~ 127)만을 할당할 수 있다.
char c;

// num 변수에는 4바이트 정수 타입의 값(-2,124,483,648 ~ 2,124,483,647)만을 할당할 수 있다.
int num;</code></pre><h5 id="반면-자바스크립트는-var-let-const-키워드를-사용해-변수를-선언하지만-따로-타입을-선언하지-않는다-따라서-어떠한-데이터-타입의-값이라도-자유롭게-할당-할-수-있다">반면 자바스크립트는 var, let, const 키워드를 사용해 변수를 선언하지만 따로 타입을 선언하지 않는다. 따라서 어떠한 데이터 타입의 값이라도 자유롭게 할당 할 수 있다.</h5>
<pre><code>var foo;
console.log(typeof foo);  // undefined

foo = 3;
console.log(typeof foo);  // number

foo = 'Hello';
console.log(typeof foo);  // string

foo = true;
console.log(typeof foo);  // boolean

foo = null;
console.log(typeof foo);  // object

foo = Symbol(); // 심벌
console.log(typeof foo);  // symbol

foo = {}; // 객체
console.log(typeof foo);  // object

foo = []; // 배열
console.log(typeof foo);  // object

foo = function () {}; // 함수
console.log(typeof foo);  // function</code></pre><blockquote>
<p>자바스크립트의 변수는 선언이 아니라 할당에 의해 타입이 결정(타입추론)된다. 그리고 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.</p>
</blockquote>
<h5 id="기본적으로-변수는-타입을-갖지-않지만-값은-타입을-갖는다-다시말해-현재-변수에-할당되어-있는-값에-의해-변수의-타입이-동적으로-결정된다는-말이다">기본적으로 변수는 타입을 갖지 않지만 값은 타입을 갖는다. 다시말해 현재 변수에 할당되어 있는 값에 의해 변수의 타입이 동적으로 결정된다는 말이다.</h5>
<h4 id="6102-동적-타입-언어와-변수">6.10.2 동적 타입 언어와 변수</h4>
<h5 id="동적-타입-언어는-변수에-어떤-데이터-타입의-값이라도-자유롭게-할당할-수-있다는-이점이-있지만-구조적인-단점이-있다">동적 타입 언어는 변수에 어떤 데이터 타입의 값이라도 자유롭게 할당할 수 있다는 이점이 있지만 구조적인 단점이 있다</h5>
<blockquote>
<p>동적 타입 단점</p>
</blockquote>
<li>변할수 있는 변수 값은 복잡한 프로그램에서 추적이 어려울 수 있다.</li>
<li>값의 변경에 의해 타입도 언제든 변경이 되어서 동적 타입 언어의 변수는 값을 확인하기 전에는 타입을 확신 할 수 없다</li>
<li>개발자의 의도와 상과없이 자바스크립트가 암묵적으로 타입이 자동으로 변환 될 수 있다.</li>

<h5 id="이러한-이유로-변수를-사용하기-전에-데이터-타입을-체크해야-하는-경우가-있지만-이는-매우-번거롭다-따라서-변수를-사용할때-주의할-사항은-다음과-같다">이러한 이유로 변수를 사용하기 전에 데이터 타입을 체크해야 하는 경우가 있지만 이는 매우 번거롭다. 따라서 변수를 사용할때 주의할 사항은 다음과 같다</h5>
<blockquote>
</blockquote>
<p>변수 사용시 주의할 사항</p>
<li>변수는 필요한 경우 최소한으로 유지해야 한다. 자바스크립트는 동적 언어 이기 때문에 무분별한 변경시 타입을 잘못 예측해 오류를 발생 시킨다.</li>
<li>변수의 유효범위(스코프)는 최대한 좁게 만들어 변수의 부작용을 억제해야 한다. 유효범위가 넓으면 변수로 인해 오류가 발생할 확률이 높다.</li>
<li>전역변수는 최대한 자제해야 한다. 어디서든지 변경 가능한 전역변수는 의도치 않게 값이 변경될 가능성이 놓고 코드에 영향을 줄 수 있다.</li>
<li>변수보다는 상수(const)를 사용해 값의 변경을 억제한다</li>
<li>변수 이름은 목적이나 의미를 파악할 수 있게 네이밍한다</li>
<

<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="라인-피드와-캐리지-리턴">라인 피드와 캐리지 리턴</h5>
<blockquote>
<p>개행 문자는 텍스트의 한 줄이 끝남을 표시하는 문자 또는 문자열인데 라인 피드와 캐리지 리턴이 있다. 라인피드(\n)는 커서를 정지한 상태에서 종이를 한 줄 올리는 것이고, 캐리지 리턴(\r)은 종이를 움직이지 않고 커서를 맨 앞줄로 이동하는 것이다. <br />
<a href="https://ko.wikipedia.org/wiki/%EC%83%88%EC%A4%84_%EB%AC%B8%EC%9E%90">위키피디아 LF와CR의 차이</a></p>
</blockquote>
<h5 id="선언과-정의">선언과 정의</h5>
<blockquote>
<p>undefined에서 말하는 정의란 변수에 값을 할당하여 변수의 실체를 명확이 하는 것이다. 다른 언어와 달리 자바스크립의 경우 변수를 선언하면 암묵적으로 정의가 이루어지기 때문에 선언과 정의의 구분이 모호하지만 ECMAScript 사양에서는 변수는 '선언하다'라고 표현하고, 함수는 '정의한다'라고 표현하다.</p>
</blockquote>
<h5 id="데이터-타입에-따라-확보되는-메모리-공간의-크기">데이터 타입에 따라 확보되는 메모리 공간의 크기</h5>
<blockquote>
<p>ECMAScript에서는 문자열과 숫자 타입 외의 데이터 타입의 크기를 명시적으로 규정하고 있지 않으며 따라서 문자열과 숫자타입을 제외하고 확보되는 데이터 타입에 따라 확보되는 메모리 공간의 코기는 자바스크립느 엔진 제조사의 구현에 따라 다를 수 있다.</p>
</blockquote>
<h5 id="심벌-테이블">심벌 테이블</h5>
<blockquote>
<p>컴파일러 또는 인터플리터는 심벌 테이블이라고 부르는 자료 구조를 통해 식별자를 키로 바인딩된 값의 메모리 주소,데이터 타입,스코프 등을 관리한다.<br />
<a href="https://ko.wikipedia.org/wiki/%EC%8B%AC%EB%B3%BC_%ED%85%8C%EC%9D%B4%EB%B8%94">위키 피디아 심벌 테이블</a></p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/06.md">wikibooks</a></h4>