# Week2 Reading Task


## **📘 Title**

> ℹ️ *APA. 인용 방식 권고*
> Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks. In F. Pereira, C. J. C. Burges, L. Bottou, & K. Q. Weinberger (Eds.), Advances in Neural Information Processing Systems (Vol. 25, pp. 1097–1105). Curran Associates, Inc.

---


## **📖 Abstract**

> ℹ️ *본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.*
> CNN을 대규모 이미지 dataset에 성공적으로 학습 시켰다. 빠른 학습을 위해 ReLU와 GPU를 병렬시켰으며, FC layer의 overfitting을 방지하기 위해 "dropout" 방법을 사용했다.
> 결과적으로 이전의 SOTA보다 훨씬 더 나은 성능을 달성했다.

---


## **📚 Background**

> ℹ️ *논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리*
> 
> 
> **📍 Related Work 1**
> 기존에는 activation function으로 sigmoid와 tanh를 주로 사용했으나, 이 함수들은 gradient vanishing 문제를 일으키는 saturating 함수였으며 학습이 느리다는 단점이 있었음
> --> **ReLU(Nair & Hinton (2010))**: non-saturating 함수, 빠른 학습이 가능
> 
> **📍 Related Work 2**
> **Dropout(Hinton et al. (2012))**: overfitting 방지, 랜덤하게 뉴런을 비활성화하여 모델의 일반화 성능 강화

---


## **🔍 Methods**

> **✅ 사용된 연구 방법**
> 1. 5 conv layers + 3 fc layers
> 2. ReLU 사용(모든 layer에)
> 3. 2개의 GPU 병렬 학습(GPU가 특정 layer에서만 서로 communicate) -> 대규모 학습 가능
> 4. Local Response Normalization: 같은 위치에서 다른 커널이 낸 activation을 경쟁시키며 generalization 개선(평균을 빼지 않고 인접 뉴런들의 크기에 따라 나눠서 정규화)
> 5. Overlapping Pooling(stride<kernel size): edge에 있는 중요한 정보도 보존하면서 feature간 경쟁을 유도해 중요한 정보만 남김 -> overfitting 억제
> 6. Dropout 정규화 적용
>
> 
> **✅ 실험 설계**
> 1. Dataset: ImageNet ILSVRC-2010
> 2. Data Augmentation: random crop(input size 224x224에 맞춰) + horizontal reflection + PCA on the set of RGB pixel
> 3. Details of learning setting: SGD + momentum, weight decay, mini-batch size 128
> 4. Evaluation: Top-1 / Top-5 error rate
>    
> **📍 모델 비교** 
> 1. SIFT + FVs(Traditional Method): Top-5 error=26.2%
> 2. 1 CNN(AlexNet): Top-5 error=18.2%
> 3. 5 CNNs(Ensemble): Top-5 error=16.4%
> 4. 7 CNNs* (Pretrain + Ensemble): **Top-5 error=15.3%** --> 최종 AlexNet의 성능

---


## **🔍 Experiments**

> **✅ 데이터셋**
> ImageNet ILSVRC-2010
> 
> **✅ Models**
> 1. SIFT + FVs(Traditional Method)
> 2. 1 CNN(AlexNet)
> 3. 5 CNNs(Ensemble)
> 4. 7 CNNs* (Pretrain + Ensemble)
> 
> **✅ Evaluation Metrics**
> Top-1 / Top-5 error rate
> 
> **✅ Implementation Details**
> SGD + momentum 0.9, weight decay 0.0005, mini-batch size 128, lr(초기: 0.01, 성능 정체시 1/10로 감소) 

---


## **📖 Conclusion**

> **✅ Limitation**
> 모델 크기가 너무 무겁고, 파라미터가 너무 많음
> GPU 없이는 추론 조차 불가능함
> 
> **✅ Contribution**
> 1. ReLU의 사용으로 빠른 학습이 가능
> 2. FC layer에 Dropout 기법을 적용해 overfitting을 해결
> 3. GPU 병렬 연산으로 대규모 CNN 학습을 가능하게 함

---


## **🤔 Question**

> ℹ️ *본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.*
> 
> 
> **📍 이 논문이 등장하게 된 이유 + 이 논문이 관련 Task에 기여한 내용**
> 대규모 CNN 학습을 가능하도록 하는 GPU 병렬 연산--> GPU 딥러닝 시대의 개막...
> 
> **📍 배울 수 있었던 내용과 추가로 궁금한 점**
> Ensemble과 pretraining으로 최종 Top-5 error=15.3%라는 성능을 달성했는데 Ensemble과 Pretraining의 방법이 달랐다면 성능이 더 높아졌을까?
> 
