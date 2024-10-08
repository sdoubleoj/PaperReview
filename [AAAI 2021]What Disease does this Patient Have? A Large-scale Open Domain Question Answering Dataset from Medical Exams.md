# [AAAI 2021] What Disease does this Patient Have? A Large-scale Open Domain Question Answering Dataset from Medical Exams
- MedQA paper

-   대규모 Medical QA 데이터셋
-   기존의 OpenQA 시스템이 잘 다루지 못하는 복잡한 의료 Question 포함

<img alt="Examples of MedQA" src="https://github.com/user-attachments/assets/30ff506f-a4cb-4de1-99c8-c6931858baf1"/>

## 연구 목적

-   의료 분야의 Question은 일반적인 상식이나 간단한 텍스트 정보 이상의 복잡한 논리적 추론과 깊이 있는 전문 지식 요하기 때문에, 기존의 OpenQA 데이터셋으로는 모델이 의료 질문에 대한 제대로 된 답변을 할 수 없음

## MedQA 데이터셋

-   구성
    -   총 61,097개의 의료 질문  
        (미국(USMLE), 중국(MCMLE), 대만(TWMLE)의 **의학 시험**에서 수집된 12,723개의 영어, 34,251개의 간체 중국어, 14,123개의 번체 중국어)
    -   자유형 4지선다형 질문(Free-from Multiple-Choice Question) (정답3, 오답1)
-   방법론
    1.  Question과 Answer 수집
        -   USMLE: 의학 시험 준비 리소스(예: MedBullets, Amboss, Lecturio)에서 수집
        -   MCMLE: 의학 시험 준비 리소스에서 수집
        -   TWMLE: 국가시험 공식 웹사이트에서 PDF 형식으로 시험 자료 수집 후 텍스트 데이터로 변환
        -   처리: 중복 제거, 3개 간 균형을 맞추기 위해 각 질문에 대한 답변 선택지 중 하나를 무작위로 삭제해 총 4개의 선택지(정답3, 오답1)로 조정
    2.  문서 수집
        -   의학 텍스트 수집
        -   미국, 대만: 18권의 영어 의학 교과서에서 텍스트 수집
        -   중국: MCMLE 시험 준비서 33권에서 간체 중국어 텍스트 수집
        -   처리: PDF에서 OCR 기술을 사용해 텍스트로 변환, 철자 오류 수정 및 기타 전처리 작업을 거쳐 단락 단위로 분할
    3.  데이터 커버리지 검증
        -   수집된 문서가 데이터셋의 질문에 대해 충분한 정보를 제공할 수 있는지 평가
        -   무작위로 선택된 100개의 질문에 대해 의학 전문가들이 수집된 텍스트 자료에서 정답을 찾을 수 있는지 검증
    4.  다국어 데이터셋
        -   중국어 -> 영어로 번역

## 의학 데이터셋의 핵심 챌린지 (논문 복붙)

1.  전문 지식  
    대부분의 기존 QA 데이터 세트에서 질문 답변 프로세스는 **언어에 대한 기본적인 이해와 일반적인 세계 지식 추론에 크게 의존**합니다. 일부 연구에서는 사전 학습된 대규모 언어 모델이 언어 지식 외에도 일정 수준의 상식 및 상징적 추론 능력을 갖추고 있으며(Talmor 외. 2019; Petroni 외. 2019), 이는 현재 QA 모델의 놀라운 성능에 크게 기여할 수 있다는 사실이 밝혀졌습니다. 그러나 데이터 세트의 모든 질문에 대한 답변을 위해서는 풍**부한 전문 분야별 지식, 특히 의료 지식이 필요**하므로 모델은 **의료적 맥락에 대한 깊은 이해가 필요**합니다.
2.  질문의 다양성  
    임상의학 분야는 다양한 주제에 대해 질문할 수 있을 만큼 다양합니다. 일반적으로 질문에는 두 가지 범주가 있습니다:  
    1). 예를 들어 "다음 중 정신분열증에 속하는 증상은 무엇입니까?"와 같이 하나의 **지식**을 묻는 질문입니다.  
    2). 이 질문은 먼저 환자의 상태를 설명한 다음 가장 확실한 진단 / 가장 적절한 치료법 / 필요한 검사 / 특정 상태의 메커니즘 / 특정 치료의 가능한 결과 등을 묻습니다.  
    표 1은 유형 2의 대표적인 두 가지 예를 보여줍니다. 표 6은 개발 세트에서 무작위로 선택한 100개의 질문을 표기하여 각 데이터 세트에 대해 이 두 가지 유형의 질문이 차지하는 비율을 요약한 것입니다. 일반적으로 **유형 1 문제는 한 단계 추론**이 필요한 반면 유형 2 문제는 **다중 홉 추론**이 필요하므로 유형 1 문제보다 훨씬 더 복잡하여 독해 모델뿐만 아니라 관련 텍스트 검색 모듈에도 문제를 부과합니다. 예를 들어, 표 1의 첫 번째 문제를 풀기 위해 모델은 먼저 **긴 설명 문단에서 이 환자의 증상을 추출, 이해, 해석**한 다음, **이 증상을 수백만 개의 의학 지식 텍스트 저격과 매칭하여 가장 연관성이 높은 것을 찾아내고, 마지막으로 답 선택을 위한 근거 문장을 찾아내야 합니다.**
