<h2 id="19-프로토타입-02">19. 프로토타입 02</h2>
<hr />
<h3 id="196-객체-생성-방식과-프로토타입의-결정">19.6 객체 생성 방식과 프로토타입의 결정</h3>
<h5 id="객체-생성-방법">객체 생성 방법</h5>
<blockquote>
<ul>
  <li> 객체 리터럴
  <li> Object 생성자 함수
  <li> 생성자 함수
  <li> Object.create 메서드
  <li> 클래스
  </ul>
</blockquote>
<h5 id="이들의-공통점은-ordinaryobjectcreate에-의해-생성된다는-점이며-프로토-타입은-ordinaryobjectcreate에-전달되는-인수에-의해-결정된다에-전달되는-인수에-의해-결정된다">이들의 공통점은 OrdinaryObjectCreate에 의해 생성된다는 점이며 프로토 타입은 OrdinaryObjectCreate에 전달되는 인수에 의해 결정된다에 전달되는 인수에 의해 결정된다.</h5>
<blockquote>
<p>OrdinaryObjectCreate<br />
자바스크립트 내부에서 객체를 생성할 때 사용되는 추상 연산(abstract operation) 중 하나이다. 이 연산은 자바스크립트의 엔진 내부에서 실제로 객체를 생성하는 데 사용한다.</p>
</blockquote>
<h4 id="1961-객체-리터럴에-의해-생성된-객체의-프로토타입">19.6.1 객체 리터럴에 의해 생성된 객체의 프로토타입</h4>
<h5 id="객체-리터럴에-의해-생성되는-객체의-프로토타입은-objectprototype이다">객체 리터럴에 의해 생성되는 객체의 프로토타입은 Object.prototype이다.</h5>
<pre><code class="language-js">const obj = {x:1};</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/21b69e5e-fefc-49ae-b936-3c091ceb36e5/image.png" /></p>
<h5 id="객체-리터럴에-의해-생성된-obj-객체는-objectprototype을-상속받는다">객체 리터럴에 의해 생성된 obj 객체는 Object.prototype을 상속받는다.</h5>
<pre><code class="language-js">const obj = { x: 1 };

// 객체 리터럴에 의해 생성된 obj 객체는 Object.prototype을 상속받는다.
console.log(obj.constructor === Object); // true
console.log(obj.hasOwnProperty('x'));    // true</code></pre>
<h4 id="1962-object-생성자-함수에-의해-생성된-객체의-프로토타입">19.6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입</h4>
<h5 id="object-생성자-함수에-의해-생성된-obj-객체는-objectprototype을-프로토타입으로-갖게-되며-이로써-objectprototype을-상속받는다">Object 생성자 함수에 의해 생성된 obj 객체는 Object.prototype을 프로토타입으로 갖게 되며 이로써 Object.prototype을 상속받는다</h5>
<pre><code class="language-js">const obj = new Object();
obj.x = 1;

// Object 생성자 함수에 의해 생성된 obj 객체는 Object.prototype을 상속받는다.
console.log(obj.constructor === Object); // true
console.log(obj.hasOwnProperty('x'));    // true</code></pre>
<h5 id="객체-리터럴-방식은-객체-리터럴-내부에-프로퍼티를-추가하지만-object-생성자-함수-방식은-일단-빈-객체를-생성한-이후-프로퍼티를-추가해야-한다">객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만 Object 생성자 함수 방식은 일단 빈 객체를 생성한 이후 프로퍼티를 추가해야 한다.</h5>
<h4 id="1963-생성자-함수에-의해-생성된-객체의-프로토타입">19.6.3 생성자 함수에 의해 생성된 객체의 프로토타입</h4>
<h5 id="생성자-함수에-의해-생성된-객체의-프로토타입은-생성자-함수의-prototype-프로퍼티에-바인딩-되어-있는-객체다">생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩 되어 있는 객체다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

