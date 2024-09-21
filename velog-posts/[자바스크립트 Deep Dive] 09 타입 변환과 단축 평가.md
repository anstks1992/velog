<h2 id="09-타입-변환과-단축평가">09. 타입 변환과 단축평가</h2>
<hr />
<h3 id="91-타입-변환이란">9.1 타입 변환이란?</h3>
<blockquote>
<h5 id="자바스크립트의-개발자의-의도에-따라-다른-타입으로-변환할-수-있는데-이러한-것을-명시적-타입-변환-또는-타입-캐스팅이라고-한다">자바스크립트의 개발자의 의도에 따라 다른 타입으로 변환할 수 있는데 이러한 것을 '명시적 타입 변환' 또는 '타입 캐스팅'이라고 한다</h5>
</blockquote>
<pre><code class="language-javascript">var x = 10;

// 명시적 타입 변환
// 숫자를 문자열로 타입 캐스팅한다.
var str = x.toString();
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10</code></pre>
<blockquote>
<h5 id="개발자의-의도와-상관없이-자바스크립트-엔진에-의해-타입이-자동으로-변환되는-것을-암묵적-타입-변환-또는-타입-강제-변환-이라-한다">개발자의 의도와 상관없이 자바스크립트 엔진에 의해 타입이 자동으로 변환되는 것을 '암묵적 타입 변환' 또는 '타입 강제 변환' 이라 한다.</h5>
</blockquote>
<pre><code class="language-javascript">var x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
var str = x + '';
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10</code></pre>
<h3 id="92-암묵적-타입-변환">9.2 암묵적 타입 변환</h3>
<blockquote>
<h5 id="암묵적-타입-변환이-발생하면-문자열숫자불리언과-같은-원시-타입-중-하나로-변한다">암묵적 타입 변환이 발생하면 문자열,숫자,불리언과 같은 원시 타입 중 하나로 변한다.</h5>
</blockquote>
<pre><code class="language-javascript">// 피연산자가 모두 문자열 타입이어야 하는 문맥
'10' + 2 // -&gt; '102'

// 피연산자가 모두 숫자 타입이어야 하는 문맥
5 * '10' // -&gt; 50

// 피연산자 또는 표현식이 불리언 타입이어야 하는 문맥
!0 // -&gt; true
if (1) { }</code></pre>
<h4 id="921-문자열-타입으로-변환">9.2.1 문자열 타입으로 변환</h4>
<blockquote>
<h5 id="자바스크립트-엔진은-문자열-연결-연산자-표현식을-평가하기-위헤-문자열-연결-연산자의-피연산자-중에서-문자열-타입이-아닌-피연산자를-문자열-타입으로-암묵적-타입-변환-한다br">자바스크립트 엔진은 문자열 연결 연산자 표현식을 평가하기 위헤 문자열 연결 연산자의 피연산자 중에서 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환 한다.<br /></h5>
</blockquote>
<h5 id="산술-연산자-중에--연산자만이-피연산자-중-하나가-문자열이고-다른-하나가-숫자일경우-문자열로-변환해준다">산술 연산자 중에 '+' 연산자만이 피연산자 중 하나가 문자열이고 다른 하나가 숫자일경우 문자열로 변환해준다</h5>
<pre><code class="language-javascript">// 숫자 타입
0 + ''         // -&gt; &quot;0&quot;
-0 + ''        // -&gt; &quot;0&quot;
1 + ''         // -&gt; &quot;1&quot;
-1 + ''        // -&gt; &quot;-1&quot;
NaN + ''       // -&gt; &quot;NaN&quot;
Infinity + ''  // -&gt; &quot;Infinity&quot;
-Infinity + '' // -&gt; &quot;-Infinity&quot;

// 불리언 타입
true + ''  // -&gt; &quot;true&quot;
false + '' // -&gt; &quot;false&quot;

// null 타입
null + '' // -&gt; &quot;null&quot;

// undefined 타입
undefined + '' // -&gt; &quot;undefined&quot;

