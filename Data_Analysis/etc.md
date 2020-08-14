### Shingle size
Shingle size란 전처리 방법으로, 이상 탐지 알고리즘에서 shingling은 연속성을 지닌 데이터에서 길이 s만큼이 시퀀스를 s-차원의 벡터로 변환함으로써 1차원 데이터를 s-차원 데이터로 바꾸는 기술이다. 
shingle size가 너무 작을 경우, Random cut Forest알고리즘이 데이터의 작은 변화에도 심하게 영향을 받을 수 있다. 반면 사이즈가 너무 크면, 작은 크기의 이상치를 탐지하지 못할 수 있다. ref. [[ML] 'Robust Random Cut Forest for anomaly detection' 설명 및 library (Online Anomaly Detection)
](https://hororolol.tistory.com/m/238?category=806087)
