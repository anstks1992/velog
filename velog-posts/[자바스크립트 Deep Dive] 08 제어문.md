<h2 id="08-제어문">08. 제어문</h2>
<hr />
<blockquote>
<h5 id="제어문은-조건에-따라-코드-블록을-실행조건문하거나-실행반목문할-때-사용한다">제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 실행(반목문)할 때 사용한다.</h5>
</blockquote>
<h3 id="81-블록문">8.1 블록문</h3>
<blockquote>
<h5 id="블록문은-0개-이상의-문을-중괄호로-묶은-것으로-자바스크립트는-블록문을-하나의-실행-단위로-취급한다-일반적으로-제어문이나-함수를-정의할-때-사용하는-것이-일반적이다">블록문은 0개 이상의 문을 중괄호로 묶은 것으로 자바스크립트는 블록문을 하나의 실행 단위로 취급한다. 일반적으로 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.</h5>
</blockquote>
<pre><code class="language-javascript">// 블록문
{
  var foo = 10;
}

// 제어문
var x = 1;
if (x &lt; 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}</code></pre>
<h3 id="82-조건문">8.2 조건문</h3>
<blockquote>
<h5 id="조건문은-주어진-조건식의-평가-결과에-따라-블록문의-실행을-결정하며-조건식은-불리언-값으로-평가될-수-잇는-표현식이다">조건문은 주어진 조건식의 평가 결과에 따라 블록문의 실행을 결정하며 조건식은 불리언 값으로 평가될 수 잇는 표현식이다</h5>
</blockquote>
<h4 id="821-ifelse-문">8.2.1 if...else 문</h4>
<h5 id="if-문의-조건식은-불리언-값으로-평가되며-불리언-값이-아닌-값으로-평가되면-암묵적으로-불리언-값으로-강제-변환된다">if 문의 조건식은 불리언 값으로 평가되며 불리언 값이 아닌 값으로 평가되면 암묵적으로 불리언 값으로 강제 변환된다.</h5>
<pre><code class="language-javascript"> if(조건식){
 //조건식1이 참이면 이 코드 블록이 실행된다
 //두번 이상 사용x
} else if(조건식2) {
 //조건식2가 참이면 이 코드 블록이 실행된다
 //여러번 사용 가능
}
else { 
 //조건식이 거짓이면 이 코드 블록이 실행된다
 //두번 이상 사용x
}</code></pre>
<pre><code class="language-javascript">// if 문
if (num &gt; 0) {
  kind = '양수'; // 음수를 구별할 수 없다
}
console.log(kind); // 양수

// if...else 문
if (num &gt; 0) {
  kind = '양수';
} else {
  kind = '음수'; // 0은 음수가 아니다.
}
console.log(kind); // 양수

// if...else if 문
if (num &gt; 0) {
  kind = '양수';
} else if (num &lt; 0) {
  kind = '음수';
} else {
  kind = '영';
}
console.log(kind); // 양수</code></pre>
<h5 id="대부분의-if-else-문은-삼항-조건-연산자로-바꿔-쓸-수-있다">대부분의 if else 문은 삼항 조건 연산자로 바꿔 쓸 수 있다.</h5>
<pre><code class="language-javascript">-if else문

// x가 짝수이면 result 변수에 문자열 '짝수'를 할당하고, 홀수이면 문자열 '홀수'를 할당한다.
var x = 2;
var result;

if (x % 2) { // 2 % 2는 0이다. 이때 0은 false로 암묵적 강제 변환된다.
  result = '홀수';
} else {
  result = '짝수';
}

console.log(result); // 짝수

-삼항 조건 연산자

var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수

-경우의 수가 세가지인 경우
var num = 2;

// 0은 false로 취급된다.
var kind = num ? (num &gt; 0 ? '양수' : '음수') : '영';

