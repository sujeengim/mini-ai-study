# feature selection 
- 가지고 있는 데이터 중에서 예측할 값과 학습에 사용할 값을 분리해준다. 
- 예측할 변수가 총 몇개인지 파악한다. 
- 예측할 변수를 제외한 나머지 변수를 학습에 참여시킨다. 
- 학습에 사용하기에 train 데이터
```python
# 총 변수가 8개 였고, 만약 예측할 변수가 2개 라면 
# 예측할 변수1 분리    
val1 = train['val1']
# 예측할 변수2 분리    
val2 = train['val2']

# 학습에 사용할 독립변수 X 변수 할당    
features = ['학습변수1', '학습변수2', '학습변수3', '학습변수4',	'학습변수5',	'학습변수6']    
X = train[features]

```

# 모델 선언
- 각 예측 변수마다 모델을 만들어 주고, 각각 train 데이터로 학습시킨다. 
- 나중에 그렇게 학습되어 나온 결과만 합친다. 
- predict를 할 때 test 데이터의 features를 사용한다. 
```python
val1_model = DecisionTreeRegressor()
val2_model = DecisionTreeRegressor()

val1_model.fit(X, val1)
val2_model.fit(X, val2)

val1_predict = val1_model.predict(test[features])
val2_predict = val2_model.predict(test[features])
```