const me = new Person('Lee');</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/353b11cd-12a0-4aa8-94c3-b7012446acb0/image.png" /></p>
<h5 id="프로토타입은-객체다-따라서-일반-객체와-같이-프로토타입에도-프로퍼티를-추가삭제할-수-있다-그리고-이렇게-추가삭제된-프로퍼티는-프로토타입-체인에-즉가-반영된다">프로토타입은 객체다. 따라서 일반 객체와 같이 프로토타입에도 프로퍼티를 추가/삭제할 수 있다. 그리고 이렇게 추가/삭제된 프로퍼티는 프로토타입 체인에 즉가 반영된다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function () {
  console.log(`Hi! My name is ${this.name}`);
};

//person 생성자 함수를 통해 생성된 모든 객체는 프로토타입에 추가된 sayHello 메서드를 상속받아 사용할 수 있다
const me = new Person('Lee');
const you = new Person('Kim');

me.sayHello();  // Hi! My name is Lee
you.sayHello(); // Hi! My name is Kim</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/46df815c-69d5-4b7d-bf72-7127cb91f920/image.png" /></p>
<h3 id="197-프로토타입-체인">19.7 프로토타입 체인</h3>
<h5 id="생성자-함수에-의해-생성된-me-객체는-objectprototype의-메서드인-hsaownproperty를-호출할-수-있다">생성자 함수에 의해 생성된 me 객체는 Object.prototype의 메서드인 hsaOwnProperty를 호출할 수 있다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function () {
  console.log(`Hi! My name is ${this.name}`);
};

const me = new Person('Lee');

// hasOwnProperty는 Object.prototype의 메서드다.
console.log(me.hasOwnProperty('name')); // true

// me 객체의 프로토타입은 Person.prototype이다
Object.getPrototypeOf(me) === Person.prototype; // -&gt; true