3.  여러 증거에 대한 복잡한 추론  
    데이터의 많은 질문에는 **여러 증거 조각에 대한 복잡한 멀티홉 추론**이 포함됨. 예를 들어, 두 번째 예시는 **세 가지 증거에 대해 여러 단계의 추론**이 필요한 전형적인 질문으로, 증상과 징후를 통해 증거 1과 2를 보고 이 환자가 루게릭병 환자일 가능성이 높다는 것을 알 수 있습니다. 그 후 증거 3을 통해 가족성 루게릭병의 유전적 돌연변이 가능성이 있는 것은 SOD1이라는 것을 알 수 있으며, 이것이 정답입니다. 
4.  노이즈가 많은 증거 검색  
    대규모 텍스트에서 관련 정보를 검색하는 것은 짧은 텍스트를 읽는 것보다 훨씬 더 어렵습니다. 교과서의 구절은 종종 질문에 대한 답을 직접적으로 제공하지 않으며, 가장 널리 채택된 용어 매칭 기반 정보 검색(IR) 시스템으로 검색된 많은 구절은 노이즈가 많고 특히 유형 2 문제의 경우 관련성이 없는 것으로 판명됩니다. **다중 홉 추론이 필요한 문제의 경우 모델은 여러 구절에 흩어져 있는 모든 관련 정보를 식별**해야 하며, 단 하나의 증거라도 놓치면 실패로 이어질 수 있습니다.

## QA 방법론 제시

-   Rule-based Method
    -   Pointwise Mutual Information (PMI)  
        : 질문과 답변 선택지 사이의 연관성을 측정하는 기법
        1.  **n-그램 추출**: 질문과 각 답변 선택지에서 unigram(단어), bigram(두 단어), trigram(세 단어), 그리고 skip-bigram을 추출합니다.
        2.  **PMI 점수 계산**: 추출된 n-그램 쌍 사이의 연관성을 계산하기 위해 PMI 점수를 사용합니다. PMI 점수는 두 n-그램이 주어진 문서 컬렉션에서 얼마나 자주 함께 등장하는지를 기반으로 계산됩니다. 이 점수가 높을수록 두 n-그램이 강하게 연관되어 있음을 의미합니다.
        3.  **답변 선택**: 각 질문-답변 쌍에 대해 모든 n-그램 쌍의 PMI 점수를 평균화한 후, 가장 높은 점수를 가진 답변을 선택합니다.
    -   Information Retrieval (IR)
        -   **질문과 답변 선택지**에 대해 문서에서 관련된 문장을 검색하고, 이 문장들을 기반으로 답변을 도출
        -   **IR-ES**: Apache Lucene과 Elasticsearch를 기반으로 한 표준 텍스트 검색 시스템을 사용.
            -   입력(검색 쿼리): 질문과 답변 선택지를 결합
            -   출력: 검색 엔진에서 반환된 **상위 N개의 문장들에 대해 점수**를 매긴 후, 가장 높은 점수를 받은 답변
        -   **IR-CUSTOM**: BM25 가중치 재조정 메커니즘을 적용한 향상된 IR 시스템. 이 방법은 **문서와 질문의 길이를 고려하여 더 정교한 점수 계산을 수행**. 또한, 영어 질문에 대해서는 Snowball 스테밍을 수행하고, MetaMap 도구를 사용하여 의료와 관련 없는 단어를 제거하여 검색 성능을 향상
-   Neural Models  
    : Document Retriever와 Document Reader로 구성  
    1.  Document Retriever  
        IR 시스템을 사용하여 질문에 적합한 문서를 검색하는 역할. 검색된 문서들 중에서 상위 N개의 문단을 선택하여 다음 단계인 문서 읽기(Document Reader)로 전달.
    2.  Document Reader
        -   **MAX-OUT**
            -   **bi-directional GRU**(Gated Recurrent Unit)를 사용해 문서와 질문-답변 쌍을 인코딩. 인코딩된 벡터에 대해 max-pooling을 수행하여 최종 벡터를 생성한 후, 이 벡터를 기반으로 답변의 확률 점수를 계산. 이 점수가 가장 높은 답변을 선택.
            -   입력: 문서(Document Retriever의 출력)와 질문-답변(4개 선택지) 쌍
            -   출력: 선택지별 확률
        -   **PLM(BERT, RoBERTa 등)**
            -   BERT와 같은 사전 학습된 언어 모델을 fine-tuning하여 의료 질문에 대한 답변을 예측
            -   입력: **질문과 선택지를 문서 텍스트와 결합**
            -   출력: 선택지별 확률
            -   **BERT**: 기본적으로 BERT-Base 모델을 사용, 다양한 버전의 BERT 모델들이 사용됨.  
                (예를 들어, BioBERT는 의학 문서에 특화된 BERT 모델이고, ClinicalBERT는 임상 기록에 맞게 추가로 학습된 BERT 모델)
            -   **RoBERTa**: BERT보다 더 큰 데이터와 긴 학습 과정을 통해 성능을 향상시킨 모델
