- COVID-19 Synthetic QA System



# Dataset
  - CORD19와 LitCOVID initiative를 통해 구축된 참고 표준 데이터셋
  - Gold-Standard dataset 데이터셋 (공중 보건 전문가들이 수작업

# Structure

<img width="897" alt="image" src="https://github.com/user-attachments/assets/aac44f63-4984-412b-a823-7b343e220cef">

1. Retriever
  - input: 질문 q
  -  질문 q과 관련된 문서 D를 검색
  -  질문의 단어와 문서 내 단어의 빈도 및 희귀성을 고려하여 문서의 관련성을 점수화
  - Algorithm: BM25
    - Text Retriever에 사용되는 Ranking Function
    - q에 대해 각 D의 점수를 계산하여 해당 D가 질문과 얼마나 관련성이 높은지 평가
    - (BM25수식)
    - (IDF 수식)

2. Reader: Transformer-based MPNet

<img width="848" alt="image" src="https://github.com/user-attachments/assets/d9793d2d-3639-4670-9fcf-771f9b7f5600">

  - input: 검색된 문서 D & 질문 q
  - algorithm: MPNet
  - MPNet을 사용하여 검색된 문서에서 질문에 대한 답변 추출
  - 입력 텍스트를 Embedding Vector로 변환한 후, 이를 기반으로 문장 간의 관계를 파악하고 특정 질문에 대한 답을 추출
  - 문맥을 이해하기 위해 문서와 질문을 함께 입력으로 받아 Self-Attention 메커니즘을 통해 각 단어의 중요도를 계산하고, 그 결과로 얻어진 벡터를 기반으로 질문에 대한 답변을 도출
  - (Self-Attention 수식)

# Experiment
- Baseline
  - BERT, XLNET, ALBERT, BART, ELECTRA, Funnel,. Longformer, COBERT, COVID-QA
- Metric
    - Retriever
      : Precision, Recall, Mean Reciprocal Rank(MRR), Mean average precision (MAP)
    - Reader
      : F1, Acc, EM, SAS
