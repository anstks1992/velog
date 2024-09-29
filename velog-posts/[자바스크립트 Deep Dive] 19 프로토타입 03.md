<h2 id="19-프로토타입-03">19. 프로토타입 03</h2>
<hr />
<h3 id="1910-instanceof-연산자">19.10 instanceof 연산자</h3>
<blockquote>
<p>instanceof 연산자는 우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true로 평가되고, 그렇지 않으면 않은 경우에는 false로 평가된다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 프로토타입으로 교체할 객체
const parent = {};

// 프로토타입의 교체
Object.setPrototypeOf(me, parent);

// Person 생성자 함수와 parent 객체는 연결되어 있지 않다.
console.log(Person.prototype === parent); // false
console.log(parent.constructor === Person); // false

// Person.prototype이 me 객체의 프로토타입 체인 상에 존재하지 않기 때문에 false로 평가된다.
console.log(me instanceof Person); // false

// Object.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
console.log(me instanceof Object); // true</code></pre>
<blockquote>
<p>instanceof 연산자는 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수를 찾는 것이 아니라 생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.</p>
</blockquote>
<pre><code class="language-js">// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 프로토타입으로 교체할 객체
const parent = {};

// 프로토타입의 교체
Object.setPrototypeOf(me, parent);

// Person 생성자 함수와 parent 객체는 연결되어 있지 않다.
console.log(Person.prototype === parent); // false
console.log(parent.constructor === Person); // false

// parent 객체를 Person 생성자 함수의 prototype 프로퍼티에 바인딩한다.
Person.prototype = parent;

// Person.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
console.log(me instanceof Person); // true

// Object.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
console.log(me instanceof Object); // true</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/8b1e34d0-90a9-45cf-99a4-2dd380c665cd/image.png" /></p>
<h5 id="instanceof-연산자를-함수로-표현하면-다음과-같다">instanceof 연산자를 함수로 표현하면 다음과 같다.</h5>
<pre><code class="language-js">function isInstanceof(instance, constructor) {
  // 프로토타입 취득
  const prototype = Object.getPrototypeOf(instance);

  // 재귀 탈출 조건
  // prototype이 null이면 프로토타입 체인의 종점에 다다른 것이다.
  if (prototype === null) return false;

  // 프로토타입이 생성자 함수의 prototype 프로퍼티에 바인딩된 객체라면 true를 반환한다.
  // 그렇지 않다면 재귀 호출로 프로토타입 체인 상의 상위 프로토타입으로 이동하여 확인한다.
  return prototype === constructor.prototype || isInstanceof(prototype, constructor);
}

console.log(isInstanceof(me, Person)); // true
console.log(isInstanceof(me, Object)); // true
console.log(isInstanceof(me, Array));  // false</code></pre>
<h5 id="생성자-함수에-의해-프로토타입이-교체되어-constructor-프로퍼티와-생성자-함수-간의-연결이-파괴되어도-생성자-함수의-prototype-프로퍼티와-프로토타입-간의-연결은-파괴되지-않으므로-instanceof는-아무런-영향도-받지-않는다">생성자 함수에 의해 프로토타입이 교체되어 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴되어도 생성자 함수의 prototype 프로퍼티와 프로토타입 간의 연결은 파괴되지 않으므로 instanceof는 아무런 영향도 받지 않는다.</h5>
<h3 id="1911-직접상속">19.11 직접상속</h3>
<h4 id="19111-objectcreate에-의한-직접-상속">19.11.1 Object.create에 의한 직접 상속</h4>
<h5 id="objectcreate-메서드는-명시적으로-프로토타입을-지정하여-새로운-객체를-생성하고-추상-연산-ordinaryobjectcreate를-호출한다">Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성하고 추상 연산 OrdinaryObjectCreate를 호출한다.</h5>
<p> OrdinaryObjectCreate</p>
<ul style="font-size: 17px;">
<li> 첫번째 매개변수 : 생성할 객체의 프로토타입으로 지정할 객체를 전달
<li> 두번째 매개변수 : 생성할 객체의 프로퍼티 키와 프로퍼티 디스크립터 객체로 이루어진 객체를 전달
</ul>
<br /> 이 객체의 형식은 Object.defineProperties 메서드의 두 번째 인수와 동일하다.

