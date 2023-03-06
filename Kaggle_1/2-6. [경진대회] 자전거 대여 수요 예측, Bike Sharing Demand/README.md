# Part II. 머신러닝 문제해결








# Chapter 6. [경진대회] 자전거 대여 수요 예측 
### Bike Sharing Demand
### Forecast use of a city bikeshare system
![img](./img/2-6-1.png)
- [Kaggle Link](https://www.kaggle.com/competitions/bike-sharing-demand)



## 0. 경진대회 이해

- 워싱턴 D.C의 자전거 무인 대여 시스템 과거 기록을 기반으로 향후 자전거 대여 수요를 예측하는 대회

### 주어진 데이터
- 2011년부터 2012년까지 2년간의 자전거 대여 데이터 
- 캐피털 바이크셰어 회사가 공개한 운행 기록에 다양한 외부 소스에서 얻은 당시 날씨 정보를 조합하여 만들었음.

- 데이터는 한 시간 간격으로 기록되어 있음
- 훈련 데이터: 1일 ~ 19일까지의 기록
- 테스트 데이터: 20일 ~ 월말까지의 기록

- 피처
    - 대여 날짜
    - 시간
    - 요일
    - 계절
    - 날씨
    - 실제 온도
    - 체감 온도
    - 습도
    - 풍속
    - 회원 여부

- 이 데이터를 활용해 시간별 자전거 대여 수량을 예측 $\Rightarrow$ 회귀 문제

    






> - **피처 (feature)**: 원하는 값을 예측하기 위해 활용한은 데이터
> - **타깃 값 (Target Value)**: 예측해야 할 값




### Evaluation

- 평가지표와 제출 형식
- Submissions are evaluated one the **Root Mean Squared Logarithmic Error (RMSLE)**. The RMSLE is calculated as
$$\sqrt{\dfrac{1}{N} \sum^n_{i=1} ( \log(p_i + 1) - \log(a_i + 1))^2}$$

- **Submission Format**
    - Your submission file must have a header and should be structured in the following format:
    ```
    datetime,count
    2011-01-20 00:00:00,0
    2011-01-20 01:00:00,0
    2011-01-20 02:00:00,0
    ...
    ...
    ```
    - 제출 형식은 일시(datetime)와 데여 수량(count)으로 구성되어 있음.
    