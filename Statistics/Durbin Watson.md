# Today I Learned - 2022/09/28 Wed

# 더빈 왓슨(Durbin Watson) 검정
- 회귀분석의 가정 중 **오차항이 독립성을 만족하는지를 검정**하기 위해 사용한다.
- **더빈 왓슨 통계량이 2에 가까울수록 오차항의 자기상관이 없음(독립)** 을 의미한다.
- 더빈 왓슨 통게량이 0에 가까울수록 양의 상관관계가 있고, 4에 가까울수록 음의 상관관계가 있음을 의미한다.
- 따라서 0 또는 4에 가까울수록 잔차들 간의 상관관계가 있어서 회귀식이 부적합함을 의미한다.
- 주로 시계열분석에서 자주 사용된다.
