**Week3 Reading Task**

**📘 Title**

> ℹ️ APA. 인용 방식 권고 He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 770–778.
> 

---

**📖 Abstract**

> ℹ️ 본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.
> 

신경망을 깊게 학습시키는 데 어려움이 존재함. 단순히 층을 쌓는 방식은 성능 저하(degradation problem) 발생우려가 있기 때문에 섣불리 무작정 층을 쌓을 수는 없는 상황..

이에 대한 대안으로 ‘Residual Learning’을 제안하게 됨! 출력을 그대로 맞추는 방식 대신, 입력에 어떤 변화(차이)를 더해줘야 하는지만 배우도록 우회적인 방향을 제시함

이로 인해 성능 최적화가 수월해졌고, 더 깊은 네트워크에서도 안정적 학습 가능하게 되는 성과를 냄 (Ex - ImageNet에서 152-layer ResNet 달성, VGG 대비 연산량 적으면서도 성능 훨씬 좋음, ILSVRC 2015 1위 기록 등 ..)

---

**📚 Background**

> ℹ️ 논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리
> 
> 
 **📍 Related Work 1: Residual Representation**
> 
이미지 검색, 분류에서 residual 기반 표현법(Fisher Vector, VLAD)이 사용됨! 잔차 표현이 기존 벡터 직접 인코딩보다 효율적임
> 
 **📍 Related Work 2: Shortcut Connections**
> 
MLP, Inception, Highway Network 등에서 shortcut connection 연구됨. Highway Network는 gating 사용했으나 깊은 네트워크에서 성능 개선 제한적. 반면 ResNet은 단순 identity shortcut 사용으로 최적화 문제 해결
> 

---

**🔍 Methods**

✅ **사용된 연구 방법**: 잔차 학습 프레임워크 제안! 각 블록이 F(x) + x의 구조를 학습하도록 함
> 
> 
 **✅ 실험 설계:** plain network와 residual network를 동일 파라미터, FLOPs 조건으로 맞춰 비교하려 함. ImageNet에서는 18/34/50/101/152층, CIFAR-10에서는 20~1202층까지 확장해, 데이터 크기에 따른 최적화 안정성과 성능 변화를 관찰함
>
 **📍 모델 비교**: plain 모델은 깊어질수록 학습 실패와 성능 저하가 발생했으나, residual 모델은 더 깊어질수록 오히려 에러 감소해나가는 성과를 보임. 특히 ResNet-152는 VGG보다 연산 적으면서 성능은 크게 앞섰고, CIFAR-10에서도 110층까지 성능 개선이 이어졌음
> 

---

**🔍 Experiments**

 ✅ **데이터셋**: ImageNet, CIFAR-10
> 
**✅ Models:** bottleneck 블록(1x1–3x3–1x1 conv) + identity shortcut. 152-layer 모델 구현
> 
**✅ Evaluation Metrics:** top-1, top-5 error, CIFAR-10 classification error, COCO mAP
> 
**✅ Implementation Details:** Batch Normalization, SGD Optimization, weight decay=0.0001, momentum=0.9, learning rate schedule 적용, Dropout은 사용 X
> 

---

**📖 Conclusion**

 ✅ **Limitation:** CIFAR-10에서 1202-layer 모델은 오히려 과적합되는 결과가 나타남. 즉, 지나치게 깊은 네트워크는 데이터 크기와 불균형 발생 (여전히 . . !)
> 
> 
 **✅ Contribution:** 기존에 가지고 있었던 degradation problem을 해결하고, 더 깊은 네트워크에서도 안정적 최적화시킬 수 있다는 실험 결과를 가져옴. 즉 이후의 모델 개발의 가능성(?)을 열어준 역할. 이후 Computer Vision Task들에서 ResNet이 표준 구조로 자리 잡게 됨
> 

---

**🤔 Question**

> ℹ️ 본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.
> 
- 왜 더 다양한 정규화 기법을 적용하지 않았을까? 궁금합니다. 대표적으로 Dropout을 사용하지 않았다고 했는데, 이미 Batch Normalization으로도 충분하다고 느꼈기 때문이라는 판단인지 혹은 본 연구의 목적 자체는 ‘깊은 네트워크의 최적화’가 초점이었기에 그것만 비교하기 위해서 별도의 영향 요소를 배제하기 위함이었을지, 어떻게 생각하시는지 궁금합니다 !
- ImageNet에서 잘 되는데, 데이터가 작은 경우에는 residual learning이 여전히 효과적일지도 궁금합니다! 데이터셋의 특징에 따라서도 상이하게 결과가 나타날 것 같아 생각하다보니 든 궁금증이었습니다.
