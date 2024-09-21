<p>Github에 그동안 push만 하고 잔디 확인을 안했는데 오늘 확인해 보니 잔디가 안심어져 있었다. 이전에도 한 번 이런적이 있어서 생각나는 원인이 있었는데 github에 등록된 이메일과 이름이 컴퓨터 git에 저장된 이메일과 이름이 달라서 발생한 문제다. 최근에 github를 새롭게 수정하면서 계정정보를 바꿨던거 같은데 그게 원인이라고 생각했다.</p>
<h2 id="🔑해결방법-1">🔑해결방법 1</h2>
<h3 id="1-github-계정-정보-확인-하기">1. github 계정 정보 확인 하기</h3>
<h5 id="github-setting---public-profile에서-name확인---emails에서-primary-이메일-확인하기">github setting -&gt; public profile에서 name확인 -&gt; Emails에서 primary 이메일 확인하기</h5>
<h3 id="2-git-계정이름-계정-이메일-확인">2. git 계정이름, 계정 이메일 확인</h3>
<pre><code class="language-js">git config --list</code></pre>
<h5 id="cmd나-git-bash에서-위에-명령어를-치고-username-과-useremail을-확인한다">cmd나 git bash에서 위에 명령어를 치고 user.name 과 user.email을 확인한다.</h5>
<h3 id="3-이메일-이름-설정">3. 이메일 이름 설정</h3>
<pre><code class="language-js">git config user.name &quot;Your name&quot;
git config user.email &quot;Your email&quot;</code></pre>
<h5 id="github와-local-git의-내용이-일치하지-않으면-일치되도록-바꿔주기">github와 local git의 내용이 일치하지 않으면 일치되도록 바꿔주기</h5>
<hr />
<p>대부분의 잔디 심기 문제는 여기서 해결될거다. 나도 저번에 잔디 심기 문제가 있었을때 이 방법으로 해결했다. </p>
<p>하지만 이번에는 push를 해도 여전히 잔디가 심어지지 않았다. </p>
<p>그러다가 branch default 설정 문제도 있다고 해서 해결방법을 찾아보고 해결하였다.</p>
<hr />
<h2 id="🔑해결방법-2">🔑해결방법 2</h2>
<h5 id="검색해보니-default-branch와-commit한-branch가-다를-경우에-잔디가-안-심어-진다고-한다">검색해보니 Default branch와 Commit한 branch가 다를 경우에 잔디가 안 심어 진다고 한다.</h5>
<h5 id="내가-작업을-진행한-branch는-master였지만-github에-default로-설정되어-있던-branch는-main이어서-잔디가-심어지지-않았던-것이다">내가 작업을 진행한 branch는 master였지만 github에 default로 설정되어 있던 branch는 main이어서 잔디가 심어지지 않았던 것이다.</h5>
<h3 id="default-branch-바꿔주기">Default branch 바꿔주기</h3>
<h5 id="github-해당-repository---setting---general---default-branch에서-현재-작업하고-있는-branch를--default로-바꿔주기">github 해당 Repository -&gt; Setting -&gt; General -&gt; Default branch에서 현재 작업하고 있는 branch를  default로 바꿔주기</h5>