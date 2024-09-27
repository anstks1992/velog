<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/45c1c24f-2475-4b3e-b7ea-1eb4f64a4674/image.png" /></p>
<p>HTTP (HyperText Transfer Protocol)와 HTTPS (HyperText Transfer Protocol Secure)는 웹에서 정보를 주고받기 위한 프로토콜이다.</p>
<h2 id="http-hypertext-transfer-protocol">HTTP (HyperText Transfer Protocol)</h2>
<ul>
<li>HTTP는 웹 브라우저와 웹 서버 사이의 데이터를 전송하기 위한 통신 프로토콜이다
<li>기본적으로 데이터를 암호화하지 않고 전송하기 때문에 제3자가 데이터를 쉽게 볼 수 있다.
<li>HTTP는 포트 번호 80을 사용한다.
<li>보안이 필요하지 않은 일반 웹사이트에서 주로 사용된다.
 </ul>

<h2 id="https-hypertext-transfer-protocol-secure">HTTPS (HyperText Transfer Protocol Secure)</h2>
<ul>
<li>HTTPS는 HTTP에 보안을 추가한 프로토콜로, 데이터가 전송되는 동안 SSL/TLS 암호화 기술을 사용해 데이터를 보호한다
<li>암호화 기술을 통해제3자가 데이터를 도청하거나 변조할 수 없도록 방지한다.
<li>HTTPS는 포트 번호 443을 사용하며, 대부분의 웹사이트에서 보안을 위해 HTTPS를 사용한다
<li>보안이 중요한 사이트, 예를 들어 온라인 뱅킹, 이메일 서비스 등에서 사용한다
</ul>

<blockquote>
<h4 id="❓-ssl--tls">❓ SSL / TLS</h4>
<p>웹 상에서 데이터를 안전하게 주고받기 위한 암호화 프로토콜</p>
</blockquote>
<ul>
<li> SSL : 초기버전이며 보안에 취약점이 있어 현재 브라우저에서는 쓰지 않는다.
<li> TLS : SSL의 여러 보안 취약점을 보완하기 위해 설계된 후속 프로토콜로 SSL에 비해 강력한 암호 알고리즘과 간소화된 핸드셰이크 과정등 현재 웹사이트 및 어플리케이션에서 주로 쓰인다.
</ul>

<h3 id="https-연결과정">HTTPS 연결과정</h3>
<ol>
<li>클라이언트(브라우저)가 서버에 자신이 지원하는 TLS 버전과 암호화 알고리즘을 서버에 보내면서 최초 연결 시도를 함</li>
<li>서버는 받은 요청을 분석후 자신의 SSL/TLS 인증서를 클라이언트에 전송</li>
<li>브라우저는 인증서의 유효성을 검사하고 세션키를 발급함</li>
<li>브라우저는 세션키를 보관하며 추가로 서버의 공개키로 세션키를 암호화하여 서버로 전송함</li>
<li>서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음</li>
<li>클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행함</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/79dac829-3346-4e75-8b48-1e655b1aed27/image.png" /></p>
<blockquote>
<h4 id="❓-공개키--비밀키">❓ 공개키 / 비밀키</h4>
</blockquote>
<ul>
  <li> 공개키 : 누구에게나 공개할 수 있는 키이며 주로 데이터를 암호화하거나, 디지털 서명을 검증하는 데 사용
    <li> 비밀키 : 공개키와 짝을 이루는 비밀 키로, 소유자만 알고 있어야 한다. 데이터를 복호화하거나, 디지털 서명을 생성하는 데 사용
      </ul>


<h2 id="http-vs-https">HTTP vs HTTPS</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>HTTP</th>
<th>HTTPS</th>
</tr>
</thead>
<tbody><tr>
<td>보안성</td>
<td>데이터가 암호화 안됨</td>
<td>데이터 암호화</td>
</tr>
<tr>
<td>포트</td>
<td>80번</td>
<td>443번</td>
</tr>
<tr>
<td>SSL/TLS</td>
<td>인증서    없음</td>
<td>SSL/TLS 인증서를 필요로 함</td>
</tr>
<tr>
<td>속도</td>
<td>HTTPS보다 빠름 (암호화 부하가 없음)</td>
<td>암호화로 인해 HTTP보다 느릴 수 있음</td>
</tr>
<tr>
<td>데이터 무결성</td>
<td>데이터가 쉽게 변조될 수 있음</td>
<td>데이터가 변조되거나 손상될 가능성이 적음</td>
</tr>
</tbody></table>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://mangkyu.tistory.com/98">HTTP와 HTTPS의 개념 및 차이점</a>
<a href="https://velog.io/@hyoribogo/what-is-the-defference-between-http-and-https">HTTP와 HTTPS의 차이는 무엇일까?</a>
<a href="https://tiptopsecurity.com/how-does-https-work-rsa-encryption-explained/">https://tiptopsecurity.com/how-does-https-work-rsa-encryption-explained/</a></p>