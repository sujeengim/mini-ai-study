- 범주형 정제하기, 스케일링, 변수선택
# 범주형 정제하기 
1. 레이블 인코딩
2. 원핫인코딩

### 1. 레이블 인코딩
- pd.factorize(df[‘m1’])[0].reshape(-1,1)
    - factorize는 (인코딩된 정수 배열, 고유값 배열) 튜플을 반환함
- Sklearn 사용
    - From sklearn.preprocessing import LabelEncoder
    - Le = LabelEncoder()
    - df[‘new’] = le.fit_transform(df[‘m1’])
        - > reshape 필요없음
    - 디코딩 : le.inverse_transform(df[‘new’]).reshape(-1,1)

### 2. 원핫인코딩
- Pd.get_dummies(df[‘m1’])
    - > 인덱스마다 m1의 원핫인코딩 결과가 적용된 칼럼 반환
- pd.get_dummies(df, df[‘m1’])
    - > 원핫인코딩 결과를 데이터프레임에 반영
- Sklearn 사용
    - Oh = OneHotEncoder()
    - En = oh.fit_transform(df[‘m1’].values.reshape(-1,1).toarray() : 원핫인코딩 하기 
    - df_onehot = pd.DataFrame(en, columns=‘m1_’ + str(oh.categories_[0][I]) for i in range(len(oh.categories_[0]))]) : 데이터프레임으로 만들기 
    - new_df = pd.concat([df, df_onehot], axis=1) : 원본에 붙이기


# 스케일링
1. 정규화
2. 표준화

### 1.정규화
- Min Max scaling : 데이터 범위를 0~1로 변환
- Scikit-learn의 MinMaxScaler() 존재
- Df = (df - df.min())/(df.max()-df.min())

### 2.표준화
- StandardScaling : 평균 0, 표준편차 1인 표준 정규분포로 변환
- scikit-learn의 StandardScaler() 존재
- Df = (df - df.mean())/df.std()

<img width="586" height="232" alt="image" src="https://github.com/user-attachments/assets/6f72e0b7-7a20-4022-a8f9-3053f9fc3832" />


# 변수 선택
- 특성 선택이라고도 함
- 사용 가능한 변수 중 모델 훈련에 가장 효과적인 특성의 부분집합을 선택하여 학습 모델을 구축하는 것
- 문제 유형, 데이터, 학습 알고리즘에 따라 선택 방법 달라짐
- 목적
    - 학습에 사용하는 특징 수 줄이기
    - 모델의 예측 성능 유지
1. RFE
2. RFE-CV
3. UFS

### 1. RFE(Recursive Feature Elimination)
- 원하는 변수의 수에 도달할 때까지 가장 중요하지 않은 변수를 재귀적으로 제거
- 중요성 결정 방법
    - 의사결정 나무의 변수 중요도
    - 선형 모델의 계숫값
    - 신경망의 가중치 계수의 크기
    - 등등….
 
### 2. RFE-CV(Recursive Feature Elimination with Cross Validation)
- RFE에 교차 검증 추가한 것
- 변수 제거마다 교차 검증을 사용하여 모델 훈련하고 평가하여 더 정확한 평가

## 3. UFS(Univariate Feature Selection)
- 일변량 통계 테스트를 기반으로 최상의 변수를 선택하여 작동
- 특정 검정 통계(f-value, 카이제곱값 등)를 계산하여 각 변수를 평가하고, 가장 높은 점수를 가진 변수를 선택함
- 개별 변수만 평가하는 것이 간단하고 빠르다. 
- 변수간 관계를 고려하지 않아 항상 최상의 특성 세트를 식별하지 못할 수 있음
