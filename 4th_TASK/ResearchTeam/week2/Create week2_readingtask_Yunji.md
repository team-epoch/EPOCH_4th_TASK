**📘 Title**

> ℹ️ APA. 인용 방식 권고
> 
- MAIN: Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks.
- SUB: In F. Pereira, C. J. C. Burges, L. Bottou, & K. Q. Weinberger (Eds.), Advances in Neural Information Processing Systems (Vol. 25, pp. 1097–1105). Curran Associates, Inc.

---

**📖 Abstract**

> ℹ️ 본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.
> 

ImageNet의 방대한 규모의 데이터셋을 분류하는 데 있어서 본 모델이 좋은 성과를 냈다. Top-1 error(모델이 예측한 가장 높은 확률의 label이 실제 정답과 다른 경우의 비율)가 37.5%, Top-5 error(모델이 예측한 상위 5개 label 중 정답이 없을 확률)가 17.0%로, 기존 모델보다 나은 성능을 보인다. 

CNN만의 구조적인 특징과 더불어 빠른 학습을 위해 GPU와 비포화 함수를 사용하고, 과적합 방지를 위해 Dropout이라는 효과적인 정규화 기술을 도입한 것이 비결이었다고 볼 수 있다.

---

**📚 Background**

> ℹ️ 논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리
> 
>
**📍 Related Work 1: stationarity & locality**

- stationarity of statistics: 이미지 내의 특징이 어디에서 나타나든 그 통계적 성질은 같다는 가정. 특정 feature가 이미지의 어느 위치에서든 나타날 수 있고, 그렇기 때문에 그 위치에 상관 없이 동일한 feature라면 같은 의미를 가짐
    - 예를 들어, 고양이의 그림을 검지한다고 쳤을 때 고양이의 눈이 왼쪽 위에 있든 오른쪽 아래에 있든, ‘눈’이라는 특징 자체는 위치에 관계 없이 동일하게 유효함
        
        ⇒ 그렇기 때문에 하나의 필터로 전체 이미지를 슬라이딩하면서 특징을 추출해도 문제 없음
        
 - locality: 이미지에서 가까이 있는 픽셀들끼리는 서로 더 밀접한 관계를 가진다는 뜻
     - 예를 들어, 고양이 그림에서 눈의 모양은 눈을 이루는 몇 개의 인접한 픽셀로 구성됨. 반면 눈과 꼬리처럼 서로 멀리 떨어진 부분은 직접적인 관련이 없음. 이런 식으로 좁은 구역에서 인접한 픽셀들끼리는 관련성이 더 있는 셈!
 - CNN에서 적용되는 방식
     - stationarity: 같은 필터(가중치, 크기)를 이미지 전체에 공유함 → 어느 구역이든 큰 차이 X
     - locality: 작은 크기의 필터(좁은 구역)로 지역적인 특징을 추출함
 
> **📍 Related Work 2: conv layer와 모델의 깊이의 연관성**
> 
> <aside>
> 
> conv layer 하나라도 줄이면 안되기 때문에 depth가 중요함을 깨달았다 .. 라고 나왔는데 왜 conv layer과 depth과 관련있는지 문득 궁금해서 알아본 결과입니다!
> 
> </aside>
 
 - CNN의 depth = convolutional layer의 개수를 주로 의미하고 해당 layer는 이미지로부터 특징을 추출하는 역할을 함. layer가 깊어질수록 특징도 점점 복잡해짐
     - 예를 들어, 초반은 edge, texture 등의 저수준 특징을 잡아낸다면 중간은 shapes나 patterns, 후반에는 object parts나 semantic 정보 등을 캐치해냄
     - 즉 depth는 모델의 표현력과 밀접한 연관성이 있는 셈
 - 당시에는 GPU 성능 한계로 인해 깊은 CNN을 실제로 학습하는 사례가 거의 없었음. 그렇기에 AlexNet은 depth가 실제 성능에 얼마나 중요한지 실험적으로 입증한 유의미한 사례가 됨
     - 이후 ResNet 등의 더 깊은 모델이 나오게 되는 계기가 되었으며, ‘depth matters’라는 개념을 딥러닝 분야에 정착시키는 데 기여함

