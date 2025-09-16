# Week4 Reading Task


## **📘 Title**

> ℹ️ *APA. 인용 방식 권고*   
 Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. Advances in neural information processing systems, 30.
>

---


## **📖 Abstract**

> ℹ️ *본인의 방식으로 재해석 해주세요. 그대로 가져오는 것은 금합니다.*   
2017년, Recurrent, Convolution을 완전히 배제하고 Attention에만 의존하는 신경망 Transformer이 등장했다. 이 모델의 등장 전후로 자연어처리의 양상은 완전히 달라졌으며, 현재 우리가 편하게 사용하는 ChatGPT 등 생성형AI역시 Transformer 기반이다. 자연어처리 뿐 아니라, CV, Multimodal 등 수많은 AI분야에서 지금까지 활용되고 있으며, 수많은 분야에서 SOTA를 달성했다.
>

---


## **📚 Background**

> ℹ️ *논문의 주제와 관련된 기존 연구들 및 배경 지식을 정리*
> 
> 
> **📍 Related Work 1**   
Sequence-to-Sequence : Encoder, Decoder라는 두 개의 RNN으로 구성되며, 기계번역, 요약, 챗봇 등 다양한 NLP에 사용되는 모델이다. 초기 seq2seq 모델은 긴 문장을 하나의 고정된 Context Vector로 압축해야 했기 때문에, 문장이 길어질수록 정보가 손실되었다.
> 
> **📍 Related Work 2**
>LSTM : RNN의 long-term dependencies를 해결하기 위해 고안된 RNN의 한 종류다. 일반적인 RNN은 문장이 길어질수록 초반부의 정보가 희미해져가는 Vanishing Gradient가 발생하지만, LSTM은 이를 극복하고 먼 과거의 정보도 기억할 수 있다.

---


## **🔍 Methods**

> **✅ 사용된 연구 방법**   
> RNN과 CNN을 완전히 제거하고, Attention이라는 메커니즘만으로 Sequence 변환 모델을 구축하였다.   
seq2seq모델과 마찬가지로 Encoder와 Decoder를 사용하지만, 둘 다 Attention Block과 Position-wise Feed-Forward Network로 연결된다.   
RNN처럼 순환적인 구조는 없지만, Multi-Head Attention을 통해 Self Attention을 여러 번 병렬로 수행하여 모델이 다양한 관점에서 정보에 Attention 하도록 하였다.
> 
> **✅ 실험 설계**   
> English-to-German translation task   
Ecnglish Constituency Parsing task 
> **📍 모델 비교**   
GNMT (Google’s Neural Machine Translation, 2016)   
ConvS2S (Convolutional Sequence to Sequence, 2017)   
기존 attention-based RNN 모델들

---


## **🔍 Experiments**

> **✅ 데이터셋**
> WMT 2014 English–German translation task(4.5M)
WMT 2014 English–French translation task (36M)
> 
> **✅ Models**   
> Transformer   
> **✅ Evaluation Metrics**   
> BLEU score   
> **✅ Implementation Details**   
>Optimizer : Adam (β₁=0.9, β₂=0.98, ε=1e-9)   
Warmup steps : 4000, step^0.5 decrease   
Regularization : Dropout rate 0.1   
8개의 NVIDIA P100 GPU 사용   
Base 모델: 약 12시간 학습   
Big 모델: 약 3.5일 학습   


---


## **📖 Conclusion**

> **✅ Limitation**   
>  트랜스포머는 문장 길이가 길어질수록 Attention의 계산량이 시퀀스 길이의 제곱 O(n^2)에 비례하여 급증하고, 이는 Bottleneck을 유발한다.   
순서를 직접적으로 처리하지 않고 위치 인코딩(Positional Encoding)에 의존하고 이는 순서 정보가 중요한 일부 작업에서 RNN보다 불리할 수 있다.   
> 
> **✅ Contribution**   
>순차적으로 단어를 처리해야 하는 RNN과 달리, 모든 단어를 동시에 병렬로 처리할 수 있게 함으로써 훈련 속도를 획기적으로 향상시켰다.
어텐션 메커니즘만으로도 매우 강력한 모델을 만들 수 있음을 증명하였고, 이후 NLP외에도 각종 딥러닝 모델의 핵심 구성 요소가 되었다.

---


## **🤔 Question**

> ℹ️ *본인이 수행한 학습에 대해 스스로 질문하고 답해보세요.*
> 
> 
> **📍 이 논문이 등장하게 된 이유 + 이 논문이 관련 Task에 기여한 내용**   
CNN 기반 모델은 병렬화는 가능했지만, 장기 의존성을 포착하기 위해서는 깊은 네트워크가 필요했다. 또한 순차적 구조 없이, 병렬적으로 시퀀스 간의 의존성을 학습할 필요가 있었다. Attention 구조를 통해 RNN/CNN을 대체할 수 있는 새로운 아키텍처를 제안하였고, NLP 외에도 현대 딥러닝 모델들의 기반 아키텍처가 되었다.
> 
> **📍 배울 수 있었던 내용과 추가로 궁금한 점**   
>현재 대부분의 NLP에 Transformer를 사용하고 있는데, 아직 NLP 분야 내에서 Transformer보다 RNN/CNN이 우세한 분야가 있는지 궁금했다. 임베디드, IoT등 메모리, 계산량이 제한적인 환경에선 아직 RNN이 다소 유리하다고 한다. (온라인 음성인식)
> 
