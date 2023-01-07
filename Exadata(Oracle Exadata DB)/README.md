# Exadata(Oracle Exadata)(Exadata DB)
오라클 엑사데이터(Oracle Exadata, Oracle Exadata Database Machine) 또는 엑사데이터(Exadata)는 오라클 데이터베이스를 구동하는데 최적화된 컴퓨팅 플랫폼이다.

엑사데이터는 인텔 x86-64 연산 및 스토리지 서버, RoCE 또는 인피니밴드 네트워킹, 퍼시스턴트 메모리(PMEM), NVMe 플래시, 특수 소프트웨어의 스케일아웃을 포함하는, 하드웨어 및 소프트웨어 결합 플랫폼이다.

Exadata는 완전히 새로운 제품이 아니다. 그 내부의 오라클 S/W 바이너리는 기존과 동일하기도 한다. 다만 스토리지 레이어가 다르다. 스토리지 레이어에는 cellsrv라는 스토리지 I/O 처리 엔진이 내장되어 있어 최적화된 I/O 처리를 수행한다. 스토리지 서버 안에 장착되는 디스크를 Cell이라고 부르기 때문에 보통 스토리지 서버를 Cell 서버라고 부르기도 한다. Exadata를 개발하는 프로젝트 명이 SAGE(Storage Applicance for Grid Environment)일 정도로 이 스토리지 레이어는 중요하다.

현대의 서버의 성능에 가장 큰 영향을 주는 것은 I/O다. 특히 DB는 I/O 성능에 큰 영향을 받는다. Exadata는 I/O에 획기적인 개선이 있기 때문에 아주 뛰어난 성능을 발휘할 수 있는 것이다. 변화된 점은 기존의 **스토리지 저장 장치**를 하드디스크가 아닌 **플래시**로 구성했다는 부분이다. 이를 통해 디스크 I/O의 성능을 극대화할 수 있으며, 데이터의 처리 속도 면에서 우위를 선점할 수 있다.

<br/>

## Exadata Architecture
Exadata는 다음의 기술들을 도입하여 DB 서버와 Storage 사이의 I/O 병목 현상을 해결하였다.

<br/>

### 1. Infiniband
Infiniband는 DB 서버와 스토리지 서버 사이에 존재한다. 대역폭이 약 초당 40Gb 정도 되는데 기존 대비 훨씬 큰 처리량(기존 대비 5배 이상)이다. DB 서버와 스토리지 서버 사이에도 Infiniband로 연결하는 스위치가 존재하지만 하나 이상의 Rack으로 구성 시 Rack끼리 연결 시에도 Infiniband로 연결하는 스위치가 존재한다.

사실 Infiniband는 오라클에 의한 새로운 개념이 아니다. 컴팩/IBM/HP의 Future I/O, 인텔/MS/Sun의 Next Generation I/O 이 두 기술이 1999년 합쳐져서 만들어졌다. Exa 이외에도 많은 클라우드 컴퓨터와 수퍼 컴퓨터들이 Infiniband를 사용하고 있다.

이더넷과는 다소 차이가 있다. 계층적 스위치 방식이 아니고 스위치 패브릭 방식의 아키텍처이다. 모든 전송은 채널 어댑터에서 시작하거나 끝난다. 각 프로세서는 HCA(호스트 채널 어댑터)를 가지고 있고, 각 주변 장치는 TCA(타켓 채널 어댑터)를 가지고 있다.

Infiniband와 경쟁하는 것은 기가 비트 이너넷이다. 2012년 기준으로 세계 500 수퍼 컴퓨터(Top 500)에서 Infiniband는 226개, 기가 비트 이더넷은 188개 사용되었다.

<br/>

### 2. MPP(Massively Parallel Processing)
Storage에 MPP 개념을 도입

- 스토리지를 Parallel Storage Grid로 구성한다. 즉 여러 Cell 서버가 되는 것이다.
- 위의 Cell 서버에 데이터를 분할하여 저장하고 처리한다.

장점 : 스토리지의 병목 현상 해결, Shared Nothing 형태로 관리할 수 있어 H/W의 Scale-out를 구현할 수 있다.  
시스템을 확장 시에 용량과 성능을 동시에 향상 시킬 수 있다.
- SMP -> 모든 CPU가 동일한 메모리, 디스크, I/O 공유
- MPP -> 각기 다른 CPU, 디스크, I/O를 사용

<br/>

### 3. Flash Disk
과거에는 디스크가 느려서 Random I/O의 병목이 발생했다. Exa는 스토리지 서버 내에 Flash Cache라는 Flash Disk 기반 캐시가 존재한다. 속도가 향상됐다.

테이블과 인덱스가 Flash Cache에 저장되어 있다면 Disk I/O 없이 Cache 내 값을 사용한다. X3 부터는 Write-back 옵션이 추가되었는데 이는 DML을 Cache 할 수 있는 것이다.

- Smart Caching : Flash에 Cache 하는 것
- Smart Flash Cache : Flash에서 직접 조회