---

**🔍 Methods**

 ✅ 사용된 연구 방법
> 
> 
 **✅ 실험 설계**
 
- ImageNet 데이터셋을 이용해 대규모 이미지 분류 문제를 해결하는 CNN 설계
 - 5개의 conv layer + 3개의 fully connected layer로 구성된 깊은 네트워크 사용
 - 성능 향상과 학습 속도 개선을 위해 ReLU, Dropout, Data augmentation, Local Response Normalization, GPU 최적화 기법 등을 적용
 
 **📍 모델 비교**
 
- 구조 변경 시도: conv layer를 줄이면 성능 하락 → depth(깊이)의 중요성 입증!
- Dropout, LRN 등의 적용 여부에 따라 성능 차이 확인

---

**🔍 Experiments**

✅ 데이터셋
 
 - ImageNet ILSVRC-2010/2012 (train: 약 120만 장, val: 5만 장, test: 15만 장)
 - 1000 클래스 x 1000개의 이미지
 - 입력 이미지 크기는 256×256으로 통일 후 중앙 crop함
 - 픽셀 단위 평균값을 빼는 정규화만 수행하였음 (그 외 전처리는 따로 진행하지 않음)
 
 **✅ Model Architecture**
 
 - 총 8개 layer (5 Conv + 3 FC) 구조 + 1000개 클래스에 대한 softmax 출력
 - ReLU 활성화 함수 → 빠른 수렴, gradient 소실 문제 완화
 - Dropout, Data augmentation → 과적합 방지
 - LRN(Local Response Normalization) → 일반화 향상
 - GPU 2개 병렬 처리 + 2D convolution 연산 최적화 구현

**✅ Evaluation Metrics**
 
 - Top-1 error: 37.5%
 - Top-5 error: 17.0%
 - 당시 기준으로 기존 모델 대비 큰 성능 우위 입증
 
 **✅ Implementation Details**
 
 - 2개의 GTX 580 (3GB) GPU로 5~6일 학습
 - GPU를 활용한 2D convolution 연산 직접 최적화

---

**📖 Conclusion**

 **✅ Limitation**
 
 - 기술의 발전을 통해 CNN을 양껏 테스트할 기회가 왔음에도 불구하고 당시의 GPU 메모리 제한과 긴 학습 시간(5~6일)이라는 제약이 있었음
     
     → 더 깊은 모델이나 더 큰 배치 처리는 당시 하드웨어로는 어려웠음. 만일 더 나은 환경이었다면 더 좋은 학습 결과가 있었을 듯.
     
 
 **✅ Contribution**
 
 - 대규모 이미지 데이터셋을 다룰 수 있는 깊은 CNN 구조 제시
 - Dropout, ReLU, GPU 최적화 등 여러 기법을 실제 시스템에 성공적으로 통합
 - 이후 딥러닝 발전의 기초 구조와 방향성 제시

---

**🤔 Question**

> ℹ️ 본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.
> 
**📍 이 논문이 등장하게 된 이유 + 이 논문이 관련 Task에 기여한 내용**

- 아이디어적인 기술이 발전함에 따라 HW가 따라오는 속도에 차이가 있다는 것을 해당 논문을 읽으면서 문득 생각하게 되었다. 아이디어적인 측면에서만 기술이 앞서가는 것이 아니라 이를 실험하고 입증할 수 있는 하드웨어도 뒷받침되어야 한다는 게 새삼 느껴졌고, 더 나은 GPU나 환경이 있으면 더 나은 결과를 이끌어낼 수 있음을 많은 연구자들에게 영향을 끼치지 않았을까 ..!

 **📍 배울 수 있었던 내용과 추가로 궁금한 점**

- 왜 다른 정규화 기법들은 놔두고 Local Response Normalization 기법을 사용했었을지 의문. 사실 이번 논문을 읽어보면서 처음 접하게 된 개념이라, 최근에는 왜 그렇게까지 널리 사용되지 않을지 ..