<pre><code class="language-js">/**
* 지정된 프로토타입 및 프로퍼티를 갖는 새로운 객체를 생성하여 반환한다.
* @param {Object} prototype - 생성할 객체의 프로토타입으로 지정할 객체
* @param {Object} {propertiesObject} - 생성할 객체의 프로퍼티틑 갖는 객체
* @ returns {Object} 지정된 프로토타입 및 프로퍼티를 갖는 새로운 객체
*/
Object.crate(prototype[,propertierObject])</code></pre>
<pre><code class="language-js">// 프로토타입이 null인 객체를 생성한다. 생성된 객체는 프로토타입 체인의 종점에 위치한다.
// obj → null
let obj = Object.create(null);
console.log(Object.getPrototypeOf(obj) === null); // true
// Object.prototype을 상속받지 못한다.
console.log(obj.toString()); // TypeError: obj.toString is not a function

// obj → Object.prototype → null
// obj = {};와 동일하다.
obj = Object.create(Object.prototype);
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true

// obj → Object.prototype → null
// obj = { x: 1 };와 동일하다.
obj = Object.create(Object.prototype, {
  x: { value: 1, writable: true, enumerable: true, configurable: true }
});
// 위 코드는 다음과 동일하다.
// obj = Object.create(Object.prototype);
// obj.x = 1;
console.log(obj.x); // 1
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true

const myProto = { x: 10 };
// 임의의 객체를 직접 상속받는다.
// obj → myProto → Object.prototype → null
obj = Object.create(myProto);
console.log(obj.x); // 10
console.log(Object.getPrototypeOf(obj) === myProto); // true

// 생성자 함수
function Person(name) {
  this.name = name;
}

// obj → Person.prototype → Object.prototype → null
// obj = new Person('Lee')와 동일하다.
obj = Object.create(Person.prototype);
obj.name = 'Lee';
console.log(obj.name); // Lee
console.log(Object.getPrototypeOf(obj) === Person.prototype); // true</code></pre>
<h5 id="objectcreate-메서드는-첫-번째-매개변수에-전달할-객체의-프로토타입-체인에-속하는-객체를-생성한다-즉-객체를-생성하면서-직접적으로-상속을-구현하는-것이다-이-메서드의-장점은-다음과-같다">Object.create 메서드는 첫 번째 매개변수에 전달할 객체의 프로토타입 체인에 속하는 객체를 생성한다. 즉 객체를 생성하면서 직접적으로 상속을 구현하는 것이다. 이 메서드의 장점은 다음과 같다.</h5>
<ul style="font-size: 17px;">
<li> new 연산자가 없이도 객체를 생성할 수 있다.
<li> 프로토타입을 지정하면서 객체를 생성할 수 있다.
<li> 객체 리터럴에 의해 생성된 객체도 상속받을 수 있다.
</ul>

<h5 id="objectprototype의-빌트인-메서드들은-모든-객체의-프로토타입-체인의-종점-즉-objectprototype의-메서드이므로-모든-객체가-상속받아-호출할-수-있다">Object.prototype의 빌트인 메서드들은 모든 객체의 프로토타입 체인의 종점, 즉 Object.prototype의 메서드이므로 모든 객체가 상속받아 호출할 수 있다.</h5>
<pre><code class="language-js">const obj = { a: 1 };

obj.hasOwnProperty('a');       // -&gt; true
obj.propertyIsEnumerable('a'); // -&gt; true</code></pre>
<h5 id="그런데-eslint에서는-objectprototype의-빌트인-메서드를-직접적으로-호출하는-것을-권장하지-않는다-objectcreate-메서드를-통해-프로토타입-체인의-종점에-위치하는-객체를-생성할-수-있기-때문이다">그런데 ESLint에서는 Object.prototype의 빌트인 메서드를 직접적으로 호출하는 것을 권장하지 않는다. Object.create 메서드를 통해 프로토타입 체인의 종점에 위치하는 객체를 생성할 수 있기 때문이다.</h5>
<pre><code class="language-js">// 프로토타입이 null인 객체, 즉 프로토타입 체인의 종점에 위치하는 객체를 생성한다.
const obj = Object.create(null);
obj.a = 1;

console.log(Object.getPrototypeOf(obj) === null); // true

