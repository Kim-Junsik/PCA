# PCA(Principal Component Analysis)

* PCA는 데이터의 분산(variance)을 최대한 보존하면서 데이터의 분산(variance)을 최대한 보존하면서 서로 직교하는 새 기저(축)를 찾아, 고차원 공간의 표본들을 선형 연관성이 없는 저차원 공간으로 변환하는 기법이다.

<img width="300" alt="pca" src="https://user-images.githubusercontent.com/46274774/81775618-2201df80-9528-11ea-884d-41c99ab09187.png">

* 위 이미지에의 좌표는 각 데이터를 나타내며 (x<sub>1</sub>, y<sub>1</sub>)...(x<sub>i</sub>, y<sub>j</sub>) 까지의 데이터가 이루는 타원형 모형은 두 벡터로 데이터의 분포를 잘 나태낼 수 있다는 것이다.
* 즉 PCA는 데이터 하나 하나에 대한 성분을 분석하는 것이 아니라, 여러 데이터들이 모여 하나의 분포를 이룰 때 이 분포의 주 성분을 분석해 주는 방법이다.
* PCA는 2차원 데이터 집합에 대해 PCA를 수행하면 2개의 서로 수직인 주성분 벡터를 반환하고, 3차원 점들에 대해 PCA를 수행하면 3개의 서로 수직인 주성분 벡터들을 반환한다.
  
<img width="694" alt="다차원 pca" src="https://user-images.githubusercontent.com/46274774/81775802-773df100-9528-11ea-834a-c8b68c35df91.png">

### 분산의 보존
* 저차원의 초평면에 데이터를 투영하기 전에 먼저 적절한 초평면을 선택해야 한다. PCA는 데이터의 분산이 최대가 되는 축을 찾으며 원본 데이터셋과 투영된 데이터셋 간의 평균제곱거리를 최소화 하는 축을 찾는다.

<img width="595" alt="분산보존" src="https://user-images.githubusercontent.com/46274774/81775826-858c0d00-9528-11ea-9522-c92bf6897bcc.png">

* 위 그림에서 각 축으로의 투영중 C<sub>1</sub>으로의 투영이 분산이 잘 보존됨을 알 수 있다.

### 주성분(Principal Component)
* 주성분 분석은 데이터를 한개의 축으로 사상시켰을 때 그 분산이 가장 커지는 축을 첫 번째 주성분, 두 번째로 커지는 축을 두 번째 주성분으로 놓이도록 새로운 좌표계로 데이터를 선형 변환한다
* PCA에서는 주성분 분석을 응용한 방법으로 주성분은 그 방향으로 데이터들의 분산이 가장 큰 방향벡터를 의미한다. 또한 이후의 주성분들은 이전의 주성분들과 직교한다는 제약 아래에 가장 큰 분산을 갖고 있다는 식으로 정의되어있다. 중요한 성분들은 공분산 행렬의 고유 벡터이기 때문에 직교하게 된다.

### 계산
* PCA를 계산하는데는 평균을 0으로 놓고 시작한다. 다음 행렬 X는 각각의 열벡터 x<sub>i</sub>의 행렬이며 n은 samples, d는 features 이며 각 열의 평균이 0인 상태 (즉 feature의 평균을 뺀 상태)라고 가정한다.

![image](https://user-images.githubusercontent.com/46274774/82009857-68cc1280-96ab-11ea-88d0-5d83885b9d1a.png)
* 데이터 행렬 X를 이용해 공분산 행렬을 구한다. 여기서 공분산행렬은 각 feature의 변동이 얼마나 닮아있나를 확인하기위한 행렬이며, 닮은 정도(공분산 행렬)을 얻기 위해서는 내적이 필요하다.

![image](https://user-images.githubusercontent.com/46274774/82010371-db89bd80-96ac-11ea-92aa-1d83bc0b424e.png)


* 여기서 주대각선 성분(dot(x<sub>1</sub>, x<sub>1</sub>), dot(x<sub>2</sub>, x<sub>2</sub>), ... dot(x<sub>d</sub>, x<sub>d</sub>))같은 경우 1번 feature와 1번 feature의 변위가 닯은 정도를 나타내므로 이는 ***분산쳐럼*** 보인다.
* 주대각 성분을 제외한 나머지 성분 (dot(x<sub>i</sub>, x<sub>j</sub>) 단 i&ne;j)같은 경우 i번과 j번 feature의 닮은 정도를 나타냐며 이는 ***공분산쳐럼*** 보인다.
* 여기서 dot연산(내적)은 교환법칙이 성립하며 따라서 dot(x<sub>i</sub>, x<sub>j</sub>) = dot(x<sub>j</sub>, x<sub>i</sub>)이다.
* 따라서 X<sup>T</sup>X는 Symmetric Matrix이다.

* (X<sup>T</sup>X)<sub>ij</sub>는 i번째 feature와 j번째 feature의 변동이 닮은 정도를 나타내며, 여기서의 문제점은 데이터의 수에 의존한다는 것이다.
즉 데이터가 많아지면 그 값이 커지게 된다.
* 이를 해결하기위해 n으로 나누어 준다.

![image](https://user-images.githubusercontent.com/46274774/82011153-0b39c500-96af-11ea-8130-76e24a9bde64.png)

* 즉 convariance matrix의 i번째 행과 j번째 행은 i번 feature와 j번 feature가 서로 함께 변하는 정도를 의미한다.

![image](https://user-images.githubusercontent.com/46274774/82011371-ca8e7b80-96af-11ea-92ab-f61262b9b2a6.png)

* 다시 PCA로 넘어와서 PCA는 고차원의 데이터를 저차원으로 데이터의 구조는 보존하며 어떻게 차원을 축소하는가하는 방법이다. (예를 들어 2차원 평면상의 산점도를 어떻게 1차원 직선에 데이터의 구조를 보존하며 projection 시키는것이 좋은가하는 것이다.
* 이때 주축(principal axis)에 projection 시키는것이 가장 적절하며, 이때의 분산을 가장 큰 값을 가지게 된다. 즉 데이터의 분산(variance)가 클 수록 데이터의 구조를 잘 살려준다고 할 수 있다.
* 선형 변환에서의 주축을 eigenvector라고 하며 eigenvector를 찾는다는 것은 선형변환을 했을때 크기만 바뀌고 방향은 바뀌지 않는 벡터를 찾는다는 의미이다.

![Image 2020  5  15](https://user-images.githubusercontent.com/46274774/82011830-18f04a00-96b1-11ea-8adb-ae2fcda13ae0.png)

* 즉 projection후에 가장 큰 variance를 얻기 위해서는 eigenvector에 projection해야한다.
* N차원의 경우 N개의 eigenvector가 나오며 (Symmetric Matrix라서 이는 모두 직교한다.) K차원으로 감소시 eigenvector가 큰 K개의 eigenvector가 이루는 평면으로 데이터를 projection하여 K차원으로 감소된 데이터를 확보한다.

<핸즈온 머신러닝, 공돌이의 수학 정리 노트를 참고하여 작성>
