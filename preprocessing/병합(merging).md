# concat()
데이터의 속성이 동일한 데이터프레임을 합칠 때 사용
- 파라미터
  - ignore_index = boolean : false인 경우 df 합쳐질 때 기존 인덱스 유지  -> 인덱스 중복 발생 가능
  - axis : 행별병합, 칼럼 병합
  - join = outer(합집합)/inner(교집합)
  - verify_integrity = boolean : True인 경우 인덱스 중복시 에러 메시지 출력 
```python
pd.concat([df1, df2], ignore_index=False)

pd.concat([df1, df2], join='outer')
```

# merge()
서로 다른 형태와 값의 데이터프레임을 병합할 때 사용
- 파라미터
  - on : 어떤 컬럼 기준으로 병합할지 컬럼 작성
  - how = inner/left/right/outer :
    - 일치값 존재할 경우만 가져오기/왼쪽 기준으로 오른쪽 df 를 병합(없으면 nan)/오른쪽 기준으로 왼쪽 df 를 병합(없으면 nan)/left와 right합한 df 병합
   
```python
pd.merge(df1, df2, on='m1', how='inner')
```
