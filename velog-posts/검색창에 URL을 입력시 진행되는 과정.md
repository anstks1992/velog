<p>웹 브라우저에서 사용자가 URL을 입력하고 검색을 수행할 때 진행되는 과정은 여러 단계로 이루어져 있다. </p>
<p>이 과정을 <a href="https://www.google.com">https://www.google.com</a> 로 예를 들어 정리 하겠다.</p>
<h2 id="검색창에-url을-입력시-진행되는-과정">검색창에 URL을 입력시 진행되는 과정</h2>
<h3 id="1-url-입력">1. URl 입력</h3>
<ul>
<li>사용자가 브라우저 주소창에 www.google.com을 입력한다.
<li>브라우저는 이 URL을 해석하여 "www.google.com"이라는 도메인 이름이 있는 서버로 요청을 보낼 준비를 한다.
</ul>

<h3 id="2-dns-조회-domain-name-system-lookup">2. DNS 조회 (Domain Name System Lookup)</h3>
<ul>
<li>도메인은 기억하기 쉬운 주소이며 특정 서버의 IP 주소이다. 인터넷 상에서는 IP 주소로 서버를 식별한다.
<li>브라우저는 먼저 로컬 캐시에 저장된 DNS 정보를 확인하여 해당 도메인의 IP 주소가 있는지 확인한다. 
<li>없다면 DNS 서버(일반적으로 인터넷 서비스 제공업체(ISP)나 구글의 DNS 서버(8.8.8.8))에 해당 도메인의 IP 주소를 요청한다.
<li>DNS 서버는 도메인 이름과 연결된 IP 주소(구글 예: 142.250.190.78)를 반환한다.
</ul>

<blockquote>
<p>❓  DNS(Domain Name Server)
인터넷 전화번호부와 같다. DNS는 웹 사이트의 IP 주소와 도메인 주소를 연결해 주는 시스템이며, 인터넷의 모든 URL에는 고유한 IP 주소가 할당되어 있다. IP주소는 엑세스 요청 웹 사이트의 서버를 호스팅 하는 컴퓨터에 속한다.</p>
</blockquote>
<h3 id="3-tcp-연결-설정">3. TCP 연결 설정</h3>
<p>웹 브라우저가 인터넷에서 서버를 찾으면 웹 서버와 TCP 연결을 설정하고, HTTP를 통해 통신을 시작한다.</p>
<blockquote>
<p>❓ TCP
TCP (전송 제어 프로토콜)은 두 개의 호스트를 연결하고 데이터 스트림을 교환하게 해주는 중요한 네트워크 프로토콜이다. TCP는 데이터와 패킷이 보내진 순서대로 전달하는 것을 보장해준다.</p>
</blockquote>
<blockquote>
<p>❓ TCP 3-way Handshake
브라우저는 해당 IP 주소로 TCP 연결을 설정하는데 이때 3-way Handshake 과정이 발생한다.<br /></p>
</blockquote>
<p>1) SYN 패킷 전송 : 클라이언트(브라우저)가 서버에 연결을 시작하겠다는 신호를 보냅니다.
2) SYN-ACK 패킷 수신 : 서버가 이 요청을 받았음을 확인하고 연결을 수락하겠다는 신호를 보냅니다.
3) ACK 패킷 전송 : 클라이언트가 연결이 성립되었음을 확인하고 응답합니다.</p>
<h3 id="4-https-요청-및-ssltls-handshake">4. HTTPS 요청 및 SSL/TLS Handshake</h3>
<p><a href="http://www.google.com%EC%9D%80">www.google.com은</a> HTTPS를 사용하기 때문에 브라우저는 SSL/TLS Handshake를 통해 암호화된 통신 채널을 설정한다.</p>
<h3 id="5-http-요청-전송">5. HTTP 요청 전송</h3>
<p>브라우저는 구글 서버에 GET 요청을 통해 <a href="http://www.google.com%EC%9D%98">www.google.com의</a> 페이지를 요청한다.</p>
<p>이 요청은 다음과 같은 데이터를 포함한다.</p>
<ul>
<li>요청 라인: GET / HTTP/1.1
<li>헤더: 호스트 정보(Host: googel.com), 사용자 에이전트 정보 등
<li>본문: 클라이언트가 서버로 전송하는 데이터를 포함하는 부분 
</ul>

<h3 id="6-서버의-응답">6. 서버의 응답</h3>
<p>구글 서버는 클라이언트의 요청을 처리하여, 요청된 페이지의 HTML, CSS, JavaScript 파일 등을 브라우저로 전송</p>
<p>이 응답은 다음과 같은 데이터를 포함한다.</p>
<ul>
<li>상태 라인: HTTP/1.1 200 OK
<li>헤더: 콘텐츠 타입(Content-Type: text/html), 콘텐츠 길이(Content-Length) 등
<li>본문: 구글 웹페이지의 HTML 코드
</ul>

<h3 id="7-브라우저의-렌더링">7. 브라우저의 렌더링</h3>
<ul>
<li>브라우저는 수신된 HTML 파일을 파싱하면서 필요한 추가 리소스(CSS, JS, 이미지 등)를 서버에 추가 요청한다.
<li>렌더링 엔진이 DOM 트리를 생성하고, CSS 파일을 로드하여 CSSOM 트리를 만든후 이후 두 트리가 결합하여 렌더 트리를 형성하고 브라우저가 페이지를 그리기 시작한다.
<li>자바스크립트는 DOM을 조작하거나 이벤트를 처리하며 페이지 동작에 영향을 미친다.
</ul>

<p>브라우저의 렌더링 과정에 대한 자세한 내용은 <a href="https://velog.io/@anstks1992/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%A0%8C%EB%8D%94%EB%A7%81-%EA%B3%BC%EC%A0%95">브라우저 렌더링 과정</a>을 참고하자</p>
<h3 id="8-사용자에게-페이지-표시">8. 사용자에게 페이지 표시</h3>
<p>브라우저는 렌더 트리 기반으로 페이지를 화면에 그려서 사용자가 구글의 홈 화면을 볼 수 있도록 한다.</p>
<h2 id="검색-진행-과정-요약">검색 진행 과정 요약</h2>
<ol>
<li>url -&gt; 주소입력</li>
<li>dns 조회 -&gt; ip주소 검색 및 요청</li>
<li>tcp 연결 -&gt; tcp 연결 설정</li>
<li>http 요청 -&gt; 암호화된 통신 채널 설정</li>
<li>http 요청 전송 -&gt;  get요청으로 페이지 요청</li>
<li>서버 응답 -&gt; 서버에서 요청된 페이지 처리 및 전송</li>
<li>브라우저 렌더링 -&gt; 렌더링 및 페이지 구성</li>
<li>사용자에게 페이지 표시 -&gt; 화면 표시</li>
</ol>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://hyunki99.tistory.com/109">브라우저 주소창에 URL을 입력 시 일어나는 일 정리 (DNS)</a>
<a href="https://developer.mozilla.org/ko/docs/Glossary/TCP">MDN - TCP</a>
<a href="https://aws.amazon.com/ko/blogs/korea/what-happens-when-you-type-a-url-into-your-browser/">AWS - 웹 브라우저에 URL을 입력하면 어떤 일이 생기나요?</a></p>