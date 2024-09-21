<h2 id="11-원시-값과-객체의-비교">11. 원시 값과 객체의 비교</h2>
<hr />
<blockquote>
<ul>
  <li> 원시타입 : 변경 불가능한 값,변수에 할당 시 실제 값이 저장,원시 값이 복사
  <li> 객체타입 : 변경 가능한 값, 변수에 할당 시 참조 값이 저장, 참조 값이 복사
  </ul>
</blockquote>
<h3 id="111-원시-값">11.1 원시 값</h3>
<h4 id="1111-변경-불가능한-값">11.1.1 변경 불가능한 값</h4>
<blockquote>
<p>원시 타입의 값, 즉 원시 값은 변경 불가능 한 값
<br />변경 불가능 하다는 것은 변수가 아니라 값에 대한 진술이다</p>
</blockquote>
<h5 id="변수는-언제든지-재할당을-통해-값을-변경-할-수-있지만-상수는-단-한번만-할당이-가능하므로-변수-값을-변경-할-수-없다">변수는 언제든지 재할당을 통해 값을 변경 할 수 있지만 상수는 단 한번만 할당이 가능하므로 변수 값을 변경 할 수 없다.</h5>
<pre><code class="language-js">// const 키워드를 사용해 선언한 변수는 재할당이 금지된다. 상수는 재할당이 금지된 변수일 뿐이다.
const o = {};

// const 키워드를 사용해 선언한 변수에 할당한 원시값(상수)은 변경할 수 없다.
// 하지만 const 키워드를 사용해 선언한 변수에 할당한 객체는 변경할 수 있다.
o.a = 1;
console.log(o); // {a: 1}</code></pre>
<blockquote>
<p>원시 값을 재할당 한다는 것은 이전의 원시 값을 변경하는게 아니라 새로운 메모리 공간을 확보하고 재할당 한 값을 새로운 메모리에 저장한 후 새로운 메모리 공간의 주소를 참조한다는 의미이다.<br />
즉 이것을 불변성이라고 하는데 불변성을 같는 원시 값을 할당한 변수는 재할당 이외에 변변수 값을 변경할 수 있는 방법이 없다.</p>
</blockquote>
<h4 id="1112-문자열과-불변성">11.1.2 문자열과 불변성</h4>
<h5 id="밑의-예시에서-두번째-문이-실행되면-이전에-hello가-수정되는-것이-아니라-새로운-문자열-world를-생성하고-식별자-str을-이것을-가리킨다-즉-hello와-world는-둘다-메모리에-존재하고-식별자-str이-가리키는-메모리만-변경-된-것-이다">밑의 예시에서 두번째 문이 실행되면 이전에 hello가 수정되는 것이 아니라 새로운 문자열 world를 생성하고 식별자 str을 이것을 가리킨다. 즉 hello와 world는 둘다 메모리에 존재하고 식별자 str이 가리키는 메모리만 변경 된 것 이다.</h5>
<pre><code class="language-js">var str = &quot;hello&quot;
str = 'world'
// world</code></pre>
<h5 id="문자열은-변경-불가능한-값이기-때문에-s로-변경이-안된다">문자열은 변경 불가능한 값이기 때문에 'S'로 변경이 안된다</h5>
<pre><code class="language-js">var str = 'string';

// 문자열은 유사 배열이므로 배열과 유사하게 인덱스를 사용해 각 문자에 접근할 수 있다.
// 하지만 문자열은 원시값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다.
str[0] = 'S';

console.log(str); // string</code></pre>
<h5 id="변수에-문자열을-변경하는-것이-아닌-새로운-문자열을-재할당-하는-것은-가능하다">변수에 문자열을 변경하는 것이 아닌 새로운 문자열을 재할당 하는 것은 가능하다.</h5>
<h4 id="1113-값에-의한-전달">11.1.3 값에 의한 전달</h4>
<h5 id="변수에-원시-값을-갖는-변수를-할당하면-할당받는-변수에는-할당되는-변수의-원시-값이-복사되어-전달된다-이를-값에-의한-전달이라-한다">변수에 원시 값을 갖는 변수를 할당하면 할당받는 변수에는 할당되는 변수의 원시 값이 복사되어 전달된다. 이를 값에 의한 전달이라 한다.</h5>
<pre><code class="language-js">var score = 80;
// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy); // 80,80
console.log(score === copy); // true
</code></pre>
<h5 id="score와-copy의-값-80은-다른-메모리-공간이-저장된-별개의-값이다-그렇기-때문에-score값을-변경해도-copy-변수의-값에는-어떠한-영향도-주지-않는다">score와 copy의 값 80은 다른 메모리 공간이 저장된 별개의 값이다. 그렇기 때문에 score값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않는다</h5>
<pre><code class="language-js">var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy);    // 80  80
console.log(score === copy); // true

