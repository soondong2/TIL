# Today I Learned - 2022/05/09 Mon

## 📌 조건문
### If문
```python
if 조건1:
	조건1이 True일 경우 실행할 내용
elif 조건2:
	조건2가 True일 경우 실행할 내용
else:
	모든 조건이 True가 아닐 경우 실행할 내용
```

### 비교 연산자
| 연산자 | 내용 |
| --- | --- |
| == | 같다 |
| ≠ | 같지 않다 |
| A > B | A가 B보다 크다 |
| A < B | A가 B보다 작다 |
| A ≥ B | A가 B보다 크거나 같다 |
| A ≤ B | A가 B보다 작거나 같다 |

### 논리 연산자
| 연산자 | 내용 |
| --- | --- |
| and | 그리고 |
| or | 또는 |
| not | 부정 |

```python
x in list : 리스트 안에 x가 있으면 True
x not in 문자열 : 문자열 안에 x가 없으면 True
```

### pass vs continue
|| pass | continue |
| --- | --- | --- |
| 사용 시기 | 빈 무언가를 만들고 error가 발생하지 않기를 바랄 때 | 특정 조건에서 continue 아래 코드를 생략하고 다음 순번으로 넘어가고 싶을 때 |
| 차이점 | 아무것도 실행되지 않음 | 코드에 영향을 미친다 (특정 조건 거르기) |

### 조건문 간소화
```python
if score >= 80: print("Success")
else: print("Fail")
```

```python
print("Success") if score >= 80 else print("Fale")
```
