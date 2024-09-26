<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/4870e784-2141-4dbb-879c-e36f2a92853a/image.png" /></p>
<h2 id="19-프로토타입">19. 프로토타입</h2>
<hr />
<blockquote>
<p>자바스크립트는 객체 기반의 프로그래밍 언어이며 자바스크립트를 이루고 있는 (원시타입을 제외한) 모든 값들(함수,배열,정규 표현식등)은 객체다.</p>
</blockquote>
<h3 id="191-객체지향-프로그램">19.1 객체지향 프로그램</h3>
<blockquote>
<p>객체 지향 프로그래밍은 객체의 집합이며 실체를 인식하는 시도에서 시작한다. 실체는 특징이나 성질을 나타내는 '속성'을 가지고 있고 이를 통해 실체를 인식하거나 구별할 수 있다. 이때 내가 필요한 속성만 간추쳐 내어 표현하는 것을 '추상화'라 한다.</p>
</blockquote>
<pre><code class="language-js">// 이름과 주소 속성을 갖는 객체
const person = {
  name: 'Lee',
  address: 'Seoul'
};

console.log(person); // {name: &quot;Lee&quot;, address: &quot;Seoul&quot;}</code></pre>
<blockquote>
<p>객체는 속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료구조이다.</p>
</blockquote>
<blockquote>
<p>객체는 객체의 '상태'를 나타내는 데이터와 그 데이터를 조작할수 있는 '동작'을 하나의 단위로 묶어서 생각한다. 따라서 객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조이다.</p>
</blockquote>
<pre><code class="language-js">const circle = {
  radius: 5, // 반지름 (상태)

  // 원의 지름: 2r
  getDiameter() { //동작
    return 2 * this.radius;
  },

  // 원의 둘레: 2πr
  getPerimeter() {//동작
    return 2 * Math.PI * this.radius;
  },

  // 원의 넓이: πrr
  getArea() {//동작
    return Math.PI * this.radius ** 2;
  }
};

console.log(circle);
// {radius: 5, getDiameter: ƒ, getPerimeter: ƒ, getArea: ƒ}

console.log(circle.getDiameter());  // 10
console.log(circle.getPerimeter()); // 31.41592653589793
console.log(circle.getArea());      // 78.53981633974483</code></pre>
<h3 id="192-상속과-프로토-타입">19.2 상속과 프로토 타입</h3>
<blockquote>
<p>상속은 어떠 객체의 프로퍼티 또는 메서드를 다른객체가 상속받아 그대로 사용할 수 있는 것을 말한다.</p>
</blockquote>
<blockquote>
<p>자바스크립트는 프토로타입을 기반으로 상속을 구현해 불필요한 중복을 제거하여 코드의 재사용을 가능하게 한다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  //프로토타입 안쓰고 불필요하게 중복시
  /* 
  this.getArea = function(){
  return Math.PI * this.redius ** 2;
  */
}

// Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를
// 공유해서 사용할 수 있도록 프로토타입에 추가한다.
// 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩되어 있다.
Circle.prototype.getArea = function () {
  return Math.PI * this.radius ** 2;
};

// 인스턴스 생성
const circle1 = new Circle(1);
const circle2 = new Circle(2);

// Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는
// 프로토타입 Circle.prototype으로부터 getArea 메서드를 상속받는다.
// 즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유한다.
console.log(circle1.getArea === circle2.getArea); // true

