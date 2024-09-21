<h2 id="07연산자">07.연산자</h2>
<hr />
<pre><code class="language-js">// 산술 연산자
5 * 4 // -&gt; 20
// 문자열 연결 연산자
'My name is ' + 'Lee' // -&gt; 'My name is Lee'
// 할당 연산자
color = 'red' // -&gt; 'red'
// 비교 연산자
3 &gt; 5 // -&gt; false
// 논리 연산자
true &amp;&amp; false // -&gt; false
// 타입 연산자
typeof 'Hi' // -&gt; string</code></pre>
<h3 id="71-산술-연산자">7.1 산술 연산자</h3>
<blockquote>
<h5 id="산술-연산자는-피연산자를-대상으로-수학적-계산을-대상으로-수학적-계산을-수행해-새로운-숫자-값을-만든다">산술 연산자는 피연산자를 대상으로 수학적 계산을 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만든다</h5>
</blockquote>
<h4 id="711-이항-산술-연산자">7.1.1 이항 산술 연산자</h4>
<blockquote>
<h5 id="이항-산술-연산자는-2개의-피연산자를-산술-연산하여-숫자-값을-만든다">이항 산술 연산자는 2개의 피연산자를 산술 연산하여 숫자 값을 만든다.</h5>
</blockquote>
<pre><code class="language-js">5 + 2;  -&gt; 7 //덧셈 
5 - 2;  -&gt; 3 //뺄셈
5 * 2;  -&gt; 10 //곱셈
5 / 2;  -&gt; 2.5 //나눗셈
5 % 2;  -&gt; 1 //나머지</code></pre>
<h4 id="712-단항-산술-연산자">7.1.2 단항 산술 연산자</h4>
<blockquote>
<h5 id="단항-산술-연산자는-1개의-피연산자를-산술-연산하여-숫자-값을-만든다">단항 산술 연산자는 1개의 피연산자를 산술 연산하여 숫자 값을 만든다.</h5>
</blockquote>
<pre><code class="language-js">var x = 1;

// ++ 연산자는 피연산자의 값을 변경하는 암묵적 할당이 이뤄진다.
x++; // x = x + 1;
console.log(x); // 2

// -- 연산자는 피연산자의 값을 변경하는 암묵적 할당이 이뤄진다.
x--; // x = x - 1;
console.log(x); // 1</code></pre>
<h5 id="증가감소-연산자는-위치에-의미가-있다">증가/감소 연산자는 위치에 의미가 있다</h5>
<blockquote>
<li>피연산자 앞에 위치한 증가/감소 연산자는 먼저 피연산의 값을 증가/감소시킨 후, 다른 연산을 수행한다</li>
</blockquote>
<li>피연산자 뒤에 위치한 증가/감소 연산자는 먼저 다른 연산을 수행한 후 피연산의 값을 증가/감소시킨다</li>

<pre><code class="language-js">var x = 5, result;

// 선할당 후증가(postfix increment operator)
result = x++;
console.log(result, x); // 5 6

// 선증가 후할당(prefix increment operator)
result = ++x;
console.log(result, x); // 7 7

// 선할당 후감소(postfix decrement operator)
result = x--;
console.log(result, x); // 7 6

// 선감소 후할당 (prefix decrement operator)
result = --x;
console.log(result, x); // 5 5</code></pre>
<h5 id="-단항-연산자는-피연산자에-아무런-효과가-없다">+ 단항 연산자는 피연산자에 아무런 효과가 없다</h5>
<pre><code class="language-js">// 아무런 효과가 없다.
+10;    // -&gt; 10
+(-10); // -&gt; -10</code></pre>
<h5 id="숫자-타입이-아닌-피연산자에-단항-연산자를-사용하면-피연산자를-숫자-타입으로-변환하여-반환한다">숫자 타입이 아닌 피연산자에 +단항 연산자를 사용하면 피연산자를 숫자 타입으로 변환하여 반환한다.</h5>
<pre><code class="language-js">var x  = '1';

// 문자열을 숫자로 타입 변환한다.
console.log(+x); // 1
// 부수 효과는 없다.
console.log(x);  // &quot;1&quot;

// 불리언 값을 숫자로 타입 변환한다.
x = true;
console.log(+x); // 1
// 부수 효과는 없다.
console.log(x);  // true

