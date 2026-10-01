# 📘 SQL_BASIC 5주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 날짜/시간 데이터와 조건문을 학습합니다. 특히 `CASE WHEN`은 SQL 문제 풀이와 데이터 분석에서 자주 사용되므로, 직접 분류 기준을 만들고 결과를 확인하는 연습을 해주세요.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_5th_TIL

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기

### 4-6. 조건문(CASE WHEN, IF)

---

## ✨ 선택 강의

- 4-5. 시간 데이터 연습문제: 날짜/시간 함수를 더 연습하고 싶을 때 선택 수강
- 4-7. 조건문 연습문제: CASE WHEN과 IF를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | ✅ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | ✅ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- DATE
- DATETIME
- TIMESTAMP
- EXTRACT
- DATETIME_TRUNC
- FORMAT_DATETIME
- CASE WHEN
- IF

## 01.

```
개념 이름: EXTRACT
개념 설명:
날짜나 시간 데이터에서 연도, 월, 일, 시간 같이 특정 시간 단위의 숫자 값만 추출하는 함수를 의미한다. 영단어 원 뜻과 동일한 의미를 갖고 있어서 직관적인데 특정 계절에도 적용되고 집계를 위해 자주 사용할 것이라 생각한다.

예시 쿼리: 책 관련이라 생각해보면,
  SELECT 
      EXTRACT(MONTH FROM START_DATE) AS 대여_월,
      COUNT(HISTORY_ID) AS 대여_건수
  FROM
      CAR_RENTAL_COMPANY_RENTAL_HISTORY
  GROUP BY
      EXTRACT(MONTH FROM START_DATE)
  ORDER BY
      대여_월
이 정도로 생각해 볼 수 있다.
```

## 02.

```
개념 이름: IF
개념 설명:
IF문은 공통적으로 프로그래밍 언어에서 정말 많이 쓰이는데 기능은 동일하다. 조건식이나 참 혹은 거짓일 때의 반환값이라는 인자를 받아서 처리하는 조건 함수이고, 다중 조건을 설정하려면 CASE WHEN이 더 적합하다. 빠르게 단일 분류만 설정할 때는 그냥 IF문을 써서 짧게 쿼리문의 가독성을 높이는 것이 더 좋다고 생각한다.

예시 쿼리:
  SELECT 
      RENTAL_ID,
      IF(OVERDUE_DAYS > 0, '연체 도서', '정상 반납') AS 반납_구분
  FROM
      BOOK_RENTAL_HISTORY
```

## (선택) 03.

```
개념 이름: DATETIME_TRUNC
개념 설명:
날짜나 시간 데이터를 지정한 시간 단위의 시작 시점으로 절삭해서 표준화 해주는 함수라고 볼 수 있다. 타임스탬프 데이터가 다 다르게 나와있으면 월 혹은 일 단위의 동일한 기준 시점으로 맞춰줘야 하기 때문에 많이 쓰인다. 실제로 토프를 진행하면서도 데이터 내 타임스탬프 형태가 다 다르게 표기되어 있어서 팀원들이 전처리 과정에서 동일 형식으로 지정해줬던 기억이 난다.

헷갈린 점:
사실 특정 단위의 값만 숫자로 뽑아내는 EXTRACT와의 차이에 있어서 좀 생각해보기도 했다. EXTRACT(MONTH FROM ...)처럼 쓰면 단순 정수값만 반환하기 때문에 2025년 10월과 2026년 10월처럼 연도가 다른 데이터들이 하나로 뭉쳐서 처리될 위험이 있다. 이럴때 DATETIME_TRUNC(..., MONTH)를 쓰면 연도 정보까지도 정리해서 해당 월의 첫날로 묶어주기 때문에 연도별 추이를 왜곡 없이 분석할 수 있다. 이렇게 각 쿼리문에서의 용도 차이를 구분하는 것이 중요하다고 생각한다.
```

---

# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
- 문제 풀이 정답 화면 캡처
- SQL 실행 결과 화면 캡처

---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

풀이 과정:

SELECT 
    HISTORY_ID,
    CAR_ID,
    DATE_FORMAT(START_DATE, '%Y-%m-%d') AS START_DATE,
    DATE_FORMAT(END_DATE, '%Y-%m-%d') AS END_DATE,
    CASE 
        WHEN DATEDIFF(END_DATE, START_DATE) + 1 >= 30 THEN '장기 대여'
        ELSE '단기 대여'
    END AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE LIKE '2022-09%'
ORDER BY HISTORY_ID DESC

