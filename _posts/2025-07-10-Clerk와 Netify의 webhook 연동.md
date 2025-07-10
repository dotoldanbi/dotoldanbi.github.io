\### nextjs에서 사용자 인증을 제공하는 Clerk을 사용하는 경우 session과 user관련 clerk에서 발생하는 event 처리가 필요하다.



이를 구현하기 위해 다음과 같은 순서의 실행이 필요하다.

1\. github repository에 commit \& push

2\. netify에서 해당 github repository의 deploy

3\. netify에서 제공되는 domain 취득

4\. netify - project - deploy메뉴의 build hooks 항목에서 'Add build hook'으로 hook을 추가하며 hook url은 3번의 domain + clerk webhook경로인 '/api/webhooks' 이다

5\. Clerk관련하여 Clertk Secret Key와  Webhook Secret 문자열이 필요하며 이는 환경변수로 제공되어야 한다

6\. Clerk - Project - Developers - Webhooks 메뉴에서 Add Endpoint로 Endpoint를 추가한다. endpoint는 4번과 동일하다.

7\. 추가된 endpoint를 클릭하여 상세페이지로 이동하여 Subscribed event를 수정한다(user와 session관련 이벤트 추가)

8\. nextjs의 clerk webhook route파일에 log문자열을 출력하여 netify console에서 확인한다. netify의 log는 Logs - Functions에서 확인할 수 있다.

```

Jul 9, 06:31:12 PM: 09097959 INFO Event type: session.created

Jul 9, 06:31:12 PM: 09097959 INFO ✅ Clerk Webhook 수신됨:

Jul 9, 06:31:12 PM: 09097959 INFO Event data: {  

abandon\_at: 1754643255534,  

actor: null,  

client\_id: 'client\_2zd5cQxu9YBORl2Mwwj2BPFkubF',  

created\_at: 1752051255534,  

expire\_at: 1752656055534,  

id: 'sess\_2zdBpwXUK6SXKzinU9ZiSWrNUva',  

last\_active\_at: 1752051255534,  

object: 'session',  

status: 'active',  

updated\_at: 1752051255580,  

user\_id: 'user\_2zaD48Mj3r1CearXqizczjc1EbJ'  

}

```



9\.  이후 event type에 따른 기능 구현