// 심벌 타입
(Symbol()) + '' // -&gt; TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''           // -&gt; &quot;[object Object]&quot;
Math + ''           // -&gt; &quot;[object Math]&quot;
[] + ''             // -&gt; &quot;&quot;
[10, 20] + ''       // -&gt; &quot;10,20&quot;
(function(){}) + '' // -&gt; &quot;function(){}&quot;
Array + ''          // -&gt; &quot;function Array() { [native code] }&quot;</code></pre>
<h4 id="922-숫자-타입으로-변환">9.2.2 숫자 타입으로 변환</h4>
<blockquote>
<h5 id="자바스크립트-엔진은-산술-연산자의-피연산자-중에서-숫자-타입이-아닌-피연산자를-숫자-타입으로-암묵적-타입-변환-한다">자바스크립트 엔진은 산술 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환 한다.</h5>
</blockquote>
<pre><code class="language-javascript">1 - '1'   // -&gt; 0
1 * '10'  // -&gt; 10
1 / 'one' // -&gt; NaN</code></pre>
<h5 id="비교-연산자의-역할은-불리언-값을-만드는-것이다">비교 연산자의 역할은 불리언 값을 만드는 것이다</h5>
<pre><code class="language-javascript">//숫자 타입이 아닌 피연산자를 숫자 타입으로 변화하여 불리언 값 표시 
'1' &gt; 0  // -&gt; true </code></pre>
<h5 id="-단항-연산자는-피연산자가-숫자-타입의-값이-아니면-숫자-타입의-값으로-암묵적-타입-변환을-수행한다">'+' 단항 연산자는 피연산자가 숫자 타입의 값이 아니면 숫자 타입의 값으로 암묵적 타입 변환을 수행한다</h5>
<pre><code class="language-javascript">// 문자열 타입
+''       // -&gt; 0
+'0'      // -&gt; 0
+'1'      // -&gt; 1
+'string' // -&gt; NaN

// 불리언 타입
+true     // -&gt; 1
+false    // -&gt; 0

// null 타입
+null     // -&gt; 0

// undefined 타입
+undefined // -&gt; NaN

// 심벌 타입
+Symbol() // -&gt; TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}             // -&gt; NaN
+[]             // -&gt; 0
+[10, 20]       // -&gt; NaN
+(function(){}) // -&gt; NaN</code></pre>
<h4 id="923-불리언-타입으로-변환">9.2.3 불리언 타입으로 변환</h4>
<blockquote>
<h5 id="if문이나-for문과-같은-제어문-또는-삼항-조건-연산자의-조건식은-불리언-값으로-평가되는-표현식이다br">if문이나 for문과 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값으로 평가되는 표현식이다<br /></h5>
</blockquote>
<h5 id="자바스크립트-엔진은-불리언-타입이-아닌-값을-truthy값-또는-falsy-값으로-구분한다">자바스크립트 엔진은 불리언 타입이 아닌 값을 truthy값 또는 falsy 값으로 구분한다</h5>
<pre><code class="language-javascript">if ('')    console.log('1');
if (true)  console.log('2');
if (0)     console.log('3');
if ('str') console.log('4');
if (null)  console.log('5');

// 2 4</code></pre>
<blockquote>
<p>false로 평가되는 값들</p>
</blockquote>
<ul>
  <li>false</li>
    <li>undefined</li>
    <li>null</li>
    <li>0,-0</li>
    <li>NaN</li>
  <li>''(빈 문자열)</li>
  </ul>

<pre><code class="language-javascript">// 전달받은 인수가 Falsy 값이면 true, Truthy 값이면 false를 반환한다.
function isFalsy(v) {
  return !v;
}

// 전달받은 인수가 Truthy 값이면 true, Falsy 값이면 false를 반환한다.
function isTruthy(v) {
  return !!v;
}

// 모두 true를 반환한다.
isFalsy(false);
isFalsy(undefined);
isFalsy(null);
isFalsy(0);
isFalsy(NaN);
isFalsy('');

// 모두 true를 반환한다.
isTruthy(true);
isTruthy('0'); // 빈 문자열이 아닌 문자열은 Truthy 값이다.
isTruthy({});
isTruthy([]);</code></pre>
<h3 id="93-명시적-타입-변환">9.3 명시적 타입 변환</h3>
<h4 id="931-문자열-타입으로-변환">9.3.1 문자열 타입으로 변환</h4>
<blockquote>
<h5 id="문자열-타입이-아닌-값을-문자열-타입으로-변환하는-방법">문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법</h5>
</blockquote>
<ul>
  <li>String 생성자 함수를 new 연산자 없이 호출하는 방법
      <li>Object.prototype.toString 메서드를 사용하는 방법
          <li> 문자열 연결 연산자를 이용하는 방법
 </ul>