// obj는 Object.prototype의 빌트인 메서드를 사용할 수 없다.
console.log(obj.hasOwnProperty('a')); // TypeError: obj.hasOwnProperty is not a function</code></pre>
<h4 id="19112-객체-리터럴-내부에서-proto에-의한-직접-상속">19.11.2 객체 리터럴 내부에서 <strong><strong>proto</strong></strong>에 의한 직접 상속</h4>
<h5 id="두-번째-인자로-프로퍼티를-정의하는-것은-번거롭다-이에따라-es6에서는-객체-리터럴-내부에서-proto-접근자-프로퍼티를-사용하여-직접-상속을-구현할-수-있다">두 번째 인자로 프로퍼티를 정의하는 것은 번거롭다. 이에따라 ES6에서는 객체 리터럴 내부에서 <strong><strong>proto</strong></strong> 접근자 프로퍼티를 사용하여 직접 상속을 구현할 수 있다.</h5>
<pre><code class="language-js">const myProto = { x: 10 };

// 객체 리터럴에 의해 객체를 생성하면서 프로토타입을 지정하여 직접 상속받을 수 있다.
const obj = {
  y: 20,
  // 객체를 직접 상속받는다.
  // obj → myProto → Object.prototype → null
  __proto__: myProto
};
/* 위 코드는 아래와 동일하다.
const obj = Object.create(myProto, {
  y: { value: 20, writable: true, enumerable: true, configurable: true }
});
*/

console.log(obj.x, obj.y); // 10 20
console.log(Object.getPrototypeOf(obj) === myProto); // true</code></pre>
<h3 id="1912-정적-프로퍼티메서드">19.12 정적 프로퍼티/메서드</h3>
<h5 id="정적-프로퍼티메서드는-생성자-함수로-인스턴스를-생성하지-않아도-참조호출할-수-있는-프로퍼티메서드를-말한다">정적 프로퍼티/메서드는 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메서드를 말한다.</h5>
<h5 id="생성자-함수는-객체이므로-자신의-프로퍼티메서드를-소유할-수-있다-생성자-함수-객체가-소유한-프로퍼티메서드를-프로퍼티메서드라고-한다-정적-프로퍼티메서드는-생성자-함수가-생성한-인스턴스로-참조호출할-수-없다">생성자 함수는 객체이므로 자신의 프로퍼티/메서드를 소유할 수 있다. 생성자 함수 객체가 소유한 프로퍼티/메서드를 프로퍼티/메서드라고 한다. 정적 프로퍼티/메서드는 생성자 함수가 생성한 인스턴스로 참조/호출할 수 없다.</h5>
<pre><code class="language-js">// 생성자 함수
function Person(name) {
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function () {
  console.log(`Hi! My name is ${this.name}`);
};

// 정적 프로퍼티
Person.staticProp = 'static prop';

// 정적 메서드
Person.staticMethod = function () {
  console.log('staticMethod');
};

const me = new Person('Lee');

// 생성자 함수에 추가한 정적 프로퍼티/메서드는 생성자 함수로 참조/호출한다.
Person.staticMethod(); // staticMethod

// 정적 프로퍼티/메서드는 생성자 함수가 생성한 인스턴스로 참조/호출할 수 없다.
// 인스턴스로 참조/호출할 수 있는 프로퍼티/메서드는 프로토타입 체인 상에 존재해야 한다.
me.staticMethod(); // TypeError: me.staticMethod is not a function</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/29c9a3e1-a0df-4826-b27d-ef3030972ad5/image.png" /></p>
<h5 id="생성자-함수가-생성한-인스턴스와-달리-정적-프로퍼티메서드는-인스턴스의-프로토타입-체인에-속한-객체의-프로퍼티메서드가-아니므로-인스턴로-접근할-수-없다">생성자 함수가 생성한 인스턴스와 달리 정적 프로퍼티/메서드는 인스턴스의 프로토타입 체인에 속한 객체의 프로퍼티/메서드가 아니므로 인스턴로 접근할 수 없다.</h5>
<ul style="font-size: 17px;">
<li>Object.create : Object 생성자 함수의 정적 메서드, Object 생성자 함수가 생성한 객체로 호출할 수 없다.
<li>Object.prototype.hasOwnProperty : Object.prototype의 메서드, Object.prototype(모든 객체의 프로토타입 체인의 종점)의 메서드이므로 모든 객체가 호출할 수 있다.
</ul>

<pre><code class="language-js">// Object.create는 정적 메서드다.
const obj = Object.create({ name: 'Lee' });

// Object.prototype.hasOwnProperty는 프로토타입 메서드다.
obj.hasOwnProperty('name'); // -&gt; false</code></pre>
<h5 id="메서드-내에서-인스턴스를-참조할-필요가-없다면-정적-메서드로-변경하여도-동작한다-프로토타입-메서드를-호출하려면-인스턴스를-생성해야-하지만-정적-메서드-인스턴스를-생성하지-않아도-호출-할-수-있다">메서드 내에서 인스턴스를 참조할 필요가 없다면 정적 메서드로 변경하여도 동작한다. 프로토타입 메서드를 호출하려면 인스턴스를 생성해야 하지만 정적 메서드 인스턴스를 생성하지 않아도 호출 할 수 있다.</h5>
<pre><code class="language-js">function Foo() {}

// 프로토타입 메서드
// this를 참조하지 않는 프로토타입 메소드는 정적 메서드로 변경해도 동일한 효과를 얻을 수 있다.
Foo.prototype.x = function () {
  console.log('x');
};

const foo = new Foo();
// 프로토타입 메서드를 호출하려면 인스턴스를 생성해야 한다.
foo.x(); // x

// 정적 메서드
Foo.x = function () {
  console.log('x');
};

// 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있다.
Foo.x(); // x</code></pre>
<h3 id="1913-프로퍼티-존재-확인">19.13 프로퍼티 존재 확인</h3>
<h4 id="19131-in연산자">19.13.1 in연산자</h4>
<h5 id="in연산자는-객체-내에-특정-프로퍼티가-존재하는지-여부를-확인한다">in연산자는 객체 내에 특정 프로퍼티가 존재하는지 여부를 확인한다.</h5>
<pre><code class="language-js">/**
* key: 프로퍼티 키를 나타내는 문자열
* object : 객체로 평가되는 표현식
*/
key in object</code></pre>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul'
};

