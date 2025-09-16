# Week2 Reading Task


## **📘 Title**

> ℹ️ *APA. 인용 방식 권고*
> Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. Advances in neural information processing systems, 30.

---


## **📖 Abstract**

> ℹ️ *본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.*
> 기존의 convolution을 기반으로 sequence transduction 모델과 달리 Transformer라는 새로운 네트워크를 제안하여
  attention 매커니즘만을 기반으로 한다. 기존의 SOTA 모델보다 더 나은 성능을 보였다.

---


## **📚 Background**

> ℹ️ *논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리*
> 
> 
> **📍 Related Work 1**
> **RNN, CNN을 기반으로 한 sequential computation**: RNN은 병렬화가 불가능, CNN은 병렬화가 가능하나 멀리 떨어진 단어 사이의 dependency를 학습하는데 필요한 연산이 커짐
> **📍 Related Work 2**
> **Self-attention**: 문장 안의 모든 위치를 직접 연결할 수 있어 거리와 무관하게 dependency를 효율적으로 학습할 수 있다.  

---


## **🔍 Methods**

> **✅ 사용된 연구 방법**
> 1. 기존 RNN/LSTM, CNN 기반 구조를 모두 배제하고, 전적으로 Self-Attention에 기반한 Transformer 아키텍처를 제안함
> 2. 인코더–디코더 구조를 유지하되, 각 층을 Multi-Head Self-Attention + Feed-Forward Network로 구성함
> 3. 위치 정보를 보완하기 위해 Positional Encoding 도입
> 
> **✅ 실험 설계**
> 1. WMT 2014 English–German, English–French를 주요 벤치마크로 설정
> 2. Base 모델(N=6, d_model=512, 8 heads) vs. Big 모델(N=6, d_model=1024, 16 heads)
> 3. 8 × NVIDIA P100 GPU, 3.5일 학습
> 4. 평가 지표: BLEU score
>    
> **📍 모델 비교** 
> 기존 RNN/CNN 기반 모델 vs. Transformer

---


## **🔍 Experiments**

> **✅ 데이터셋**
> WMT 2014 English–German(약 450만 문장), WMT 2014 English–French(약 3600만 문장), English Constituency Parsing(추가 검증용)
> 
> **✅ Models**
> 1. Transformer(Base, Big)
> 2. RNN 기반 모델
> 3. CNN 기반 모델
>    
> **✅ Evaluation Metrics**
> BLEU score
> 
> **✅ Implementation Details**
> 1. Optimization: Adam optimizer, learning rate warm-up, decay schedule
> 2. Regularization: Dropout, Label Smoothing (ε = 0.1)
> 3. 8 × NVIDIA P100 GPU
> 4. 토큰화: Byte-Pair Encoding (BPE) 기반 단어 분리

---


## **📖 Conclusion**

> **✅ Limitation**
> 1. 당시에는 주로 기계 번역(MT) 중심으로 검증됨
> 2. 대규모 데이터와 자원이 필요하다.
> 3. Self-Attention은 모든 토큰 쌍을 고려해야 하므로 시퀀스 길이가 길어질수록 연산량이 증가
>    
> **✅ Contribution**
> 1. RNN과 CNN을 배제하고 오로지 Self-attention만을 사용해 구성한 최초의 sequence transduction 모델이었다.
> 2. 기존 RNN과 CNN을 기반으로 한 모델 대비 훨씬 더 빠른 학습 속도와 더 큰 batch 처리 가능해
> 3. SOTA 달성
> 4. 번역 외에도 다른 NLP 과제에도 적용 가능

---


## **🤔 Question**

> ℹ️ *본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.*
> 
> 
> **📍 이 논문이 등장하게 된 이유 + 이 논문이 관련 Task에 기여한 내용**
> 기존 RNN/LSTM 기반 모델은 순차적 연산을 해야 하기 때문에 병렬화가 불가능했고, 긴 sequence에서 dependecny 학습에 한계가 있었다.
> 병렬화가 가능한 CNN 기반 모델도 등장했지만, 멀리 떨어진 단어 간의 관계 학습이 비효율적이었다.
> 기존의 RNN과 CNN을 모두 제거하고, 오직 "Self-Attention"만으로 구성된 최초의 sequence 모델을 제안했고, 기계 번역에서 기존 최고 성능을 크게 뛰어넘으면서 번역 품질과 병렬화, 학습 효율을 동시에 달성했다.
>
> **📍 배울 수 있었던 내용과 추가로 궁금한 점**
> self-attention의 연산량 문제를 해결한 이후 연구가 있는지? 어떤 방식으로 해결했는지 궁금하다.
> Transformer가 NLP 분야 뿐만 아니라 여러 영역에도 사용되고 있는데 구체적으로 어떻게 확장될 수 있었는지 궁금하다.
> 
