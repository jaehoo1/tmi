# 특수문자
특수문자(기호)의 읽는 법, (개발)사용 용도 등

|특수문자|영문|한글|주 용도|
|---|---|---|---|
|\`|backtick, grave|백틱|<li>Markdown : `인라인 코드`</li><li>Javascript, Kotlin : 템플릿 리터럴</li>|
|\`\`\`<br/>~~~|||<li>Markdown : 코드 블럭</li>|
|~|tilde|틸드, 물결표|<li>Markdown : ~~취소선~~</li>|
|!|exclamation mark|느낌표|<li>Markdown : 링크, 파일, 이미지 콘텐츠 등</li><li>Code : Not 연산</li>|
|@|at sign, commercial at|골뱅이|<li>Markdown : 미디어 콘텐츠</li><li>Java : Annotation</li><li>Javascript : Decorator</li><li>[CSS import](https://www.biew.co.kr/tag/Link%20%EB%B0%A9%EC%8B%9D%20vs%20%40import%20%EB%B0%A9%EC%8B%9D%20%EC%B0%A8%EC%9D%B4)</li><li>Server(email) : 계정@도메인</li>|
|#|crosshatch, number sign, pound, hash, sharp|크로스해치, 샵, 번호 기호, 해시, 파운드|<li>Python : 주석</li><li>Expr : 숫자 포맷</li>|
|#!|shebang|셔뱅, 샤-뱅, 해시뱅, 파운드-뱅, 해시-플링, 크런치뱅|<li>sh : 인터프리터 지정</li>|
|$|dollar sign|달러|<li>sh : 변수</li><li>RegEx : ~~로 끝나는 문자그룹, n번째 문자그룹</li>|
|%|percent sign|퍼센트, 나머지연산, 모듈로|<li>Code : 나머지 연산</li><li>SQL : LIKE</li>|
|^|caret|캐릿, 제곱, 햇|<li>Code : XOR 연산</li><li>RegEx : ~~로 시작하는 문자그룹</li>|
|&|ampersand|앰퍼샌드, 앤드|<li>Code : 비트, 논리 AND 연산</li><li>HTML : 특수문자</li>|
|*|asterisk|애스터리스크, 아스테리스크, 별표, 곱하기|<li>곱연산</li><li>[와일드카드 문자](https://ko.wikipedia.org/wiki/%EC%99%80%EC%9D%BC%EB%93%9C%EC%B9%B4%EB%93%9C_%EB%AC%B8%EC%9E%90)</li>|
|( )|parenthesis|소괄호|<li>연산 우선 순위 지정</li><li>Code : 함수 파라미터 지정</li><li>Python : Tuple</li>|
|-|hyphen minus, hyphen, minus, dash|하이픈, 빼기, 대시|<li>sh : 옵션</li><li>뺄셈 연산</li><li>SQL : 주석</li>|
|_|underscore, underline|언더스코어, 언더바, 밑줄|<li>스네이크 표기법</li>|
|=|equal sign|이퀄, 는, 등호|<li>변수 대입, 비교 연산</li>|
|+|plus sign|플러스, 더하기|<li>덧셈 연산</li>|
|[ ]|brackets|브래킷, 브라켓, 브라킷, 대괄호|<li>Code : 배열</li><li>RegEx : 범위 안의 문자들</li>|
|{ }|braces|브레이스, 중괄호|<li>중괄호 블럭(`for`, `if` 등)</li><li>Python : Dictionary</li><li>[JSON](https://ko.wikipedia.org/wiki/JSON) 객체</li><li>RegEx : n번 반복되는 문자 그룹</li>|
| \ |back slash|백슬래시, 역슬래시, 원화|<li>[이스케이프 시퀀스](https://learn.microsoft.com/ko-kr/cpp/c-language/escape-sequences?view=msvc-170)</li><li>Windows : 폴더 구분</li>|
|\||vertical bar, pipe|버티컬 바, 파이프|<li>Code : 비트, 논리 OR 연산</li><li>sh : 표준 출력 - 표준 입력 연결</li>|
|;|semicolon|세미콜론|<li>문(장)의 끝</li>|
|:|colon|콜론|<li>키: 값</li><li>Python : 슬라이싱</li><li>vi : 모드 변경</li>|
|'|apostrophe|아포스트로피, 어파스트로피, 어퍼스트로피, 싱글 쿼테이션, 작은 따옴표|<li>C / C++, Java : char</li><li>문자열</li>|
|"|quotation|쿼테이션, 큰 따옴표|<li>문자열</li>|
|,|comma, virgule|콤마, 반점, 쉼표|<li>구분자</li>|
|.|dot, period, full stop|마침표, 닷, 점, 피리어드|<li>소수점</li>|
|< >|angle brackets|앵글 브래킷 / 브라킷|<li>대소 비교 연산</li><li>비트 shift 연산</li><li>제네릭</li>|
|/|slash|슬래시, 나누기|<li>나눗셈 연산</li><li>Linux, Unix : 폴더 구분</li>|
|?|question mark|물음표|<li>나눗셈 연산</li><li>Linux, Unix : 폴더 구분</li><li>RegEx : 앞의 문자가 있을 수도 있고 없을 수도 있음</li>|

<br/>

## Reference
- https://jdm.kr/blog/87
- https://www.ihee.com/688
- https://chinsun9.github.io/2021/08/15/english-name-of-special-characters/