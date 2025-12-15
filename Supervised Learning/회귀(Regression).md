# 회귀
1. 선형회귀
    - From sklearn.linear_model import LinearRegression
        - 하이퍼파라미터
            - fit_intercept : 절편값의 계산 여부 지정
        - 학습 후 갖는 속성
            - coef_ : 학습된 모델 특성의 가중치 추정값
            - intercept_ : 학습된 모델의 절편 추정값
    - 예외적인 데이터에 민감하게 반응하거나 범위 벗어난 데이터에 추정함
  

## 사용 예시 
```python 
from sklearn.linear_model import LinearRegression
reg = LinearRegression()
reg.fit(x_train, y_train)
print('기울기', reg.coef_)
print('절편', reg.intercept_)
```
