### Abstract

- LLM이 명시적으로 생성해 내는 Explanation/Rationale과 LLM 의 최종 판단 사이의 관계성을 분석하고, 이를 통해 LLM 신뢰성을 직간접적으로 평가하고자 하는 시도

### Introduction

- CoT 등의 방법론으로 생성해 내는 LLM이 자연어 설명이나 추론 과정은 Sound Plausible
- 그러나 모델의 최종 판단에 실질적으로 영향을 준 요인들과 모델이 생성해 낸 설명이 얼마나 일치하는지는 불명확
    
    ⇒ 본 논문에서 상관적 설명 신뢰성(Correlational Explanatory Faithfulness, CEF)이라는 새로운 평가 메트릭을 제안하여 좀 더 정교하게 모델의 판단과 설명을 평가
    

### Related Work

- Atanasova et al. (2023)의 반사실 테스트(Counterfactual Test, CT)
    - CT는Input Query에 일부 텍스트를 삽입하는 방법론(Interventional Addition, IA)을 사용
    - CT-Unfaithfulness는 Model Explanation에 대한 평가 지표
    - 삽입된 일부 텍스트로 인해 모델 예측이 변경되었을 때, 모델이 생성한 설명에 추가된 내용이 언급되지 않는 경우 해당 설명이 Unfaithful하다고 보는 것
    - (1) 모델의 최종 예측이 변경되었을 때에만 IA가 유효했다고 판단하며, (2) 설명이 IA를 언급하는지 여부를 이진법으로 측정 (Classification Threshold = 0.5로 상정)
    - 한계
        - 만약 모델이 Context 전체를 설명으로 포괄하여 생성해버리면, 낮은 설명 퀄리티임에도 불구하고 해당 설명은 Faithful하다고 판단
        - 모델 예측의 변화 폭은 고려하지 않음
        
        ⇒ 모델이 생성한 설명과 실제 예측 사이의 관련성을 CT 방법론에 반영하는 것이 필요
        
        ⇒ CEF (Correlational Explanatory Faithfulness) 평가 메트릭 제안
        

### Method

- CEF
    - Intervention* Impact**와 Explanation Mention***의 관련도를 Pearson Correlation으로 측정하는 방법론
        
        * Intervention: 단어를 삽입해 input query를 변형하는 것
        
        ** Intervention Impact: 모델의 Prediction에 대한 Intervention의 유효성
        
        *** Explanation Mention: 모델이 설명에서 Intervention을 중요하게 다루는 정도
        
    
    ![CEF 메트릭 예시: Intervention 전후 모델 예측과 설명 변화 측정](https://github.com/user-attachments/assets/c97b0dd1-da2f-400e-995f-0364c2702f2b)
    
      CEF 메트릭 예시: Intervention 전후 모델 예측과 설명 변화 측정
    
    - Intervention: 단어를 삽입해 input query를 변형하는 것
        - 모델의 Intervention 전후 Predictions에 대한 Total Variation Distance (TVD)로 측정
        - TVD를 통해서 해당 Intervention이 모델 예측에 얼마나 영향을 주었는지를 수치화할 수 있음
            
            ![TVD 값과 Inserted Text 가 모델에 미친 영향의 상관관계](https://github.com/user-attachments/assets/13ff80ce-a64e-4f4d-a8ac-941304ab52d9)
            
              TVD 값과 Inserted Text 가 모델에 미친 영향의 상관관계
            
    - Mention importance: CT 방법론에서 사용했던 언급 유무 기준의 이진법을 사용
        - 이에 따라 CEF는 점 이분 상관 계수로 측정될 수 있음

### E**xperimental Result & Conclusion**

- 본 논문에서는 CEF 메트릭과 CT 방법론을 적용하여, 상관적 반사실 테스트(Correlational Counterfactual Test, CCT)를 제안하고 Llama2 모델을 3개의 대표적인 Classification Benchmark 인 e-SNLI, ComVE, ECQA에 대해서 테스트함

![3가지 벤치마크에서 기존 CT 방법론 및 CCT로 측정한 Faithfulness 성능 비교](https://github.com/user-attachments/assets/b8665d3d-c766-43bc-bf08-30a61882e9ae)

    3가지 벤치마크에서 기존 CT 방법론 및 CCT로 측정한 Faithfulness 성능 비교

- ECQA는 모델의 설명이 Intervention에 대해 거의 언급하는 경향을 보이지만, 해당 Intervention이 모델의 예측에는 거의 영향을 주지 않는 것을 확인할 수 있음. 즉, 모델에게 중요했던 부분이 무엇이었는지 설명에 전혀 반영되지 않았다고 해석. CCT는 이 부분을 수치화해서 표현할 수 있음을 확인