console.log(circle1.getArea()); // 3.141592653589793
console.log(circle2.getArea()); // 12.566370614359172</code></pre>
<h3 id="193-프로토타입-객체">19.3 프로토타입 객체</h3>
<h5 id="프로토타입-객체란-객체지향-프로그래밍의-근간을-이루는-객체-간-상속을-구현하기-위해-사용된다">프로토타입 객체란 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용된다.</h5>
<h5 id="객체가-생성될-때-생성-방식에-따라-프로토타입이-결정되고-prototype에-저장된다">객체가 생성될 때 생성 방식에 따라 프로토타입이 결정되고 [[Prototype]]에 저장된다.</h5>
<h4 id="1931-__proto__-접근자-프로퍼티">19.3.1 <strong>__</strong>proto__ 접근자 프로퍼티</h4>
<blockquote>
<p>모든 객체는 <strong>__</strong>proto__접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/6d25f466-1b0f-44a1-8109-bcde7dc6cd9c/image.png" /></p>
<h5 id="1-__-proto-__-는-접근자-프로퍼티다">1) <strong>__</strong> proto __ 는 접근자 프로퍼티다.</h5>
<h5 id="원칙적으로-내부슬롯과-내부-메서드에-직접적으로-접근할-수-있는-방법을-없지만-간접적으로-objectprototype__proto__-접근자-프로퍼티를-사용하여-접근-가능하다">원칙적으로 내부슬롯과 내부 메서드에 직접적으로 접근할 수 있는 방법을 없지만 간접적으로 Object.prototype.<strong>__</strong>proto__ 접근자 프로퍼티를 사용하여 접근 가능하다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/15390b17-845b-46d1-a338-b05acc543bcd/image.png" /></p>
<h5 id="__proto__는-gettersetter-함수라고-부르는-접근자-함수-프로퍼티를-통해-prototype내부-슬롯의-값-즉-프로토타입을-취득하거나-할당한다"><strong>__</strong>proto__는 getter/setter 함수라고 부르는 접근자 함수 프로퍼티를 통해 [[Prototype]]내부 슬롯의 값, 즉 프로토타입을 취득하거나 할당한다.</h5>
<pre><code class="language-js">const obj = {};
const parent = { x: 1 };

// getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입을 취득
obj.__proto__;
// setter함수인 set __proto__가 호출되어 obj 객체의 프로토타입을 교체
obj.__proto__ = parent;

console.log(obj.x); // 1</code></pre>
<h5 id="2-__proto__-접근자-프로퍼티는-상속을-통해-사용된다">2) <strong>__</strong>proto__ 접근자 프로퍼티는 상속을 통해 사용된다.</h5>
<h5 id="__proto____-접근자-프로퍼티는-객체가-직접-소유하는-프로퍼티가-아니라-objectprototype의-프로퍼티다-모든-객체는-상속을-통해-objcetprototype__proto-접근자를-사용할-수-있다"><strong>__</strong>proto____ 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티다. 모든 객체는 상속을 통해 Objcet.prototype.<strong>__proto</strong> 접근자를 사용할 수 있다.</h5>
<pre><code class="language-js">const person = { name: 'Lee' };

// person 객체는 __proto__ 프로퍼티를 소유하지 않는다.
console.log(person.hasOwnProperty('__proto__')); // false

// __proto__ 프로퍼티는 모든 객체의 프로토타입 객체인 Object.prototype의 접근자 프로퍼티다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get: ƒ, set: ƒ, enumerable: false, configurable: true}

// 모든 객체는 Object.prototype의 접근자 프로퍼티 __proto__를 상속받아 사용할 수 있다.
console.log({}.__proto__ === Object.prototype); // true</code></pre>
<h5 id="3-proto-접근자-프로퍼티를-통해-프로타입에-접근하는-이유">3) <strong><strong>proto</strong></strong> 접근자 프로퍼티를 통해 프로타입에 접근하는 이유</h5>
<h5 id="proto-접근자-프로퍼티를-사용하는-이유는-상호-참조에-의해-프로토타입-체인이-생성되는-것을-방지하기-위해서다"><strong><strong>proto</strong></strong> 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서다.</h5>
<pre><code class="language-js">const parent = {};
const child = {};

