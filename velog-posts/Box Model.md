<p>CSS Box Model은 웹 페이지에서 요소들이 차지하는 공간을 이해하고 배치하는 데 매우 중요한 개념이다. 모든 HTML 요소는 사각형 박스 형태로 표현되며, 이 박스는 요소의 크기와 외관을 정의한다. Box Model은 요소의 크기와 여백을 결정하는 네 가지 영역으로 구성된다.</p>
<h2 id="1-content-콘텐츠-영역">1. Content (콘텐츠 영역)</h2>
<li>설명<br /> 요소 안에 실제로 들어가는 텍스트나 이미지 등의 내용이 표시되는 영역이다.</li><br />
<li>특징<br /> 콘텐츠 영역의 크기는 요소의 width와 height 속성으로 지정한다.</li>

<h2 id="2-padding-패딩-영역">2. Padding (패딩 영역)</h2>
<li>설명<br /> 콘텐츠와 테두리 사이의 내부 여백이다. 콘텐츠가 테두리에 너무 붙지 않도록 여유 공간을 준다.</li><br />
<li>특징<br /> 패딩은 투명하며, padding 속성으로 각 면의 크기를 설정할 수 있다. 각 면을 개별적으로 설정할 수 있다(padding-top, padding-right, padding-bottom, padding-left)</li><br />
<li>중요<br /> 패딩은 콘텐츠 영역을 확장시키기 때문에, 요소의 width와 height에 더해져 요소가 차지하는 실제 공간이 커진다.</li>

<h2 id="3-border-테두리-영역">3. Border (테두리 영역)</h2>
<li>설명<br /> 콘텐츠와 패딩을 둘러싸는 테두리 영역이다.</li><br />
<li>특징<br /> border 속성을 사용하여 테두리의 두께, 스타일(예: 실선, 점선 등), 색상을 설정할 수 있다.</li><br />
<li>중요<br /> 테두리의 두께도 요소가 차지하는 전체 크기에 영향을 미친다.</li>

<h2 id="4-margin-외부-여백-영역">4. Margin (외부 여백 영역)</h2>
<li>설명<br /> 요소와 다른 요소 사이의 외부 여백이다. 요소의 바깥쪽에 위치하며, 요소 간의 간격을 조절하는 데 사용된다.</li><br />
<li>특징<br /> margin 속성으로 설정하며, 각 면의 여백을 개별적으로 조정할 수 있다. (margin-top, margin-right, margin-bottom, margin-left)</li><br />
<li>중요<br /> 마진은 투명하며, 요소 간의 간격을 결정한. 또한, 수직 방향 마진은 마진 병합(Margin Collapse) 현상이 발생할 수 있는데, 이는 인접한 요소들 간에 더 큰 마진만 적용되는 현상이다.</li>

<p><img alt="" src="https://velog.velcdn.com/images/anstks1992/post/c6a1915d-b0ed-485f-ad1b-7268f5142db8/image.png" /></p>
<h3 id="📄-reference">📄 Reference</h3>
<p><a href="https://www.zerocho.com/category/CSS/post/582ddf81d4416a001860e75d">제로초: CSS 박스 모델(box-model)</a>
<a href="https://developer.mozilla.org/ko/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model">MDN: CSS 기본 박스 모델 입문</a></p>