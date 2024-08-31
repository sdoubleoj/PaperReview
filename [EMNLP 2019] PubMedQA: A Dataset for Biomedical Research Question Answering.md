<img width="300" alt="image" src="https://github.com/user-attachments/assets/830e2c7e-fc1f-42d6-af4a-a629ee17fb81">

- PubMed의 약 760,000개의 논문 제목이 질문 형식으로 작성
- 그 중 약 120,000개의 논문이 구조화된 초록(즉, "서론", "결과" 등으로 나누어진 초록)
- 논문 제목 > 질문
- 초록의 결론 파트 > 해당 질문에 대한 긴 답변으로 간주

### Question Source
- Biomedical 연구 논문 중 질문 형식의 제목 @PubMed

### Answer Format
- Yes/No/Maybe
- 질문에 대한 논문의 abstract에서 도출된 결론 기반

### Annotation Method
- manual & automatic
- 1000개의 질문에 대해 2명의 의학 전문가가 주석
  1. 문맥(초록 전체)과 긴 답변(초록의 결론)을 모두 사용해 답변 결정
  2. 문맥만 사용해 답변 주석
  - 두 주석자가 동일한 답변을 내리지 않았을 경우, 상호 협의를 통해 결정
- 211,300개의 질문과 답변은 자동 생성

### Dataset Size
- total 273,500개
  - PQA-L(abeled): 1,000개의 전문가 주석이 달린 QA
  - PQA-U(nlabeled): 61,200개의 레이블이 없는 Q
  - PQA-A(rtificial): 211,300개의 인공적으로 생성된 QA
    - NP-(VBP/VBZ)의 POS 태깅 구조를 가진 제목을 질문으로 변환
      - "Effect of Drug X on Disease Y" > "Does Drug X affect Disease Y?"
      - Using Stanford CoreNLP parser
      - 변환 규칙
        - 제목의 주요 동사나 명사를 기반으로 질문 구성 ("Impact of A on B" > "Does A impact B?")
        - 앞부분에 코퓰라(“이다”, “있다”) 또는 보조 동사(“한다”, “하다”)를 단순 이동하거나 추가하여 질문으로 변환하고 일관성을 위해 뒤에서 수정(예: 물음표 추가)
    - "Yes/No" 답변 생성: VB의 부정 상태에 따라 생성
      1. "Yes": 만약 논문의 제목이나 결론에서 긍정적인 단서(예: "enhances", "improves", "increases")가 발견될 경우
      2. "No": 부정적인 단서(예: "decreases", "reduces", "does not affect")가 포함된 경우

### OpenQA?
- yes
  - PubMed에 포함된 다양한 연구 논문에서 정보를 수집하고 이를 종합하여 답변을 도출

