# 정렬과 연산

ORDER BY 구를 사용하여 검색결과의 행 순서를 바꿀 수 있다. (정렬)

- 언제나 정해진 순서로 결괏값을 얻기 위해서는 ORDER BY 구를 지정해야 한다.

## ORDER BY로 행 정렬

```sql
SELECT 열명 FROM 테이블명 WHERE 조건식 ORDER BY 열명
SELECT 열명 FROM 테이블명 ORDER BY 열명
```

### DESC를 통한 내림차순 정렬

기본 정렬은 오름차순으로 가능하다. 내림차순으로 정렬 하기 위해서는 다음과 같이 지정해야 한다.

```sql
SELECT 열명 FROM 테이블명 ORDER BY 열명 DESC
```

- DESC(descendant) / 하강 / 내림차순
- ASC(ascendant) / 상승 / 오름차순

### 대소관계

ORDER BY로 정렬할 때는 값의 대소관계가 중요하다. 수치형 데이터와 날짜시간형 데이터는 숫자크기가 판별이 비교적 쉽지만 문제는 문자열형 데이터이다.

- 알파벳이나 한글 자모음 배열순서를 사용하면 문자를 차례대로 나열할 수 있다.
- 알파벳, 한글 순이며 한글은 자음, 모음 순이다.

__문자열형 데이터의 대소관계는 사전식 순서에 의해 결정된다결정된다. 따라서 수치형과 문자열형 데이터는 대소관계의 계산 방법이 다르니 주의를 요한다.__

### 복수 열로 정렬 지정

```sql
SELECT 열명 FROM 테이블명 WHERE 조건식
ORDER BY 열명1 [ASC|DESC], 열명2 [ASC|DESC]...
```

열명1의 기준으로 먼저 정렬하고 값이 같을 때는 열명2 기준으로 정렬한다.

## LIMIT로 결과 행 수 제한

```sql
SELECT 열명 FROM 테이블명 LIMIT 행수 [OFFSET 시작행]
SELECT 열명 FROM 테이블명 WHERE 조건식 ORDER BY 열명 LIMIT 행수
```

LIMIT 구는 표준 SQL은 아니다. MySQL과 PosterSQL에서 사용할 수 있는 문법이다. LIMIT 구는 SELECT 명령의 마지막에 지정하는 것으로 WHERE 구나 ORDER BY 구 뒤에 지정한다.

Oralce은 대신 ROWNUM이라는 열을 사용해 WHERE 구로 조건을 지정하여 행을 제한할 수 있다.

```sql
SELECT * FROM sample33 WHERE ROWNUM <= 3
```

ROWNUM은 클라이언트에게 결과가 반환될 때 각 행에 할당되는 행 번호이다 단 ROWNUM으로 행을 제한할 때는 WHERE 구로 지정하므로 정렬하기 전에 처리되어 LIMIT로 행을 제한한 경우와 결괏값이 다르다. 이 문제는 서브쿼리로 해결 가능하다.

## 오프셋 지정

페이지네이션에 주로 사용된다.

```sql
SELECT 열명 FROM 테이블명 LIMIT 행수 OFFSET 위치
```

## 함수와 연산자

```sql
함수명 (인수1, 인수2... )
```

함수명에 따라 연산 방법이 결정된다. 함수도 연산자도 표기 방법이 다를 뿐, 같은 것이다.

이름에 ASCII 문자 이외의 것을 포함할 경우는 더블쿼트로 둘러싸서 지정한다. (MySQL에서는 백쿼트)

- 더블쿼트로 둘러싸면 명령구먼을 분석할 때 데이터베이스 객체의 이름이라고 간주한다.
- 싱클쿼트로 둘러싸는 것은 문자열 상수이다.

### 별명 사용하기

 `WHERE구 -> SELEC구 -> ORDER BY 구`

## 수치, 문자열, 날짜 연산

### 수치 연산

## CASE 문들
