# [NeurIPS 2023] Direct preference optimization: Your language model is secretly a reward model

### 핵심
- On-Policy Preference Data
  - On-Policy Data는 SFT로 생성한 데이터
  - DPO는 SFT Model의 분포를 Preference에 맞추는 Alignment Learning
  - 사용하고자 하는 Preference Data를 가지고 SFT를 먼저한 후(Positive 답변만 이용한다든지 등), DPO 수행해야 함. 그래야 원하는 Alignment Learning이 가능함.
- DPO의 약점
  - Preference Set이 고정되어 있기 때문에, offline 학습이 이뤄짐. 이에 따라 퍼포먼스 로스 발생.
  - Safety같은 복잡한 Preference는 어려움

- DPO paper
- Reinforcement Learning, Preference Alignment Learning, Fine-tuning

# Abstract
- LM을 Pre-training 시키는 과정은 Unsupervised이기 때문에, LM의 행동을 정밀하게 제어하기 어려움.
- 기존에는 RLHF을 통해 LM에 대한 Steerability를 확보했음.
  - RLHF(Reinforcement Learning from Human Feedback)
    - ML에서 인간의 피드백으로부터 직접 ReWard Model을 학습시키고, 해당 모델을 Reward Objective로 사용하여 Proximal Policy Optimization와 같은 최적화 알고리즘을 통해 RL을 사용하여 에이전트의 Policy를 최적화하는 기술
  그러나 RLHF는 학습 과정이 복잡하고 불안정함.
- 본 논문은 RLHF의 Reward Model을 Reparameterize하여, Optimization Policy를 Closed Form으로 추출함.
  결과적으로 간단한 Classification Loss만으로 RLHF를 수행할 수 있게 함.
- DPO 알고리즘의 장점
  1. 안정적이며 높은 성능
  2. 적은 계산량
  3. fine-tuning이나 hyperparameter tuning 과정에서 LM에서 샘플링 불필요
  4. 간단한 구현 및 훈련
  5. control sentiment of generation에서 PPO 기반 RL 능가
  6. summarization과 single-turn dialogue에서 응답의 품질 일치 및 개선

# Introduction

# Related Work

# Preliminaries

## SFT
## Reward Modeling Phase
## RL Fine-Tuning Phase

# Direct Preference Optimization
## DPO Objective 유도 과정
## DPO Update

# Theoretical Analysis of DPO

# Experiment

## Task 1. Sentiment Generation
## Task 2. Single-Turn Dialogue
## Evaluation
## Method
## Unlikelihood
