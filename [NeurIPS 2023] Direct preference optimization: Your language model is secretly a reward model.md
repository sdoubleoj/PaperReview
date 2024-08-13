# [NeurIPS 2023] Direct preference optimization: Your language model is secretly a reward model

### 핵심
- On-Policy Preference Data
  - On-Policy Data는 SFT로 생성한 데이터
  - DPO는 SFT Model의 분포를 Preference에 맞추는 Alignment Learning
  - 사용하고자 하는 Preference Data를 가지고 SFT를 먼저한 후(Positive 답변만 이용한다든지 등), DPO 수행해야 함. 그래야 원하는 Alignment Learning이 가능함.
- DPO의 약점
  - Preference Set이 고정되어 있기 때문에, offline 학습이 이뤄짐. 이에 따라 퍼포먼스 로스 발생.
  - Safety같은 복잡한 Preference는 어려움
