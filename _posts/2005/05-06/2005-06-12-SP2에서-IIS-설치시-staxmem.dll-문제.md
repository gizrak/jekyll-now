---
title: "SP2에서 IIS 설치시 staxmem.dll 문제"
categories:
  - 인터넷
---

혹시나 인터넷 정보 서비스(IIS)를 설치하다가 나와같은 문제를 발견하는 사람이 있을것 같다. 확실히 우리나라 지식 어쩌고의 한계라 함은 어떤 전문적인 필요에서는 별로 소용이 없다는 것다. 특히 IT 분야의 그것에서는...  
  
윈도 XP SP2에서 웹서버를 설치하다가 다음과 같은 문구를 본 사람이 있을 것이다.  
  
**Setup cannot copy the file staxmem.dll ...insert "Windows XP Professional Service Pack 2 CD"**  
  
분명히 해당 폴더에 같은 파일이름이 존재하고 아무런 문제가 없는데 계속 저런 현상이 발생한다. 네이버에 물어봤더니 IIS가 8번째 줄에 있는 거라는둥 파일이 깨졌을지 모르니 스캔을 해보라는둥... 어이가 없었다. ㅡㅡ;  
  
역시나 우리의 친구 **구글**... 조금만 뒤졌더니 나온다. 우선은 이 문제의 원인부터 알아보자. 문제의 원인은 처음부터 SP2가 적용된 버젼의 윈도우를 설치한 사람에게서 나온다. 즉 SP1에서의 파일과 호환이 되지 않는 문제가 생기는거다.  
  
솔직히 구글에서도 조금 삽질했다. 한참 이곳저곳 링크타고 다녀보면서 이상한 방법은 다 따라해봤으나 전부 소용없었다. 재릴리즈인지 뭔지 그거도 해보고 서비스팩을 새로운 방식으로 새로 깔아보기도 하고.... 근데 해결책은 생각보다 쉬웠다.  
  
콘솔 모드로 들어가서 다음과 같이 입력하면 된다.  
  
**esentutl /p %windir%/security/database/secedit.sdb**  
  
그러면 안전모드가 어떻고 하면서 경고 창이 뜬다. 그냥 계속 진행을 시키면 된다. 이제부터는 IIS 설치시 dll 파일에 관한 문제없이 정상적으로 설치가 진행된다.  
  
(출처: <http://www.ilovett.com/blog/2004/10/03/>)
