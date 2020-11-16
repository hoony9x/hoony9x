## "Spotboard DOMjudge converter" 업데이트 
- 2019.08
- [여기](https://github.com/spotboard/domjudge-converter/pull/6) 를 클릭하여 PR 보기.

이 프로젝트("domjudge-converter")는 Node.js 로 작성되었으며 CLI 환경에서 실행됩니다. 
이 도구를 사용하면 DOMjudge 의 API 를 통해 대회의 결과물을 Spotboard 에서 표시할 수 있습니다. 

DOMjudge 는 현재 ICPC Seoul Regional 에서 사용되는 대회 시스템입이며 Spotboard 는 이 대회에서 대회 중 scoreboard 표시 및 시상식 전 award ceremony 에서 사용되고 있습니다. 

본 프로젝트는 이전에 DOMjudge 5.3 을 대상으로 개발이 되었습니다. 

Pull Request 작성 시점 기준으로 DOMjudge 의 최신 버전은 7 입니다. 이 버전부터 내부 구조 및 API 가 대대적으로 변경이 되었으며 하위 호환성은 없는 상태입니다. 즉, 기존 코드를 최신 DOMjudge 에서 사용할 수 없었습니다. 

최신 버전에서 사용 가능하도록 하기 위해서 본 프로젝트의 코드를 대거 수정했습니다.