# Week2 Reading Task


## **📘 Title**

> ℹ️ *APA. 인용 방식 권고*
> Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks. In F. Pereira, C. J. C. Burges, L. Bottou, & K. Q. Weinberger (Eds.), Advances in Neural Information Processing Systems (Vol. 25, pp. 1097–1105). Curran Associates, Inc.

---


## **📖 Abstract**

> ℹ️ *본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.*
> 대규모 CNN을 ImageNet에 학습. 입력은 224×224. 5개 합성곱층(convolutional layers)과 3개 완전연결층(fully connected layers). ReLU로 빠른 학습. GPU 기반 합성곱 최적화. FC 층에 drop out 적용. ILSVRC-2010에서 Top-1 37.5% Top-5 17.0%. 2012 대회 변형 모델 Top-5 15.3%. 이전 기법 대비 큰 개선. 

---


## **📚 Background**

> ℹ️ *논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리*
> 
> 
> **📍 Related Work 1**
> 소규모 데이터와 manual feature-engineering 중심의 접근이 일반적이었음. SIFT와 Fisher Vector가 강력한 기준선이었음. 이 기준선은 ILSVRC-2012에서 Top-5 26.2%를 기록. 
> **📍 Related Work 2**
> CNN은 local connectivity와 weight sharing으로 매개변수 효율적임. 그러나 대규모 학습엔 연산량이 병목이었음. 대형 데이터와 GPU가 제약 완화함. 비전 커뮤니티는 학습 기반 접근의 확장성을 과소평가했음.
>
---

## **🔍 Methods**

> **✅ 사용된 연구 방법**
>  supervised learning으로 deep CNN 학습함. 모든 conv와 FC에 ReLU 적용함. LRN 사용함. k=2 n=5 alpha=1e-4 beta=0.75임. overlapping pooling 사용함. s<z 설정임. data augmentation 두 가지 사용함. random crop과 horizontal flip. RGB-PCA color jitter 사용함. FC 두 층에 dropout 적용함. 2-GPU model parallel 사용함. 특정 layer에서만 통신함
> 
> **✅ 실험 설계**
> ILSVRC-2010을 주 평가로 사용함. ILSVRC-2012에 variant 제출함. 지표는 Top-1과 Top-5임.
> **📍 모델 비교** 
> 단일 CNN이 SIFT+FV보다 우수함. 2-GPU 분할로 1-GPU 대비 Top-1 −1.7pp Top-5 −1.2pp 개선됨.

---


## **🔍 Experiments**

> **✅ 데이터셋**
> ImageNet LSVRC. 1000 클래스. train 1.2M. 대규모 고해상도 이미지.
> 
> **✅ Models**
> 8 learnable layers, 5 conv 3 FC 구성, ReLU everywhere. LRN은 conv1과 conv2 뒤에 둠. max-pool은 두 LRN 뒤와 conv5 뒤에 둠. conv1 11×11 stride 4 96개, conv2 5×5 256개, conv3 3×3 384개, conv4 3×3 384개, conv5 3×3 256개. FC 4096-4096-1000. 최종 1000-way softmax.
> **✅ Evaluation Metrics**
> ILSVC 표준, top1, top5 사용
> **✅ Implementation Details**
> optimizer는 SGD, batch 128, momentum 0.9, weight decay 0.0005, 초기 lr 0.01, val error 정체 시 *0.1로 감소. 약 90 epochs 학습. 2×GTX580으로 5–6일 소요. 일부 bias를 1로 초기화. ReLU 활성 초기에 유리. test 시 dropout scaling 0.5 사용.

---


## **📖 Conclusion**

> **✅ Limitation**
> compute와 memory 제약 큼. 더 큰 모델과 더 긴 학습이 필요. video로 확장 필요. unsupervised pre-training 없이도 성능 나왔으나 compute 증가 시 효과 기대.
> 
> **✅ Contribution**
> large-scale supervised CNN의 실효성 입증. ReLU로 학습 속도 개선. 2-GPU 병렬로 대형 모델 학습 가능. LRN과 overlapping pooling으로 generalization 향상. crop과 RGB-PCA로 invariance 강화. FC dropout으로 overfitting 억제. ILSVRC에서 큰 폭의 SOTA 갱신.

---


## **🤔 Question**

> ℹ️ *본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.*
> 
> 
> **📍 이 논문이 등장하게 된 이유 + 이 논문이 관련 Task에 기여한 내용**
> feature engineering 기반 접근의 확장성 한계 있었. 데이터와 compute가 커질수록 end-to-end learning이 우위. 본 논문이 그 가설을 대규모 실험으로 검증. object classification에서 deep CNN의 유효성을 확립. 커뮤니티 패러다임 전환 촉발.
> **📍 배울 수 있었던 내용과 추가로 궁금한 점**
> LRN이 BatchNorm 시대에도 유효?
> pre-training 없이 동일 성능 재현 가능?
> 