// child의 프로토타입을 parent로 설정
child.__proto__ = parent;
// parent의 프로토타입을 child로 설정
parent.__proto__ = child; // TypeError: Cyclic __proto__ value</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/ef89ce94-c266-4da4-b78f-dbddf418b76f/image.png" /></p>
<h5 id="프로토타입-체인이-순환-방향으로-발생시-프로토타입-종점이-존재하지-않게-되어-프로퍼티-검색시-무한-루프에-빠지게-된다-따라서-프로토-타입-체인은-한쪽방향으로만-흘려야-된다">프로토타입 체인이 순환 방향으로 발생시 프로토타입 종점이 존재하지 않게 되어 프로퍼티 검색시 무한 루프에 빠지게 된다. 따라서 프로토 타입 체인은 한쪽방향으로만 흘려야 된다.</h5>
<h5 id="4-proto-접근자-프로퍼티를-코드-내에서-직접-사용하는-것은-권장하지-않는다">4) <strong><strong>proto</strong></strong> 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.</h5>
<h5 id="모든-객체가-proto-접근자-프로퍼티를-사용할-수-있는-것은-아니기-때문에-직접-사용이-권장-되지-않는다">모든 객체가 <strong><strong>proto</strong></strong> 접근자 프로퍼티를 사용할 수 있는 것은 아니기 때문에 직접 사용이 권장 되지 않는다.</h5>
<pre><code class="language-js">// obj는 프로토타입 체인의 종점이다. 따라서 Object.__proto__를 상속받을 수 없다.
const obj = Object.create(null);

// obj는 Object.__proto__를 상속받을 수 없다.
console.log(obj.__proto__); // undefined

// 따라서 __proto__보다 Object.getPrototypeOf 메서드를 사용하는 편이 좋다.
console.log(Object.getPrototypeOf(obj)); // null</code></pre>
<h5 id="프로토타입의-참조를-취득하고-싶은-경우에는-objectgetprototype메서드를-사용하고-프로토타입-교체시-objectsetprototype메서드-사용이-권장된다">프로토타입의 참조를 취득하고 싶은 경우에는 Object.getPrototype메서드를 사용하고, 프로토타입 교체시 Object.setPrototype메서드 사용이 권장된다.</h5>
<pre><code class="language-js">const obj = {};
const parent = { x: 1 };

// obj 객체의 프로토타입을 취득
Object.getPrototypeOf(obj); // obj.__proto__;
// obj 객체의 프로토타입을 교체
Object.setPrototypeOf(obj, parent); // obj.__proto__ = parent;

console.log(obj.x); // 1</code></pre>
<h4 id="1932-함수-객체의-prototype-프로퍼티">19.3.2 함수 객체의 prototype 프로퍼티</h4>
<blockquote>
<p>함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.</p>
</blockquote>
<pre><code class="language-js">// 함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}).hasOwnProperty('prototype'); // -&gt; true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty('prototype'); // -&gt; false</code></pre>
<h5 id="생성자-함수로서-호출할-수-없는-함수-즉-non-constructor인-화살표-함수와-es6-메서드-축약-표현으로-정의한-메서드는-prototype-프로퍼티를-소유하지-않으며-프로토타입도-생성하지-않는다">생성자 함수로서 호출할 수 없는 함수, 즉 non-constructor인 화살표 함수와 ES6 메서드 축약 표현으로 정의한 메서드는 prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않는다</h5>
<pre><code class="language-js">// 화살표 함수는 non-constructor다.
const Person = name =&gt; {
  this.name = name;
};

