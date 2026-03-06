### 데이터 모델링 유의사항

중복성 최소화   
유연성 높임: 데이터의 정의를 프로세스와 분리   
일관성 유지

### 데이터 모델링의 단계

1. 개념 데이터 모델링   
   핵심 엔터티와의 관계를 추출

2. 논리 데이터 모델링   
   개념 모델을 기반으로 데이터 구조를 구체적으로 설계   
   속성 정의, 식별자 정의, 관계 제약조건 정의, **정규화수행**

3. 물리 데이터 모델   
   논리 데이터 모델을 기반으로 **실제 DB에 구현하기 위한 설계 단계**   
   성능고려, 실제테이블생성, 인덱스 설계

### 데이터베이스 스키마 구조

1. 외부 스키마   
   사용자 또는 응용 프로그램이 DB를 바라보는 관점입니다.   
   즉 사용자별로 필요한 데이터만 보여주는 뷰(View) 입니다.   
   사용자 관점(User View), 여러 개 존재 가능, 필요한 데이터만 제공, VIEW 형태로 구현   
   -> 같은 데이터지만 사용자마다 다른 형태로 보임

2. 개념 스키마     
   DB 전체의 논리적 구조를 정의한 것   
   조직 전체가 공유하는 통합된 데이터 구조   
   단 하나만 존재, DB의 전체 논리 구조 정의, 엔터티, 관계, 제약조건 정의, **ERD가 이 단계에 해당**

3. 내부 스키마   
   데이터가 실제로 어떻게 저장되는지 정의   
   물리적 저장 구조, 저장 방식 정의, 인덱스, 블록 구조, 접근 경로

### 데이터 독립성

스키마 3구조를 만든 이유가 데이터 독립성 때문입니다.   
논리적 독립성: 외부 스키마 ← 개념 스키마 변화: VIEW는 그대로 유지 - 프로그램 수정 최소화   
물리적 독립성: 개념 스키마 ← 내부 스키마 변화: 테이블 구조는 동일 - 응용프로그램 영향 없음

### 엔터티 vs 인스턴스 vs 속성

엔터티:   
업무에서 데이터로 저장해야하는 대상, 관리해야하는 대상   
-> 업무에서 관리가 필요한 정보의 집합(테이블)   
인스턴스가 2개 이상 존재해야 함, 속성을 가짐, 다른 엔터티와 관계를 가짐

인스턴스:   
엔터티에 실제로 저장된 하나의 데이터   
-> 테이블에서 하나의 행

속성:   
엔터티가 가지는 톡징 또는 성질   
-> 테이블에서 칼럼   
업무에서 관리해야 할 엔터티의 구체적인 정보 항목   
엔터티의 최소 데이터 단위

### 엔터티 분류

1. 성격 기준

1) 유형 엔터티
   물리적으로 존재하는 대상(고객)
2) 개념 엔터티
   물리적으로 존재하지 않는 개념적 정보(부서)
   관리의 목적
3) 사건 엔터티
   업무에서 발생한 사건이나 행위

2. 발생시점 기준

1) 기본 엔터티
   업무에서 독립적으로 생성되는 엔터티
   타 엔터티에 의존 안함.
2) 중심 엔터티
   기본 엔터티로부터 생성(업무의 핵심 데이터)
   예시: 주문, 계약
3) 행위 엔터티
   업무 활동으로 발생하는 엔터티
   이벤트 기록, 중심엔터티에 의존적
   예시: 주문기록, payment

### 속성 4가지

| 속성 종류 | 설명              |
|-------|-----------------|
| 기본 속성 | 업무에서 원래 존재하는 속성 |
| 설계 속성 | 시스템 설계 중 추가된 속성 |
| 파생 속성 | 다른 속성에서 계산되는 속성 |
| 복합 속성 | 여러 속성으로 구성      |

설계속성: 상품코드, 고객번호

### 정규형

1. 제1정규형   
   속성의 값이 원자값이어야함.   
   -> 하나의 칼럼에 여러 값들어가면 안됨.   

2. 제2정규형   
   부분 함수종속 제거   
   -> 복합키 일부에만 종속되는 경우   
   예시: 학생ID | 과목ID | 학생이름   
   학생- 학생이름, 학생id-과목id

3. 제3정규형   
   이행적 함수 종속 제거   
   A-B-C

### SQL 문장들