// person 객체에 name 프로퍼티가 존재한다.
console.log('name' in person);    // true
// person 객체에 address 프로퍼티가 존재한다.
console.log('address' in person); // true
// person 객체에 age 프로퍼티가 존재하지 않는다.
console.log('age' in person);     // false</code></pre>
<h5 id="in연산자는-확인-대상-객체의-프로퍼티만-아니라-확인-대상-객체가-상속받은-모든-프로토타입의-프로퍼티를-확인하므로-주의가-필요하다">in연산자는 확인 대상 객체의 프로퍼티만 아니라 확인 대상 객체가 상속받은 모든 프로토타입의 프로퍼티를 확인하므로 주의가 필요하다.</h5>
<pre><code class="language-js">console.log('toString' in person); // true
// in연산자가 proson 객체가 속한 프로토타입 체인 상에 존재하는 모든 프로토타입에서 toString프로퍼티를 검색했기 때문에 true가 나온다. toString은 Object.prototype메서드다.</code></pre>
<h5 id="in연산자-대신-reflecthas-메서드를-사용할-수-있다">in연산자 대신 Reflect.has 메서드를 사용할 수 있다.</h5>
<pre><code class="language-js">const person = { name: 'Lee' };

console.log(Reflect.has(person, 'name'));     // true
console.log(Reflect.has(person, 'toString')); // true</code></pre>
<h4 id="19132-objectprototypehasownproperty">19.13.2 Object.prototype.hasOwnProperty</h4>
<h5 id="objectprototypehasownproperty-메서드를-사용해도-객체에-특정-프로퍼티가-존재하는지-확인할-수-있다">Object.prototype.hasOwnProperty 메서드를 사용해도 객체에 특정 프로퍼티가 존재하는지 확인할 수 있다.</h5>
<pre><code class="language-js">console.log(person.hasOwnProperty('name')); // true
console.log(person.hasOwnProperty('age'));  // false</code></pre>
<h5 id="프로퍼티-키가-객체-고유의-프로퍼티-키인-경우에만-true를-반환하고-상속받은-프로토타입의-프로퍼티-키인-경우-false를-반환한다">프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true를 반환하고 상속받은 프로토타입의 프로퍼티 키인 경우 false를 반환한다.</h5>
<pre><code class="language-js">console.log(person.hasOwnProperty('toString')); // false</code></pre>
<h3 id="1914-프로퍼티-열거">19.14 프로퍼티 열거</h3>
<h4 id="19141-forin문">19.14.1 for...in문</h4>
<h5 id="객체의-모든-프로퍼티-만큼-순회하며-열거하려면-forin-문을-사용한다">객체의 모든 프로퍼티 만큼 순회하며 열거하려면 for...in 문을 사용한다</h5>
<blockquote>
<p>for (변수선언문 in 객체) {...}</p>
</blockquote>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul'
};