// 불리언 값을 숫자로 타입 변환한다.
x = false;
console.log(+x); // 0
// 부수 효과는 없다.
console.log(x);  // false

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
x = 'Hello';
console.log(+x); // NaN
// 부수 효과는 없다.
console.log(x);  // &quot;Hello&quot;</code></pre>
<h5 id="-단항-연산자는-피연산자의-부호를-반전한-값을-반환한다--단항-연산자와-마찬가지로-숫자-타입이-아닌-피연산자에-사용하면-피연산자를-숫자-타입으로-변화하여-반환한다">-단항 연산자는 피연산자의 부호를 반전한 값을 반환한다. + 단항 연산자와 마찬가지로 숫자 타입이 아닌 피연산자에 사용하면 피연산자를 숫자 타입으로 변화하여 반환한다.</h5>
<pre><code class="language-js">// 부호를 반전한다.
-(-10); // -&gt; 10

// 문자열을 숫자로 타입 변환한다.
-'10'; // -&gt; -10

// 불리언 값을 숫자로 타입 변환한다.
-true; // -&gt; -1

// 문자열은 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
-'Hello'; // -&gt; NaN</code></pre>
<h4 id="713-문자열-연결-연산자">7.1.3 문자열 연결 연산자</h4>
<blockquote>
<h5 id="연산자는-피연산자-중-하나-이상이-문자열인-경우-문자열-연결-연산자로-동작한다">+연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다.</h5>
</blockquote>
<pre><code class="language-js">// 문자열 연결 연산자
'1' + 2; // -&gt; '12'
1 + '2'; // -&gt; '12'

// 산술 연산자
1 + 2; // -&gt; 3

// true는 1로 타입 변환된다.
1 + true; // -&gt; 2

// false는 0으로 타입 변환된다.
1 + false; // -&gt; 1

// null은 0으로 타입 변환된다.
1 + null; // -&gt; 1

// undefined는 숫자로 타입 변환되지 않는다.
+undefined;    // -&gt; NaN
1 + undefined; // -&gt; NaN</code></pre>
<h5 id="자바스크립트에서는-true를-1로-false를-0으로-반환한다-이를-암묵적-타입-변환-또는-타입-강제-변환이라고-한다">자바스크립트에서는 true를 1로 false를 0으로 반환한다. 이를 암묵적 타입 변환 또는 타입 강제 변환이라고 한다.</h5>
<h3 id="72-할당-연산자">7.2 할당 연산자</h3>
<table>
<thead>
<tr>
<th>할당 연산자</th>
<th>예</th>
<th>동일표현</th>
<th>부수효과</th>
</tr>
</thead>
<tbody><tr>
<td>=</td>
<td>x=5</td>
<td>x=5</td>
<td>o</td>
</tr>
<tr>
<td>+=</td>
<td>x+=5</td>
<td>x=x+5</td>
<td>o</td>
</tr>
<tr>
<td>-+</td>
<td>x-=5</td>
<td>x=x-5</td>
<td>o</td>
</tr>
<tr>
<td>*=</td>
<td>x*=5</td>
<td>x=x*5</td>
<td>o</td>
</tr>
<tr>
<td>/=</td>
<td>x/=5</td>
<td>x=x/5</td>
<td>o</td>
</tr>
<tr>
<td>%=</td>
<td>x%=5</td>
<td>x=x%5</td>
<td>o</td>
</tr>
</tbody></table>
<pre><code class="language-js">var x;

x = 10;
console.log(x); // 10

x += 5; // x = x + 5;
console.log(x); // 15

x -= 5; // x = x - 5;
console.log(x); // 10

x *= 5; // x = x * 5;
console.log(x); // 50

x /= 5; // x = x / 5;
console.log(x); // 10

x %= 5; // x = x % 5;
console.log(x); // 0

var str = 'My name is ';

// 문자열 연결 연산자
str += 'Lee'; // str = str + 'Lee';
console.log(str); // 'My name is Lee'</code></pre>
<h5 id="할당문은-값으로-평가되는-표현식인-문으로서-할당된-값으로-평가된다">할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다.</h5>
<pre><code class="language-js">var a, b, c;

// 연쇄 할당. 오른쪽에서 왼쪽으로 진행.
// ① c = 0 : 0으로 평가된다
// ② b = 0 : 0으로 평가된다
// ③ a = 0 : 0으로 평가된다
a = b = c = 0;

