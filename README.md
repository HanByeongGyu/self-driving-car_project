# self-driving-car_project
first_project




AlexNet 
2012년에 개최한 ILSVRC 대회의 우승을 차지했다. 활성화 함수로는 LeNet-5에서 사용되었던 Tanh 함수 대신에 ReLU 함수가 사용되었다. ReLU는 rectified linear unit의 약자이다. 같은 정확도를 유지하면서 Tanh을 사용하는 것보다 6배나 빠르다고 한다. AlexNet 이후에는 활성화함수로 ReLU 함수를 사용하는 것이 선호되고 있다.
dropout: 과적합(over-fitting)을 막기 위해서 규제 기술의 일종인 dropout을 사용했다. dropout이란 fully-connected layer의 뉴런 중 일부를 생략하면서 학습을 진행하는 것이다[5]. 몇몇 뉴런의 값을 0으로 바꿔버린다. 따라서 그 뉴런들은 forward pass와 back propagation에 아무런 영향을 미치지 않는다. dropout은 훈련시에 적용되는 것이고, 테스트시에는 모든 뉴런을 사용한다.
overlapping pooling: CNN에서 pooling의 역할은 컨볼루션을 통해 얻은 특성맵의 크기를 줄이기 위함이다. LeNet-5의 경우 평균 풀링(average pooling)이 사용된 반면, AlexNet에서는 최대 풀링(max pooling)이 사용되었다. 또한 LeNet-5의 경우 풀링 커널이 움직이는 보폭인 stride를 커널 사이즈보다 작게 하는 overlapping pooling을 적용했다. 따라서 정확히 말하면 LeNet-5는 non-overlapping 평균 풀링을 사용한 것이고, AlexNet은 overlapping 최대 풀링을 사용한 것이다.
local response normalization (LRN): 신경생물학에는 lateral inhibition이라고 불리는 개념이 있다. 활성화된 뉴런이 주변 이웃 뉴런들을 억누르는 현상을 의미한다. lateral inhibition 현상을 모델링한 것이 바로 local response normalization이다. 강하게 활성화된 뉴런의 주변 이웃들에 대해서 normalization을 실행한다. 주변에 비해 어떤 뉴런이 비교적 강하게 활성화되어 있다면, 그 뉴런의 반응은 더욱더 돋보이게 될 것이다. 반면 강하게 활성화된 뉴런 주변도 모두 강하게 활성화되어 있다면, local response normalization 이후에는 모두 값이 작아질 것이다.
data augmentation: 과적합을 막기 위해 dropout 말고도 또다른 방법이 사용되었다. 과적합을 막는 가장 좋은 방법 중 하나는 데이터의 양을 늘리는 것이다. 훈련시킬 때 적은 양의 데이터를 가지고 훈련시킬 경우 과적합될 가능성이 크기 때문이다. 따라서 AlexNet의 개발자들은 data augmentation이란 방법을 통해 데이터의 양을 늘렸다.



VGG16 
VGGNet은 옥스포드 대학의 연구팀 VGG에 의해 개발된 모델로써, 2014년 이미지넷 이미지 인식 대회에서 준우승을 한 모델이다. 여기서 말하는 VGGNet은 16개 또는 19개의 층으로 구성된 모델을 의미한다(VGG16, VGG19로 불림). 이전에 포스팅한 VGG-F, VGG-M, VGG-S와는 차이가 있다. 그 모델들은 8개의 층을 가진 AlexNet과 유사한 모델들이다. 하지만 AlexNet와 같이 병렬적 구조로 이뤄지진 않았다. 
VGG 연구팀은 깊이의 영향만을 최대한 확인하고자 컨볼루션 필터커널의 사이즈는 가장 작은 3 x 3으로 고정했다. 3 x 3 필터로 세 차례 컨볼루션을 하는 것이 7 x 7 필터로 한 번 컨볼루션하는 것보다 나은 점은 가중치 또는 파라미터의 갯수의 차이다. 3 x 3 필터가 3개면 총 27개의 가중치를 갖는다. 반면 7 x 7 필터는 49개의 가중치를 갖는다. CNN에서 가중치는 모두 훈련이 필요한 것들이므로, 가중치가 적다는 것은 그만큼 훈련시켜야할 것의 갯수가 작아진다. 따라서 학습의 속도가 빨라진다. 동시에 층의 갯수가 늘어나면서 특성에 비선형성을 더 증가시키기 때문에 특성이 점점 더 유용해진다.