console.log(kind); // 양수
</code></pre>
<h5 id="조건에-따라-단순히-값을-결정하여-변수에-할당하는-경우-if-else문보다-삼항-조건-연산자를-사용하는-편이-가독성이-좋다-하지만-실행해야-할-내용이-복잡하여-여러-줄의-문이-필요하다면-if-else문이-가독성이-더-좋다">조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 if else문보다 삼항 조건 연산자를 사용하는 편이 가독성이 좋다. 하지만 실행해야 할 내용이 복잡하여 여러 줄의 문이 필요하다면 if else문이 가독성이 더 좋다</h5>
<h4 id="822-switch문">8.2.2 switch문</h4>
<blockquote>
<h5 id="switch-문은-주어진-표현식을-평가하여-그-값과-일치하는-표현식을-갖는-case-문으로-실행-흐름을-옮긴다">switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다.</h5>
</blockquote>
<pre><code class="language-javascript">switch (표현식){
case 표현식1:
switch 문의 표현식과 표현식1이 일치하면 실행되는 문
break;
case 표현식2:
switch 문의 표현식과 표현식2이 일치하면 실행되는 문
break;
default:
switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문 
}</code></pre>
<h5 id="불리언-값으로-평가되는-if-else문과-달리-switch문의-표현식은-문자열이나-숫자-값인-경우가-많다">불리언 값으로 평가되는 if else문과 달리 switch문의 표현식은 문자열이나 숫자 값인 경우가 많다.</h5>
<h5 id="break가-없으면-실행문이-switch-문을-탈출하지-않고-switch-문이-끝날-때까지-이후의-모든-case-문과-default-문을-실행한다">break가 없으면 실행문이 switch 문을 탈출하지 않고 switch 문이 끝날 때까지 이후의 모든 case 문과 default 문을 실행한다.</h5>
<h5 id="다시말해-monthname-변수에-november가-할당된-후-switch-문을-탈출하지-않고-연이어-december가-제할당되고-마지막으로-invalid-month가-할당되어-출력된다">다시말해 monthName 변수에 November가 할당된 후 switch 문을 탈출하지 않고 연이어 december가 제할당되고 마지막으로 invalid month가 할당되어 출력된다</h5>
<pre><code class="language-javascript">// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1: monthName = 'January';
    break;
  case 2: monthName = 'February';
    break;
  case 3: monthName = 'March';
    break;
  case 4: monthName = 'April';
    break;
  case 5: monthName = 'May';
    break;
  case 6: monthName = 'June';
    break;
  case 7: monthName = 'July';
    break;
  case 8: monthName = 'August';
    break;
  case 9: monthName = 'September';
    break;
  case 10: monthName = 'October';
    break;
  case 11: monthName = 'November';
    break;
  case 12: monthName = 'December';
    break;
  default: monthName = 'Invalid month';
}

console.log(monthName); // November</code></pre>
<h5 id="default-문은-switch-문의-맨-마지막에-위치하므로-default-문의-실행히-종료되면-switch-문을-빠져나간다">default 문은 switch 문의 맨 마지막에 위치하므로 default 문의 실행히 종료되면 switch 문을 빠져나간다.</h5>
<pre><code class="language-javascript">var year = 2000; // 2000년은 윤년으로 2월이 29일이다.
var month = 2;
var days = 0;