// 프로토타입의 프로토타입은 언제사 object.prototype이다.
Object.getPrototypeOf(Person.prototype) === Object.prototype; // -&gt; true</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/8365f64e-6745-4c0e-937c-2ef4a34b0e76/image.png" /></p>
<blockquote>
<p>자바스크립트는 객체의 프로퍼티(메서드 포함)에 접근할려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 이를 프로토타입 체인이라 한다. 프로토타입 체인은 자바스크립트가 객체지향 프로그래밍의 상속을 구현하는 메커니즘이다.</p>
</blockquote>
<pre><code class="language-js">// hasOwnProperty는 Object.prototype의 메서드다.
// me 객체는 프로토타입 체인을 따라 hasOwnProperty 메서드를 검색하여 사용한다.
me.hasOwnProperty('name'); // -&gt; true</code></pre>
<h5 id="메서드를-호출하면-다음과-같은-과정을-거쳐-메서드를-메서드를-검색한다">메서드를 호출하면 다음과 같은 과정을 거쳐 메서드를 메서드를 검색한다.</h5>
<h5 id="1--먼저-hasownproperty-메서드를-호출한-me-객체에서-hasownproperty-메서드를-검색한다-me-객체에서는-hasownproperty-메서드가-없으므로-프로토타입-체인을-따라-다시말해-prototype-내부-슬롯에-바인딩되어-있는-프로토타입197의-personprototype으로-이동하여-hasownproperty-메서드를-검색한다">1)  먼저 hasOwnProperty 메서드를 호출한 me 객체에서 hasOwnProperty 메서드를 검색한다. me 객체에서는 hasOwnProperty 메서드가 없으므로 프로토타입 체인을 따라, 다시말해 [[Prototype]] 내부 슬롯에 바인딩되어 있는 프로토타입(19.7의 Person.prototype)으로 이동하여 hasOwnProperty 메서드를 검색한다.</h5>
<h5 id="2-personprototype에서-hasownproperty-메서드가-없으므로-프로토타입-체인을-따라-다시-말해-prototype-내부-슬롯에-바인딩되어-있는-프로토타입19-7-objectprototype으로-이동하여-hasownproperty-메서드를-검색한다">2) Person.prototype에서 hasOwnProperty 메서드가 없으므로 프로토타입 체인을 따라, 다시 말해 [[Prototype]] 내부 슬롯에 바인딩되어 있는 프로토타입(19-7 Object.prototype)으로 이동하여 hasOwnProperty 메서드를 검색한다.</h5>
<h5 id="3-objectprototype에는-hasownproperty-메서드가-존대한다-자바스크립트-엔진은-objectprototypehasownproperty-메서드를-호출한다-이때-objectprototypehasownproperty-메서드의-this에는-me-객체가-바인딩-된다">3) Object.prototype에는 hasOwnProperty 메서드가 존대한다. 자바스크립트 엔진은 Object.prototype.hasOwnProperty 메서드를 호출한다. 이때 Object.prototype.hasOwnProperty 메서드의 this에는 me 객체가 바인딩 된다.</h5>
<pre><code class="language-js">Object.prototype.hasOwnProperty.call(me, 'name');</code></pre>
<blockquote>
<p>모든 객체는 Object.prototype을 상속 받는다. Object.prototype은 프로토 타입 체인의 종점이다.</p>
</blockquote>
<blockquote>
<p>자바스크립트 엔진은 객체 간의 상속 관계로 이루어진 계층적인 구조에서 객체의 프로퍼티를 검색한다.<br />
따라서 프로토 타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘이다.</p>
</blockquote>
<blockquote>
<p>식별자는 스코프 체인에서 검색한다. 자바스크립트 엔진은 함수의 중첩 관계로 이루어진 스코프의 계층적인 구조에서 식별자를 검색한다 <br />
따라서 스코프 체인은 식별자 검색을 위한 메커니즘이라고 할 수 있다.</p>
</blockquote>
<h5 id="먼저-스코프-체인에서-me-식별자를-검색한다-me-식별자는-전역에서-선언되었으므로-전역-스코프에서-검색된다-me-식별자를-검색한-다음-me-객체의-프로토타입-체인에서hasownproperty-메서드를-검색한다">먼저 스코프 체인에서 me 식별자를 검색한다. me 식별자는 전역에서 선언되었으므로 전역 스코프에서 검색된다. me 식별자를 검색한 다음, me 객체의 프로토타입 체인에서hasOwnProperty 메서드를 검색한다.</h5>
<pre><code class="language-js">me.hasOwnProperty('name');</code></pre>
<blockquote>
<p>스코프 체인과 프로토타입 체인은 서로 연관없이 별로도 동작하는 것이 아니라 서로 협력하여 식별자와 프로퍼티를 검색하는데 사용된다.</p>
</blockquote>
<h3 id="198-오버라이딩과-프로퍼티-섀도잉">19.8 오버라이딩과 프로퍼티 섀도잉</h3>
<pre><code class="language-js">const Person = (function () {
  // 생성자 함수
  function Person(name) {
    this.name = name;
  }

  // 프로토타입 메서드
  Person.prototype.sayHello = function () {
    console.log(`Hi! My name is ${this.name}`);
  };

  // 생성자 함수를 반환
  return Person;
}());

const me = new Person('Lee');

// 인스턴스 메서드
me.sayHello = function () {
  console.log(`Hey! My name is ${this.name}`);
};

