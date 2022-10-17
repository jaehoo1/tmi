(서버에 클라이언트가 많아질 때) 인프라를 업그레이드하는 방법

<br/>

## Scale Up(스케일 업)
기존의 서버 그 자체 성능을 올려 처리 능력을 향상시키는 것 (ex : 성능이나 용량 증강을 목적으로 하나의 서버에 디스크를 추가하거나 CPU나 메모리를 업그레이드, AWS의 EC2 인스턴스 사양 ↑)

수직 스케일링(vertical scaling)이라고도 함

<br/>

## Scale Out(스케일 아웃)
서버(장비)의 대수를 늘림. (비슷한 사양의) 서버를 추가로 연결해 처리할 수 있는 데이터 용량이 증가할 뿐만 아니라 기존의 서버 부하를 분담해 성능 향상의 효과를 기대

수평 스케일링(horizontal scaling)이라고도 함

<br/>

## 비교
||Scale Up(스케일 업)|Scale Out(스케일 아웃)|
|---|---|---|
|유지보수 및 관리|쉬움|여러 노드에 적절히 부하분산 필요|
|확장성|제약이 있음|스케일 업에 비해 자유로움|
|장애복구|서버가 1대, 다운타임이 있음|장애 탄력성이 있음|
|서버 비용|성능 증가에 따른 비용 증가폭이 큼|스케일 아웃보다는 비용 부담이 적음|
|운영 비용|서버 대수가 증가하진 않으므로 변화없음|대수가 늘어날수록 관리 편의성이 떨어지며, 운영 비용 증가|
|주요 기술(App 관점)|고성능 CPU, 메모리 확장, SSD|Sharding, Query-off Loading, Queue, In Memory Cache, NoSQL, Object Storage, Distributed Storage|
|적용|<ul><li>온라인 금융 거래와 같이 워크플로우 기반의 빠르고 정확하면서 단순한 처리가 필요한 [OLTP(Online Transaction Processing)](https://github.com/jaehoo1/tmi/tree/main/OLTP%2C%20OLAP#oltponline-transaction-processing)</li><li>고성능 Legacy 어플리케이션</li></ul>|<ul><li>대량의 데이터 처리와 복잡한 쿼리가 이루어지는 [OLAP(Online Analytical Processing)](https://github.com/jaehoo1/tmi/tree/main/OLTP%2C%20OLAP#olaponline-analytical-processing)(ex : 빅데이터의 데이터 마이닝, 검색엔진 데이터 분석 처리)</li><li>분산처리 시스템</li></ul>|

<br/>

### Reference
https://m.blog.naver.com/islove8587/220548900044  
https://tecoble.techcourse.co.kr/post/2021-10-12-scale-up-scale-out/