## 카카오
- 2020.06.29 - 2020.09.28

### "신규 서비스" 운영 및 관리에 필요한 Admin System 개발

"신규 서비스"를 관리, 운영하기 위한 기능을 제공하는 Admin 개발을 진행했습니다. 
- 관리, 운영의 주 대상은 "신규 서비스" 가입자의 상태 및 이용 내역 
- 개인정보를 다루는 시스템이기 때문에, Admin 유저 (카카오 사원) 에 대해서 접근통제 및 로그 기록을 수행 

저는 본 시스템의 Backend, Frontend 개발 및 배포 과정 구성을 진행했습니다. 

#### 기술 스택 적용 상세

Spring Boot: Admin 의 Backend 구성 시 사용 
Spring Security: Admin 에 로그인 시 ID, PW 의 인증 및 사내 LDAP 계정 연동을 위해 사용 
Vault: 설정 파일 or 환경변수로 주입하기에 다소 민감한 Credential 값을 주입할 때 사용 
Redis: Spring Security 에서 생성하는 Session 정보 저장 시 사용, 실 운영 환경에서 여러 서버 간 세션 정보 공유 목적 
ElasticSearch: Admin 에서 발생되는 로그 기록을 저장 
MySQL: Admin 에서 필요한 정보(Admin 유저, 권한 관리 등)를 저장 
Vue: Admin 의 Web Frontend 구성 시 사용, Single Page Application 으로 동작 
Docker, Kubernetes: FE 와 BE 코드를 Docker Image 로 빌드한 후, 해당 이미지를 K8s Cluster 상에 배포 

재직 기간동안 아래 기능들을 구현했습니다. 
- 로그인: 사내 LDAP 계정을 이용하여 로그인하도록 하기 위해, 사내 LDAP 계정 API 서버와 연계하여 로그인 처리. 
로그인은 기본적으로 Spring Security 의 formLogin 을 사용하며, LDAP 계정 로그인 구현을 위해, ID 와 PW 를 검증하는 Authentication Provider 를 customize 하여 작성 

- 인증 및 인가: 요청을 보낸 사용자 식별 및 가지고 있는 권한 확인하여 요청을 보낸 API 에 접근할 수 있는지 확인. 
로그인 성공 시, Spring Security 는 인증 정보를 세션에 저장, Frontend 로는 세션 Key 를 Cookie 의 형태로 전달. 
이후 이 Cookie 와 함께 요청이 들어오면 Spring Security 는 요청을 보낸 사용자의 식별, 권한 체크 및 요청한 API 에 대한 접근 통제를 수행. 

- 유저(어드민), 그룹, 권한 관리: 어드민 유저를 역할에 따라 일정 그룹으로 나누고, 그룹별로 접근 가능한 API 를 제한. 
User, Group, Permission 이라는 3개의 JPA Entity 를 이용, User 와 Group 은 N:1, Group 과 Permission 은 1:M 관계. 
유저는 1개의 그룹에 소속될 수 있으며, 권한 값들의 세팅은 Group 에 대해서 진행. 
로그인 시 다음 과정을 거쳐서 유저의 권한을 확인. 
1. 유저 정보 조회 
2. 유저가 소속된 그룹 조회 
3. 그룹이 가진 권한 값들 조회 

- 로그 기록 남기기: 각 유저가 요청을 보낼 때마다의 기록을 남겨서, 추후 문제 발생 시 tracking 용도로 사용. 
Spring Actuator 의 Http Trace 이용, 모든 요청에 대해 기록을 JSON string 형태로 stdout 출력. 이 기록은 fluentd -> kafka -> logstash 를 거쳐서 ElasticSearch 에 기록. 

- "신규 서비스" 가입자 정보 조회 및 서비스 이용 내역 조회

글 작성 시점을 기준으로 카카오에서 아직 정식 출시되지 않은 서비스여서 서비스명 노출이 불가능합니다.  
따라서 "신규 서비스" 로 적었습니다.