ResNet18
ResNet은 마이크로소프트에서 개발한 알고리즘이다. 그것도 북경연구소의 중국인 연구진이 개발한 알고리즘이다. 기존의 신경망은 입력값 x를 타겟값 y로 매핑하는 함수 H(x)를 얻는 것이 목적이었다. 그러나 ResNet은 F(x) + x를 최소화하는 것을 목적으로 한다. x는 현시점에서 변할 수 없는 값이므로 F(x)를 0에 가깝게 만드는 것이 목적이 된다. F(x)가 0이 되면 출력과 입력이 모두 x로 같아지게 된다. F(x) = H(x) - x이므로 F(x)를 최소로 해준다는 것은 H(x) - x를 최소로 해주는 것과 동일한 의미를 지닌다. 여기서 H(x) - x를 잔차(residual)라고 한다. 즉, 잔차를 최소로 해주는 것이므로 ResNet이란 이름이 붙게 된다. ResNet은 기본적으로 VGG-19의 구조를 뼈대로 한다. 거기에 컨볼루션 층들을 추가해서 깊게 만든 후에, shortcut들을 추가하는 것이 사실상 전부다. 34층의 ResNet은 처음을 제외하고는 균일하게 3 x 3 사이즈의 컨볼루션 필터를 사용했다. 그리고 특성맵의 사이즈가 반으로 줄어들 때, 특성맵의 뎁스를 2배로 높였다.




GoogLeNet
GoogLeNet은 2014년 이미지넷 이미지 인식 대회(ILSVRC)에서 VGGNet(VGG19)을 이기고 우승을 차지한 알고리즘이다. 
먼저 주목해야할 것은 1 x 1 사이즈의 필터로 컨볼루션해주는 것이다. 구조도를 보면 곳곳에 1 x 1 컨볼루션 연산이 있음을 확인할 수 있다. 19층1 x 1 컨볼루션은 어떤 의미를 갖는 것일까? 왜 해주는 것일까? GoogLeNet에서 1 x 1 컨볼루션은 특성맵의 갯수를 줄이는 목적으로 사용된다. 특성맵의 갯수가 줄어들면 그만큼 연산량이 줄어든다.의 VGG19보다 좀 더 깊은 22층으로 구성되어 있다.
GoogLeNet은 총 9개의 인셉션 모듈을 포함하고 있다. GoogLeNet에 실제로 사용된 모듈은 1x1 컨볼루션이 포함된 (b) 모델이다. 아까 살펴봤듯이 1x1 컨볼루션은 특성맵의 장수를 줄여주는 역할을 한다. 노란색 블럭으로 표현된 1x1 컨볼루션을 제외한 나이브(naive) 버전을 살펴보면, 이전 층에서 생성된 특성맵을 1x1 컨볼루션, 3x3 컨볼루션, 5x5 컨볼루션, 3x3 최대풀링해준 결과 얻은 특성맵들을 모두 함께 쌓아준다. AlexNet, VGGNet 등의 이전 CNN 모델들은 한 층에서 동일한 사이즈의 필터커널을 이용해서 컨볼루션을 해줬던 것과 차이가 있다. 따라서 좀 더 다양한 종류의 특성이 도출된다. 여기에 1x1 컨볼루션이 포함되었으니 당연히 연산량은 많이 줄어들었을 것이다.
AlexNet, VGGNet 등에서는 fully connected (FC) 층들이 망의 후반부에 연결되어 있다. 그러나 GoogLeNet은 FC 방식 대신에 global average pooling이란 방식을 사용한다. global average pooling은 전 층에서 산출된 특성맵들을 각각 평균낸 것을 이어서 1차원 벡터를 만들어주는 것이다. 1차원 벡터를 만들어줘야 최종적으로 이미지 분류를 위한 softmax 층을 연결해줄 수 있기 때문이다. 만약 전 층에서 1024장의 7 x 7의 특성맵이 생성되었다면, 1024장의 7 x 7 특성맵 각각 평균내주어 얻은 1024개의 값을 하나의 벡터로 연결해주는 것이다. 이렇게 해줌으로 얻을 수 있는 장점은 가중치의 갯수를 상당히 많이 없애준다는 것이다. 만약 FC 방식을 사용한다면 훈련이 필요한 가중치의 갯수가 7 x 7 x 1024 x 1024 = 51.3M이지만 global average pooling을 사용하면 가중치가 단 한개도 필요하지 않다.
 네트워크의 깊이가 깊어지면 깊어질수록 vanishing gradient 문제를 피하기 어려워진다. 그러니까 가중치를 훈련하는 과정에 역전파(back propagation)를 주로 활용하는데, 역전파과정에서 가중치를 업데이트하는데 사용되는 gradient가 점점 작아져서 0이 되어버리는 것이다. 따라서 네트워크 내의 가중치들이 제대로 훈련되지 않는다. 이 문제를 극복하기 위해서 GoogLeNet에서는 네트워크 중간에 두 개의 보조 분류기(auxiliary classifier)를 달아주었다. 보조 분류기의 구성을 살펴보면, 5 x 5 평균 풀링(stride 3) -> 128개 1x1 필터커널로 컨볼루션 -> 1024 FC 층 -> 1000 FC 층 -> softmax 순이다. 이 보조 분류기들은 훈련시에만 활용되고 사용할 때는 제거해준다.