```
- 장기/단기 대여를 나눈 기준:
 대여 시작일(START_DATE)부터 대여 종료일(END_DATE)까지의 총 대여 기간이 30일 이상인지 여부를 확인해야 하기 때문에 대여 당일도 이용 일수 1일로 포함되어 두 날짜의 단순 차이에 1을 더한 실제 대여 일수가 30 이상이면 '장기 대여', 그렇지 않으면 '단기 대여'로 분류했다.

- 사용한 날짜 계산 방식:
 두 날짜 사이의 일수 차이를 계산하는 DATEDIFF(종료일, 시작일) 함수를 사용했다. 주의사항에 날짜 포맷(YYYY-MM-DD)을 정확히 맞추기 위해서DATE_FORMAT(날짜, '%Y-%m-%d') 함수를 적용하여 출력했다.

- CASE WHEN으로 만든 컬럼:
 조건에 따라 '장기 대여' 또는 '단기 대여'라는 텍스트 값을 부여하는 RENT_TYPE 컬럼을 만들었다. CASE WHEN 조건을 통해 계산된 대여 일수가 30일 이상이면 '장기 대여'를 반환하도록 설정하고, ELSE를 통해 나머지 조건에서는 '단기 대여'로 지정되도록 하고 END AS RENT_TYPE으로 컬럼명을 부여했다.
```

<img width="2570" height="1478" alt="image" src="https://github.com/user-attachments/assets/9af5953e-0ad5-49e0-b686-b47aa50b2e61" />

## 🧩 문제 2

문제 링크: [한 해에 잡은 물고기 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298516)

풀이 과정:
SELECT 
    COUNT(ID) AS FISH_COUNT
FROM 
    FISH_INFO
WHERE 
    YEAR(TIME) = 2021

```
- 문제에서 요구한 연도: 물고기를 잡은 날짜를 기준으로 한 2021년

- 사용한 날짜 조건: YEAR(TIME) = 2021 조건을 사용하였고, DATE 컬럼인 TIME에서 연도 부분만 추출하는 YEAR() 함수를 활용해서 2021년에 해당하는 데이터만 필터링하도록 지정하였다.

- 집계한 대상: 2021년에 잡힌 물고기의 개수를 집계하기 위해서 ID 컬럼을 집계 대상으로 설정하여 COUNT(ID)를 실행했다. LENGTH 컬럼 10cm 이하 물고기는 NULL 값을 가지기 때문에 COUNT(LENGTH)를 사용하면 결측치가 제외되어 왜곡이 발생할 수 있다는 점에서 NULL 값이 없는 ID 컬럼으로 지정하는 것이 맞다고 판단했다.
```
<img width="2454" height="1402" alt="image" src="https://github.com/user-attachments/assets/6cee8561-13c3-4d3b-a08b-691e81a32d16" />
<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. -->

## 🧩 문제 3

문제 링크: [조건에 부합하는 중고거래 상태 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164672)

풀이 과정:
SELECT 
    BOARD_ID,
    WRITER_ID,
    TITLE,
    PRICE,
    CASE 
        WHEN STATUS = 'SALE' THEN '판매중'
        WHEN STATUS = 'RESERVED' THEN '예약중'
        WHEN STATUS = 'DONE' THEN '거래완료'
    END AS STATUS
FROM 
    USED_GOODS_BOARD
WHERE 
    CREATED_DATE = '2022-10-05'
ORDER BY 
    BOARD_ID DESC

```
- 날짜 조건: CREATED_DATE가 2022년 10월 5일인 데이터만 필터링하는 조건이기에 WHERE CREATED_DATE = '2022-10-05' 쿼리문을 작성하여 해당 일자에 등록된 게시물만 추출하도록 설정했다.

- CASE WHEN으로 바꾼 값:
 STATUS값을 한글 명칭으로 변환하는 과정을 CASE WHEN으로 수행했고, SALE이면 판매중으로, RESERVED면 예약중, DONE이면 거래완료로 상태별 매핑 조건을 직접 지정해서 변환해야 한다.

- ELSE에 해당하는 경우:
 문제에서 제시된 세 가지 상태 외의 값이 들어오거나 NULL 값 같은 게 들어오는 경우를 ELSE라고 볼 수 있다. 문제에서 제시하는 조건을 모두 작성해서 혹시 모를 오류 가능성을 없도록 만드는 것이 좋다고 판단했다.

- 정렬 기준: BOARD_ID 컬럼을 기준으로 한 내림차순 정렬이고, 문제의 요구에 따라 ORDER BY BOARD_ID DESC로 작성해서 게시글 번호 큰 순서대로 출력했다.
```
<img width="2302" height="1364" alt="image" src="https://github.com/user-attachments/assets/189f6891-3be3-4ec0-b58d-d9fec39a9e3f" />