// non-constructor는 prototype 프로퍼티를 소유하지 않는다.
console.log(Person.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않는다.
console.log(Person.prototype); // undefined

// ES6의 메서드 축약 표현으로 정의한 메서드는 non-constructor다.
const obj = {
  foo() {}
};

// non-constructor는 prototype 프로퍼티를 소유하지 않는다.
console.log(obj.foo.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않는다.
console.log(obj.foo.prototype); // undefined</code></pre>
<blockquote>
<p>모든 객체가 가지고 있는(정확히는 Object.prototype으로부터 상속받은) <strong>__</strong>proto__ 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다</p>
</blockquote>
<table>
<thead>
<tr>
<th>구분</th>
<th>소유</th>
<th>값</th>
<th>사용주체</th>
<th>사용목적</th>
</tr>
</thead>
<tbody><tr>
<td><strong>__</strong>proto__ 접근자 프로퍼티</td>
<td>모든 객체</td>
<td>프로토타입의 참조</td>
<td>모든 객체</td>
<td>객체가 자신의 프로토 타입에 접근 또는 교체하기 위해 사용</td>
</tr>
<tr>
<td>prototype프로퍼티</td>
<td>constructor</td>
<td>프로토타입의 참조</td>
<td>생성자 함수</td>
<td>생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용</td>
</tr>
</tbody></table>
<pre><code class="language-js">// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 결국 Person.prototype과 me.__proto__는 결국 동일한 프로토타입을 가리킨다.
console.log(Person.prototype === me.__proto__);  // true</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/b4270416-b44b-4be4-a137-9c2909bdb1fe/image.png" /></p>
<h4 id="1933-프로토타입의-constructor-프로퍼티와-생성자-함수">19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수</h4>
<h5 id="모든-프로토타입은-constructor-프로퍼티를-갖는데-이-프로퍼티는-prototype-프로퍼티로-자신을-참조하고-있는-생성자-함수를-가리킨다">모든 프로토타입은 constructor 프로퍼티를 갖는데 이 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다.</h5>
<pre><code class="language-js">// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// me 객체의 생성자 함수는 Person이다.
console.log(me.constructor === Person);  // true</code></pre>
<h3 id="194-리터럴-표기법에-의해-생성된-객체의-생성자-함수와-프로토타입">19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입</h3>
<h5 id="생성자-함수에-의해-생성된-인스턴스는-프로토타입의-constructor-프로퍼티에-의해-생성자-함수와-연결된다-이때-constructor-프로퍼티가-가리키는-생성자-함수는-인스턴스를-생성한-생성자-함수다">생성자 함수에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티에 의해 생성자 함수와 연결된다. 이때 constructor 프로퍼티가 가리키는 생성자 함수는 인스턴스를 생성한 생성자 함수다.</h5>
<pre><code class="language-js">// obj 객체를 생성한 생성자 함수는 Object다.
const obj = new Object();
console.log(obj.constructor === Object); // true

// add 함수 객체를 생성한 생성자 함수는 Function이다.
const add = new Function('a', 'b', 'return a + b');
console.log(add.constructor === Function); // true

// 생성자 함수
function Person(name) {
  this.name = name;
}

// me 객체를 생성한 생성자 함수는 Person이다.
const me = new Person('Lee');
console.log(me.constructor === Person); // true</code></pre>
<blockquote>
<p>프로토 타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재한다.</p>
</blockquote>
<h5 id="리터럴-표기법에-의해-생성된-객체는-생성자-함수에-의해-생성된-객체는-아니지만-생성자-함수와-객체로서-동일한-특성을-갖는다">리터럴 표기법에 의해 생성된 객체는 생성자 함수에 의해 생성된 객체는 아니지만 생성자 함수와 객체로서 동일한 특성을 갖는다.</h5>
<pre><code class="language-js">// foo 함수는 Function 생성자 함수로 생성한 함수 객체가 아니라 함수 선언문으로 생성했다.
function foo() {}

// 하지만 constructor 프로퍼티를 통해 확인해보면 함수 foo의 생성자 함수는 Function 생성자 함수다.
console.log(foo.constructor === Function); // true</code></pre>
<h3 id="195-프로토타입의-생성-시점">19.5 프로토타입의 생성 시점</h3>
<blockquote>
<p>프로토 타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.</p>
</blockquote>
<h4 id="1951-사용자-정의-생성자-함수와-프로토타입-생성-시점">19.5.1 사용자 정의 생성자 함수와 프로토타입 생성 시점</h4>
<blockquote>
<p>생성자 함수로서 호출할 수 있는 함수, 즉 construuctor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.</p>
</blockquote>
<pre><code class="language-js">// 함수 정의(constructor)가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
console.log(Person.prototype); // {constructor: ƒ}

// 생성자 함수
function Person(name) {
  this.name = name;
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/69e974b8-50cd-472a-a311-0e03b3641f8c/image.png" /></p>
<h5 id="빌트인-생성자-함수가-아닌-사용자-생성자-함수는-자신이-평가되어-함수-객체로-생성되는-시점에-프로토타입도-더불어-생성되며-생성된-프로토-타입의-프로토타입은-언제나-objectprototype이다">빌트인 생성자 함수가 아닌 사용자 생성자 함수는 자신이 평가되어 함수 객체로 생성되는 시점에 프로토타입도 더불어 생성되며, 생성된 프로토 타입의 프로토타입은 언제나 Object.prototype이다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/eca6cab9-536f-4842-9bbf-366e5284cd12/image.png" /></p>
<h4 id="1952-빌트인-생성자-함수와-프토로타입-생성-시점">19.5.2 빌트인 생성자 함수와 프토로타입 생성 시점</h4>
<h5 id="object-string-number-function-array-regexp-date-promise등과-같은-빌트인-생성자-함수도-일반-함수와-마찬가지로-빌트인-생성자-함수가-생성되는-시점에-프로토타입이-생성된다">Object, String, Number, Function, Array, RegExp, Date, Promise등과 같은 빌트인 생성자 함수도 일반 함수와 마찬가지로 빌트인 생성자 함수가 생성되는 시점에 프로토타입이 생성된다.</h5>
<h5 id="모든-빌트인-생성자-함수는-전역-객체가-생성되는-시점에-생성된다-생성된-프로토타입은-빌트인-생성자-함수의-prototype-프로퍼티에-바인딩된다">모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성된다. 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩된다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/4b09b968-0e58-4544-849d-a09cdc8152cd/image.png" /></p>
<blockquote>
<p>객체가 생성되기 전에 생성자 함수와 프로토타입은 이미 객체화되어 존대한다. 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토 타입은 생성된 객체의 [Prototype]] 내부 슬롯에 할당된다.</p>
</blockquote>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="objectprototype">Object.prototype</h5>
<blockquote>
<p>모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여있다. 자바스크립트 엔진은 객체의 프로퍼티(메서드포함)에 접근 하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 <strong>__</strong>proto__ 접근자 프로퍼티가 가리키는 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 접근한다. <br />
프로토타입 체인의 종점, 즉 프로토 타입 체인의 최상위 객체는 Object.prototype이며, 이 객체의 프로퍼티와 메서드는 모든 객체에 상속된다. </p>
</blockquote>
<h5 id="추상-연산">추상 연산</h5>
<blockquote>
<p>추상연산은 ECMAScript 사양에서 내부동작의 구현 알고리즘을 표현한 것이다.</p>
</blockquote>
<h5 id="전역-객체">전역 객체</h5>
<blockquote>
<p>전역 객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체다.<br />
전역객체는 표준 빌트인 객체(Object,String,Number,Function,Array 등)들과 환경에 따른 호스트 객체(클라이언트 Web Api, Node.js의 호스트 Api) 그리고 var 키워드로 선언한 전역 변수와 전역 함수를 프로퍼티로 갖는다.</p>
</blockquote>
<pre><code class="language-js">// 전역 객체 window는 브라우저에 종속적이므로 아래 코드는 브라우저 환경에서 실행해야 한다.
// 빌트인 객체인 Object는 전역 객체 window의 프로퍼티다.
window.Object === Object // true</code></pre>
<h3 id="😲-느낀점">😲 느낀점</h3>
<p>개인적으로 지금까지 이 책에서 공부했던 내용중에 가장 난해한 파트였던거 같다. 프론트 개발자로서 자바스크립트에서 알아야 하는 내용은 분명하지만 실무에서 이것을 인지하고 작업한 기억이 없고 두번에 나눠서 정리 해야 할 만큼 내용도 너무많다... 무엇보다 객체지향이 관련된 파트라 그런지 내용들이 확실히 추상적이다.</p>
<p>하지만 이러한 추상적이고 깊은 내용들을 공부하기 위해 이 책의 공부를 시작한거니 나아가야겠지..
이 파트는 한 번 읽고 정리하는 걸로는 어림도 없고 여러번 읽어 봐야 될 것같다.</p>
<h3 id="📄-reference">📄 Reference</h3>
<h4 id="자바스크립트-deep-dive">자바스크립트 deep dive</h4>
<h4 id="wikibooks"><a href="https://github.com/wikibook/mjs/blob/master/19.md">wikibooks</a></h4>