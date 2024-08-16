<img width="1304" alt="overview of LIQUID" src="https://github.com/user-attachments/assets/0975d588-65c3-4173-a065-43d3622e73d2">
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
   - 모델에 Passage c와 Question q를 입력, 후보 답안 a1~aM에 대한 Confidence Score 출력
   - 답변 집합인 A={a1,...,aM} 중 Confidence Score < Threshold τ 이하인 후보 답변 an은 A에서 삭제되어 A′ = {a′1 ~ a′M′}(M′ ≤ M) 출력
   - Filtering 후 0개 또는 1개의 답이 남는 경우 해당 <c,q,A'>는 사용하지 않음

7. Question Re-Generation
   - 필터링된 후보 답안 A′에 맞게 Question 재생성
   - 현재 답안 세트 == 이전 답안 세트가 될 때 까지 OR 최대 반복 횟수 T에 도달할 때까지 필터링과 재생성 반복

8. Specifying Answer Position
   - 모델 학습 시, Passage c에서 Answer의 시작과 끝 위치 필요
   - QA 모델에서 Confidence Score가 가장 높은 Span을 Answer 문자열의 답 위치로 사용

9. Answer Expansion
   - 초기 NER 단계에서 오답이 추출되어 시작부터 불완전한 초기 QA 인스턴스 <c, q, A>로부터 위 과정이 진행될 수 있음.
   - Filtering 단계에서 오답을 제외시킬 수 있지만, 이는 근원적인 해결이 아님.
   - 따라서 Filtering에서 사용한 모델을 사용, 필터링된 집합 A′ 중 Confidence Score가 가장 낮은 답변 an보다 높은 Score를 가진 추가 답변 am을 식별하여 해결
   - 위 과정을 거쳐 확장된 집합 A′′로 q′′를 생성
   - QA 모델이 q′′에 대해 A′′를 필터링하지 않으면 〈c, q′′, A′′〉는 최종 인스턴스로 사용