// 인스턴스 메서드가 호출된다. 프로토타입 메서드는 인스턴스 메서드에 의해 가려진다.
me.sayHello(); // Hey! My name is Lee</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/92aefbe7-c498-4a5a-b797-05b786e792aa/image.png" /></p>
<h5 id="프로토타입-프로퍼티와-같은-이름의-프로퍼티를-인스턴스에-추가하면-프로토타입-체인을-따라-프로토타입-프로퍼티를-검색하여-프로토타입-프로퍼티를-덮어쓰는-것이-아니라-인스턴스-프로퍼티로-추가한다">프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 프로토타입 체인을 따라 프로토타입 프로퍼티를 검색하여 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가한다.</h5>
<h5 id="이때-인스턴스-메서드-sayhello는-프로토타입-메서드-sayhello를-오버라이딩했고-프로토타입-메서드-sayhello는-가려진다">이때 인스턴스 메서드 sayHello는 프로토타입 메서드 sayHello를 오버라이딩했고 프로토타입 메서드 sayHello는 가려진다</h5>
<blockquote>
<p>이처럼 상속 관계에 의해 프로퍼티가 가려지는 현상을 프로퍼티 섀도잉이라 한다.</p>
</blockquote>
<h5 id="추가한-인스턴스-메서드-sayhello를-삭제하려할-때-당연히-프로토타입-메서드가-아닌-인스턴스-메서드-sayhello가-삭제-된다">추가한 인스턴스 메서드 sayHello를 삭제하려할 때 당연히 프로토타입 메서드가 아닌 인스턴스 메서드 sayHello가 삭제 된다.</h5>
<pre><code class="language-js">// 인스턴스 메서드를 삭제한다.
delete me.sayHello;
// 인스턴스에는 sayHello 메서드가 없으므로 프로토타입 메서드가 호출된다.
me.sayHello(); // Hi! My name is Lee</code></pre>
<h5 id="하위-객체를-통해-프로토타입의-프로퍼티를-변경-또는-삭제하는-것은-불가능하다-하위-객체를-통해-프로토타입에-get-액세스는-허용-set-액세스는-허용되지-않는다">하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는 것은 불가능하다. 하위 객체를 통해 프로토타입에 get 액세스는 허용, set 액세스는 허용되지 않는다.</h5>
<pre><code class="language-js">// 프로토타입 체인을 통해 프로토타입 메서드가 삭제되지 않는다.
delete me.sayHello;
// 프로토타입 메서드가 호출된다.
me.sayHello(); // Hi! My name is Lee</code></pre>
<h5 id="프로토타입-프로퍼티를-변경-또는-삭제하려면-하위-객체를-통해-프로토타입-체인으로-접근하는-것이-아니라-프로토타입에-직접-접근해야-한다">프로토타입 프로퍼티를 변경 또는 삭제하려면 하위 객체를 통해 프로토타입 체인으로 접근하는 것이 아니라 프로토타입에 직접 접근해야 한다.</h5>
<pre><code class="language-js">// 프로토타입 메서드 변경
Person.prototype.sayHello = function () {
  console.log(`Hey! My name is ${this.name}`);
};
me.sayHello(); // Hey! My name is Lee

// 프로토타입 메서드 삭제
delete Person.prototype.sayHello;
me.sayHello(); // TypeError: me.sayHello is not a function</code></pre>
<h3 id="199-프로토타입의-교체">19.9 프로토타입의 교체</h3>
<h5 id="프로토-타입은-임의의-다른-객체로-변경할-수-있다-이러한-특징을-활용하여-객체-간의-상속-관례를-동적으로-변경할-수-있다">프로토 타입은 임의의 다른 객체로 변경할 수 있다. 이러한 특징을 활용하여 객체 간의 상속 관례를 동적으로 변경할 수 있다.</h5>
<h4 id="1991-생성자-함수에-의한-프로토타입의-교체">19.9.1 생성자 함수에 의한 프로토타입의 교체</h4>
<pre><code class="language-js">const Person = (function () {
  function Person(name) {
    this.name = name;
  }

  // ① 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
  Person.prototype = {
    sayHello() {
      console.log(`Hi! My name is ${this.name}`);
    }
  };

  return Person;
}());

