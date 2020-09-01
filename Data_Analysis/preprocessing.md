# Data Preprocessing (데이터 전처리)

### Feature Selection
일종의 최적화 <br>
필요성: output을 예측하는데에 상관 없는 변수들이 존재하면 computational cost가 늘어나고, overfitting 초래. <br>
장점: 학습 시간 단축, 모델의 분산을 줄여서 보다 robust하게 학습 됨. 모델 간소화가 결과 해석에 더 유용하다. 
- 방법1. Wrapper method: 단순한 방법이다. feature의 조합을 정하고, 기계 학습을 돌리고, 성능을 평가한다. 이를 조합을 바꿔가면서 반복. -> 가장 성능 좋은 조합 찾기.
  - 단점: 너무 많은 시간 비용 필요함. 그리고 훈련 dataset에 overfitting 될 위험 있음.
- 방법2. Filter method: 전처리 과정에서 미리 Feature Selection을 통계적 방법으로 실행하고, 모델을 적합하는 방법. 가장 많이 쓰는 방법은 종속변수와 독립변수 간의 피어슨 상관계수를 이용하는 것이다.
![image](https://user-images.githubusercontent.com/30011635/91785759-15250b00-ec41-11ea-86ac-14b5eaa42592.png)
- 방법3. Embedded method: 모델 자체에 feature selection 기능이 추가 돼 있는 경우다. 예를 들어 Lasso Regression, Ridge Regression, Decision Tree등의 알고리즘은 모델 자체에서 feature selection이 수행 된다. <br>
<b>가장 많이 사용되는 feature selection method는 Filter method다.</b>
