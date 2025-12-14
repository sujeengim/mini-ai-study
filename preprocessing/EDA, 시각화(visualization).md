# EDA와 시각화 
1. 지표로 탐색
2. 시각화로 탐색
   
*데이터의 특성을 완전히 이해하기 위해서는 다양한 관점에서 데이터를 탐색하는 것 외에 데이터에 대한 도메인 지식을 갖춰야 함

## 1. 지표로 탐색
### <일변량>
- 요약통계량 확인
  - df.describe() : 수치형 데이터 요약 통계량 확인
      - Count, mean, std, min, 사분위, max -> 문자/범주형은 nan으로 표시
  - df.describe(include=‘all’) : 문자/범주형 데이터 포함한 요약 통계량 확인 
      - Unique, top, freq -> 수치형은 nan으로 표시
- 빈도표 확인
  - df[‘m1’].value_counts()

### <다변량>
- 상관계수 확인
  - df.corr() : 수치형 상관관계 확인
- 교차표 확인
  - pd.crosstab(df[‘m1’], df[‘m2’]) : 두 범주형 데이터의 상관관계 확인

## 2. 시각화로 탐색
### <일변량>
- 선
    - plt.plot(df[‘m1’])
- 막대
    - plt.bar(df.index, df[‘m1’])
- 파이
    - Plt.pie(df, labels=df.index, autopct=‘%.1f%%’)
- 히스토그램
    - plt.hist(df[‘m1’], bins=10) : m1을 구간을 10개 구간으로 나눠서 그리기 
- 상자
    - Plt.boxplot(list(df[‘m1’]))
    - Df.boxplot(by=‘m1’, column=‘m2’, figsize=())
    - -> x축을 m1으로, y축을 m2로 

### <다변량>
- 산점도
    - 수치형
        - Plt.scatter(x=df[‘m1’], y=df[‘m2’])
    - 범주형
        - Sns.catplot(y=‘m1’, x=‘m2’, col=‘m3’, data=df)
        - ->m1별 m2를 m3로 구분하여 시각화 
- 히트맵 
    - Heat = df.corr()
    - plt.pcolor(heat)
    - plt.xticks(np.arange(0.5, len(heat.columns), 1), heat.columns)
    - plt.yticks(np.arange(0.5, len(heat.index), 1), heat.index)
    - plt.colorbar()
- 선형회귀모델 
    - 산점도와 회귀선 함께 그리기
    - sns.lmplot(x=‘m1’, y=‘x2’, data=df, scatter_kws={‘color’:’blue’}, line_kws={‘color’:’red’})
- 빈도
    - Sns.countplot(x=‘m1’, hue=‘m2’, data=df)
    - -> 데이터의 빈도를 m1으로 구분하여 m2별로 시각화
- 조인트
    - 산점도와 히스토그램 함께 그리기 
    - Kind 파라미터로 산점도가 아닌 hex, reg, kde도 가능
    - sns.jointplot(x=‘m2’, y=‘m1’, data=df)
- 히트맵
    - sns.heatmap(df.corr())

## 시각화 사용법
```python
import matplotlib.pyplot as plt
plt.figure() : 시각화 영역 설정
plt.plot() : 그래프 그리기 plot()을 다른 그래프로 변경하여
plt.xlabel(‘x축’)
plt.ylabel(‘y축’)
plt.show() : 시각화그래프 보이기 
```
## 예시
```python
label = df.index
plt.figure()
plt.bar(label, df[‘m1’])
plt.xlabel(‘index’)
plt.ylabel(‘m1’)
plt.show()
```
