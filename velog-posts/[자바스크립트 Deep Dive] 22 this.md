<h2 id="22-this">22. this</h2>
<hr />
<h3 id="221-this-키워드">22.1 this 키워드</h3>
<blockquote>
<p>메서드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.</p>
</blockquote>
<pre><code class="language-js">const circle = {
  // 프로퍼티: 객체 고유의 상태 데이터
  radius: 5,
  // 메서드: 상태 데이터를 참조하고 조작하는 동작
  getDiameter() {
    // 이 메서드가 자신이 속한 객체의 프로퍼티나 다른 메서드를 참조하려면
    // 자신이 속한 객체인 circle을 참조할 수 있어야 한다.
    return 2 * circle.radius;
  }
};

console.log(circle.getDiameter()); // 10</code></pre>
<h5 id="자기-자신이-속한-객체를-재귀적으로-참조하는-방식은-옳지-않다-생성자-함수-방식으로-인스턴스를-생성하는-경우를-생각해보자">자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 옳지 않다. 생성자 함수 방식으로 인스턴스를 생성하는 경우를 생각해보자</h5>
<pre><code class="language-js">function Circle(radius) {
  // 이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
  ????.radius = radius;
}

Circle.prototype.getDiameter = function () {
  // 이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
  return 2 * ????.radius;
};

// 생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수를 정의해야 한다.
const circle = new Circle(5);</code></pre>
<h5 id="생성자-함수를-정의하는-시점에는-아직-인스턴스를-생성하기-이전이므로-인스턴스를-가리키는-식별자를-알-수-없다-따라서-자신이-속한-객체-또는-인스턴스를-가리키는-특수한-식별자가-필요하고-이것이-this이다">생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 인스턴스를 가리키는 식별자를 알 수 없다. 따라서 자신이 속한 객체 또는 인스턴스를 가리키는 특수한 식별자가 필요하고 이것이 this이다.</h5>
<blockquote>
<p>this는 자신이 속한 객체 또는 자신이 생성할 인스트런스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.</p>
</blockquote>
<h5 id="this는-암묵적으로-생성되며-어디서든-참조-가능하며-지역변수-처럼-사용도-가능하다">this는 암묵적으로 생성되며 어디서든 참조 가능하며 지역변수 처럼 사용도 가능하다.</h5>
<blockquote>
<p>단, this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 결정된다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
}

Circle.prototype.getDiameter = function () {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  return 2 * this.radius;
};

// 인스턴스 생성
const circle = new Circle(5);
console.log(circle.getDiameter()); // 10</code></pre>
<blockquote>
<p>타 언어와 달리 자바스크립트의 this는 함수가 호출되는 방식에 따라 this에 바인딩될 값, 즉 this바인딩이 동적으로 결정된다.</p>
</blockquote>
<h5 id="this는-전역에서나-함수-내부에서도-참조가-가능하지만-일반적으로-this는-객체의-프로퍼티나-메서드를-참조하기-위한-자기-참조-변수-이므로-일반적으로-객체의-메서드-내부-또는-생성자-함수-내부에서만-의미가-있다">this는 전역에서나 함수 내부에서도 참조가 가능하지만 일반적으로 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수 이므로 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다.</h5>
<h3 id="222-함수-호출-방식과-this-바인딩">22.2 함수 호출 방식과 this 바인딩</h3>
<blockquote>
<p>this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.</p>
</blockquote>
<h4 id="함수-호출-방식은-일반-함수-메서드-생성자-functionprototypeapplycallbind-메서드에-의한-간접-호출등-다양하다">함수 호출 방식은 일반 함수, 메서드, 생성자, Function.prototype.apply/call/bind 메서드에 의한 간접 호출등 다양하다.</h4>
<pre><code class="language-js">// this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
const foo = function () {
  console.dir(this);
};

// 동일한 함수도 다양한 방식으로 호출할 수 있다.

