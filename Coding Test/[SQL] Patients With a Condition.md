# Today I Learned - 2022/12/01 Thur

# Patients With a Condition
- 출처 : https://leetcode.com/problems/patients-with-a-condition/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT patient_id, patient_name, conditions
FROM Patients
WHERE conditions REGEXP '^DIAB10| DIAB1.*$'
```
정규 표현식을 사용하였다. `SDIAB100`인 경우는 출력되어선 안 되고, `ABC DIAB100`인 경우는 `DIAB10`를 인식할 수 있도록 하였다.
