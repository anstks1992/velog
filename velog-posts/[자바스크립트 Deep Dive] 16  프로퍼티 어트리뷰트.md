<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/25ae2628-cbd3-4b42-b537-a5f49e9116c0/image.png" /></p>
<h2 id="16-프로퍼티-어트리뷰트">16. 프로퍼티 어트리뷰트</h2>
<hr />
<h3 id="161-내부-슬롯과-내부-메서드">16.1 내부 슬롯과 내부 메서드</h3>
<blockquote>
<p>내부 슬롯과 내부 메서드는 자바스크립트 엔진의 내부 로직이므로 자바스크립트는 원칙적으로 직접 접근하거나 호출할 수 있는 방법을 제공 안한다. 단, 일부에서는 간접적으로 접근할 수 있는 수단을 제공하기는 한다.</p>
</blockquote>
<pre><code class="language-js">const o = {};

// 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없다.
o.[[Prototype]] // -&gt; Uncaught SyntaxError: Unexpected token '['
// 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기는 한다.
o.__proto__ // -&gt; Object.prototype</code></pre>
<h3 id="162-프로퍼티-어트리뷰트와-프로퍼티-디스크립터-객체">16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체</h3>
<blockquote>
<p>자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.</p>
</blockquote>
<pre><code class="language-js">const person = {
  name: 'Lee'
};

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.
console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: &quot;Lee&quot;, writable: true, enumerable: true, configurable: true}</code></pre>
<h3 id="163-데이터-프로퍼티와-접근자-프로퍼티">16.3 데이터 프로퍼티와 접근자 프로퍼티</h3>
<blockquote>
<ul>
  <li> 데이터 프로퍼티 : 키와 값으로 구성된 일반적인 프로퍼티
  <li> 접근자 프로퍼티 : 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수
  </ul>
</blockquote>
<h4 id="1632-접근자-프로퍼티">16.3.2 접근자 프로퍼티</h4>
<blockquote>
<ul>
  <li> get : 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수다. 접근자 프로퍼티 키로 프로퍼티 값에 접근하며 프로퍼티 어트리뷰트의 값 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.
  <li> set : 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할때 호출되는 접근자 함수다.접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰트의 값 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다
  </ul>
</blockquote>
<pre><code class="language-js">const person = {
  // 데이터 프로퍼티
  firstName: 'Ungmo',
  lastName: 'Lee',

  // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set fullName(name) {
    // 배열 디스트럭처링 할당: &quot;31.1 배열 디스트럭처링 할당&quot; 참고
    [this.firstName, this.lastName] = name.split(' ');
  }
};

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(person.firstName + ' ' + person.lastName); // Ungmo Lee

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = 'Heegun Lee';
console.log(person); // {firstName: &quot;Heegun&quot;, lastName: &quot;Lee&quot;}

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // Heegun Lee

// firstName은 데이터 프로퍼티다.
// 데이터 프로퍼티는 [[Value]], [[Writable]], [[Enumerable]], [[Configurable]] 프로퍼티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log(descriptor);
// {value: &quot;Heegun&quot;, writable: true, enumerable: true, configurable: true}

// fullName은 접근자 프로퍼티다.
// 접근자 프로퍼티는 [[Get]], [[Set]], [[Enumerable]], [[Configurable]] 프로퍼티 어트리뷰트를 갖는다.
descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log(descriptor);
// {get: ƒ, set: ƒ, enumerable: true, configurable: true}</code></pre>
<h3 id="164-프로퍼티-정의">16.4 프로퍼티 정의</h3>
<h5 id="objectdefineproperty-메서드를-사용하면-프로퍼티의-어트리뷰트를-정의할-수-있다">Object.defineProperty 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다.</h5>
<pre><code class="language-js">const person = {};

// 데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName', {
  value: 'Ungmo',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(person, 'lastName', {
  value: 'Lee'
});

let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log('firstName', descriptor);
// firstName {value: &quot;Ungmo&quot;, writable: true, enumerable: true, configurable: true}

// 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName {value: &quot;Lee&quot;, writable: false, enumerable: false, configurable: false}

// [[Enumerable]]의 값이 false인 경우
// 해당 프로퍼티는 for...in 문이나 Object.keys 등으로 열거할 수 없다.
// lastName 프로퍼티는 [[Enumerable]]의 값이 false이므로 열거되지 않는다.
console.log(Object.keys(person)); // [&quot;firstName&quot;]

// [[Writable]]의 값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없다.
// lastName 프로퍼티는 [[Writable]]의 값이 false이므로 값을 변경할 수 없다.
// 이때 값을 변경하면 에러는 발생하지 않고 무시된다.
person.lastName = 'Kim';

// [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 삭제할 수 없다.
// lastName 프로퍼티는 [[Configurable]]의 값이 false이므로 삭제할 수 없다.
// 이때 프로퍼티를 삭제하면 에러는 발생하지 않고 무시된다.
delete person.lastName;

// [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 재정의할 수 없다.
// Object.defineProperty(person, 'lastName', { enumerable: true });
// Uncaught TypeError: Cannot redefine property: lastName

descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName {value: &quot;Lee&quot;, writable: false, enumerable: false, configurable: false}

