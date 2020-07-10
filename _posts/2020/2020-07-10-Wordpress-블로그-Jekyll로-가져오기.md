---
title: "Wordpress 블로그 Jekyll로 가져오기"
categories:
  - 블로그
comments: true
gallery:
  - url: /assets/images/posts/2020/2020-07-10-1.jpg
    image_path: assets/images/posts/2020/2020-07-10-1.jpg
  - url: /assets/images/posts/2020/2020-07-10-2.jpg
    image_path: assets/images/posts/2020/2020-07-10-2.jpg
---

블로그를 마지막으로 했던게 6년 전인가 보다. 2004년 7월에 시작해서 2014년 12월까지 글이 남아 있다. 그 동안 작성한 글의 총 개수는 295개인데 초기에 대부분의 글이 작성되었다.

{% include gallery caption="한 달 평균 2.5개 정도" %}

워드프레스를 다시 공개로 바꿀까 했다가 마음을 바꿨다. 몇 가지 이유가 있다.
1. 하나로 통합하자!
1. 저작권 개념이 없던 시절의 막 퍼온 것들이 있더라.
1. 원본을 최대한 보존하겠지만, 시대 상황에 맞는 보정이 필요한 글들이 보인다.

마음의 결정을 했으니 이제 남은 건 노가다 삽질 뿐... 이라고 생각했다가 대박을 발견했다. 역시 전 검색해 보면 전 세계 누군가는 나와 같은 고민을 했나 보다. Wordpress를 Markdown으로 convert 해주는 것을 누가 구현해 놓았다.
<https://github.com/lonekorean/wordpress-export-to-markdown>

## 작업 순서

간략하게 순서는 아래와 같다.
1. nodeJS를 설치한다 (자세한 설명은 여기서는 패스)
1. wordpress.com 설정으로 들어가서 블로그 전체를 export 한다 (<https://wordpress.org/support/article/tools-export-screen/>)
1. export 후 다운로드 받은 파일명을 export.xml로 변경한다.
1. 위 github 프로젝트를 clone하고 export.xml을 동일한 디렉토리로 복사한다.
1. `npm install && node index.js` 명령 수행하면 끝!

![](/assets/images/posts/2020/2020-07-10-6.jpg)

아주 훌률하다. 이렇게 하면 동일 경로 output 하위 각 post 별로 디렉토리가 생성되고, 거기에 `index.md`와 `images` 디렉토리가 생성된다. 폴더명 한글이 조금 아쉽지만 작성된 `index.md` 파일엔 전혀 문제가 없다.

![](/assets/images/posts/2020/2020-07-10-3.jpg)
![](/assets/images/posts/2020/2020-07-10-4.jpg)
![](/assets/images/posts/2020/2020-07-10-5.jpg)

잔손질은 필요하다. 이미지 경로 변경하고 카테고리 입력 같은 작업을 마치고, 예전 블로그를 다시 가져오려고 한다. SI 식으로 이름을 짓자면 ``차세대 통합 프로젝트``라고 할까.
