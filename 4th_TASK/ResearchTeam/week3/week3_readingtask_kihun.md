# Week3 Reading Task


## **📘 Title**

> ℹ️ *APA. 인용 방식 권고*
> He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 770–778.

---


## **📖 Abstract**

> ℹ️ *본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.*
> 주요 문제의식: very deep plain network에서 depth 증가 시 training error 역전 증가하는 degradation problem 관찰됨.
> 핵심 아이디어: target mapping H(x)를 직접 학습하지 않고 residual F(x)=H(x)−x를 학습. output을 y=F(x)+x로 구성. identity shortcut로 parameter 증가 없이 gradient 흐름 개선. 차원 불일치 시 projection shortcut 사용.
> 결과: ImageNet에서 50/101/152-layer ResNet이 18/34-layer 대비 성능 향상. single-model 152-layer top-5 val 4.49%. ensemble top-5 test 3.57%. ILSVRC 2015 1위.
> 

---


## **📚 Background**

> ℹ️ *논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리*
> 
> 
> **📍 Related Work 1**
> depth 확대가 성능에 중요하나 plain network는 depth 증가 시 optimization 난이도 상승으로 training error 증가. BN 사용해도 degradation problem 존재함.
> **📍 Related Work 2**
> shortcut 기반 구조가 학습을 용이하게 할 수 있음. identity shortcut이 parameter 없이 작동. projection shortcut은 차원 매칭용으로 사용 가능.

---


## **🔍 Methods**

> **✅ 사용된 연구 방법**
> residual learning 채택. block 단위로 y=F(x,{W_i})+x 구성.
> F는 2-layer 또는 3-layer conv로 구현. 동일 차원은 identity shortcut.
> 차원 변경은 1×1 projection shortcut로 매칭. addition 후 활성함수 적용.
> 
> **✅ 실험 설계**
> ImageNet용으로 bottleneck block 도입.
> 1×1-3×3-1×1로 채널 축소-연산-확장.
> identity shortcut 사용 시 연산량과 파라미터 효율 유지.
> projection을 과도하게 쓰면 비용 증가
> **📍 모델 비교** 
> plain-18/34 vs ResNet-18/34로 degradation 유무 비교.
> 이후 ResNet-50/101/152로 depth scaling.
> ResNet이 일관되게 우세.

---


## **🔍 Experiments**

> **✅ 데이터셋**
> ImageNet ILSVRC 2012. train 1.28M. val 50k. test 100k. top-1, top-5 error로 평가.
> CIFAR-10. train 50k. test 10k. 간단한 구조로 매우 깊은 network 분석
> **✅ Models**
> ImageNet: 18/34 plain과 대응 ResNet. bottleneck으로 50/101/152 구성
> CIFAR-10: 6n+2 layer 설계. shortcut은 identity 사용. n은 {3,5,7,9,18}. 최대 1202-layer 실험.
> **✅ Evaluation Metrics**
> classification: top-1, top-5 error. detection: mAP@.5, mAP@[.5:.95].
> **✅ Implementation Details**
> ImageNet:
> - scale jittering 256–480.
> - 224 crop. color augmentation.
> - BN은 conv 뒤 activation 전.
> - SGD batch 256. lr 0.1에서 시작 후 plateau마다 /10.
> - total 60×10^4 iters. weight decay 1e-4.
> - momentum 0.9.
> - dropout 미사용.
> - test는 10-crop 또는 fully-conv multi-scale.
> CIFAR-10:
> - batch 128.
> - lr 0.1.
> - schedule 32k, 48k decay.
> - 64k stop.
> - 4-pixel pad 후 32×32 random crop.
> - flip.
> - dropout 없음.
> - 110-layer는 warm-up 0.01 사용 후 0.1 복귀. 

---


## **📖 Conclusion**

> **✅ Limitation**
> CIFAR-10에서 1202-layer는 110-layer보다 test error 높음.
> overfitting 추정.
> 강한 regularization 결합 필요성 언급
> 
> **✅ Contribution**
> residual learning 공식을 block 단위로 정식화.
> identity shortcut로 parameter 증가 없이 optimization 용이화.
> bottleneck으로 depth와 효율 동시 확보.
> very deep network에서 degradation 문제 해소.
> ImageNet SOTA 및 detection 전이 성과 달성.

---


## **🤔 Question**

> ℹ️ *본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.*
> extremely deep에서 generalization 저하를 막는 regularization 조합 최적해 무엇?
> projection shortcut 비율과 성능-효율 trade-off 최적점?
> detection에서 BN freezing 대신 다른 normalization 선택?
> 
