# **Part III. 딥러닝 문제해결**








# **Chapter 11. [경진대회] 항공 사진 내 선인장 식별**
### **Aerial Cactus Identification**
### Determine whether an image contains a columnar cactus

![img](./img/2-6-1.png)

- [Kaggle Link](https://www.kaggle.com/c/aerial-cactus-identification)


</br>
</br>


# 0. 경진대회 이해 💁🏻‍♂️

- **Goal**: 항공 사진에서 선인장(cactus)을 찾아내는 것이 목표

- 앞의 경진대회들과 달리, 이번 경진대회에서는 `csv` 파일에 더해 '이미지 파일'도 제공.

</br>

## 0-1. 데이터 특징 📚


- 주어진 데이터는 다음과 같다:
    - `train.zip`: 훈련 이미지 데이터(`jpg` 형식) 압축 파일
    - `test.zip`: 테스트 이미지 데이터(`jpg` 형식) 압축 파일
    - `train.csv`: 훈련 이미지 데이터 파일명 및 타깃값 (타깃값은 0 또는 1)
    - `sample_submission.csv`: 샘플 제출 파일



</br>


- <u>우리는 테스트 이미지 데이터에 선인장이 있을 확률을 예측</u>해야 함.










</br>
</br>













# 1. 분석 정리 및 모델링 전략

## 1-1. 분석 정리

1. `csv` 파일의 `id` 피처는 이미지 파일명입니다. 파일의 경로명만 추가하면 파일의 위치를 바로 얻어올 수 있습니다.


2. 제공된 이미지 파일들은 낮은 해상도의 컬러 이미지($32 \times 32 \times 3$)입니다.






</br>



## 1-2. 모델링 전략


- 이번 장은 딥러닝 모델(CNN)을 다루는 방법에 집중합니다.
- 베이스라인에서 얕은 CNN을 기본적인 설정만으로 만들어보면서 전체적인 흐름을 익힌다.
- 성능 개선에서는 더 깊은 CNN에 몇가지 최적화 요소를 추가

</br>

- **베이스라인 모델**: 얕은 CNN
    - **신경망 구조**: 합성곱 x 2, 풀링, 평탄화, 전결합
    - **옵티마이저**: SGD
    

</br>

- **성능 개선**: 살짝 깊은 CNN
    - **데이터 증강**: 다양한 변환기 사용
    - **신경망 구조**: 합성곱 x 5, 배치 정규화, 풀링, 평탄화, 전결합 x 2
    - **옵티마이저**:Adamax
    - **기타**: 훈련 에폭 수 증가
    

</br>
</br>

# 2. 핵심 요약

1. 딥러닝 모델은 곳곳에서 난수를 활용하므로 매번 같은 결과를 얻으려면 **시드값**을 잘 **고정**해야 합니다.

2. **GPU를 활용**하면 딥러닝의 방대한 연산 시간을 크게 단축 가능

3. 파이토치에서는 **`Dataset` 클래스**를 상속하여 데이터셋을 준비

4. 파이토치의 **`DataLoader` 클래스**는 Dataset으로부터 배치 크기만큼씩 데이터를 불러와주는 역할

5. **이미지 변환기**는 원본 이미지를 특정한 형태로 변화시켜준다.

6. **데이터 증강**이란 원본 이미지에 다양한 변환을 가하여 데이터 수를 늘리는 기법
    - 훈련 데이터 수가 부족할 때 아주 유용

</br>


7. `Torchvision`의 `transforms` 모듈은 다양한 이미지 변환기를 제공

8. **CNN**은 합성곱 계층을 포함한 딥러닝 모델로, 이미지(영상) 인식 분야에서 많이 활용됨

9. **손실 함수**는 모델 훈련 과정에서 예측값과 실제값의 차이를 구하는 함수
    

10. **활성화 함수**는 신경망 계층에서 입력값을 어떤 값으로 변환해 출력할지 결정하는 함수
    - 여기서는 ReLU와 Leaky ReLU를 이용

</br>


11. **옵티마이저**는 최적 가중치를 찾아주는 함수
    - 확률적 경사 하강법(SGD)을 기반 이론으로 하여 다양하게 보완하여 사용

</br>

12. - **에폭**: '훈련 데이터 전체'를 '한 번' 훑었음
    - **배치 크기**: 매 훈련 이터레이션에서 한 번에 훈련할 데이터 개수
    - **반복 횟수**: 1 에폭의 훈련을 완료하는 데 필요한 훈련 이터레이션


</br>

13. **배치 정규화**: 계층 간 데이터 분포의 편차를 줄이는 작업
    - 신경망 계층마다 입력 데이터 분포가 다르면 훈련 속도가 느려지고 과대적합될 수 있음.