switch (month) {
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    // 윤년 계산 알고리즘
    // 1. 연도가 4로 나누어떨어지는 해(2000, 2004, 2008, 2012, 2016, 2020...)는 윤년이다.
    // 2. 연도가 4로 나누어떨어지더라도 연도가 100으로 나누어떨어지는 해(2000, 2100, 2200...)는 평년이다.
    // 3. 연도가 400으로 나누어떨어지는 해(2000, 2400, 2800...)는 윤년이다.
    days = ((year % 4 === 0 &amp;&amp; year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}

console.log(days); // 29</code></pre>
<h3 id="83-반복문">8.3 반복문</h3>
<blockquote>
<h5 id="반복문은-조건식의-평가-결과가-참인-경우-코드-블록을-실행한다-그후-조건식을-다시-평가하여-여전히-참인-경우-코드-블록을-다시-실행하며-조건식이-거짓일-때까지-반복된다">반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행하며 조건식이 거짓일 때까지 반복된다</h5>
</blockquote>
<h4 id="831-for-문">8.3.1 for 문</h4>
<blockquote>
<p>for(변수 선언문 또는 할당문; 조건문; 증감식){
 조건식이 참인 경우 반복 실행될 문;
}</p>
</blockquote>
<h5 id="for문은-조건식이-평가될-때가지-코드-블록을-반복한다">for문은 조건식이 평가될 때가지 코드 블록을 반복한다</h5>
<pre><code class="language-javascript">for (var i = 0; i &lt; 2; i++) {
  console.log(&quot;결과값:&quot;,i);
}

결과값: 0,1</code></pre>
<blockquote>
<h5 id="for문-실행-순서">for문 실행 순서</h5>
</blockquote>
<ol>
<li>for 문을 실행하면 맨 먼저 변수 선언문 var i = 0이 실행된다. 변수 선언문은 단 한 번만 실행된다. </li>
<li>변수 선언문의 실행이 종료되면 조건식이 실행된다. 현재 i 변수의 값은 0으므로 조건식의 평과 결과는 true이다</li>
<li>조건식의 평과 결과가 true이므로 코드 블록이 실행된다. 증감문으로 실행 흐름이 이동하는 것이 아니라 코드 블록으로 실행 흐름이 이동하는 것에 주의</li>
  <li>코드 블록의 실행이 종료되면 증감식 i++가 실행되어 i 변수의 값은 1이 된다</li>
<li>증감식 실행이 종료되면 다시 조건식이 실행된다. 변수 선언문이 실행되는 것이 아니라 조건식이 실행되는다는 점에 주의하자(앞에 언급 했듯이 변수 선언문은 단 한번만 실행된다) 현재 i 변서의 값은 1이므로 조건식의 평가 결과는 true이다.</li>
  <li>조건식의 평가 결과가 true이므로 코드 블록이 다시 실행된다. </li>
<li>코드 블록의 실행이 종료되면 증감식 i++가 실행되여 i 변수의 값은 2가 된다.
<li>증감식 실행이 종료되면 다시 조건식이 실행도니다. 현재 i 변수의 값은 2이므로 조건식의 평가 결과는 false다. 조건식의 평가 결과가 false이므로 for 문이 실행이 종료된다.</li>
</ol>

<h5 id="for문-내에-for문을-중첩해-사용할-수-있다-이름-중첩-for문-이라고-한다">for문 내에 for문을 중첩해 사용할 수 있다. 이름 중첩 for문 이라고 한다</h5>
<pre><code class="language-javascript">//두 눈의 합이 6이 되는 모든 경우의 수 구하기
for (var i = 1; i &lt;= 6; i++) {
  for (var j = 1; j &lt;= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]`);
  }
}

[1,5]
[2,4]
[3,3]
[4,2]
[5,1]</code></pre>
<h4 id="832-while-문">8.3.2 while 문</h4>
<blockquote>
<h5 id="while문은-주어진-조건식의-평가-결과가-참이면-코드-블록을-계속해서-반복-실행하고-for문과-달리-반복-횟수가-불명확할-때-주로-사용한다">while문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행하고 for문과 달리 반복 횟수가 불명확할 때 주로 사용한다.</h5>
</blockquote>
<pre><code class="language-javascript">var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count &lt; 3) {
  console.log(count); // 0 1 2
  count++;
}</code></pre>
<h5 id="조건식의-평가-결과가-언제나-참이면-무한루프가-되고-무한루프에서-탈출하기-위헤서는-코드-블록-내에-if문으로-탈출-존건을-만들고-break-문으로-탈출한다">조건식의 평가 결과가 언제나 참이면 무한루프가 되고 무한루프에서 탈출하기 위헤서는 코드 블록 내에 if문으로 탈출 존건을 만들고 break 문으로 탈출한다</h5>
<pre><code class="language-javascript">var count = 0;

// 무한루프
while (true) {
  console.log(count);
  count++;
  // count가 3이면 코드 블록을 탈출한다.
  if (count === 3) break;
} // 0 1 2</code></pre>
<h4 id="833-dowhile-문">8.3.3 do...while 문</h4>
<blockquote>
<h5 id="do-while문은-코드-블록을-먼저-실행하고-조건식을-평가한다-따라서-코드-불록은-무조건-한-번-이상-실행한다">do while문은 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드 불록은 무조건 한 번 이상 실행한다.</h5>
</blockquote>
<pre><code class="language-javascript">var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count &lt; 3); // 0 1 2</code></pre>
<h3 id="84-break문">8.4 break문</h3>
<h5 id="switch레이블-문-반복문의-코드-블록-외에-break-문을-사용하면-에러가-발생한다">switch,레이블 문, 반복문의 코드 블록 외에 break 문을 사용하면 에러가 발생한다</h5>
<pre><code class="language-js">if (true) {
  break; // Uncaught SyntaxError: Illegal break statement
}</code></pre>
<h5 id="break문은-반복문을-더-이상-진행하지-않아도-될-때-불필요한-반복을-회피할-수-있어-유용하다">break문은 반복문을 더 이상 진행하지 않아도 될 때 불필요한 반복을 회피할 수 있어 유용하다.</h5>
<pre><code class="language-js">var string = 'Hello World.';
var search = 'l';
var index;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i &lt; string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === search) {
    index = i;
    break; // 반복문을 탈출한다.
  }
}

console.log(index); // 2

// 참고로 String.prototype.indexOf 메서드를 사용해도 같은 동작을 한다.
console.log(string.indexOf(search)); // 2</code></pre>
<h3 id="85-continue문">8.5 continue문</h3>
<h5 id="continue문은-반복문의-코드-블록-실행을-현-지점에서-중단하고-반복문의-증감식으로-실행-흐름을-이동시킨다-이때-break문처럼-반복문을-탈출하지-않는다">continue문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. 이때 break문처럼 반복문을 탈출하지 않는다</h5>
<pre><code class="language-js">var string = 'Hello World.';
var search = 'l';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i &lt; string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.match 메서드를 사용해도 같은 동작을 한다.
const regexp = new RegExp(search, 'g');
console.log(string.match(regexp).length); // 3</code></pre>
<pre><code class="language-js">// continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.
for (var i = 0; i &lt; string.length; i++) {
  // 'l'이면 카운트를 증가시킨다.
  if (string[i] === search) {
    count++;
    // code
    // code
    // code
  }
}

// continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i &lt; string.length; i++) {
  // 'l'이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== search) continue;

  count++;
  // code
  // code
  // code
}</code></pre>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/08.md">wikibooks</a></h4>