console.log(a, b, c); // 0 0 0</code></pre>
<h3 id="73-비교-연산자">7.3 비교 연산자</h3>
<blockquote>
<h5 id="비교-연산자는-좌항과-우항의-피연산자르-비교한-다음-그-결과를-boolean값으로-변환한다-주로-if문이나-for문과-같은-제어문의-조건식에서-주로-사용한다">비교 연산자는 좌항과 우항의 피연산자르 비교한 다음 그 결과를 boolean값으로 변환한다. 주로 if문이나 for문과 같은 제어문의 조건식에서 주로 사용한다</h5>
</blockquote>
<h4 id="731-동등일치-비교-연산자">7.3.1 동등/일치 비교 연산자</h4>
<table>
<thead>
<tr>
<th>비교 연산자</th>
<th>의미</th>
<th>사례</th>
<th>설명</th>
<th>부수효과</th>
</tr>
</thead>
<tbody><tr>
<td>==</td>
<td>동등 비교</td>
<td>x==y</td>
<td>x,y의 값이 같음</td>
<td>x</td>
</tr>
<tr>
<td>===</td>
<td>일치 비교</td>
<td>x===y</td>
<td>x,y의 값과 타입 같음</td>
<td>x</td>
</tr>
<tr>
<td>!=</td>
<td>부동등 비교</td>
<td>x!=y</td>
<td>x,y의 값이 다름</td>
<td>x</td>
</tr>
<tr>
<td>!==</td>
<td>불일치 비교</td>
<td>x!==y</td>
<td>x,y의 값과 타입 다름</td>
<td>x</td>
</tr>
</tbody></table>
<blockquote>
<h5 id="동등-비교-연산자는-좌항과-우항의-피연산자를-비교할-때-먼저-암묵적-타입-변환을-통해-타입을-일치시킨-후-같은-값인지-비교한다-하지만-예측하기-어려운-결과를-만들어-낸다는-단점이-있다">동등 비교(==) 연산자는 좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교한다. 하지만 예측하기 어려운 결과를 만들어 낸다는 단점이 있다.</h5>
</blockquote>
<pre><code class="language-js">// 동등 비교
5 == 5; // -&gt; true

// 타입은 다르지만 암묵적 타입 변환을 통해 타입을 일치시키면 동등하다.
5 == '5'; // -&gt; true

// 동등 비교. 결과를 예측하기 어렵다.
'0' == ''; // -&gt; false
0 == '';   // -&gt; true
0 == '0';  // -&gt; true
false == 'false';   // -&gt; false
false == '0';       // -&gt; true
false == null;      // -&gt; false
false == undefined; // -&gt; false</code></pre>
<blockquote>
</blockquote>
<h5 id="일치-비교연산자는-좌항과-우항의-피연산자가-타입도-같고-값도-같은-경우에-한하여-true를-반환한다">일치 비교(===)연산자는 좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한하여 true를 반환한다</h5>
<pre><code class="language-js">// 일치 비교
5 === 5; // -&gt; true

// 암묵적 타입 변환을 하지 않고 값을 비교한다.
// 즉, 값과 타입이 모두 같은 경우만 true를 반환한다.
5 === '5'; // -&gt; false</code></pre>
<h5 id="이때-주의해야-할점은-nan이다-따라서-숫자가-nan인지-조사하려면-빌트인-함수-numberisnan을-사용한다">이때 주의해야 할점은 Nan이다. 따라서 숫자가 NaN인지 조사하려면 빌트인 함수 Number,isNaN을 사용한다.</h5>
<pre><code class="language-js">// NaN은 자신과 일치하지 않는 유일한 값이다.
NaN === NaN; // -&gt; false