<pre><code class="language-javascript">// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 =&gt; 문자열 타입
String(1);        // -&gt; &quot;1&quot;
String(NaN);      // -&gt; &quot;NaN&quot;
String(Infinity); // -&gt; &quot;Infinity&quot;
// 불리언 타입 =&gt; 문자열 타입
String(true);     // -&gt; &quot;true&quot;
String(false);    // -&gt; &quot;false&quot;

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 =&gt; 문자열 타입
(1).toString();        // -&gt; &quot;1&quot;
(NaN).toString();      // -&gt; &quot;NaN&quot;
(Infinity).toString(); // -&gt; &quot;Infinity&quot;
// 불리언 타입 =&gt; 문자열 타입
(true).toString();     // -&gt; &quot;true&quot;
(false).toString();    // -&gt; &quot;false&quot;

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 =&gt; 문자열 타입
1 + '';        // -&gt; &quot;1&quot;
NaN + '';      // -&gt; &quot;NaN&quot;
Infinity + ''; // -&gt; &quot;Infinity&quot;
// 불리언 타입 =&gt; 문자열 타입
true + '';     // -&gt; &quot;true&quot;
false + '';    // -&gt; &quot;false&quot;</code></pre>
<h4 id="932-숫자타입으로-변환">9.3.2 숫자타입으로 변환</h4>
<blockquote>
<h5 id="숫자-타입이-아닌-값을-숫자-타입으로-변환하는-방법">숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법</h5>
  <ul>
    <li>Number 생성자 함수를 new 연산자 없이 호출
      <li>parseInt,parseFloat함수를 사용하는 방법(문자열만 숫자로)
        <li>+ 단항 연산자를 이용하는 방법
          <li>* 산술 연산자를 이용하는 방법
  </ul>
</blockquote>
<pre><code class="language-javascript">// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 =&gt; 숫자 타입
Number('0');     // -&gt; 0
Number('-1');    // -&gt; -1
Number('10.53'); // -&gt; 10.53
// 불리언 타입 =&gt; 숫자 타입
Number(true);    // -&gt; 1
Number(false);   // -&gt; 0

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
// 문자열 타입 =&gt; 숫자 타입
parseInt('0');       // -&gt; 0
parseInt('-1');      // -&gt; -1
parseFloat('10.53'); // -&gt; 10.53

// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 =&gt; 숫자 타입
+'0';     // -&gt; 0
+'-1';    // -&gt; -1
+'10.53'; // -&gt; 10.53
// 불리언 타입 =&gt; 숫자 타입
+true;    // -&gt; 1
+false;   // -&gt; 0

// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 =&gt; 숫자 타입
'0' * 1;     // -&gt; 0
'-1' * 1;    // -&gt; -1
'10.53' * 1; // -&gt; 10.53
// 불리언 타입 =&gt; 숫자 타입
true * 1;    // -&gt; 1
false * 1;   // -&gt; 0</code></pre>
<h4 id="933-불리언-타입으로-변환">9.3.3 불리언 타입으로 변환</h4>
<blockquote>
<h5 id="불리언-타입이-아닌-값을-불리언-값으로-변환하는-방법">불리언 타입이 아닌 값을 불리언 값으로 변환하는 방법</h5>
</blockquote>
<ul>
<li> Boolean 생성자 함수를 new연산자 없이 호출하는 방법
  <li>! 부정 논리 연산자를 두번 사용하는 방법
</ul>

<pre><code class="language-javascript">// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 =&gt; 불리언 타입
Boolean('x');       // -&gt; true
Boolean('');        // -&gt; false
Boolean('false');   // -&gt; true
// 숫자 타입 =&gt; 불리언 타입
Boolean(0);         // -&gt; false
Boolean(1);         // -&gt; true
Boolean(NaN);       // -&gt; false
Boolean(Infinity);  // -&gt; true
// null 타입 =&gt; 불리언 타입
Boolean(null);      // -&gt; false
// undefined 타입 =&gt; 불리언 타입
Boolean(undefined); // -&gt; false
// 객체 타입 =&gt; 불리언 타입
Boolean({});        // -&gt; true
Boolean([]);        // -&gt; true

