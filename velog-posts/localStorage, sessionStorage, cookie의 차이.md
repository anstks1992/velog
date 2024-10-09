<p>localStorage, sessionStorage, 그리고 cookie는 모두 브라우저에서 데이터를 저장하는 방법이지만, 각 방식은 저장 공간, 데이터의 유효 기간, 그리고 사용 목적에 따라 차이가 있다.<br /></p>
<h2 id="1-localstorage">1. localStorage</h2>
<li> 저장 용량:  약 5~10MB (브라우저에 따라 다름)<br /><br />
<li>유효 기간: 만료되지 않으며, 사용자가 직접 데이터를 삭제하거나 브라우저가 캐시를 정리하기 전까지 영구적으로 남아 있다.<br /><br />
<li> 데이터 접근 범위: 같은 출처(Same Origin, 즉 같은 도메인과 프로토콜) 내에서만 접근 가능. 다른 도메인에서는 접근할 수 없다.<br /><br />
<li> 용도: 사용자 설정값(예: 다크 모드, 언어 설정)이나 영구적으로 저장할 필요가 있는 데이터를 저장할 때 사용한다.<br /><br />
<li> 보안: HTTP 요청 시 서버에 자동으로 전송되지 않으며, 클라이언트 측에서만 사용된다. 스크립트를 통해서만 접근 가능하기 때문에, 민감한 정보는 저장하지 않는 것이 좋다.</li>

<h2 id="2-sessionstorage">2. sessionStorage</h2>
<li>저장 용량: localStorage와 유사하게 약 5~10MB.<br /><br />
<li>유효 기간: 현재 탭(세션)이 유지되는 동안만 유효. 브라우저 탭이나 창을 닫으면 데이터가 자동으로 삭제된다.<br /><br />
<li>데이터 접근 범위: 같은 탭 내의 같은 출처에서만 접근 가능하다. 탭 간 공유는 불가능하다.<br /><br />
<li>용도: 세션 동안만 필요한 데이터를 저장하는 용도로 사용한다. 예를 들어, 특정 탭 내에서만 사용되는 임시 데이터를 저장할 때 적합하다. 주로 사용자 인증, 장바구니 정보,페이지 이동 간의 데이터 상태 유지에 사용된다.<br /><br /> 
<li>보안: localStorage와 마찬가지로 서버로 자동 전송되지 않으며, 클라이언트 측에서만 사용된다. </li>

<h2 id="3-cookie">3. Cookie</h2>
<li>저장 용량: 제한적이며, 보통 하나의 쿠키당 최대 4KB.<br /><br />
<li>유효 기간: 개발자가 명시적으로 설정할 수 있다. 만료 시간을 설정하지 않으면 브라우저가 닫힐 때까지 유지된다(세션 쿠키).<br /><br />
<li>데이터 접근 범위: 도메인과 경로에 따라 쿠키의 접근 범위를 설정할 수 있으며, 다른 도메인에서는 접근할 수 없다. 서버와 클라이언트 양쪽에서 사용 가능.<br /><br />
<li>용도: 주로 서버와 클라이언트 간 상태를 유지하기 위해 사용된다. 로그인 상태 유지, 사용자 설정 기억(예: 언어설정 테마 등)에 자주 사용된다.<br /><br />
<li>보안: 쿠키는 HTTP 요청마다 자동으로 서버에 전송된다. HTTPS와 Secure, HttpOnly, SameSite 속성을 통해 보안 강화가 가능하다. 민감한 정보는 암호화해서 저장하는 것이 좋다.</li>

<h2 id="cookie-vs-localstorage-vs-sessionstorage-정리">Cookie vs LocalStorage vs SessionStorage 정리</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>localStorage</th>
<th>sessionStorage</th>
<th>Cookie</th>
</tr>
</thead>
<tbody><tr>
<td>저장 용량</td>
<td>약 5~10MB</td>
<td>약 5~10MB</td>
<td>최대 4KB</td>
</tr>
<tr>
<td>유효 기간</td>
<td>영구적</td>
<td>세션이 종료되면 삭제됨</td>
<td>설정된 만료 시간에 따라 다름</td>
</tr>
<tr>
<td>데이터 접근 범위</td>
<td>같은 출처 내에서만 접근 가능</td>
<td>같은 탭 내에서만 접근 가능</td>
<td>도메인 및 경로 설정에 따라 다름</td>
</tr>
<tr>
<td>자동 서버 전송</td>
<td>아님</td>
<td>아님</td>
<td>서버로 자동 전송됨</td>
</tr>
<tr>
<td>용도</td>
<td>사용자 설정값(예: 다크 모드, 언어 설정), 영구 데이터 저장</td>
<td>탭 내 임시 데이터 저장(예:사용자 인증, 장바구니 정보,페이지 이동 간의 데이터 상태 유지)</td>
<td>서버와 상태 유지, 로그인 상태 유지, 사용자 설정 기억(예: 언어설정 테마 등)</td>
</tr>
<tr>
<td>보안</td>
<td>스크립트를 통해서만 접근 가능</td>
<td>스크립트를 통해서만 접근 가능</td>
<td>HTTPS 및 속성 설정으로 보안 강화</td>
</tr>
</tbody></table>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://sunrise-min.tistory.com/entry/Cookie-vs-LocalStorage-vs-SessionStorage">Cookie vs LocalStorage vs SessionStorage</a>
<a href="https://www.instagram.com/p/C_aQYWny0Dc/?igsh=ZHJ0NXdncmdxN3Jo">쿠키vs세션</a></p>