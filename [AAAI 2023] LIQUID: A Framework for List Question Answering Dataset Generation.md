- Label이 지정되지 않은 Corpus에서 List QA 데이터셋 생성 자동화 프레임워크

# Research Purpose
- 기존 연구: 단일 범위 답변이 있는 Synthetic Question Generation
- 여러 개의 비인접 범위를 답변으로 하는 List-type Question(다지선다형 질문) Generation 연구 필요

# QA Generation Process
- Answer를 먼저 만들고 Question 생성

1. Summarization
  - BART base(CNN/Daily Mail 데이터셋으로 학습) 사용. Wikipedia나 PubMed의 Passage 요약
  - 요약에서 더 포괄적인 의미를 가진 Entity를 추출할 수 있음
    
3. Answer Extraction
   - spaCy NER Tagger와 BERN2 사용. 1의 요약된 텍스트에서 후보 답변 Named Entity 추출
   - 맥락에서 의미적으로 상관 관계가 있는 후보 답변을 구성할 수 있어 적절한 List-type Question 생성할 수 있게 함
   - Passage 전문에서 추출된 Entity 모두를 사용해 Question을 생성하는 것보다, 요약에서 추출된 Entity를 사용하는게 구체적인 Quetion을 생성할 수 있음
  
4. Question Generation
   - T5 base(SQuAD로 학습) 사용. 2에서 추출한 Entity를 a로 Passage를 c로 모델에 입력("answer: a1, .., aM Context: c")
   - 초기 QA 인스턴스 <c(passage), q(Question), A(후보 답변 집합)> 출력
     
6. Iterative Filtering
   - 답변 후보에 오답이 포함되는 것을 거르고 답변의 정확도를 높이기 위함
   - Single-span QA 모델인 RoBERTa base(2019)와 BioBERT(2020)를 SQuAD로 학습시켜 사용 (Biomedical 도메인에 대한 Linear Regression Layer 있음)
   1. 모델에 Passage c와 Question q를 입력, 후보 답안 a1~aM에 대한 Confidence Score 출력
   2. 답변 집합인 A={a1,...,aM} 중 Confidence Score < Threshold τ 이하인 후보 답변 an은 A에서 삭제되어 A′ = {a′1 ~ a′M′}(M′ ≤ M) 출력
   3. Filtering 후 0개 또는 1개의 답이 남는 경우 해당 <c,q,A'>는 사용하지 않음

7. Question Re-Generation
8. Answer Expansion
   : 답변 후보에서 생성된 