// 2. ! 부정 논리 연산자를 두번 사용하는 방법
// 문자열 타입 =&gt; 불리언 타입
!!'x';       // -&gt; true
!!'';        // -&gt; false
!!'false';   // -&gt; true
// 숫자 타입 =&gt; 불리언 타입
!!0;         // -&gt; false
!!1;         // -&gt; true
!!NaN;       // -&gt; false
!!Infinity;  // -&gt; true
// null 타입 =&gt; 불리언 타입
!!null;      // -&gt; false
// undefined 타입 =&gt; 불리언 타입
!!undefined; // -&gt; false
// 객체 타입 =&gt; 불리언 타입
!!{};        // -&gt; true
!![];        // -&gt; true
</code></pre>
<h3 id="94-단축평가">9.4 단축평가</h3>
<h4 id="941-논리-연산자를-사용한-단축-평가">9.4.1 논리 연산자를 사용한 단축 평가</h4>
<blockquote>
<h5 id="논리곱-연산자는-두-개의-피연산자-모두-true때-true를-반환한다-논리연산의-결과를-두번째-피연산자로-반환한다">논리곱(&amp;&amp;) 연산자는 두 개의 피연산자 모두 true때 true를 반환한다. 논리연산의 결과를 두번째 피연산자로 반환한다.</h5>
</blockquote>
<pre><code class="language-javascript">'Cat' &amp;&amp; 'Dog' // -&gt; &quot;Dog&quot;</code></pre>
<blockquote>
<h5 id="논리합-연산자는-하나만-true로-평가되도-true를-반환한다-논리-연산의-결과를-첫번째-피연산자-반환한다">논리합(||) 연산자는 하나만 true로 평가되도 true를 반환한다. 논리 연산의 결과를 첫번째 피연산자 반환한다</h5>
</blockquote>
<pre><code class="language-javascript">'Cat' || 'Dog' // -&gt; &quot;Cat&quot;</code></pre>
<blockquote>
<h5 id="논리곱-과-논리합-연산자는-논리-연산의-결과를-결정하는-피연산자를-타입-변환하지-않고-그대로-반환한다-br">논리곱(&amp;&amp;) 과 논리합(||) 연산자는 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. <br /></h5>
</blockquote>
<h5 id="이를-단축-평가라-한다">이를 단축 평가라 한다.</h5>
<h5 id="단축평과는-표현식을-평가하는-도중에-평가-결과가-확정된-경우-나머지-평가-과정을-생략하는-것을-말한다">단축평과는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.</h5>
<table>
<thead>
<tr>
<th>단축 평가 표현식</th>
<th>평가 결과</th>
</tr>
</thead>
<tbody><tr>
<td>true ll anything</td>
<td>true</td>
</tr>
<tr>
<td>false ll anything</td>
<td>anything</td>
</tr>
<tr>
<td>true &amp;&amp; anything</td>
<td>anything</td>
</tr>
<tr>
<td>false &amp;&amp; anything</td>
<td>false</td>
</tr>
<tr>
<td>```javascript</td>
<td></td>
</tr>
<tr>
<td>// 논리합(</td>
<td></td>
</tr>
<tr>
<td>'Cat'</td>
<td></td>
</tr>
<tr>
<td>false</td>
<td></td>
</tr>
<tr>
<td>'Cat'</td>
<td></td>
</tr>
</tbody></table>
<p>// 논리곱(&amp;&amp;) 연산자
'Cat' &amp;&amp; 'Dog'  // -&gt; &quot;Dog&quot;
false &amp;&amp; 'Dog'  // -&gt; false
'Cat' &amp;&amp; false  // -&gt; false</p>
<pre><code>
##### 단축 평가를 사용하면 if문을 대체할 수 있다.
```javascript
var done = true;
var message = '';

// 주어진 조건이 true일 때
if (done) message = '완료';

// if 문은 단축 평가로 대체 가능하다.
// done이 true라면 message에 '완료'를 할당
message = done &amp;&amp; '완료';
console.log(message); // 완료</code></pre><h5 id="조건이-false-일때-무언가를-해야-한다면-논리합-연산자-표현식으로-대체할-if문을-대체-할-수-있다">조건이 false 일때 무언가를 해야 한다면 논리합(||) 연산자 표현식으로 대체할 if문을 대체 할 수 있다.</h5>
<pre><code class="language-js">var done = false;
var message = '';

// 주어진 조건이 false일 때
if (!done) message = '미완료';

// if 문은 단축 평가로 대체 가능하다.
// done이 false라면 message에 '미완료'를 할당
message = done || '미완료';
console.log(message); // 미완료

-----------------------------------------------------

//삼항조건 연산자로 if else 대체
var done = true;
var message = '';

// if...else 문
if (done) message = '완료';
else      message = '미완료';
console.log(message); // 완료

// if...else 문은 삼항 조건 연산자로 대체 가능하다.
message = done ? '완료' : '미완료';
console.log(message); // 완료</code></pre>
<h4 id="942-옵셔널-체이닝-연산자">9.4.2 옵셔널 체이닝 연산자</h4>
<blockquote>
<h5 id="연산자--는-좌항의-피연산자가-null-또는-undefined인-경우-undefined를-반환하고-그렇지-않으면-우항의-프로퍼티를-참조한다">연산자 '?.' 는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티를 참조한다.</h5>
</blockquote>
<pre><code class="language-js">var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined</code></pre>
<h5 id="옵셔널-체인지는-피연산자가-null-또는-undefined가-아닌지-확인하고-프로퍼티를-참조할-때-유용하며-이전에는-논리-연산자-를-사용하여-확인했다">옵셔널 체인지는 피연산자가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용하며 이전에는 논리 연산자 &amp;&amp;를 사용하여 확인했다.</h5>
<pre><code class="language-js">var elem = null;