const me = new Person('Lee');</code></pre>
<h5 id="personprotype에-객체-리터럴을-할당했다-이는-person-생성자-함수가-생성할-객체의-프로토타입을-객체-리터럴로-교체한-것이다">Person.protype에 객체 리터럴을 할당했다. 이는 Person 생성자 함수가 생성할 객체의 프로토타입을 객체 리터럴로 교체한 것이다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/a207d203-9ddc-407d-a845-905bfca07a05/image.png" /></p>
<h5 id="프로토타입으로-교체한-객체-리터럴에는-constructor-프로퍼티가-없다-constructor-프로퍼티는-자바스크립트-엔진이-프로토-타입을-생성할-때-암묵적으로-추가한-프로퍼티다-따라서-me-객체의-생성자-함수를-검색하면-person이-아닌-object가-나온다">프로토타입으로 교체한 객체 리터럴에는 constructor 프로퍼티가 없다. constructor 프로퍼티는 자바스크립트 엔진이 프로토 타입을 생성할 때 암묵적으로 추가한 프로퍼티다. 따라서 me 객체의 생성자 함수를 검색하면 Person이 아닌 object가 나온다.</h5>
<pre><code class="language-js">// 프로토타입을 교체하면 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴된다.
console.log(me.constructor === Person); // false
// 프로토타입 체인을 따라 Object.prototype의 constructor 프로퍼티가 검색된다.
console.log(me.constructor === Object); // true</code></pre>
<h5 id="프로토타입을-교체하면-constructor-프로퍼티와-생성자-함수-간의-연결이-파괴되는데-이를-되살리고-싶으면-교체한-객체-리터럴에-constructor-프로퍼티를-추가하면-된다">프로토타입을 교체하면 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴되는데 이를 되살리고 싶으면 교체한 객체 리터럴에 constructor 프로퍼티를 추가하면 된다.</h5>
<pre><code class="language-js">const Person = (function () {
  function Person(name) {
    this.name = name;
  }

  // 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
  Person.prototype = {
    // constructor 프로퍼티와 생성자 함수 간의 연결을 설정
    constructor: Person,
    sayHello() {
      console.log(`Hi! My name is ${this.name}`);
    }
  };

  return Person;
}());

const me = new Person('Lee');

// constructor 프로퍼티가 생성자 함수를 가리킨다.
console.log(me.constructor === Person); // true
console.log(me.constructor === Object); // false</code></pre>
<h4 id="1992-인스턴스에-의한-프로토타입의-교체">19.9.2 인스턴스에 의한 프로토타입의 교체</h4>
<h5 id="인스턴스의-proto-접근자-프로퍼티또는-objectsetprototypeof-메서드를-통해-프로토타입을-교체할-수-있다">인스턴스의 <strong><strong>proto</strong></strong> 접근자 프로퍼티(또는 Object.setPrototypeOf 메서드)를 통해 프로토타입을 교체할 수 있다.</h5>
<h5 id="생성자-함수의-prototype-프로퍼티에-다른-임의의-객체를-바인딩하는-것은-미래에-생성할-인스턴스의-프로타입을-교체하는것과-달리-proto-접근자-프로퍼티를-통해-프로토타입을-교체하는-것은-이미-생성된-객체의-프로토-타입을-교체하는-것이다">생성자 함수의 prototype 프로퍼티에 다른 임의의 객체를 바인딩하는 것은 미래에 생성할 인스턴스의 프로타입을 교체하는것과 달리 <strong><strong>proto</strong></strong> 접근자 프로퍼티를 통해 프로토타입을 교체하는 것은 이미 생성된 객체의 프로토 타입을 교체하는 것이다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 프로토타입으로 교체할 객체
const parent = {
  sayHello() {
    console.log(`Hi! My name is ${this.name}`);
  }
};

// ① me 객체의 프로토타입을 parent 객체로 교체한다.
Object.setPrototypeOf(me, parent);
// 위 코드는 아래의 코드와 동일하게 동작한다.
// me.__proto__ = parent;

