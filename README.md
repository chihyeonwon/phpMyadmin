비박스(bWAPP) A9 phpMyAdmin BBCode Tag XSS

이 도구를 이용하여 허용받지 않은 서비스 대상으로 해킹을 시도하는 행위는 범죄 행위입니다. 해킹을 시도할 때에 발생하는 법적인 책임은 그것을 행한 사용자에게 있다는 것을 명심하시기 바랍니다.      
            
A9 - phpMyAdmin BBCode Tag XSS     

해당 취약점을 앞에서 다뤘던 내용으로 아래의 페이지를 참조해 주시기 바랍니다.       

Client-Side Code Injection (CVE-2010-4480)

허용받지 않은 서비스 대상으로 해킹을 시도하는 행위는 범죄 행위입니다. 해킹을 시도할 때에 발생하는 법적인 책임은 그것을 행한 사용자에게 있다는 것을 명심하시기 바랍니다.
 
CVE-ID CVE-2010-4480
        
개요
원격 공격자가 임의의 웹 스크립트 또는 HTML을 삽입할 수 있는 검증 미흡 오류로 크로스 사이트 스크립팅이 가능      
      
설명      
phpMyAdmin 3.3.8.1과 3.4.0-beta1 이전 버전의 error.php에서 원격 공격자가 "@" 문자가 포함된("[a@url@page]") BBcode 태그 작성을 통해 XSS 공격을 수행할 수 있습니다.        
       
- phpMyAdmin : 웹상에서 MySQL을 관리하기 위한 도구로, PHP 언어로 작성- BBcode : BBCode 또는 불리틴 보드 코드(Bulletin Board Code, 전자 게시판 부호)는 전자 게시판에 글을 작성하는데 쓰이는 가벼운 마크업 언어이다.       
- BBCode는 HTML과 거의 같은 역할을 하며 이들의 문법도 유사하다. 다만, BBCode는 대괄호를 사용하여 태그를 나타낸다.
             
- 위의 CVE 설명을 보면 error.php 페이지에서 취약점이 발생하는 것을 알 수 있습니다. error.php 페이지를 접속해 보도록 하겠습니다.          
phpmyadmin에서 error.php 페이지로 직접 호출하여 이동이 가능            
        
error.php 페이지에서 사용하는 변수는 총 두 가지로, type 변수와 error변수가 있습니다. type 변수에 입력한 문자열은 오류의 종류를 출력 합니다. error 변수는 값을 조작하여 공격 코드 삽입이 가능합니다.       
error 변수에서 BBCcode 태그를 입력하는데, @문자를 사용하여 [a@url@page] 형태로 태그를 조작합니다. 여기서 @url에 입력한 주소로 리다이렉션할 주소를 넣어주고 Help라는 문자열을 통하여 클릭했을 때 해당 URL로 이동하게 태그를 조작하였습니다.          
               
서버 관리자 및 다른 클라이언트들에게 피싱 페이지나 악성링크가 삽입된 페이지를 보내서 사용자들이 클릭을 하거나 접속을 한다면 2차 피해가 추가 발생할 수 있습니다.          
 
[POC]
http://[취약 페이지]/phpmyadmin/error.php?type=1
 
http://[취약 페이지]/phpmyadmin/error.php?error=에러를 해결하기위해 다음 사이트를 참고하십시오.+[a@https://securitycode.tistory.com@_self]Help[/a]
 
http://[취약 페이지]/phpmyadmin/error.php?type=This+is+a+client+side+hole+evidence&error=Client+side+attack+via+characters+injection[br]It%27s+possible+use+some+special+tags+too[br]Found+by+Tiger+Security+Tiger+Team+-+[a%40http://www.tigersecurity.it%40_self]This%20Is%20a%20Link[%2Fa]
 
영향을 받는 버전3.4.0-beta1 이전의 모든 버전
3.3.8.1/3.3.9.0 이전 버전해결책phpMyAdmin 3.4.0-beta1 이상으로 업그레이드하거나, 취약한 이상의 버전으로 패치
 
(참고사이트)[https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-4480]
