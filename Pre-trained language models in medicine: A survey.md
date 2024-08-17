# PLM
BERT, ChatGPT, ClinicalBERT, BioBERT, RoBERTa, etc.

# Pre-Training method
- Masked Language Modeling(MLM) ... BERT
- Few-Shot Learning ... GPT 3
- Multitask Learning ... T5, mT5

# Benchmark
- GLUE
- SQuAD

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
  - Embedding: 단어나 구문의 의미를 나타내는 숫자로 구성된 벡터
- 
  
