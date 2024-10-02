<p>var, let, const는 모두 JavaScript에서 변수를 선언할 때 사용하는 키워드이다. 각각의 동작 방식과 특성이 다르며, 이 차이를 이해하는 것이 중요하다.</p>
<h2 id="var">var</h2>
<p>var는 ES6 이전에 변수를 선언할 때 사용된 유일한 방법이었지만 let,const의 출현이후로는 사용이 권장되지는 않고 있다.</p>
<ul>
<li>스코프 : var는 함수 스코프를 가진다. 즉, 함수 내부에서 선언된 var 변수는 함수 전체에서 접근할 수 있다. 블록 스코프(if, for 등)에서는 블록 밖에서도 변수를 사용할 수 있다.
<li>재선언, 재할당 가능 : var로 선언된 변수는 같은 스코프 내에서 재선언할 수 있다.
<li>호이스팅 : var로 선언된 변수는 선언부가 해당 스코프의 최상단으로 끌어올려지는 특성을 가진다. 하지만, 변수가 선언되기 전에 값을 할당하려고 하면 undefined가 출력된다.
</ul>

<h2 id="let">let</h2>
<p>let은 ES6에서 도입된 변수 선언 방식이다. var의 문제점을 해결하기 위해 만들어졌다.</p>
<ul>
<li>스코프 : let은 블록 스코프를 가진다. 즉, let으로 선언된 변수는 해당 블록 내에서만 접근 가능하다.
<li>재선언 불가, 재할당 가능 : let으로 선언된 변수는 같은 스코프 내에서 재선언이 불가하고 재할당이 가능하다.
<li> 호이스팅 : let도 호이스팅되지만, 변수를 사용할 수 있는 시점은 선언된 이후다. 선언 전에 접근하려고 하면 오류가 발생한다.
</ul>

<h2 id="const">const</h2>
<p>const는 상수(constant)를 선언할 때 사용되며, let과 유사한 특성을 가지고 있지만 몇 가지 차이점이 있다.</p>
<ul>
<li> 스코프 : const는 let과 동일하게 블록 스코프를 가진다.
<li> 재선언 불가 : const로 선언된 변수는 재선언할 수 없다.
<li> 상수값 : const로 선언된 변수는 값을 재할당할 수 없다 하지만, const가 객체나 배열을 가리킬 경우, 그 내부의 값을 변경하는 것은 가능하다.
<li>호이스팅 : let과 같은 방식으로 호스팅이 된다.
</ul>

<h2 id="정리">정리</h2>
<table>
<thead>
<tr>
<th></th>
<th>var</th>
<th>let</th>
<th>const</th>
</tr>
</thead>
<tbody><tr>
<td>재할당</td>
<td>o</td>
<td>o</td>
<td>x</td>
</tr>
<tr>
<td>재선언</td>
<td>o</td>
<td>x</td>
<td>x</td>
</tr>
<tr>
<td>초기화 필요 여부</td>
<td>x</td>
<td>x</td>
<td>o</td>
</tr>
<tr>
<td>호이스팅</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐, 값은 undefined</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐</td>
<td>변수 선언이 스코프의 최상단으로 끌어올려짐</td>
</tr>
<tr>
<td>초기화</td>
<td>선언과동시에</td>
<td>선언-&gt;TDZ(일시적 사각지대)-&gt;초기화</td>
<td>선언-&gt;TDZ(일시적 사각지대)-&gt;초기화</td>
</tr>
<tr>
<td>스코프</td>
<td>함수</td>
<td>블록</td>
<td>블록</td>
</tr>
</tbody></table>
<p>좀더 자세하게 알고싶으면 <a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-15-letconst-%ED%82%A4%EC%9B%8C%EB%93%9C%EC%99%80-%EB%B8%94%EB%A1%9D-%EB%A0%88%EB%B2%A8-%EC%8A%A4%EC%BD%94%ED%94%84">여기</a>를 참고하자</p>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://velog.io/@anstks1992/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-15-letconst-%ED%82%A4%EC%9B%8C%EB%93%9C%EC%99%80-%EB%B8%94%EB%A1%9D-%EB%A0%88%EB%B2%A8-%EC%8A%A4%EC%BD%94%ED%94%84">[자바스크립트 Deep Dive] 15 let,const 키워드와 블록 레벨 스코프</a></p>