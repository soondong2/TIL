# Today I Learned - 2022/10/13 Thur

# 3월에 태어난 여성 회원 목록 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131120
<br>

## 문제
MEMBER_PROFILE 테이블에서 생일이 3월인 여성 회원의 ID, 이름, 성별, 생년월일을 조회하는 SQL문을 작성해주세요. 이때 전화번호가 NULL인 경우는 출력대상에서 제외시켜 주시고, 결과는 회원ID를 기준으로 오름차순 정렬해주세요

<br>

## 풀이
```sql
SELECT
    MEMBER_ID,
    MEMBER_NAME,
    GENDER,
    DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE MONTH(DATE_OF_BIRTH) IN (3)
    AND TLNO IS NOT NULL
    AND GENDER = 'W'
ORDER BY MEMBER_ID ASC;
```
<br>

- `DATE_FORMAT(column, format 형식)`을 통해 2022-10-13 00:00:00 형식을 2022-10-13 형식으로 바꿀 수 있다.
