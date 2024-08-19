# NLP Downstream Task
1. Natural Language Understanding(NLU)
   - Sentiment Analysis
   - Named Entity Recognition
   - Question Answering
   - Relation Extraction

2. Natural Language Generation(NLG)
   - Text Summarisation
   - Dialogue Generation
   - Machine Translation
   - Text Generation

3. Text Classification
   - Topic Classification
   - Spam Detection
   - Sentence Classification

4. Information Retrieval
   - Document Ranking
   - Paragraph Retrieval
   - Query-Document Matching

5. Structured Prediction
   - Syntactic Parsing (구문 분석)
     : 자연어의 구문 구조, 특히 구성 요소의 구문 관계 및 라벨링 범위 분석
   - Coreference Resolution (상호참조 해결)
     : 임의의 Entity를 표현하는 다양한 명사구를 찾아 연결
   - Semantic Role Labelling (의미역 결정: 문장 성분의 의미역 결정)

# Medical NLP Task
- Text Summarization(TS)
- Question Answering System(QAS)
- Machine Translation(MT)
- NER(Named Entity Recognition)
- Information Extraction(IE)
- Medical Education(ME)
- Relation Extraction(RE)
- Text Mining(TM)
- EHR Generation
- Phenotype Extraction

# Benchmark
- GLUE
- SQuAD

# Conferences
- Top
  - International Conference on Computational Linguistics
  - European Conference on Machine Learning and Principles and Practice of Knowledge Discovery in Databases
  - The International AAAI Conference on Web and Social Media
  - Findings of the Association for Computational Linguistics: EMNLP
- Major
  - Machine Translation
  - International Joint Conference on Neural Networks
  - AMIA Annual Symposium
- Ordinary
  - Machine Learning for Healthcare Conference
  - ACM International Conference on Intelligent Computing and its Emerging Applications
  - Clinical Natural Language Processing
  - International Conference on Asian Language
  - IEEE International Conference on Emergency Science and Information Technology
  - Health Text Mining and Information Analysis
  - Language Resources and Evaluation Conference

# Journals
- Knowledge-Based Systems
- Applied Soft Computing
- Computer Methods And Programs in Biomedicine
- IEEE Transactions on Multimedia
- Journal of the American Medical Informatics Association Bioinformatics
- Scientific Reports
- Journal of Biomedical Informatics
- Data Intelligence
- JMIR Medical Education
- BMC Medical Informatics and Decision Making
- Arabian Journal for Science and Engineering
- Applied Sciences
- Irish Journal of Medical Science
- International Journal of Environmental Research and Public Health PLoS Digital Health
- Database
- arXiv/bioRxiv Preprint

# Contribution
- proactive, personalized, convenient healthcare
- improve clinical decision-making
- support **personalized medicine** and **evidence-based treatment plans** via extracting relevant information from unstructured data in medical records, literature, and research findings

# Challenges
- the lack of large, high-quality datasets
- specialized vocabulary
- ethical considerations
- regulatory bottlenecks
- healthcare involves complex decision making regarding diagnosis, treatment options, and follow-up care

# PLMs
- PLM(Pre-trained Language Model)
- 대규모 텍스트 데이터셋으로 pre-training된 언어 모델
- 언어 모델은 이를 통해 해당 텍스트 데이터셋의 단어와 구문 간의 통계적 관계를 학습, 이를 기반으로 Text Generation, Language Translation, Question Answering 등의 태스크를 수행할 수 있음
- PLM은 Self-Supervised Learning(SSL) 기술을 사용해 학습됨
  - SSL: LM에 학습 내용을 명시적으로 알려주지 않는 대신, 어떤 태스크(문장의 다음 단어 예측, 문장 간 유사도 판단 등)를 해야하는지 알려줌
- SSL을 통해 LM은 단어와 구문의 의미를 다운스트림 태스크에 맞게 표현(= Embeddings)하는 방법을 학습함
  - Embedding: 단어나 구문의 의미를 나타내는 숫자로 구성된, 수백 또는 수천 개의 차원으로 구성된 벡터
- LM은 pretraining 후 특정 태스크에 맞게 **Fine-Tuning** 할 수 있음
   - Fine-Tuning: 특정 태스크에 대한 Label이 지정된 데이터셋으로 학습시켜 해당 태스크에 대한 성능을 향상시킴
- Transfer Learning을 통해 다른 도메인에 사용할 수 있음
  - Transfer Learning
    - 특정 도메인에 학습된 신경망(PLM)의 가중치 값을 초기화하지 않고, 그 일부 능력을 유사하거나 전혀 새로운 분야에서 사용되는 신경망의 학습에 이용하는 방법
    - Transfer Learning 후 Fine Tuning

1. GPT (Generative Pre-trained Transformer)
   
     <img alt="Full_GPT_architecture" src="https://github.com/user-attachments/assets/ca124ef1-877e-4ecf-81b0-2b9656e27825" width="50%" height="50%"/>
     
   - Structure: Transformer의 Decoder 기반
   - Pre-Training Data: Unlabelled large-scale text corpora
   - Pre-Training Strategy
     - Autoregressive Training으로 모델이 마스킹이나 삭제없이 Unidirection(왼쪽>오른쪽)으로만 텍스트 예측
   - Text Generation 특화

