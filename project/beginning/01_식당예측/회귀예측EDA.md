# 시각화
## 데이터로 그래프 그리기 
```python
# 파이썬 warning 무시
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)

# 시각화를 위한 라이브러리
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm

# 한글 폰트 설정
fe = fm.FontEntry(fname='NotoSansKR-Regular.otf', name='NotoSansKR')
fm.fontManager.ttflist.insert(0, fe)
plt.rc('font', family='NotoSansKR')

# figure와 axes 생성
fig, ax = plt.subplots(dpi=150)

# 타이틀, x축, y축 라벨 설정
ax.set_title("제목")
ax.set_xlabel('x축 라벨')
ax.set_ylabel('y축 라벨')

# 데이터 플롯
ax.plot(df.index, df['컬럼명']) #x,y 설정

# 그래프 표시
plt.show()
```

## 조건 추가하여 그래프 그리기 
```python
# 데이터 준비
x = ['조건 A인 경우', '조건 B인 경우']
y = [df[df['조건 확인할 컬럼'] < 조건 기준]['나타낼 컬럼명'].mean(), 
     df[df['조건 확인할 컬럼'] >= 조건 기준]['나타낼 컬럼명'].mean()] # 원하는 조건대로 데이터프레임 설정해주기

# 그래프 생성
fig, ax = plt.subplots(dpi=150)
ax.set_title("타이틀")  # 타이틀 설정
ax.set_xlabel('x축')  # x축 라벨 설정
ax.set_ylabel('y축')  # y축 라벨 설정

# 막대 그래프 그리기
ax.bar(x, y)

# 그래프 표시
plt.show()
```

## 데이터 분포 확인
<img width="490" height="366" alt="image" src="https://github.com/user-attachments/assets/a8a00904-4026-4a98-bc83-d8a4776a9c3a" />

그냥 지그재그 처럼 보이지만! 이런 형태는 '반복적인 패턴'이 보인다고 할 수 있다. 
무엇을 기준으로 반복하고 있는지 (특정 구간이 있는지, 요일마다 반복되는지 등) 확인해보기. 
이를통해 종속변수의 패턴과 특성을 파악하고, 해당 구간에 맞는 모델을 선택하여 예측을 할 수 있다. 

## 그룹화하여 시각화
월 마다 추이가 궁금하다면
```python
# 1. 일자(2025-09-19)에서 월 컬럼 추가하기 
def month(text:str):
    return text[5:7] #이부분만 바꾼다면 월, 연도, 일자 별로 확인 가능하겠죠

df['월'] = df['일자'].map(month)

# 그래프 생성 및 설정
fig, ax = plt.subplots(figsize=(15, 5))

# 2. 월별로 평균내어 시각화
df.groupby('월').mean()['석식계'].plot(ax=ax)

plt.show()
```


# 이상치 제거 
## 불리언 인덱싱 
df[조건] 이 만족하는 행이나 열을 선택할 수 있다. 
```python
df2 = df[df['컬럼'] != 0]
```

## 특정 조건의 행열 선택 
loc[행 인덱스 조건, 열 인덱스 조건] 으로 추출해서 
값을 변경할 수 있다. 
```python
# 예시
df.loc[df['조건 확인할 컬럼'] == 'hello', '추출된 df에서 변경할 컬럼명'] = 변경할 값
```