// for...in 문의 변수 key에 person 객체의 프로퍼티 키가 할당된다.
for (const key in person) {
  console.log(key + ': ' + person[key]);
}
// name: Lee
// address: Seoul</code></pre>
<h5 id="forin-문은-상속받은-프로토타입의-프로퍼티까지-열거한다">for...in 문은 상속받은 프로토타입의 프로퍼티까지 열거한다.</h5>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul'
};

// in 연산자는 객체가 상속받은 모든 프로토타입의 프로퍼티를 확인한다.
console.log('toString' in person); // true

// for...in 문도 객체가 상속받은 모든 프로토타입의 프로퍼티를 열거한다.
// 하지만 toString과 같은 Object.prototype의 프로퍼티가 열거되지 않는다.
for (const key in person) {
  console.log(key + ': ' + person[key]);
}

// name: Lee
// address: Seoul</code></pre>
<h5 id="위-예제에서-tostring과-같은-obejctprototype의-프로퍼티는-열거되지-않는다-이는-tostring-메서드가-열거할-수-없도록-정의되어-있는-프로퍼티이기-때문이다">위 예제에서 toString과 같은 Obejct.prototype의 프로퍼티는 열거되지 않는다 이는 toString 메서드가 열거할 수 없도록 정의되어 있는 프로퍼티이기 때문이다</h5>
<h5 id="다시말해-objectprototypetostring-프로퍼티의-프로퍼티-어트리뷰트-enumerable의-값이-false이기-때문이다-프로퍼티-어트리뷰트-enumerable은-프로퍼티의-열거-기능-여부를-나타내며-불리언-값을-갖는다">다시말해 Object.prototype.toString 프로퍼티의 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false이기 때문이다. 프로퍼티 어트리뷰트 [[Enumerable]]은 프로퍼티의 열거 기능 여부를 나타내며 불리언 값을 갖는다.</h5>
<pre><code class="language-js">// Object.getOwnPropertyDescriptor 메서드는 프로퍼티 디스크립터 객체를 반환한다.
// 프로퍼티 디스크립터 객체는 프로퍼티 어트리뷰트 정보를 담고 있는 객체다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, 'toString'));
// {value: ƒ, writable: true, enumerable: false, configurable: true}</code></pre>
<blockquote>
<p>for...in문을 좀 더 정확하게 표현하면 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로터피 중에서 프로퍼티 어트리뷰트[[Enumerable]]의 값이 true인 프로퍼티를 순회하며 열거한다.</p>
</blockquote>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul',
  __proto__: { age: 20 }
};

for (const key in person) {
  console.log(key + ': ' + person[key]);
}
// name: Lee
// address: Seoul
// age: 20</code></pre>
<h5 id="forin-문은-프로퍼티-키가-심벌인-프로퍼티는-열거하지-않는다">for...in 문은 프로퍼티 키가 심벌인 프로퍼티는 열거하지 않는다.</h5>
<pre><code class="language-js">const sym = Symbol();
const obj = {
  a: 1,
  [sym]: 10
};

for (const key in obj) {
  console.log(key + ': ' + obj[key]);
}
// a: 1</code></pre>
<h5 id="상속받은-프로퍼티는-제외하고-객체-자신의-프로퍼티만-열거하려면-objectprototypehasownproperty-메서드를-사용하여-객체-자신의-프로퍼티인지-확인해야-한다">상속받은 프로퍼티는 제외하고 객체 자신의 프로퍼티만 열거하려면 Object.prototype.hasOwnProperty 메서드를 사용하여 객체 자신의 프로퍼티인지 확인해야 한다.</h5>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul',
  __proto__: { age: 20 }
};

