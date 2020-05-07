# SQL

(정답) (가) regexp_like
(해설) regexp_like () 함수를 이용하여 like 연산자의 확장된 표현을 할 수 있다 정규 표현식에서 제공하는
메타문자 형식을 regexp_like 함수와 함께 사용하면 보기처럼 간소화된 표현을 할 수 있다

(정답) ORDERED USE_NL(D) / LEADING(E) USE_NL(D) / USE_NL(E, D) / USE_NL(E D) (해설) ORDERED 힌트는 FROM 절에 작성한 순서대로 읽으라는 의미이고, LEADING(E)는 E 라는 ALIAS 테이블을 우선적(Driving table)으로 읽고 실행하라는 의미이다. 그리고, USE_NL 힌트를 통해 Nested loop 조인 대상을 지정하게 된다.

5. 다음 보기 중 INDEX 를 생성하는 CREATE 문으로 옳지 않은 것은
①CREATE INDEX TB_INDEX ON
제품 ( 제품코드
②CREATE INDEX TB_INDEX ON
제품 제품코드 생산일자
③CREATE UNIQUE INDEX TB_INDEX ON
제품 생 산일자
④CREATE NONUNIQUE
INDEX TB_INDEX ON 제품 제품코드
(정답) 4 (해설)
-- BITMAP INDEX : CREATE BITMAP INDEX index_name ON schema(column);
-- unique INDEX : CREATE UNIQUE INDEX index_name ON schema(column);
-- 결합 INDEX : CREATE INDEX index_name ON schema(column,2,3);
-- non unique INDEX : CREATE INDEX index_name ON schema(column);
4번의 BTREE는 옵션에 존재 하지 않으면 일반적으로 CREATE INDEX ~ 로 시작하는 구문이 BTREE INDEX를 생성하는 구문이 된다.

(정답) LEVEL (해설) 계층형 질의문의 Level은 문제의 설명처럼 계층 구조의 행 순위나 레벨을 명시적으로 표시할 수 있다. 이렇게 하면 보고서를 보다 쉽게 읽을 수 있게 된다. Level은 오라클에서 실행되는 모든 쿼리 내에서 사용 가능한 pseudocolumn 으로 트리 내에서 어떤 단계(Level)에 있는지를 나타내는 정수 값이다. Level은 계층형 쿼리에서만 값을 갖고 일반 쿼리에서는 0 값을 갖는다.

(정답) 제품번호, 고객번호 (해설) 결합인덱스의 선행 칼럼은 사용된 조건이 어떤 연산 처리를 하는지에 따라 결정된다. 일반적으로 점조건(=, IN)과 선분조건(like, between 등)일 경우 처리 범위를 줄일 수 있는 점 조건이 선행칼럼으로 적합하다. 따라서, 위 조건에서 제품번호 = :data1 과 고객번호 IN ('1011','2022') 가 해당된다
4.

[https://sqltest.net/](https://sqltest.net/)

\(해설\) 1\) WHERE 절에는 그룹함수 조건을 사용할 수 없고, HAVING절에 작성해야 한다.   
3\) USING절에 사용되는 양쪽 테이블의 공통 컬럼에는 접두어\(prefix\) = ALIAS 는 사용 할 수 없다.   
4\) LIKE 연산자에 사용되는 와일드카드 기능 기호는 %과 \_\(언더스코어\)만 가능하다.

\(정답\) between interval '1' year preceding and current row   
\(해설\) RANGE는 로우가 아닌 논리적인 범위로 WINDOW 절을 지정할 때 사용하고, between interval '1' year preceding은 각 로우의 입사일 기준으로1년 전에 속하는 입사일을 가진 로우가 시작 위치가 된다. 즉, ORDER BY절에서 사용한 입사일 컬럼 값에 대해 상수로 범위를 지정하는 역할을 한다. 위 결과에서 ‘SMITH’ 인 경우는 그 입사일 이전 1년의 값이 없으므로 자신의 값이 나왔고, ‘ALLEN’부터 누적이 시작된 것이다. ※

\(가\) /_+ index\_desc\(s sales\_cust\_idx\)_    
\(나\) rownum = 1   
SELECT /_+ index\_desc\(s sales\_cust\_idx\)_ / 판매량   
FROM 영업실적 s   
WHERE 제품ID = 712   
and 고객ID = 20180   
and rownum = 1;  
\(해설\) 보유한 인덱스를 역순으로 스캔하여\(INDEX\_DESC\) 마지막 한 건만\(ROWNUM=1\) 액세스하고 중단할 수 있는 방법을 제공한다.

[https://sqltest.net/](https://sqltest.net/)