// 접근자 프로퍼티 정의
Object.defineProperty(person, 'fullName', {
  // getter 함수
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true
});

descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log('fullName', descriptor);
// fullName {get: ƒ, set: ƒ, enumerable: true, configurable: true}

person.fullName = 'Heegun Lee';
console.log(person); // {firstName: &quot;Heegun&quot;, lastName: &quot;Lee&quot;}</code></pre>
<h3 id="165-객체-변경-방지">16.5 객체 변경 방지</h3>
<h5 id="자바스크립트는-객체의-변경을-방지하는-다양한-메서드를-제공한다">자바스크립트는 객체의 변경을 방지하는 다양한 메서드를 제공한다.</h5>
<h4 id="1651-객체확장금지">16.5.1 객체확장금지</h4>
<h5 id="objectpreventextensions-메서드는-객체의-확장을-금지한다-즉-확장이-금지된-객체는-프로퍼티-추가가-금지된다">'Object.preventExtensions' 메서드는 객체의 확장을 금지한다. 즉 확장이 금지된 객체는 프로퍼티 추가가 금지된다.</h5>
<pre><code class="language-js">const person = { name: 'Lee' };

// person 객체는 확장이 금지된 객체가 아니다.
console.log(Object.isExtensible(person)); // true

// person 객체의 확장을 금지하여 프로퍼티 추가를 금지한다.
Object.preventExtensions(person);

// person 객체는 확장이 금지된 객체다.
console.log(Object.isExtensible(person)); // false

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 추가는 금지되지만 삭제는 가능하다.
delete person.name;
console.log(person); // {}

// 프로퍼티 정의에 의한 프로퍼티 추가도 금지된다.
Object.defineProperty(person, 'age', { value: 20 });
// TypeError: Cannot define property age, object is not extensible</code></pre>
<h4 id="1652-객체-밀봉">16.5.2 객체 밀봉</h4>
<h5 id="objectseal메서드는-객체를-밀봉한다-밀봉된-객체는-읽기와-쓰기만-가능하다">'Object.seal'메서드는 객체를 밀봉한다. 밀봉된 객체는 읽기와 쓰기만 가능하다.</h5>
<pre><code class="language-js">const person = { name: 'Lee' };

// person 객체는 밀봉(seal)된 객체가 아니다.
console.log(Object.isSealed(person)); // false

// person 객체를 밀봉(seal)하여 프로퍼티 추가, 삭제, 재정의를 금지한다.
Object.seal(person);

// person 객체는 밀봉(seal)된 객체다.
console.log(Object.isSealed(person)); // true

// 밀봉(seal)된 객체는 configurable이 false다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
  name: {value: &quot;Lee&quot;, writable: true, enumerable: true, configurable: false},
}
*/

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 삭제가 금지된다.
delete person.name; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 값 갱신은 가능하다.
person.name = 'Kim';
console.log(person); // {name: &quot;Kim&quot;}

// 프로퍼티 어트리뷰트 재정의가 금지된다.
Object.defineProperty(person, 'name', { configurable: true });
// TypeError: Cannot redefine property: name</code></pre>
<h4 id="1652-객체-동결">16.5.2 객체 동결</h4>
<h5 id="objectfreeze-메서드는-객체를-동결한다-동결된-객체는-읽기만-가능하다">'Object.freeze' 메서드는 객체를 동결한다. 동결된 객체는 읽기만 가능하다.</h5>
<pre><code class="language-js">const person = { name: 'Lee' };

// person 객체는 동결(freeze)된 객체가 아니다.
console.log(Object.isFrozen(person)); // false

// person 객체를 동결(freeze)하여 프로퍼티 추가, 삭제, 재정의, 쓰기를 금지한다.
Object.freeze(person);

// person 객체는 동결(freeze)된 객체다.
console.log(Object.isFrozen(person)); // true

// 동결(freeze)된 객체는 writable과 configurable이 false다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
  name: {value: &quot;Lee&quot;, writable: false, enumerable: true, configurable: false},
}
*/

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 삭제가 금지된다.
delete person.name; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 값 갱신이 금지된다.
person.name = 'Kim'; // 무시. strict mode에서는 에러
console.log(person); // {name: &quot;Lee&quot;}

// 프로퍼티 어트리뷰트 재정의가 금지된다.
Object.defineProperty(person, 'name', { configurable: true });
// TypeError: Cannot redefine property: name</code></pre>
<h3 id="😲-느낀점">😲 느낀점</h3>
<p>이 부분을 공부하면서 솔직히 이런거 까지 알아야하나? 싶을만큼 한번도 본적이 없는 것들이 많았다. 특히 객체 변경 금지는 내가 개발자를 하면서 쓸일이나 있을까 싶은 것 들이었다. 그래서 다른 분들이 자바스크립트 deep dive 정리해놓은거를 찾아보니 역시나 아예 건너뛴분들이 많은 파트였다. 아예 정리를 안할까도 했지만 '아 이런게 있구나'하고 가볍게 정리만 하기로 했다.</p>
<h3 id="📄-reference">📄 Reference</h3>
<p>자바스크립트 deep dive
[wikibooks]
(<a href="https://github.com/wikibook/mjs/blob/master/16.md">https://github.com/wikibook/mjs/blob/master/16.md</a>)</p>