<br/>

### 4. Offloading
예전 시대에 서버는 DB 서버 + 스토리지 서버를 의미했다. 스토리지는 단지 데이터의 저장 역할을 담당할 뿐이었다. 그리고 DB의 성능은 I/O에 좌우되었다.

현재는? Exa의 스토리지(서버)는 자신의 CPU와 메모리를 가지고 SQL 처리를 수행할 수 있게 되었다.

Offloading은 기존 DB에서 처리한 것을 스토리지 레이어로 offload하여 처리한다는 개념이다. 말이 좀 어려운데 다시 말하자면 DB 서버와 스토리지 서버 간 방대한 데이터를 이동하는데 소모되는 비용을 줄이는데 목표가 있다.

대표적인 예가, `WHERE` 절에 만족하는 row를 필터링(Predicate Filtering)하고, 필요한 컬럼만 추출(Column Projection)하는 것이다.

이 Offloading 기법을 통해 최소한의 결과만 DB 서버로 넘어간다. 따라서 전송량이 줄어든다.

이를 구현하기 위한 기능들은 Smart Scan, Simple Join 등을 포함하여 여러가지가 있다.

<br/>

## Exadata 주요기능
Exadata는 표준 Oracle Architecture가 가지고 있는 한계점을 극복하기 위해 Storage 서버에 다음의 기능들을 추가하였다.

<br/>

### 1. Smart Scan
Smart Scan은 Storage 서버에서 DB 서버로 전송하는 데이터 양을 최소화하기 위해 필요한 블록만 액세스하고, 조건을 만족하는 로우 중 필요한 컬럼만 선별하여 DB 서버로 전송하는 처리 방식을 말한다.

<br/>

### 2. Storage Index
Storage Index는 Smart Scan을 지원하는 용도로 사용된다. 테이블을 Storage Region으로 나누고, 각 Region 별로 컬럼의 최대/최소값을 저장한다. `WHERE` 절 조건을 판단하여 컬럼이 Storage Unit의 최소, 최대 범위에 속하지 않는다면 해당 블록은 액세스하지 않는다.

<br/>

### 3. Flash Cache
Ranodm I/O 성능 향상을 위해 Storage 서버에 내장된 Disk Cache이다. Random I/O 시 Disk에서 블록을 탐색하기 전에 Flash Cache에 해당 블록이 존재한다면 Flash Cache에서 해당 블록을 탐색한다.

<br/>

### 4. HCC(Hybrid Columnar Compression)
스토리지 비용 절감과 Disk I/O를 줄이기 위해 Compression Unit 내에서 컬럼 별로 데이터를 재구성하여 정렬한 후 압축하는 기법으로 약 10× 정도로 데이터를 압축할 수 있다.

<br/>

## Smart Scan
Smart Scan은 위에서 말한 Predicate Filtering, Column Projection, 그리고 Storage Index에 의해 구현된다고 할 수 있다.
- Predicate Filtering
  - `WHERE` 절이 있어야 함
  - 필요한 레코드만 반환하는 Exa의 기능
- Column Projection
  - 필요한 컬럼만 반환 -> DB 서버와 스토리지 서버 사이 데이터량을 최소화한다.
  - `V$SQL` 뷰 내에는 다음과 같은 컬럼을 가지고 있다.
    - `IO_CELL_OFFLOAD_ELIGIBLE_BYTES` : 절감 예상 데이터량 정의
    - `IO_INTERCONNECT_BYTES` : 스토리지 서버에서 실제 반환한 데이터량
- Storage Index
  - `WHERE` 절이 있어야 함
  - Storage Index의 목적은 DB 서버로 전송될 데이터량을 줄이는 것이 아니라, 스토리지 서버 자체에서 데이터를 읽는 시간을 줄이기 위함이다.
  - 기존 인덱스 : 읽어야 할 블록을 찾는다.
  - Storage Index : 읽지 않아도 될 블록을 제거한다.

1. DB 서버는 Cell 서버로 I/O를 요청한다.
2. Cell 서버의 Storage Index를 사용 가능하면 불필요한 블록을 Skip하고 필요한 블록들만 필터링하여 액세스한다.
3. 액세스한 블록에서 `WHERE` 절에 만족하는 행만 필터링한다.
4. 조건을 만족한 행에서 `SELECT` 절이나 `JOIN` 조건에 해당하는 컬럼만 추출한다.
5. 최종적으로 필요한 최소한의 데이터들만 DB 서버로 전송한다.

<br/>

## Reference
- https://ko.wikipedia.org/wiki/%EC%98%A4%EB%9D%BC%ED%81%B4_%EC%97%91%EC%82%AC%EB%8D%B0%EC%9D%B4%ED%84%B0
- https://sarc.io/index.php/oracledatabase/562-about-oracle-exadata-1
- https://m.blog.naver.com/acornedu/220957947103
- https://sarc.io/index.php/oracledatabase/571-about-oracle-exadata-2
- https://blog.b2en.com/tag/Oracle%20Exadata