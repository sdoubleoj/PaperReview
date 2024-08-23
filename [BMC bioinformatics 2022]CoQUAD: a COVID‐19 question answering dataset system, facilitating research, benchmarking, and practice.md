- COVID-19 Synthetic QA Dataset

# Dataset
  - CORD19와 LitCOVID initiative를 통해 구축된 참고 표준 데이터셋
  - Gold-Standard dataset 데이터셋 (공중 보건 전문가들이 수작업

# Structure
1. Retriever: BM25 Algorithm
  - BM25
    - Text Retriever에 사용되는 Ranking Function
    - 각 doc의 점수를 계산하여 해당 doc이 질문과 얼마나 관련성이 높은지 평가
$$
\text{BM25}(q, D) = \sum_{i=1}^{n} \text{IDF}(q_i) \cdot \frac{f(q_i, D) \cdot (k_1 + 1)}{f(q_i, D) + k_1 \cdot \left(1 - b + b \cdot \frac{|D|}{\text{avgdl}}\right)}
$$
$$
\text{IDF}(q_i) = \log \left(\frac{N - n(q_i) + 0.5}{n(q_i) + 0.5} + 1\right)
$$

2. Reader: Transformer-based MPNet
