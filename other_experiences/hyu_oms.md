## 대학교 축제 주점용 주문관리시스템 개발 및 운영
- 2014.07 - 2019.09

### 학교 축제 주점에서 사용 가능한 Web 기반 시스템 개발 및 운영

이 시스템은 저가 처음으로 진행한 개인 프로젝트입니다. 

학부 1학년 때 학과 주점 운영에 참여하면서 

본 시스템은 대학교 축제 주점에서 종이 주문서를 사용하여 발생하는 불편함을 해소하기 위해 개발을 하게 되었습니다. 

첫 버전은 2014년에 개발했으며 언어는 PHP, DB는 MySQL 을 사용했습니다. 
그리고 첫 운용을 해 본 결과 반응이 좋아서 매년 축제마다 본 시스템을 운영하고 있습니다. 

2016년에는 백엔드로 Node.JS(with ExpressJS), 프론트엔드에는 AngularJS 를 이용하여 두 번째 버전을 만들었습니다. 
이는 첫 버전에서 발생한 여러 가지 비효율적인 부분을 개선하기 위해 진행했습니다. 
비효율적인 부분은 다음과 같았으며 다음과 같이 개선을 했습니다. 
* 서버에서의 세션 관리에 문제가 생길 경우 로그인이 풀리는 현상이 발생 -> JsonWebToken 사용으로 서버에서 인증상태를 관리하지 않도록 변경 
* 웹 화면에서의 정보 변경 시 전체 페이지가 새로 로드되어 새로운 정보를 받아보는 데 지연됨 -> 프론트엔드를 Single Page Application (완벽한 SPA는 아닙니다) 으로 구성하고 서버와의 요청 및 응답은 전부 JSON format 으로 주고받도록 하여 서버는 순수하게 API 역할만 하도록 변경. 
* 프론트엔드 로드로 인해 API 서버의 요청까지 지연되는 현상이 발생 -> 프론트엔드만 제공하는 Static 서버를 따로 구성하여 백엔드 서버와 분리. 

2017년에는 백엔드로 Python3(with Flask), 프론트엔드에는 React 를 사용하여 세 번째 버전을 만들었습니다. 

2019년에는 프론트엔드 디자인을 일부 변경하였습니다. (React 는 그대로 사용) 
그리고 Node.JS 에서 async/await 키워드 지원으로 인해 비동기 코드를 동기식 코드처럼 작성이 가능하여 가독성 향상을 할 수 있게 되어서 서버 언어를 다시 Node.JS (with ExpressJS) 로 변경했습니다. 

2020년의 경우, 코로나 19 이슈로 인해 운영을 하지 못했습니다.