// Number.isNaN 함수는 지정한 값이 NaN인지 확인하고 그 결과를 불리언 값으로 반환한다.
Number.isNaN(NaN); // -&gt; true
Number.isNaN(10);  // -&gt; false
Number.isNaN(1 + undefined); // -&gt; true</code></pre>
<h5 id="숫자-0도-주의해야-한다-양의-0과-음의-0이-있는데-이들을-비교하면-true를-반환한다">숫자 0도 주의해야 한다. 양의 0과 음의 0이 있는데 이들을 비교하면 true를 반환한다.</h5>
<pre><code class="language-js">// 양의 0과 음의 0의 비교. 일치 비교/동등 비교 모두 결과는 true이다.
0 === -0; // -&gt; true
0 == -0;  // -&gt; true</code></pre>
<blockquote>
<h5 id="부동등-비교-연산자와-불일치-비교-연산자는-각각-동등-비교-연산자와-일치-비교--연산자의-반대-개념이다">부동등 비교 연산자(!=)와 불일치 비교 연산자(!==)는 각각 동등 비교(==) 연산자와 일치 비교 (===) 연산자의 반대 개념이다.</h5>
</blockquote>
<pre><code class="language-js">// 부동등 비교
5 != 8;   // -&gt; true
5 != 5;   // -&gt; false
5 != '5'; // -&gt; false

// 불일치 비교
5 !== 8;   // -&gt; true
5 !== 5;   // -&gt; false
5 !== '5'; // -&gt; true</code></pre>
<h4 id="732-대소-관계-비교-연산자">7.3.2 대소 관계 비교 연산자</h4>
<blockquote>
<h5 id="대소-관계-비교-연산자는-피연산자의-크기를-비교하여-불리언-값을-반환-한다">대소 관계 비교 연산자는 피연산자의 크기를 비교하여 불리언 값을 반환 한다</h5>
</blockquote>
<table>
<thead>
<tr>
<th>대소 관계 비교 연산자</th>
<th>예제</th>
<th>설명</th>
<th>부수효과</th>
</tr>
</thead>
<tbody><tr>
<td>&gt;</td>
<td>x&gt;y</td>
<td>x가y보다 크다</td>
<td>x</td>
</tr>
<tr>
<td>&lt;</td>
<td>x&lt;y</td>
<td>x가y보다 작다</td>
<td>x</td>
</tr>
<tr>
<td>&gt;=</td>
<td>x&gt;=y</td>
<td>x가y보다 크거나 같다</td>
<td>x</td>
</tr>
<tr>
<td>&lt;=</td>
<td>x&lt;=y</td>
<td>x가y보다 작거나 같다</td>
<td>x</td>
</tr>
</tbody></table>
<pre><code class="language-js">// 대소 관계 비교
5 &gt; 0;  // -&gt; true
5 &gt; 5;  // -&gt; false
5 &gt;= 5; // -&gt; true
5 &lt;= 5; // -&gt; true</code></pre>
<h3 id="74-삼항-조건-연산자">7.4 삼항 조건 연산자</h3>
<blockquote>
<h5 id="삼항-조건-연산자는-첫-번째-피연산자가-true로-평가되면-두-번째-피연산자를-반환하고-false로-평가되면-세-번째-피연산자를-반환한다-즉-삼항-조건-연산자는-두-번째-피연산자-또는-세-번째-피연산자로-평가되는-표현식이다">삼항 조건 연산자는 첫 번째 피연산자가 true로 평가되면 두 번째 피연산자를 반환하고, false로 평가되면 세 번째 피연산자를 반환한다. 즉 삼항 조건 연산자는 두 번째 피연산자 또는 세 번째 피연산자로 평가되는 표현식이다.</h5>
</blockquote>
<pre><code class="language-js">var result = score &gt;= 60 ? 'pass' : 'fail'
//만약 score가 60점 이상일 겨우 true이므로 pass가 출력
//만약 score가 60점 이하일 겨우 false이므로 fail이 출력</code></pre>
<pre><code class="language-js">var x = 2;

// 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
var result = x % 2 ? '홀수' : '짝수';

console.log(result); // 짝수</code></pre>
<h5 id="삼항-조건-연산자는-조건문-형식으로-표현이-가능하지만-값처럼-사용할-수는-없다">삼항 조건 연산자는 조건문 형식으로 표현이 가능하지만 값처럼 사용할 수는 없다.</h5>
<pre><code class="language-js">var x = 2, result;

// 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
if (x % 2) result = '홀수';
else       result = '짝수';

console.log(result); // 짝수</code></pre>
<pre><code class="language-js">var x = 10;