2. BERT (Bidirectional Encoder Representations from Transformers)

     <img alt="BERT-size-and-architecture" src="https://github.com/user-attachments/assets/5d0c67aa-781b-4273-b56a-b7b27304752c" width="50%" height="50%"/>

   - Structure: Transformer의 Encoder 기반
   - Pre-Training Data: BooksCorpus (800M), English Wikipedia (2500M)
   - Pre-Training Strategy: MLM, NSP
     - Bidirectional Encoding을 사용해 Masked Language Modeling(MLM)을 사용해 단어의 왼쪽 오른쪽 문맥을 표현
       - MLM: 문장에서 단어를 Masking함으로써, 모델이 Masked 단어를 예측할 때 그 단어 양쪽에 있는 단어를 사용하도록 강제하여 텍스트에서 양방향 학습을 가능하게 함
   - 양방향성으로 인해 Language Understating에 특화

3. RoBERTa (Robustly optimized BERT)
   - BERT 기반
   - BERT의 다음 문장 예측 태스크 제거 등의 Tuning을 통해 BERT 개선

# Pre-Training method
- Masked Language Modeling(MLM) ... BERT
- Few-Shot Learning ... GPT 3
- Multitask Learning ... T5, mT5

- gradual unfreezing of layers
- differential fine-tuning rates
- stepwise unfreezing
     
# Applications of PLMs in medical fields
1. Generating Medical Texts
   - Patient Reports(환자 보고서), Discharge Summaries(퇴원 보고서), Clinical Trial Reports(임상시험 보고서)
2. Translating Medical Texts
3. Answering Medical Questions
   - valuable for doctors, patients, and researchers
4. Diagnostics
5. Developing New Treatment Methods
6. Personalised Medicine
   - personalized medicine by considering the individual characteristics of patients

# PLMs in Medical Fields

<img alt="Usage of various PLMs in various medical NLP tasks" src="https://github.com/user-attachments/assets/9ca8c38b-4db7-404d-9305-b537c1a18d32" width="50%" height="50%"/>

1. BERT: 문맥 표현과 단어 간 의미 관계 포착 능력
2. RoBERTa: BERT 보다 향상된 문맥 정보 포착 및 Entity 경계 모호성 처리 능력
3. BioBERT: BERT를 Biomedical corpora로 Transfer Lenarning
4. GPT-2
5. SciBERT, ChatGPT

# Question Answering System
- 현재 QAS 연구를 하고 있으므로, 이 부분만 리뷰

<img alt="PLMs-based model diagram for question answering system in medicine" src="https://github.com/user-attachments/assets/bccc5459-ebde-47b6-9ff9-796ed3255e25" width="50%" height="50%"/>

- 자연어 질문을 이해하고 정확하고 간결한 답변을 제공하도록 설계된 모델
- Goal: Human Understanding(특정 주제 또는 개념에 대한 지식 수준)과 Comprehension(의미를 파악하고 해석하는 능력)을 모방하여 기존 지식이나 데이터 소스를 기반으로 답변을 생성

## Method
1.Rule-based 
   - 미리 설정된 규칙에 따라 질문을 구문 분석하고 답변
   - keyword matching, information retrieval, pattern matching
2. Retrieval-based 
   - 인터넷이나 특정 DB와 같은 대규모 문서 모음에서 정보를 검색하여 질문과 관련된 답변을 찾음
   - Keyword Search, Relevance Assessment, Document Ranking
3. Knowledge Graph-based
   - 지식 그래프나 DB와 같은 구조화된 지식 소스를 사용하여 정확한 답변을 제공
   - Entity 간 관계와 속성을 이해
4. ML-based
   - 대규모 데이터셋에 대한 훈련을 통해 모델이 질문을 이해하고 답변하는 방법을 학습하도록 함
5. Hybrid
   - Retrieval-based + DL = RAG
6. Conversational and interactive Q&A
   - 개별 질문에 답변할 뿐만 아니라, 대화를 유지하면서 문맥이나 대화 기록을 기반으로 보다 관련성 있고 개인화된 답변을 제공

## Advantages of PLMs in building QAS for the Medical field
1. 대규모 텍스트 데이터로 사전 학습됨으로써, 풍부한 언어 지식과 자연어에 대한 깊은 이해를 바탕으로 의학적 질문을 잘 이해
2. BERT는 사전 학습에서 Bidirectional Context를 사용해 질문과 Passage의 맥락을 깊이있게 이해하여 의학적 질문에 대한 필수적인 정답을 추론할 수 있음
3. 뛰어난 문장 및 단어 Representation을 제공하여, 질문과 관련되는 의학 문서를 검색하고 의미와 그 의미 관계를 파악
4. 의학 텍스트 데이터(연구 논문, 전자 기록, 교과서 등)으로 Fine-Tuning 시, PLM을 의학 분야의 언어적 특성에 맞게 조정하고 의학 지식을 습득하게 함
5. Annotated QA dataset으로 Supervised Fine-Tuning 가능
6. Pre-trained representation을 사용하면 LM을 처음부터 학습시키는 것 보다 적은 데이터로 Medical QA 태스크에 효과적으로 적용할 수 있음

## Basic Application Steps

## Evaluation metrics

## Datasets

## Important research works
### Summary
### Main similarities and differences
### Limitations