## 🧩 문제 4

문제 링크: [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342)

풀이 과정:
SELECT 
    CAR_ID,
    ROUND(AVG(DATEDIFF(END_DATE, START_DATE) + 1), 1) AS AVERAGE_DURATION
FROM 
    CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY 
    CAR_ID
HAVING AVG(DATEDIFF(END_DATE, START_DATE) + 1) >= 7
ORDER BY 
    AVERAGE_DURATION DESC, CAR_ID DESC

```
- GROUP BY 기준: 문제에서 자동차 ID와 평균 대여 기간을 구하게 요구했으므로 자동차별로 묶어서 집계를 수행하기 위해 CAR_ID를 기준으로 설정했다.

- 평균을 계산한 방식:
 이 부분을 설정할 때 가장 어렵다고 느꼈는데, 대여 당일을 포함한 실제 대여 기간은 (DATEDIFF(END_DATE, START_DATE) + 1)로 구하고, 평균 함수인 AVG()를 적용했는데, 이때 소수점 두 번째 자리에서 반올림하기 위해 ROUND(..., 1) 함수를 조합했다. 표기는 소수점 첫째 자리까지라서 ROUND 함수 내 두 번째 인자가 1로 적혀 있음을 설명할 수 있다.

- HAVING에 사용한 조건:
 HAVING AVG(DATEDIFF(END_DATE, START_DATE) + 1) >= 7 조건을 사용해서 평균 대여 기간이 7일 이상인 그룹만 골라내도록 했다. SELECT에서 이미 명시했기 때문에 HAVING AVERAGE_DURATION >= 7라고 적어도 상관없었다.

- 처음 헷갈렸던 점: 앞에서 풀어봤던 문제에서도 활용했었지만 대여 기간 계산할 때 그냥 DATEDIFF(END_DATE, START_DATE)으로 적용하게 되면 대여 시작 당일이 누락되는 문제가 생기기 때문에 이를 잘 생각하고 주의해야 한다.
```

<img width="2724" height="1464" alt="image" src="https://github.com/user-attachments/assets/3cf10f58-f4d9-4c17-8e60-b094b7c887ed" />


---

# 4️⃣ 이번 주 회고

```
1. 날짜 함수 중 가장 헷갈린 함수:
두 날짜 사이의 일수를 구하는 DATEDIFF와 특정 날짜를 필터링할 때 시, 분, 초를 처리하는 방식이 가장 헷갈렸던 것 같다. 지속해서 언급하고 있지만 DATEDIFF는 단순 일수 차이만 반환하기 때문에 당일 대여처럼 시작일과 종료일이 같아도 1일로 계산해야 하는 상황에서는 + 1 보정을 해주어야 한다. 또, 날짜 컬럼에 시간 정보가 포함되어 있으면 단순히 = '2022-10-05'로 비교하면 누락이 발생할 수 있기 때문에 오류 방지를 위해서는 DATE_FORMAT(CREATED_DATE, '%Y-%m-%d') = '2022-10-05'처럼 일자 단위로 맞추거나 CREATED_DATE LIKE '2022-10-05%' 형태로 적용해 해결할 수 있었다. 따라서 데이터 형태를 파악하는 것도 중요하다는 생각을 했다.

2. CASE WHEN을 사용할 때 기억해야 할 문법: 조건이 위에서부터 순서대로 평가되기 때문에 범위가 좁거나 우선순위가 높은 조건을 먼저 배치해야 한다. 또 ELSE 절을 생략하면 어떤 WHEN 조건에도 맞지 않는 데이터가 자동 NULL 값 처리되므로 기본값이나 예외 처리를 정확하게 명시해서 작성하는 것이 결측치 방지에 중요하다.

3. 날짜/시간 데이터나 조건문을 활용해보고 싶은 분석 상황:
 주로 날짜나 시간 데이터는 구매 이력이 있거나 고객 정보가 들어있는 이커머스나 서비스 플랫폼에 많이 나타난다고 생각한다. 그래서 고객의 첫 구매일과 재구매일 사이 간격인 리텐션 주기를 도출해볼 수도 있을 것 같고, 회원가입 후 특정 기간 이내 구매 여부에 따라 신규 고객을 활성 혹은 이탈 고객으로 분류하여 마케팅적 요소로 활용해 볼 수도 있을 것 같다. 결제 시간을 기준으로 하면 심야, 오전, 오후 등 시간대별 범주를 CASE WHEN으로 나눠서 시간대별 매출 추이 비교 분석도 가능할 것 같다.
```

수고하셨습니다!