// if...else 문은 표현식이 아닌 문이다. 따라서 값처럼 사용할 수 없다.
var result = if (x % 2) { result = '홀수'; } else { result = '짝수'; };
// SyntaxError: Unexpected token if</code></pre>
<blockquote>
<h5 id="if-else-문과-달리-삼항-조건-연산자-표현식은-값으로-평가할-수-있는-표현식의-문이다">if else 문과 달리 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식의 문이다.</h5>
</blockquote>
<pre><code class="language-js">var x = 10;
// 삼항 조건 연산자 표현식은 표현식인 문이다. 따라서 값처럼 사용할 수 있다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수</code></pre>
<h5 id="조건에-따라-수행해야-할-문이-여러개면-삼항-조건-연산문보다-if-else문의-가독성이-좋다">조건에 따라 수행해야 할 문이 여러개면 삼항 조건 연산문보다 if else문의 가독성이 좋다.</h5>
<h3 id="75-논리-연산자">7.5 논리 연산자</h3>
<blockquote>
<h5 id="논리-연산자는-우항과-좌항의-피연산자부정-논리-연산자의-경우-우항의-피연산자를-논리-연산한다">논리 연산자는 우항과 좌항의 피연산자(부정 논리 연산자의 경우 우항의 피연산자)를 논리 연산한다.</h5>
</blockquote>
<table>
<thead>
<tr>
<th>논리 연산자</th>
<th>의미</th>
<th>부수 효과</th>
</tr>
</thead>
<tbody><tr>
<td>ll</td>
<td>논리합(or)</td>
<td>x</td>
</tr>
<tr>
<td>&amp;&amp;</td>
<td>논리곱(and)</td>
<td>x</td>
</tr>
<tr>
<td>!</td>
<td>부정(not)</td>
<td>x</td>
</tr>
</tbody></table>
<pre><code class="language-js">//논리합(or)은 둘 중 하나만 true여도 true
------------------------------------
true || true;   // -&gt; true
true || false;  // -&gt; true
false || true;  // -&gt; true
false || false; // -&gt; false

//논리곱(and)은 둘 다 true여야지 true
------------------------------------
true &amp;&amp; true;   // -&gt; true
true &amp;&amp; false;  // -&gt; false
false &amp;&amp; true;  // -&gt; false
false &amp;&amp; false; // -&gt; false

// 논리 부정(!)은 반대를 의미
-------------------------------------
!true;  // -&gt; false
!false; // -&gt; true</code></pre>
<h5 id="논리-부정-연산자는-불리언-값을-반환하지만-피연산자가-반드시-불리언-값일-필요는-없다-피연산자가-불리언-값이-아닐시-암묵적-불리언-타입으로-변환한다">논리 부정(!) 연산자는 불리언 값을 반환하지만 피연산자가 반드시 불리언 값일 필요는 없다. 피연산자가 불리언 값이 아닐시 암묵적 불리언 타입으로 변환한다.</h5>
<pre><code class="language-js">// 암묵적 타입 변환
!0;       // -&gt; true
!'Hello'; // -&gt; false</code></pre>
<h5 id="논리합-또는-논리곱-연산자-표현식의-경우-불리언이-아닌-2개의-피연산자중-어느-한쪽으로-평가-될-수도-있다">논리합(||) 또는 논리곱(&amp;&amp;) 연산자 표현식의 경우 불리언이 아닌 2개의 피연산자중 어느 한쪽으로 평가 될 수도 있다.</h5>
<pre><code class="language-js">// 단축 평가
'Cat' &amp;&amp; 'Dog'; // -&gt; 'Dog'</code></pre>
<h3 id="76-쉼표-연산자">7.6 쉼표 연산자</h3>
<h5 id="쉼표-연산자는-왼쪽-피연산자부터-차례대로-평가하고-평가가-끝나면-마지막-피연산자의-평가-결과를-반환한다">쉼표 연산자는 왼쪽 피연산자부터 차례대로 평가하고 평가가 끝나면 마지막 피연산자의 평가 결과를 반환한다</h5>
<pre><code class="language-js">var x, y, z;

x = 1, y = 2, z = 3; // 3</code></pre>
<h3 id="77-그룹-연산자">7.7 그룹 연산자</h3>
<h5 id="그룹-연산자는-연산자-우선순위가-가장-높다">그룹 연산자는 연산자 우선순위가 가장 높다</h5>
<pre><code class="language-js">10 * 2 + 3; // -&gt; 23

