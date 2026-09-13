# 📘 SQL_BASIC 2주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 저장된 데이터를 확인하는 방법과 `SELECT`, `FROM`, `WHERE`의 기본 구조를 학습합니다.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_2nd_TIL

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-2. 저장된 데이터 확인하기(데이터베이스, 데이터 웨어하우스, ERD)

### 2-3. 데이터 탐색(SELECT, FROM, WHERE)

---

## ✨ 선택 강의

- 2-4. SELECT 연습 문제: SELECT, FROM, WHERE를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | 🍽️ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | 🍽️ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | 🍽️ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- SELECT
- FROM
- WHERE
- 조건식
- ORDER BY
- LIMIT
- 테이블 구조 확인

## 01.

```
개념 이름: SELECT
개념 설명: 테이블에서 조회하고자 하는 특정 컬럼(열)을 지정하는 핵심 절이다.
          문자 (*)은 모든 컬럼을 조회할 때 사용하며, 필요한 컬럼만 쉼표(,)로 구분해 나열함으로써
          불필요한 데이터 조회를 줄이고 원하는 데이터만 추출할 수 있다.
예시 쿼리: SELECT
            ANIMAL_ID, NAME, DATETIME
          FROM
            ANIMAL_INS
```

## 02.

```
개념 이름: WHERE와 조건식
개념 설명: 테이블의 전체 데이터 중에서 특정 조건을 만족하는 행(Row)만 필터링하여 가져오기 위해 사용하는 절을 말한다.
          (=,>,<)와 같은 비교 연산자와 (AND, OR, NOT) 같은 논리연산자를 활용해 요건에 맞는 타겟 레코드만 선별 추출할 때 사용한다.
예시 쿼리: SELECT
            NAME, INTAKE_CONDITION
          FROM
            ANIMAL_INS
          WHERE
            INTAKE_CONDITION = 'Sick'
```

## (선택) 03.

```
개념 이름: ORDER BY
개념 설명: 조회된 결과 데이터의 출력 순서를 특정 컬럼을 기준으로 오름차순 또는 내림차순으로 정렬하는 절을 의미한다.
          쿼리 문의 가장 마지막에 실행되며, 단일 컬럼뿐만 아니라 여러 컬럼을 기준으로 우선순위를 두어 다중 정렬할 수 있다는 특징이 있다.
예시 쿼리: SELECT
            ANIMAL_ID, NAME, DATETIME
          FROM
            ANIMAL_INS
          ORDER BY
            DATETIME DESC
```

---

# 2️⃣ 수행 인증란

<img width="1160" height="1082" alt="image" src="https://github.com/user-attachments/assets/88af71b5-9e1b-41a0-8f1d-ba1ea6fe6fdb" />
<img width="2068" height="1046" alt="image" src="https://github.com/user-attachments/assets/8252c3cf-e6e9-49e1-a2f4-bc59f1aaceac" />

---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [모든 레코드 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/59034)

풀이 과정:

```
- 테이블에서 확인한 컬럼: ANIMAL_ID, ANIMAL_TYPE, DATETIME, INTAKE_CONDITION, NAME, SEX_UPON_INTAKE

- SELECT와 FROM을 작성한 방식
  : 모든 동물의 모든 정보를 조회해야 하므로 SELECT *로 전체 컬럼을 지정하고,
    문제에서 주어진 대상 테이블인 FROM ANIMAL_INS를 명시했다.
    추가로 동물 아이디 순으로 정렬하기 위해 ORDER BY ANIMAL_ID를 기본 오름차순으로 적용했다.

- 새로 배운 점
  : 전체 컬럼 조회를 위해 (*)를 사용할 수 있다는 점도 있었지만,
    ORDER BY에서 정렬 방식 지정을 생략하면 기본적으로 오름차순으로 정렬된다는 점을 새로 배울 수 있었다.

```
**<실제 작성한 코드>**

  
  <img width="580" height="542" alt="image" src="https://github.com/user-attachments/assets/1ecf2daa-ed71-4ac6-8347-c6bf2a9873a6" />

```
```
**<정답 인증>**

<img width="2804" height="1504" alt="image" src="https://github.com/user-attachments/assets/6df32d05-2cfd-48b6-9510-0d01600a76ab" />



## 🧩 문제 2

문제 링크: [아픈 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59036)

풀이 과정:

```
- 문제에서 요구한 조건: 상태(INTAKE_CONDITION)가 아픈 상태(Sick)인 동물의 아이디와 이름을 조회하고, 결과는 아이디 순으로 정렬하도록 요구했다.

- WHERE 절로 옮긴 방식
  : 문자열 조건인 'Sick'과 일치하는 행만 추출하기 위해 WHERE INTAKE_CONDITION = 'Sick'으로 코드를 작성하였다.

- 정렬 기준이 있다면 사용한 기준
  : ANIMAL_ID를 기준으로 오름차순 정렬하기 위해 ORDER BY ANIMAL_ID를 적용했다.
    위에서 배운대로 오름차순을 필요로 했기에 따로 정렬 방식을 지정할 필요가 없었다.

- 새로 배운 점
  : 문자열 값을 비교 조건으로 넣을 때는 반드시 ' '로 감싸주어야 한다는 점도 주의할 수 있었고,
    문제에서 요구한 특정 컬럼(ANIMAL_ID, NAME)만 SELECT절에 명확하게 나열하여 출력하는 방식을 확실히 익힐 수 있었다.
```
**<실제 작성한 코드>**


  <img width="838" height="672" alt="image" src="https://github.com/user-attachments/assets/5ecd130a-18e4-4313-ab69-325bef80b856" />

```
```

**<정답 인증>**
<img width="2558" height="1456" alt="image" src="https://github.com/user-attachments/assets/0b6d5b6c-26ed-45c6-a0b4-387368346ea1" />

---

# 4️⃣ 이번 주 회고

```
1. SELECT, FROM, WHERE 중 가장 헷갈린 개념:

  - 작성 순서와 실제 실행 순서의 차이

    : 쿼리를 작성할 때는 SELECT -> FROM -> WHERE 순서로 작성한다는 점을 반드시 기억하는 것이 중요했다.
      그러나 DB 내부에서는 테이블을 먼저 FROM으로 읽고 -> 조건을 필터링한 뒤(WHERE) -> 최종 컬럼을 조회(SELECT)하는 실행 순서를 거친다는 점이 초반에는 좀 헷갈렸다.

2. 문제를 풀 때 가장 자주 확인하게 된 부분

  - 별칭과 식별자 표기법

      : 컬럼에 별칭을 붙일 때 예를 들어 id AS를 할 때, 뒤에 컬럼 이름에 따옴표(' ')를 잘못 사용하면 문법 오류가 나거나 의도치 않게 동작할 수 있으므로, 따옴표 없이 쓰거나 띄어쓰기가 있는 경우 백틱(`) 또는 올바른 식별자 방식을 정확히 구분해야 한다는 점을 꼭 확인해야 한다고 생각했다.

3. 다음 주 문제 풀이에서 의식하고 싶은 습관:

    - 조건과 정렬의 명시적 작성

      : ORDER BY를 작성할 때 기본값이라도 정렬 방향(오름/내림차순)을 명확히 의식하고, 문제의 조건 요구사항을 WHERE 절에 누락 없이 체계적으로 구성하는 습관을 들이고자 한다. 이번주 풀었던 문제들은 기본적으로 연습하는 문제들이라 헷갈릴 요소들이 별로 없었지만, 이후에 조건들이 복잡해지면 기본적인 습관이나 확인할 부분이 중요하게 작용할 것이라고 생각한다.
```

수고하셨습니다!




