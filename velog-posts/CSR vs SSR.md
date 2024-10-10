<p>CSR(Client-Side Rendering)과 SSR(Server-Side Rendering)은 웹 페이지를 렌더링하는 방식인데 차이점이 있다.</p>
<h2 id="csrclient-side-rendering">CSR(Client-Side Rendering)</h2>
<li>개념 <br />CSR은 웹 애플리케이션이 클라이언트(브라우저)에서 실행되어, 페이지를 렌더링하는 방식이다. 초기 페이지 로드 시 서버로부터 최소한의 HTML과 자바스크립트 파일을 받아오고, 클라이언트 측에서 자바스크립트를 실행하여 페이지의 콘텐츠를 동적으로 렌더링한다.</li><br /> 
<li>작동 방식<br /> 
 사용자가 페이지를 요청하면 서버는 빈 HTML을 반환하고, 브라우저가 자바스크립트를 받아서 실행한 후에 데이터를 받아 화면에 표시한다.</li><br />
<li>장점<br />
1) 첫 요청 이후 빠른 페이지 전환 (SPA처럼 작동)<br />
2) 서버 부하가 적음<br />
3) 동적 콘텐츠 제공에 적합</li><br />
<li>단점<br />
1) 초기 로딩 시간이 느림 (자바스크립트를 모두 로드하고 실행해야 하기 때문)<br />
2) 검색 엔진 최적화(SEO)가 어려움 (검색 엔진이 자바스크립트를 해석하지 않으면 콘텐츠를 인식하지 못함)</li>

<h2 id="ssrserver-side-rendering">SSR(Server-Side Rendering)</h2>
<li>개념<br /> SSR은 서버에서 HTML을 렌더링하여 클라이언트에 전달하는 방식이다. 사용자가 요청할 때마다 서버는 완전한 HTML 페이지를 만들어 보내고, 브라우저는 이를 받아 즉시 화면에 표시한다.</li><br />
<li>작동 방식<br /> 서버에서 미리 페이지를 구성해 완성된 HTML을 제공하고, 클라이언트는 이를 즉시 렌더링한다. 자바스크립트는 필요한 경우 추가적으로 실행된다.</li><br />
<li>장점<br />
1) 빠른 초기 로딩 속도 (서버에서 완성된 HTML을 받음)<br />
2) SEO에 유리 (검색 엔진이 HTML을 바로 인식 가능)</li><br />
<li>단점<br />
1) 서버 부하가 큼 (각 요청마다 HTML을 생성해야 하기 때문)<br />
2) 클라이언트 측 상호작용이 느릴 수 있음 (자바스크립트가 나중에 실행됨)</li><br />

<h2 id="ssr-vs-csr-정리">SSR vs CSR 정리</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>CSR</th>
<th>SSR</th>
</tr>
</thead>
<tbody><tr>
<td>렌더링 위치</td>
<td>클라이언트 (브라우저)</td>
<td>서버</td>
</tr>
<tr>
<td>초기 로딩 속도</td>
<td>느림 (자바스크립트 로딩 후 렌더링)</td>
<td>빠름 (완성된 HTML 즉시 표시)</td>
</tr>
<tr>
<td>SEO</td>
<td>불리함 (자바스크립트를 해석해야 함)</td>
<td>유리함 (HTML이 바로 검색 엔진에 노출됨)</td>
</tr>
<tr>
<td>서버 부하</td>
<td>적음</td>
<td>큼</td>
</tr>
<tr>
<td>페이지 전환</td>
<td>빠름 (SPA 기능 활용 가능)</td>
<td>느림 (각 요청마다 새 HTML 제공)</td>
</tr>
<tr>
<td>복잡한 애니메이션 및 동적 기능</td>
<td>적합 (클라이언트에서 자바스크립트로 처리)</td>
<td>덜 적합 (서버에서 렌더링 후 동적 처리)</td>
</tr>
<tr>
<td>사용 사례</td>
<td>주로 단일 페이지 애플리케이션 (SPA)</td>
<td>콘텐츠 중심의 웹사이트, 블로그 등</td>
</tr>
</tbody></table>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://velog.io/@vagabondms/%EA%B8%B0%EC%88%A0-%EC%8A%A4%ED%84%B0%EB%94%94-SSR%EA%B3%BC-CSR%EC%9D%98-%EC%B0%A8%EC%9D%B4">[ 기술 스터디 ] SSR과 CSR의 차이</a>
<a href="https://www.youtube.com/watch?v=YuqB8D6eCKE">[10분 테코톡] 신세한탄의 CSR&amp;SSR</a></p>