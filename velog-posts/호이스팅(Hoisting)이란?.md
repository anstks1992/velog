<p>호이스팅(Hoisting)은 자바스크립트의 독특한 동작 방식 중 하나로, 변수와 함수 선언이 실제 코드가 실행되기 전에 상단으로 끌어올려지는 것처럼 동작하는 특성이다.<br />
인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다. 이로 인해 코드 작성 순서와 관계없이 변수나 함수에 접근할 수 있게 된다.</p>
<p>호이스팅의 두 가지 주요 대상은 변수 선언과 함수 선언이다.</p>
<h2 id="변수-선언의-호이스팅">변수 선언의 호이스팅</h2>
<p>자바스크립트에서 변수 선언은 호이스팅되지만, 값의 할당은 호이스팅되지 않는다. 선언만 끌어올려지고, 실제 값은 선언된 위치에서 할당된다.</p>
<h3 id="var로-선언된-변수의-호이스팅">var로 선언된 변수의 호이스팅</h3>
<p>var는 런타임 이전에 '선언 단계'와 '초기화 단계'가 한번에 진행된다</p>
<pre><code class="language-js">// var 키워드로 선언한 변수는 런타임 이전에 선언 단계와 초기화 단계가 실행된다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 있다.
console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1</code></pre>
<h3 id="let과-const로-선언된-변수의-호이스팅">let과 const로 선언된 변수의 호이스팅</h3>
<p>let,const 키워드는 var와 달리 '선언 단계'와 '초기화 단계'가 분리되어 진행된다. </p>
<pre><code class="language-js">// 런타임 이전에 선언 단계가 실행된다. 아직 변수가 초기화되지 않았다.
// 초기화 이전의 일시적 사각 지대에서는 변수를 참조할 수 없다.
console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1</code></pre>
<p>변수 호이스팅에 대해 좀 더 자세하게 알고싶으면 <a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-15-letconst-%ED%82%A4%EC%9B%8C%EB%93%9C%EC%99%80-%EB%B8%94%EB%A1%9D-%EB%A0%88%EB%B2%A8-%EC%8A%A4%EC%BD%94%ED%94%84">여기</a>를 참고하자.</p>
<h2 id="함수-선언의-호이스팅">함수 선언의 호이스팅</h2>
<p>함수 선언도 호이스팅되며, 함수 전체가 코드 상단으로 끌어올려지는 것처럼 동작한다. 함수는 호출 위치와 관계없이 정상적으로 동작한다.</p>
<pre><code class="language-js">sayHi();  //호출 //&quot;Hello!&quot;

function sayHi() { // 선언
  console.log(&quot;Hello!&quot;);
}

sayHi();</code></pre>
<p>위 코드에서 함수 선언이 호출보다 아래에 있어서 동작이 안되는 것처럼 보이지만 정상적으로 작동한다. 함수 선언이 완전히 호이스팅되어 코드 상단에서 선언된 것처럼 동작하기 때문이다.</p>
<h3 id="함수-표현식">함수 표현식</h3>
<p>함수 표현식은 변수에 할당된 함수이다. 이 경우, 변수의 호이스팅 특성에 따라 함수 표현식은 선언 후에만 사용할 수 있다.</p>
<pre><code class="language-js">sayHi();  // TypeError: sayHi is not a function

var sayHi = function() {
  console.log(&quot;Hi!&quot;);
};</code></pre>
<p>함수 호이스팅에 대해 좀 더 자세하게 알고 싶으면 <a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-12-%ED%95%A8%EC%88%98">여기</a>를 참고하자</p>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-12-%ED%95%A8%EC%88%98">[자바스크립트 Deep Dive] 12 함수</a>
<a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-15-letconst-%ED%82%A4%EC%9B%8C%EB%93%9C%EC%99%80-%EB%B8%94%EB%A1%9D-%EB%A0%88%EB%B2%A8-%EC%8A%A4%EC%BD%94%ED%94%84">[자바스크립트 Deep Dive] 15 let,const 키워드와 블록 레벨 스코프</a></p>