// 그룹 연산자를 사용하여 우선순위를 조절
10 * (2 + 3); // -&gt; 50</code></pre>
<h3 id="78-typeof-연산자">7.8 typeof 연산자</h3>
<blockquote>
<h5 id="typeof-연산자는-문자열stringnumberbooleanundefinedsymbolfunction중-하나를-반환한다">typeof 연산자는 문자열&quot;string&quot;,&quot;number&quot;,&quot;boolean&quot;,&quot;undefined&quot;,&quot;symbol&quot;,&quot;function&quot;중 하나를 반환한다.</h5>
</blockquote>
<pre><code>typeof ''              // -&gt; &quot;string&quot;
typeof 1               // -&gt; &quot;number&quot;
typeof NaN             // -&gt; &quot;number&quot;
typeof true            // -&gt; &quot;boolean&quot;
typeof undefined       // -&gt; &quot;undefined&quot;
typeof Symbol()        // -&gt; &quot;symbol&quot;
typeof null            // -&gt; &quot;object&quot;
typeof []              // -&gt; &quot;object&quot;
typeof {}              // -&gt; &quot;object&quot;
typeof new Date()      // -&gt; &quot;object&quot;
typeof /test/gi        // -&gt; &quot;object&quot;
typeof function () {}  // -&gt; &quot;function&quot;</code></pre><h5 id="null은-null이-아닌-object를-반환하는데-이것은-자바스크립트의-아직-수정되지-않은-버그이다-null-타입-확인은-연사자를-사용하는걸-권장된다">null은 null이 아닌 object를 반환하는데 이것은 자바스크립트의 아직 수정되지 않은 버그이다. null 타입 확인은 연사자(===)를 사용하는걸 권장된다.</h5>
<pre><code class="language-js">var foo = null;

typeof foo === null; // -&gt; false
foo === null;        // -&gt; true</code></pre>
<h5 id="선언하지-않은-식별자를-typeof-연산자로-연산해-보면-referenceerror가-발생하지-않고-undefined를-반환하는-거-역시-주의해야할-버그-중-하나다">선언하지 않은 식별자를 typeof 연산자로 연산해 보면 ReferenceError가 발생하지 않고 undefined를 반환하는 거 역시 주의해야할 버그 중 하나다</h5>
<pre><code class="language-js">// undeclared 식별자를 선언한 적이 없다.
typeof undeclared; // -&gt; undefined</code></pre>
<h3 id="79-지수-연산자">7.9 지수 연산자</h3>
<h5 id="지수-연산자는-좌항의-피연산자를-밑으로-우항의-피연산자를-지수로-거듭-제곱하여-숫자-값을-반환한다">지수 연산자는 좌항의 피연산자를 밑으로 우항의 피연산자를 지수로 거듭 제곱하여 숫자 값을 반환한다.</h5>
<pre><code class="language-js">2 ** 2;   // -&gt; 4
2 ** 2.5; // -&gt; 5.65685424949238
2 ** 0;   // -&gt; 1
2 ** -2;  // -&gt; 0.25</code></pre>
<h5 id="지수-연산자-이전에는-mathpow-메서드를-사용했다">지수 연산자 이전에는 Math.pow 메서드를 사용했다.</h5>
<pre><code class="language-js">Math.pow(2, 2);   // -&gt; 4
Math.pow(2, 2.5); // -&gt; 5.65685424949238
Math.pow(2, 0);   // -&gt; 1
Math.pow(2, -2);  // -&gt; 0.25

// 지수 연산자의 결합 순서는 우항에서 좌항이다. 즉, 우결합성을 갖는다.
2 ** (3 ** 2); // -&gt; 512
Math.pow(2, Math.pow(3, 2)); // -&gt; 512

// 음수를 거듭제곱의 밑으로 사용할려면 괄호로 묶어야 한다
-5 ** 2; // error
(-5) ** 2; // -&gt; 25</code></pre>
<h5 id="지수-연산자는-할당-연산자와-사용은-물론-이항-연산자-중에서-우선순위가-가장-높다">지수 연산자는 할당 연산자와 사용은 물론 이항 연산자 중에서 우선순위가 가장 높다.</h5>
<pre><code class="language-js">// 할당 연산자와 사용
var num = 5;
num **= 2; // -&gt; 25