데이터 조작어(DML): Select, Insert, Update, Delete -> SIUDelete   
데이터 정의어(DDL): Create, Alter, Drop, Rename, Truncate -> CARDrop   
데이터 제어어(DCL): Grant, Revoke   
트랜잭션 제어어(TCL): Commit, Rollback

### Null Function

| Function            | DB         | Meaning                     |
|---------------------|------------|-----------------------------|
| `NVL(x,y)`          | Oracle     | If x is NULL → return y     |
| `ISNULL(x,y)`       | SQL Server | If x is NULL → return y     |
| `IFNULL(x,y)`       | MySQL      | If x is NULL → return y     |
| `COALESCE(x,y,...)` | All DBs    | Return first NON-NULL value |

| Function      | Meaning                               |
|---------------|---------------------------------------|
| `NULLIF(x,y)` | If x = y → return NULL, else return x |

### ORACLE Commit

DDL 문장 수행하면, 실행이전, 이후에 자동으로 커밋함.   
DDL은 AUTO COMMIT FALSE해도 자동 커밋함   
DML은 AUTO COMMIT FALSE하면 커밋 안함.

### SAVEPOINT

```ORACLE
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

```SQLSERVER
SAVE TRANSACTION sp1;
ROLLBACK TRANSACTION sp1;
```

### 순수 관계 연산자

새로운 관계를 생성하는 연산

| 관계대수 연산자            | 의미        | SQL 대응                     |
|---------------------|------------|-----------------------------|
| SELECT          | 조건을 만족하는 행 선택    | WHERE    |
| PROJECT       | 특정 열 선택 | SELECT    |
| JOIN      | 두 관계 결합     | JOIN    |
| DIVIDE | 모든 조건을 만족하는 튜플 찾기   | NOT EXISTS / GROUP BY |


### TOP, WITH TIES, ORDER BY (SQL Server)

TOP can be used alone, but results may be unpredictable.   
WITH TIES must be used with ORDER BY.

---

---

---

---

---

---

---

---

---

---

---

---

---

---------------------

----
시험범위 아님

### SQL 실행계획 분석 명령어

|                      | 실제 실행 | 결과 출력 | 실행계획 | 통계 |
|----------------------|-------|-------|------|----|
| ON                   | ⭕     | ⭕     | ⭕    | ⭕  |
| ON EXPLAIN           | ⭕     | ⭕     | ⭕    | ❌  |
| ON STATISTICS        | ⭕     | ⭕     | ❌    | ⭕  |
| ON TRACEONLY         | ⭕     | ❌     | ⭕    | ⭕  |
| ON TRACEONLY EXPLAIN | ❌     | ❌     | ⭕    | ❌  |

### SQL Trace 파일을 TKPROF 유틸리티로 포멧

- SQL걸린시간 report
- 디스크로부터 읽은 블록수 report
- Parse, Execute, Fetch 각 단계의 수행 횟수 report
  ※ commit과 rollback은 안함.

### SQL Server SHOWPLAN vs TRACE

SHOWPLAN이란?
SQL을 실제로 실행하지 않고,
예상 실행계획(Estimated Execution Plan) 만 출력하는 모드

TRACE란?
SQL이 실제로 실행될 때 발생하는 이벤트를 추적하는 기능
실행 중 발생하는 내부 정보를 기록

### 인덱스 스캔 방식

| 인덱스 스캔 방식                       | 언제 사용되는가                   | 특징                      | 결과 범위 |
|---------------------------------|----------------------------|-------------------------|-------|
| **Index Unique Scan**           | PK 또는 Unique Index 조건      | 정확히 1건을 찾음              | 1건    |
| **Index Range Scan**            | 일반 조건 (=, >, <, BETWEEN 등) | 범위 검색                   | 여러 건  |
| **Index Full Scan**             | 인덱스 전체를 순서대로 읽음            | Single Block IO         | 전체    |
| **Index Fast Full Scan**        | 인덱스 전체를 빠르게 읽음             | Multi Block IO, 정렬 보장 X | 전체    |
| **Index Skip Scan**             | 복합 인덱스에서 선두 컬럼 없이 조회       | 선두 컬럼 값을 건너뛰며 탐색        | 여러 건  |
| **Index Range Scan Descending** | ORDER BY DESC와 인덱스 활용      | 역순 스캔                   | 여러 건  |

1️⃣ Index Unique Scan
PK / Unique 조건
결과 1건
가장 빠름
2️⃣ Index Range Scan
일반 인덱스 검색
범위 조건
가장 많이 사용
3️⃣ Index Full Scan
인덱스 전체 탐색
정렬된 상태 유지
Single Block IO
4️⃣ Index Fast Full Scan
인덱스 전체 탐색
Multi Block IO
정렬 보장 안됨
5️⃣ Index Skip Scan
복합 인덱스
선두 컬럼 없이 검색
6️⃣ Index Range Scan Descending
ORDER BY DESC
인덱스 역순 스캔

### 인덱스 종류

1. 클러스터드 인덱스
   테이블 데이터 자체가 인덱스 순서대로 정렬된 구조

2. 비트맵 인덱스
   데이터 존재 여부를 비트(0,1) 로 표현하는 인덱스.
   카디널리티(값의 종류 수) 낮은 컬럼에 좋음, DW 환경에 좋음

3. 리버스 키 인덱스
   인덱스 값을 거꾸로 저장하는 인덱스
   Range Scan 불가, Insert Hot Block 해결

### 옵티마이저 종류

① RBO (Rule Based Optimizer)
규칙 기반
통계정보 사용 안 함
현재 거의 사용 안 함

② CBO (Cost Based Optimizer) ⭐️⭐️⭐️
비용 기반
통계정보 사용
현재 표준
시험에서는 거의 CBO 기준으로 출제됨.

#### CBO가 판단하는 요소

선택도
카디널리티
비용
통계정보

### 인덱스 칼럼 선정 기준

1️⃣ WHERE 절에서 자주 사용되는 컬럼
2️⃣ JOIN에 사용되는 컬럼
3️⃣ 선택도가 높은 컬럼

### JOIN 알고리즘

| 구분     | NL Join            | Sort Merge Join | Hash Join     |
|--------|--------------------|-----------------|---------------|
| 기본 방식  | 반복 탐색              | 정렬 후 병합         | 해시 비교         |
| 구조     | Outer → Inner 반복   | 두 테이블 정렬 후 병합   | 작은 테이블 해시 생성  |
| 인덱스 필요 | Inner Table 인덱스 필요 | 없어도 가능          | 필요 없음         |
| 데이터 규모 | 작은 데이터             | 중간 규모           | 대용량           |
| IO 특성  | Random IO 많음       | Sequential IO   | Sequential IO |
| 특징     | 가장 기본적인 Join       | 범위 조인 가능        | 대용량에서 빠름      |

| Join 알고리즘           | Equi Join 필요 여부 |
|---------------------|-----------------|
| **NL Join**         | 필요 없음           |
| **Sort Merge Join** | 필요 없음           |
| **Hash Join**       | **필요함**         |

### 인스턴스 메모리

Instance Memory
├─ SGA (Shared Global Area)  ← 공유 메모리
└─ PGA (Program Global Area) ← 프로세스 전용 메모리

### SGA (Shared Global Area)

1️⃣ Buffer Cache
디스크의 데이터 블록을 메모리에 캐싱하는 공간

2️⃣ Library Cache
SQL 실행 계획과 SQL 문을 저장하는 공간

3️⃣ Shared Pool
SQL 실행 관련 정보를 저장하는 공유 메모리

### PGA (Program Global Area)

1️⃣ Sort Area
정렬 작업

2️⃣ Hash Area
해시 조인

3️⃣ Session Memory
세션 상태 정보

※ TEMP Tablespace
PGA 메모리가 부족할 때 사용하는 디스크 공간

### Dynamic SQL

구분방법: EXECUTE IMMEDIATE, sql := select ~~

### 옵티마이저 모드

1. ALL_ROWS
   전체 결과를 가장 빠르게 처리하도록 최적화
   전체 처리 속도 (Throughput) 최적화 - OLAP, Hash, full

2. FIRST_ROWS
   처음 몇 개의 결과를 빠르게 반환하도록 최적화
   Response Time 최적화 - OLTP, Index, NL

### 뷰 MERGING

뷰 내부 쿼리를 외부 쿼리와 합쳐 하나의 쿼리로 변환하는 옵티마이저 최적화

- View Merging을 방지하는 방법
  연산순서가 바뀌면 안되는 경우들을 넣어둔다.
  /*+ NO_MERGE(v) */ 힌트 사용
  GROUP BY + 집계조건
  DISTINCT
  ROWNUM
  윈도우함수(연산순서 바뀌면 안됨)
  CONNECT BY
  SET 연산(UNION, INTERSECT, MINUS)