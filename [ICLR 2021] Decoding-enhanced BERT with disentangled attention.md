- DeBERTa paper

# Abstract
디스엔탱글드 어텐션 메커니즘과 향상된 디코딩 방식을 통해 텍스트의 의미를 더 잘 이해

# 특징

- **디스엔탱글드 어텐션(Disentangled Attention)**:
    - **설명**: 일반적인 트랜스포머 모델에서 어텐션 메커니즘은 위치 정보와 내용 정보를 결합하여 처리합니다. 반면, DeBERTa는 위치 정보와 내용 정보를 분리하여 각각을 독립적으로 처리합니다. 이를 통해 단어의 위치와 내용 간의 상관 관계를 더 정확하게 모델링할 수 있습니다.
    - **장점**: 문맥 내에서 단어의 의미를 더 잘 이해할 수 있으며, 특히 긴 문장이나 복잡한 문장에서 더 높은 성능을 발휘합니다.
- **향상된 디코딩(Enhanced Mask Decoder)**:
    - **설명**: DeBERTa는 텍스트 디코딩 과정에서 마스크된 언어 모델링(`MLM`)을 사용하여 문맥 정보를 더 잘 활용합니다. 이는 BERT의 마스크 언어 모델링과 유사하지만, 더 정교한 디코딩 전략을 통해 문장의 자연스러움을 높입니다.
    - **장점**: 자연스러운 텍스트 생성 및 문장 완성 작업에서 우수한 성능을 보입니다.
- **자체적 위치 임베딩(Absolute Position Embedding)**:
    - **설명**: DeBERTa는 위치 정보를 모델링하기 위해 절대 위치 임베딩을 사용합니다. 이는 문맥 내 단어의 상대적 위치를 더 잘 반영하여 텍스트 이해도를 높임
        - 모든 Transformation layer들의 직후, softmax layer 전단에 absoulte position 정보를 넣어줌. 이를 통해, Transformer가 elative position을 우선 고려하되, absolute position 정보도 보완 정보로 사용.
    - **장점**: 문맥 이해도를 높이고, 특히 긴 문장 처리에서 효과적
    
    <aside>
    📌 Absolute Position 정보
    
    - mask prediction에 중요함. 특히 뉘앙스 같은 것 파악에 중요.
    - BERT는 input 정보에 absolute position 정보를 넣는 방식임.
    </aside>

    # Method

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d3d50318-705b-4369-85f8-2f0d0d9603f7/9974d45b-893c-405f-838b-2c3fa59de222/Untitled.png)

# Experiment

- base model
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d3d50318-705b-4369-85f8-2f0d0d9603f7/beb7432f-a7ad-41cc-b160-fb2863d2b252/Untitled.png)
    
- large model
    - GLUE에서 다른 large model에 비해 좋은 성능 보임
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d3d50318-705b-4369-85f8-2f0d0d9603f7/40e41f65-ec28-45ed-b32a-9fbc09c7ce48/Untitled.png)
    

# 사용한 데이터셋

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d3d50318-705b-4369-85f8-2f0d0d9603f7/ad47ba38-ebce-4cd4-b23b-16f53d615c54/Untitled.png)

# model train parameter
