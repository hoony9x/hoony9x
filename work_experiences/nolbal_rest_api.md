## 놀이의발견
- 2020.01.06 - 2020.02.28

### 기존 Web Backend 에 REST API 추가

놀이의발견 사장님페이지(https://ceo.nolbal.com) 는 Django 를 이용하여 개발이 되어 있었습니다. 
그리고 저는 여기에 REST API 의 추가를 해야 하는 상황이었습니다. 

최대한 기존 구조를 유지(실서비스 돌아가는 상황이기 때문에 기존 구조의 변경이 힘든 상황)하며 REST API 를 추가하기 위해 아래와 같은 작업을 진행했습니다. 
- Django 로 구성된 기존 웹 Backend 에 REST API 추가를 위해 DRF(Django REST Framework) 를 이용. 
- API 의 인증 수단으로는 JWT 를 사용 

인증을 할 때는 Json Web Token 을 사용하는데, 서버에서 상태를 저장하고 있을 필요가 없다는 장점이 있지만, 한번 발급된 Token은 자체적으로 무효화를 할 수 있는 방법이 존재하지 않습니다. 따라서 아래와 같이 구성을 했습니다. 
- 최초 로그인 시 access_token 과 refresh_token을 발급. 
- access_token 은 실제 인증에 사용됨. 
- refresh_token 은 access_token을 새로 갱신할 때 사용. 
- access_token 의 유효 시간은 3시간, refresh_token 의 유효 시간은 180일로 지정. 
- refresh_token 은 서버의 DB에서 별도로 관리 
- 각 사용자마다 최대 10개의 refresh_token을 가질 수 있으며 개수 초과 시 오래된 것부터 삭 제됨. 
- refresh_token 의 invalidate 는 DB에서 해당 refresh_token을 삭제하는 것으로 대응 가능.