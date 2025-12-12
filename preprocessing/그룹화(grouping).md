# 인덱스로 그룹화 (+멀티인덱싱)
```python
df.set_index(['m1','m2']) #m1과 m2를 함께 인덱스로 설정
```

# Groupby()
데이터프레임의 <u>같은 값을 하나로 묶어서</u> 통게나 집계 결과를 확인
- 데이터프레임.groupby(그룹 컬럼)[계산 컬럼].집계함수()
  
### 예시
- "월별 수당의 중심 경향"을 계산할 때
  - 그룹 컬럼: 월
  - 계산 컬럼: 수당
  - 집계함수: mean, median

- 멀티인덱싱한 경우 groupy에서 <u>특정 인덱스만 관찰하는 level</u>을 적용할 수 있음. 
 
```python
df.set_index(['m1', 'm2']).groupby(level=[0]).mean() #첫번째 인덱스만 관찰
df.set_index(['m1', 'm2']).groupby(level=[0,1]).mean() #1,2번째 인덱스 관찰
```

# Aggregate()
데이터프레임의 <u>값을 다양하게 집계</u>하여 한 번에 보기 

```python
df.set_index(['m1', 'm2']).groupby(level=[0]).aggregate([np.mean, np.max])
# mean과 max를 한번에 보기 
```

# pivot(), pivot_table()
행 데이터를 열 데이로 회전시키기 
- pivot()은 중복값이 존재할 경우 에러
```python
df.pivot(index='m1', columns='m2', values='m3')
# 위와 아래는 동일하다
df('m1', 'm2', 'm3')

df.pivot_table(index='m1', columns='m2', values='m3', aggfunc=np.mean) #aggfunc은 mean이 default
df.pivot_table(index='m1', columns='m2', values='m3', aggfunc=np.sum)
```

# stack(), unstack()
칼럼 레벨에서 인덱스 레벨로 데이터프레임 변경(unstack은 이와 반대)
- unstack을 되돌릴 땐 다시 stack 해주기 
```python
df2 = df.set_index(['m1', 'm2'])
df2.unstack(0) #m1이 인덱스 레벨에서 컬럼 레벨이 되어 컬럼이 됨.
```