score = 100;

console.log(score, copy);    // 100  80
console.log(score === copy); // false</code></pre>
<blockquote>
<p>값에 의한 표현은 오해가 있을 수 있는데 엄격하게 표현하면 변수에는 사실 값이 전달되는 것이 아니라 메모리 주소가 전달되기 때문이다. 이는 변수와 같은 식별자는 값이 아니라 메모리 주소를 기억하고 전달 하고 있기 때문이다. </p>
</blockquote>
<h5 id="값에-의한-전달은-2가지-평가-방식이-있는데-예를-들어-보자">값에 의한 전달은 2가지 평가 방식이 있는데 예를 들어 보자</h5>
<pre><code class="language-js">var score = 80;
var copy = score;</code></pre>
<ol>
<li>새로운 80을 생성해서 메모리 주소를 전달하는 방식, 이 방식은 할당 시점에 두 변수가 기억하는 메모리 주소가 다르다.
<img alt="" src="https://velog.velcdn.com/images/anstks1992/post/02af2d03-14c6-418f-a9d7-5c4ea0218b59/image.png" /></li>
</ol>
<ol start="2">
<li>score의 변수값 80의 메모리 주소를 그대로 전달하는 방식, 이 방식은 할당 시점에 두 변수가 기억하는 메모리 주소가 같다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/ec001c8b-e6cb-4124-a9f5-5ba2d2b30b46/image.png" /></p>
<blockquote>
<p>이처럼 값의 의한 전달은 값을 전달하는 것이 아니라 메모리 주소를 전달하는데 전달된 메모리 주소를 통해 메모리 공간에 접근하면 값을 참조할 수 있다.<br />
중요한것은 어느 시점이든 결국은 두 변수의 원시 값을 서로 다른 메모리 공간에 저장된 별개의 값이 되어 어느 한쪽에서 재할당을 통해 값을 변경하더라도 서로 간섭할 수 없다는 것이다.</p>
</blockquote>
<h3 id="112-객체">11.2 객체</h3>
<h4 id="1121-변경-가능한-값">11.2.1 변경 가능한 값</h4>
<blockquote>
<p>객체(참조) 타입의 값, 즉 객체는 변경 가능한 값</p>
</blockquote>
<h5 id="객체를-할당한-변수가-기억하는-메모리-주소를-통해-메모리-공간에-접근하며-참조-값변수에-생성된-객체의-메모리-주소에-접근-할-수-있다">객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하며 참조 값(변수에 생성된 객체의 메모리 주소)에 접근 할 수 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/3516b2a8-eaae-48a0-ab2b-c595067498c4/image.png" /></p>
<pre><code class="language-js">// 할당이 이뤄지는 시점에 객체 리터럴이 해석되고, 그 결과 객체가 생성된다.
var person = {
  name: 'Lee'
};

// person 변수에 저장되어 있는 참조값으로 실제 객체에 접근해서 그 객체를 반환한다.
console.log(person); // {name: &quot;Lee&quot;}</code></pre>
<blockquote>
<p>원시 값은 변경 불가능한 값이므로 원시 값을 갖는 변수의 값을 변경할려면 재할당 외에는 방법이 없다. 하지만 객체는 변경 가능한 값이다.<br /> 
따라서 객체를 할당한 변수는 재할당 없이 객체를 직접 변경할 수 있다.<br />
즉 재할당 없이 프로퍼티를 동적으로 추가할 수 있고 프로퍼티 값을 갱신할 수도 있으며 프로퍼티 자체를 삭제할 수도 있다.</p>
</blockquote>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// 프로퍼티 값 갱신
person.name = 'Kim';

// 프로퍼티 동적 생성
person.address = 'Seoul';