// elem이 Falsy 값이면 elem으로 평가되고 elem이 Truthy 값이면 elem.value로 평가된다.
var value = elem &amp;&amp; elem.value;
console.log(value); // null</code></pre>
<h5 id="논리연산자-는-좌항-피연산자가-false로-평가되는-값falseundefinednull0-0nan이면-좌항-피연산자를-그대로-반환한다">논리연산자 &amp;&amp;는 좌항 피연산자가 false로 평가되는 값(false,undefined,null,0,-0,NaN,'')이면 좌항 피연산자를 그대로 반환한다.</h5>
<pre><code class="language-js">var str = '';

// 문자열의 길이(length)를 참조한다.
var length = str &amp;&amp; str.length;

// 문자열의 길이(length)를 참조하지 못한다.
console.log(length); // ''</code></pre>
<h5 id="옵셔널-체이닝은-좌항-피연산자가-false로-평가되는-값falseundefinednull0-0nan이어도-null-또는-undefined가-아니면-우항의-프러퍼티를-참조한다">옵셔널 체이닝은 좌항 피연산자가 false로 평가되는 값(false,undefined,null,0,-0,NaN,'')이어도 null 또는 undefined가 아니면 우항의 프러퍼티를 참조한다</h5>
<pre><code class="language-js">var str = '';

// 문자열의 길이(length)를 참조한다. 이때 좌항 피연산자가 false로 평가되는 Falsy 값이라도
// null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어간다.
var length = str?.length;
console.log(length); // 0</code></pre>
<h4 id="943-null-병합-연산자">9.4.3 null 병합 연산자</h4>
<blockquote>
<h5 id="연산자--는-좌항의-피연산자가-null-또는-undefined인-경우-우항의-피연산자를-반환하고-그렇지-않으면-좌항의-피연산자르-반환한다">연산자 '??' 는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 그렇지 않으면 좌항의 피연산자르 반환한다.</h5>
</blockquote>
<pre><code class="language-js">// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
var foo = null ?? 'default string';
console.log(foo); // &quot;default string&quot;</code></pre>
<h5 id="논리연산자-는-좌항-피연산자가-false로-평가되는-값falseundefinednull0-0nan이면-우항-피연산자를-반환한다">논리연산자 ||는 좌항 피연산자가 false로 평가되는 값(false,undefined,null,0,-0,NaN,'')이면 우항 피연산자를 반환한다.</h5>
<pre><code class="language-js">// Falsy 값인 0이나 ''도 기본값으로서 유효하다면 예기치 않은 동작이 발생할 수 있다.
var foo = '' || 'default string';
console.log(foo); // &quot;default string&quot;</code></pre>
<h5 id="null-병합-연산자는-좌항-피연산자가-false로-평가되는-값falseundefinednull0-0nan이어도-null-또는-undefined가-아니면-좌항의-피연산자를-그대로-반환한다">null 병합 연산자는 좌항 피연산자가 false로 평가되는 값(false,undefined,null,0,-0,NaN,'')이어도 null 또는 undefined가 아니면 좌항의 피연산자를 그대로 반환한다.</h5>
<pre><code class="language-js">// 좌항의 피연산자가 Falsy 값이라도 null 또는 undefined가 아니면 좌항의 피연산자를 반환한다.
var foo = '' ?? 'default string';
console.log(foo); // &quot;&quot;</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<p>표준 빌트인 생성자 함수와 빌트인 메서드</p>
<blockquote>
<p>표준 빌트인 생성자 함수와 표준 빌트인 메서드는 자바스크립트에서 기본으로 제공하는 함수다.<br /> 
빌트인 생성자 함수는 객체의 새로운 인스턴스를 생성하기 위해 사용되는 함수들로, Array(), Object(), String(), Date() 등의 생성자가 있다.<br />
표준 빌트인 메서드는 내장된 객체(Object, Array, String 등)에서 사용 가능한 메서드로, 배열을 조작하거나 문자열을 변환하는 등 다양한 작업에 사용된다.</p>
</blockquote>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/09.md">wikibooks</a></h4>