me.sayHello(); // Hi! My name is Lee</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/79bfc821-40f1-41a3-a6da-03cefdbcd81d/image.png" /></p>
<h5 id="프로토타입으로-교체한-객체에는-constructor-프로퍼티가-없으므로-constructor-프로퍼티와-생성자-함수-간의-연결이-파괴된다">프로토타입으로 교체한 객체에는 constructor 프로퍼티가 없으므로 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴된다.</h5>
<pre><code class="language-js">// 프로토타입을 교체하면 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴된다.
console.log(me.constructor === Person); // false
// 프로토타입 체인을 따라 Object.prototype의 constructor 프로퍼티가 검색된다.
console.log(me.constructor === Object); // true</code></pre>
<h5 id="생성자-함수에-의한-프로토타입-교체와-인스턴스에-의한-프로토타입-교체는-같이보이지만-미묘한-차이가-있다">생성자 함수에 의한 프로토타입 교체와 인스턴스에 의한 프로토타입 교체는 같이보이지만 미묘한 차이가 있다.</h5>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/daaa9bfa-c43d-4b6d-abe9-6344f6cd3ba7/image.png" /></p>
<h5 id="프로토-타입으로-교체한-객체-리터럴에-constructor-프로퍼티를-추가하고-생성자-함수의-prototype-프로퍼티를-재설정하여-파괴된-생성자-함수와-프로토타입-간의-연결을-되살릴-수-있지만-이러한-상속관계를-동적으로-변경하는-것은-꽤나-번거롭고-권장되지-않는다">프로토 타입으로 교체한 객체 리터럴에 constructor 프로퍼티를 추가하고 생성자 함수의 prototype 프로퍼티를 재설정하여 파괴된 생성자 함수와 프로토타입 간의 연결을 되살릴 수 있지만 이러한 상속관계를 동적으로 변경하는 것은 꽤나 번거롭고 권장되지 않는다.</h5>
<pre><code class="language-js">function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 프로토타입으로 교체할 객체
const parent = {
  // constructor 프로퍼티와 생성자 함수 간의 연결을 설정
  constructor: Person,
  sayHello() {
    console.log(`Hi! My name is ${this.name}`);
  }
};

// 생성자 함수의 prototype 프로퍼티와 프로토타입 간의 연결을 설정
Person.prototype = parent;

// me 객체의 프로토타입을 parent 객체로 교체한다.
Object.setPrototypeOf(me, parent);
// 위 코드는 아래의 코드와 동일하게 동작한다.
// me.__proto__ = parent;

me.sayHello(); // Hi! My name is Lee

// constructor 프로퍼티가 생성자 함수를 가리킨다.
console.log(me.constructor === Person); // true
console.log(me.constructor === Object); // false

// 생성자 함수의 prototype 프로퍼티가 교체된 프로토타입을 가리킨다.
console.log(Person.prototype === Object.getPrototypeOf(me)); // true</code></pre>
<h3 id="📚-기타-cs-지식">📚 기타 CS 지식</h3>
<h5 id="call-메서드">call 메서드</h5>
<blockquote>
<p>call 메서드는 this로 사용할 객체를 전달하면서 함수르 호출한다. this로 사용할 객체를 전달하면서 Object.prototype.hasOwnProperty 메서드를 호출한다.</p>
</blockquote>
<h5 id="오버라이딩">오버라이딩</h5>
<blockquote>
<p>상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의하여 사용하는 방식</p>
</blockquote>
<h5 id="오버로딩">오버로딩</h5>
<blockquote>
<p>함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메서드를 구현하고 매개변수에 의해 메서드를 구별하여 호출하는 방식이다. 자바스크립트는 오버로딩을 지원하지 않지만 argument 객체를 사용하여 구현할 수는 있다.</p>
</blockquote>
<h3 id="😲-느낀점">😲 느낀점</h3>
<p>이 파트 좀 고비이긴 한 것 같다. 원래 오늘 끝낼려고 했지만 내용이 너무 많아서 읽는데 시간이 오래걸리는 것은 물론이고 추상적인 내용이라 정리하는데 어려움이 꽤 있어 책의 내용을 그냥 복붙하는 부분도 많은 것 같다. 
내일은 어떻게든 끝내야지 이 파트 빨리 넘어가고 싶어...😢</p>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 Deep Dive
<a href="https://github.com/wikibook/mjs/blob/master/19.md">wikibooks</a></p>