console.log(person); // {name: &quot;Kim&quot;, address: &quot;Seoul&quot;}</code></pre>
<h5 id="원시-값은-변경-불가능-하지만-객체는-변경-가능한-값으므로-메모리에-저장된-객체를-직접-수정할-수-있다">원시 값은 변경 불가능 하지만 객체는 변경 가능한 값으므로 메모리에 저장된 객체를 직접 수정할 수 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/19ff0961-be2b-4819-8d13-a8ccd2b5df69/image.png" /></p>
<h4 id="1122-참조에-의한-전달">11.2.2 참조에 의한 전달</h4>
<blockquote>
<p>객체를 가르키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달이라 한다.</p>
</blockquote>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// 참조값을 복사(얕은 복사)
var copy = person;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/0fba3d39-cc4e-4996-9056-839998d97904/image.png" /></p>
<h5 id="원본-person을-사본-copy에-할당하면-원본-person의-참조-값을-복사해서-copy에-저장한다-이-경우-저장된-메모리-주소는-다르지만-동일한-참조값을-갖는다-즉-원본과-사본이-모두-동일-객체를-가치기며-이것은-두-개의-식별자가-하나의-객체를-공유한다는-것을-의미한다-이-경우-어느-한쪽에서-객체를-변경하면-서로-영향을-받는다는-단점이-있다">원본 person을 사본 copy에 할당하면 원본 person의 참조 값을 복사해서 copy에 저장한다. 이 경우 저장된 메모리 주소는 다르지만 동일한 참조값을 갖는다. 즉 원본과 사본이 모두 동일 객체를 가치기며 이것은 두 개의 식별자가 하나의 객체를 공유한다는 것을 의미한다. 이 경우 어느 한쪽에서 객체를 변경하면 서로 영향을 받는다는 단점이 있다.</h5>
<pre><code class="language-js">var person = {
  name: 'Lee'
};

// 참조값을 복사(얕은 복사). copy와 person은 동일한 참조값을 갖는다.
var copy = person;

// copy와 person은 동일한 객체를 참조한다.
console.log(copy === person); // true

// copy를 통해 객체를 변경한다.
copy.name = 'Kim';

// person을 통해 객체를 변경한다.
person.address = 'Seoul';

// copy와 person은 동일한 객체를 가리킨다.
// 따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다.
console.log(person); // {name: &quot;Kim&quot;, address: &quot;Seoul&quot;}
console.log(copy);   // {name: &quot;Kim&quot;, address: &quot;Seoul&quot;}</code></pre>
<blockquote>
<p>자바스크립트에서는 결론적으로 '참조에 의한 전달'은 존재하지 않고 '값에 의한 전달'만이 존재한다</p>
</blockquote>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="자바스크립트-객체의-관리-방식">자바스크립트 객체의 관리 방식</h5>
<blockquote>
<p>일반적으로 다른 객체지향 언어는 사전에 정의된 클래스를 기반으로 객체(인스턴스)를 생성한다. 다시말해 객체를 생성하기 이전에 이미 프로퍼티와 메서드가 정해져 있으며 그대로 객체를 생성한다.<br />
이에반해 자바스크립트는 클래스 없이 객체를 생성하며 동적으로 프로퍼티와 메서드를 추가할 수 있다. 이는 사용에 편리성이 있지만 생성과 프로퍼티 접근에 비용이 많이 든다는 단점이 있다 </p>
</blockquote>
<h5 id="얕은-복사와-깊은-복사">얕은 복사와 깊은 복사</h5>
<blockquote>
<p>객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한 단계까지만 복사하는 것을 말하고 깉은 복사는 객체에 중첩되어 있는 객체까지 모두 복사하는 것을 말한다.</p>
</blockquote>
<pre><code class="language-js">const o = { x: { y: 1 } };

// 얕은 복사
const c1 = { ...o }; // 35장 &quot;스프레드 문법&quot; 참고
console.log(c1 === o); // false
console.log(c1.x === o.x); // true

// lodash의 cloneDeep을 사용한 깊은 복사
// &quot;npm install lodash&quot;로 lodash를 설치한 후, Node.js 환경에서 실행
const _ = require('lodash');
// 깊은 복사
const c2 = _.cloneDeep(o);
console.log(c2 === o); // false
console.log(c2.x === o.x); // false</code></pre>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/11.md">wikibooks</a></h4>