// 1. 일반 함수 호출
// foo 함수를 일반적인 방식으로 호출
// foo 함수 내부의 this는 전역 객체 window를 가리킨다.
foo(); // window

// 2. 메서드 호출
// foo 함수를 프로퍼티 값으로 할당하여 호출
// foo 함수 내부의 this는 메서드를 호출한 객체 obj를 가리킨다.
const obj = { foo };
obj.foo(); // obj

// 3. 생성자 함수 호출
// foo 함수를 new 연산자와 함께 생성자 함수로 호출
// foo 함수 내부의 this는 생성자 함수가 생성한 인스턴스를 가리킨다.
new foo(); // foo {}

// 4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출
// foo 함수 내부의 this는 인수에 의해 결정된다.
const bar = { name: 'bar' };

foo.call(bar);   // bar
foo.apply(bar);  // bar
foo.bind(bar)(); // bar</code></pre>
<h4 id="2221-일반-함수-호출">22.2.1 일반 함수 호출</h4>
<blockquote>
<p>기본적으로 this에는 전역 객체가 바인딩 된다.</p>
</blockquote>
<pre><code class="language-js">function foo() {
  console.log(&quot;foo's this: &quot;, this);  // window
  function bar() {
    console.log(&quot;bar's this: &quot;, this); // window
  }
  bar();
}
foo();</code></pre>
<blockquote>
<p>중첩 함수를 일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩 된다.</p>
</blockquote>
<h5 id="strict-mode가-적용된-일반-함수-내부의-this에는-undefined가-바인딩-된다">strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩 된다.</h5>
<pre><code class="language-js">function foo() {
  'use strict';

  console.log(&quot;foo's this: &quot;, this);  // undefined
  function bar() {
    console.log(&quot;bar's this: &quot;, this); // undefined
  }
  bar();
}
foo();</code></pre>
<h5 id="메서드-내에서-정의한-중첩-함수도-일반-함수로-호출하면-중첩-함수-내부의-this에는-전역-객체가-바인딩-된다">메서드 내에서 정의한 중첩 함수도 일반 함수로 호출하면 중첩 함수 내부의 this에는 전역 객체가 바인딩 된다.</h5>
<pre><code class="language-js">// var 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티다.
var value = 1;
// const 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티가 아니다.
// const value = 1;

const obj = {
  value: 100,
  foo() {
    console.log(&quot;foo's this: &quot;, this);  // {value: 100, foo: ƒ}
    console.log(&quot;foo's this.value: &quot;, this.value); // 100

    // 메서드 내에서 정의한 중첩 함수
    function bar() {
      console.log(&quot;bar's this: &quot;, this); // window
      console.log(&quot;bar's this.value: &quot;, this.value); // 1
    }

    // 메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 객체가 바인딩된다.
    bar();
  }
};

obj.foo();</code></pre>
<h5 id="콜백-함수가-일반-함수로-호출된다면-콜백-함수-내부의-this에도-전역-객체가-바인딩-된다">콜백 함수가 일반 함수로 호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩 된다.</h5>
<pre><code class="language-js">var value = 1;

const obj = {
  value: 100,
  foo() {
    console.log(&quot;foo's this: &quot;, this); // {value: 100, foo: ƒ}
    // 콜백 함수 내부의 this에는 전역 객체가 바인딩된다.
    setTimeout(function () {
      console.log(&quot;callback's this: &quot;, this); // window
      console.log(&quot;callback's this.value: &quot;, this.value); // 1
    }, 100);
  }
};

obj.foo();</code></pre>
<blockquote>
<p>이처럼 일반 함수로 호출된 모든 함수(중첩, 콜백 함수 포함) 내부의 this에는 전역 객체가 바인딩 된다.</p>
</blockquote>
<h4 id="2222-메서드-호출">22.2.2 메서드 호출</h4>
<h5 id="메서드-내부의-this는-메서드를-소유한-객체가-아닌-메서드를-호출한-객체에-바인딩된다는-것이다">메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것이다</h5>
<pre><code class="language-js">const person = {
  name: 'Lee',
  getName() {
    // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
    return this.name;
  }
};

// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Lee</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/6dfcae8b-ded4-4239-b5c8-3b9a4a3a1ee1/image.png" /></p>
<h5 id="위-예제이서-getname-프로퍼티가-가리키는-함수-객체-즉-getname-메서드는-다른-객체의-프로퍼티에-할당하는-것으로-다른-객체의-메서드가-될-수도-있고-일반-변수에-할당하여-일반-함수로-호출될-수도-있다">위 예제이서 getName 프로퍼티가 가리키는 함수 객체, 즉 getName 메서드는 다른 객체의 프로퍼티에 할당하는 것으로 다른 객체의 메서드가 될 수도 있고 일반 변수에 할당하여 일반 함수로 호출될 수도 있다.</h5>
<pre><code class="language-js">const anotherPerson = {
  name: 'Kim'
};
// getName 메서드를 anotherPerson 객체의 메서드로 할당
anotherPerson.getName = person.getName;

// getName 메서드를 호출한 객체는 anotherPerson이다.
console.log(anotherPerson.getName()); // Kim

// getName 메서드를 변수에 할당
const getName = person.getName;

// getName 메서드를 일반 함수로 호출
console.log(getName()); // ''
// 일반 함수로 호출된 getName 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다.
// 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며 기본값은 ''이다.
// Node.js 환경에서 this.name은 undefined다.</code></pre>
<h5 id="따라서-메서드-내부의-this는-프로퍼티로-메서드를-가리키고-있는-객체와는-관계가-없고-메서드를-호출한-객체에-바인딩-된다">따라서 메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩 된다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/85bea351-533b-43b3-9ac6-35931b5758b5/image.png" /></p>
<h5 id="프로토타입-메서드-내부에서-사용된-this도-일반-메서드와-마찬가지로-해당-메서드를-호출한-객체에-바인딩된다">프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩된다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

const me = new Person('Lee');

// getName 메서드를 호출한 객체는 me다.
console.log(me.getName()); // ① Lee

Person.prototype.name = 'Kim';

// getName 메서드를 호출한 객체는 Person.prototype이다.
console.log(Person.prototype.getName()); // ② Kim</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/27b5e2b2-2dbc-4e32-8816-b9d49772d9d3/image.png" /></p>
<h4 id="2223-생성자-함수-호출">22.2.3 생성자 함수 호출</h4>
<h5 id="생성자-함수-내부의-this에는-생성자-함수가미래에-생성할-인스턴스가-바인딩된다">생성자 함수 내부의 this에는 생성자 함수가(미래에) 생성할 인스턴스가 바인딩된다.</h5>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 반지름이 5인 Circle 객체를 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체를 생성
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20</code></pre>
<h4 id="2224-functionprototypeapplycallbind-메서드에-의한-간접-호출">22.2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출</h4>
<h5 id="applycallbind-메서드는-functionprototype의-메서드다-즉-이들-메서드는-모든-함수가-상속받아-사용-할-수-있다">apply,call,bind 메서드는 Function.prototype의 메서드다. 즉 이들 메서드는 모든 함수가 상속받아 사용 할 수 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/6b05acd3-3323-4419-931a-35212d314e62/image.png" /></p>
<pre><code class="language-js">apply,call 메서드 사용법
/**
* 주어진 this 바인딩과 인수 리스트 배열을 사용하여 함수를 호출한다.
* @param thisArg - this로 사용할 객체
* @param argArray - 함수에게 전달할 인수 리스트의 배열 또는 유사 배열 객체
* @returns 호출된 함수의 반환값
*/
Function.prototype.apply(thisArg[, argsArray])

/**
 * 주어진 this 바인딩과 ,로 구분된 인수 리스트를 사용하여 함수를 호출한다.
 * @param thisArg - this로 사용할 객체
 * @param arg1, agr2, ... - 함수에게 전달할 인수 리스트
 * @returns 호출된 함수의 반환값
 */
Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])</code></pre>
<blockquote>
<p>apply,call 메서드의 본질적인 기능은 함수를 호출하는 것이다.</p>
</blockquote>
<pre><code class="language-js">function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

console.log(getThisBinding()); // window

// getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
console.log(getThisBinding.apply(thisArg)); // {a: 1}
console.log(getThisBinding.call(thisArg)); // {a: 1}</code></pre>
<h5 id="apply-메서드는-호출할-함수의-인수를-배열로-묶어-전달한다">apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다.</h5>
<pre><code class="language-js">function getThisBinding() {
  console.log(arguments);
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
// apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다.
console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
// Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
// {a: 1}

// call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다.
console.log(getThisBinding.call(thisArg, 1, 2, 3));
// Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
// {a: 1}</code></pre>
<h5 id="apply와-call-메서드의-대표적인-용도는-arguments-객체와-같은-유사-배열-객체에-배열-메서드르-사용하는-경우다">apply와 call 메서드의 대표적인 용도는 arguments 객체와 같은 유사 배열 객체에 배열 메서드르 사용하는 경우다.</h5>
<pre><code class="language-js">function convertArgsToArray() {
  console.log(arguments);

  // arguments 객체를 배열로 변환
  // Array.prototype.slice를 인수없이 호출하면 배열의 복사본을 생성한다.
  const arr = Array.prototype.slice.call(arguments);
  // const arr = Array.prototype.slice.apply(arguments);
  console.log(arr);

  return arr;
}

convertArgsToArray(1, 2, 3); // [1, 2, 3]</code></pre>
<h5 id="functionprototypebind-메서드는-apply와-call-메서드와-달리-함수를-호출하지-않는다-다만-첫-번째-인수로-전달한-값으로-this-바인딩이-교체된-함수를-새롭게-생성해-반환한다">Function.prototype.bind 메서드는 apply와 call 메서드와 달리 함수를 호출하지 않는다. 다만 첫 번째 인수로 전달한 값으로 this 바인딩이 교체된 함수를 새롭게 생성해 반환한다.</h5>
<pre><code class="language-js">function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// bind 메서드는 첫 번째 인수로 전달한 thisArg로 this 바인딩이 교체된
// getThisBinding 함수를 새롭게 생성해 반환한다.
console.log(getThisBinding.bind(thisArg)); // getThisBinding
// bind 메서드는 함수를 호출하지는 않으므로 명시적으로 호출해야 한다.
console.log(getThisBinding.bind(thisArg)()); // {a: 1}</code></pre>
<h5 id="bind-메서드는-메서드의-this와-메서드-내부의-중첩-함수-또는-콜백-함수의-this가-불일치하는-문제를-해결하기-위해-유용하게-사용된다">bind 메서드는 메서드의 this와 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 불일치하는 문제를 해결하기 위해 유용하게 사용된다.</h5>
<pre><code class="language-js">const person = {
  name: 'Lee',
  foo(callback) {
    // bind 메서드로 callback 함수 내부의 this 바인딩을 전달
    setTimeout(callback.bind(this), 100);
  }
};

person.foo(function () {
  console.log(`Hi! my name is ${this.name}.`); // Hi! my name is Lee.
});</code></pre>
<h3 id="호출-방식-정리">호출 방식 정리</h3>
<table>
<thead>
<tr>
<th>함수 호출 방식</th>
<th>this바인딩</th>
</tr>
</thead>
<tbody><tr>
<td>일반 함수 호출</td>
<td>전역 객체</td>
</tr>
<tr>
<td>메서드 호출</td>
<td>메서드를 호출한 객체</td>
</tr>
<tr>
<td>생성자 함수 호출</td>
<td>생성자 함수가 (미래에) 생성할 인스턴스</td>
</tr>
<tr>
<td>Function.prototype.apply/call/bind</td>
<td>메서드에 의한 간접 호출</td>
</tr>
</tbody></table>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/22.md">wikibooks</a></p>