// 우선순위가 제일 높다
2 * 5 ** 2; // -&gt; 50</code></pre>
<h3 id="710-그-외의-연산자">7.10 그 외의 연산자</h3>
<h5 id="옵셔널-체이닝이나-null병합-연산자-같은-그-외의-연산자는-뒤에서-정리하도록-하겠다">옵셔널 체이닝(?.)이나 null(??)병합 연산자 같은 그 외의 연산자는 뒤에서 정리하도록 하겠다.</h5>
<h3 id="711-연산자의-부수-효과">7.11 연산자의 부수 효과</h3>
<h5 id="대부분의-연산자는-다른-코드에-영향을-주지-않지만-할당-연산자-증가감소--연산자는-다른-코드에-영향을-주는-부수-효과가-있다">대부분의 연산자는 다른 코드에 영향을 주지 않지만 할당 연산자(=), 증가/감소(++/--)연산자는 다른 코드에 영향을 주는 부수 효과가 있다.</h5>
<pre><code class="language-js">var x;

// 할당 연산자는 변수 값이 변하는 부수 효과가 있다.
// 이는 x 변수를 사용하는 다른 코드에 영향을 준다.
x = 1;
console.log(x); // 1

// 증가/감소 연산자(++/--)는 피연산자의 값을 변경하는 부수 효과가 있다.
// 피연산자 x의 값이 재할당되어 변경된다. 이는 x 변수를 사용하는 다른 코드에 영향을 준다.
x++;
console.log(x); // 2</code></pre>
<h3 id="712-연산자-우선순위">7.12 연산자 우선순위</h3>
<table>
<thead>
<tr>
<th>우선순위</th>
<th>연산자</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>()</td>
</tr>
<tr>
<td>2</td>
<td>new(매개변수 존재), [](프로퍼티 접근),()(함수호출), ?.(옵셔널 체이닝 연산자)</td>
</tr>
<tr>
<td>3</td>
<td>new(매개변수 미존재)</td>
</tr>
<tr>
<td>4</td>
<td>x++,x--</td>
</tr>
<tr>
<td>5</td>
<td>!x,+x,-x,++x,typeof,delete</td>
</tr>
<tr>
<td>6</td>
<td>** (이항 연산자 중에서 우선수위가 제일 높다 )</td>
</tr>
<tr>
<td>7</td>
<td>*,/,%</td>
</tr>
<tr>
<td>8</td>
<td>+,-</td>
</tr>
<tr>
<td>9</td>
<td>&lt;,&lt;=,&gt;,&gt;=,in,instanceof</td>
</tr>
<tr>
<td>10</td>
<td>==,!=,===,!==</td>
</tr>
<tr>
<td>11</td>
<td>??(null 병합 연산자)</td>
</tr>
<tr>
<td>12</td>
<td>&amp;&amp;</td>
</tr>
<tr>
<td>13</td>
<td>ㅣㅣ</td>
</tr>
<tr>
<td>14</td>
<td>삼항 조건 연산자</td>
</tr>
<tr>
<td>15</td>
<td>할당 연산자(=,+=,-=,...)</td>
</tr>
<tr>
<td>16</td>
<td>,</td>
</tr>
</tbody></table>
<h3 id="713-연산자-결합-순서">7.13 연산자 결합 순서</h3>
<table>
<thead>
<tr>
<th>결합 순서</th>
<th>연산자</th>
</tr>
</thead>
<tbody><tr>
<td>좌항 -&gt; 우항</td>
<td>+,-,/,%,&lt;,&lt;=,&gt;,&gt;=,&amp;&amp;,ㅣㅣ,.,[],(),??,?.,in,instanceof</td>
</tr>
<tr>
<td>우항 -&gt; 좌항</td>
<td>++,--,할당연산자(=,+=,-=,...),!x,+x,-x,++x,--x,typeof,delete,삼항 조건 연산자, **</td>
</tr>
</tbody></table>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="objectis-메서드">object.is 메서드</h5>
<blockquote>
<p>동등 비교 연산자(==)와 알치 비교 연산자(===)는 +0과 -0을 동일하다고 평가하고 NaN와 NaN를 비교하면 다른 값이라고 평가한다. object.is 메서드는 예측 가능한 정확한 비교 결과로 반환한다.</p>
</blockquote>
<pre><code>-0 === +0;         // -&gt; true
Object.is(-0, +0); // -&gt; false

NaN === NaN;         // -&gt; false
Object.is(NaN, NaN); // -&gt; true</code></pre><h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/07.md">wikibooks</a></h4>