for (const key in person) {
  // 객체 자신의 프로퍼티인지 확인한다.
  if (!person.hasOwnProperty(key)) continue;
  console.log(key + ': ' + person[key]);
}
// name: Lee
// address: Seoul</code></pre>
<h5 id="forin-문은-프로퍼티를-열거할-때-순서를-보장하지-않지만-대부분의-모던-자바스크립트는-순서를-보장하고-정렬을-실시한다">for...in 문은 프로퍼티를 열거할 때 순서를 보장하지 않지만 대부분의 모던 자바스크립트는 순서를 보장하고 정렬을 실시한다.</h5>
<pre><code class="language-js">const obj = {
  2: 2,
  3: 3,
  1: 1,
  b: 'b',
  a: 'a'
};

for (const key in obj) {
  if (!obj.hasOwnProperty(key)) continue;
  console.log(key + ': ' + obj[key]);
}

/*
1: 1
2: 2
3: 3
b: b
a: a
*/</code></pre>
<h5 id="배열에는-forin-문의-사용보다-일반적인-for문-또는-arrayprototypeforeach메서드를-사용하기를-권장된다">배열에는 for...in 문의 사용보다 일반적인 for문 또는 Array.prototype.forEach메서드를 사용하기를 권장된다.</h5>
<pre><code class="language-js">const arr = [1, 2, 3];
arr.x = 10; // 배열도 객체이므로 프로퍼티를 가질 수 있다.

for (const i in arr) {
  // 프로퍼티 x도 출력된다.
  console.log(arr[i]); // 1 2 3 10
};

// arr.length는 3이다.
for (let i = 0; i &lt; arr.length; i++) {
  console.log(arr[i]); // 1 2 3
}

// forEach 메서드는 요소가 아닌 프로퍼티는 제외한다.
arr.forEach(v =&gt; console.log(v)); // 1 2 3

// for...of는 변수 선언문에서 선언한 변수에 키가 아닌 값을 할당한다.
for (const value of arr) {
  console.log(value); // 1 2 3
};</code></pre>
<h4 id="19132-objetkeysvaluesentries-메서드">19.13.2 Objet.keys/values/entries 메서드</h4>
<h5 id="forin-문은-객체-자신의-고유-프로퍼티뿐-아니라-상속-받은-프로퍼티도-열거하기-때문에-객체-자신의-프로퍼티인지-확인하는-추가-처리가-필요하다">for...in 문은 객체 자신의 고유 프로퍼티뿐 아니라 상속 받은 프로퍼티도 열거하기 때문에 객체 자신의 프로퍼티인지 확인하는 추가 처리가 필요하다.</h5>
<h5 id="객체-자신의-고유-프로퍼티만-열거하기-위해서-forin문-보다-objectkeysvaluesentries-메서드를-사용하는-것을-권장하며-objectkeys-메서드는-객체-자신의-열거-가능한-프로퍼티-키를-반환한다">객체 자신의 고유 프로퍼티만 열거하기 위해서 for...in문 보다 Object.keys/values/entries 메서드를 사용하는 것을 권장하며 Object.keys 메서드는 객체 자신의 열거 가능한 프로퍼티 키를 반환한다.</h5>
<pre><code class="language-js">const person = {
  name: 'Lee',
  address: 'Seoul',
  __proto__: { age: 20 }
};

console.log(Object.keys(person)); // [&quot;name&quot;, &quot;address&quot;]</code></pre>
<h5 id="objectvalues-메서드는-객체-자신의-열거-가능한-프로피터-값을-배열로-반환한다">Object.values 메서드는 객체 자신의 열거 가능한 프로피터 값을 배열로 반환한다.</h5>
<pre><code class="language-js">console.log(Object.values(person)); // [&quot;Lee&quot;, &quot;Seoul&quot;]</code></pre>
<h5 id="objectentries-메서드는-객체-자신의-열거-가능한-프로퍼티-키와-값의-쌍의-배열을-배열에-담아-반환한다">Object.entries 메서드는 객체 자신의 열거 가능한 프로퍼티 키와 값의 쌍의 배열을 배열에 담아 반환한다.</h5>
<pre><code class="language-js">console.log(Object.entries(person)); // [[&quot;name&quot;, &quot;Lee&quot;], [&quot;address&quot;, &quot;Seoul&quot;]]

Object.entries(person).forEach(([key, value]) =&gt; console.log(key, value));
/*
name Lee
address Seoul
*/</code></pre>
<h3 id="😲-느낀점">😲 느낀점</h3>
<p>여러번 보자...</p>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/19.md">wikibooks</a></p>