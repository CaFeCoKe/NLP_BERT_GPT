# Chapter 8. Sentence Generation

## - 알고리즘 순서도<br><br>
![GPT_Algorithm](https://user-images.githubusercontent.com/86700191/164381961-fe2e4d8f-e30f-4097-9df8-318250cfde21.png)

## - GPT(Generative Pre-trained Transformer) 구성<br><br>
![GPT2](https://user-images.githubusercontent.com/86700191/164159943-6834c8c9-dc23-407d-89d2-7f3cfce773c4.png)

## - 결과
- 학습 과정 결과<br><br>
![train_result](https://user-images.githubusercontent.com/86700191/163935978-26f236fc-4ab4-4737-99ab-732c6a9a274a.PNG)
<br><br>
- 결과 (입력 : 노란 박스)
    - 잘못된 인수 설정<br><br>
   ![result_wrong](https://user-images.githubusercontent.com/86700191/163935982-2f7d9b2e-6e7f-4cac-a303-a105d290d9ca.PNG)
<br><br>
    - 긍정 라벨의 말뭉치 입력 (결과는 매변 달라짐)<br><br>
        <table border = "0">
        <tr>
            <td><img src="https://user-images.githubusercontent.com/86700191/163935983-f46ed78e-9b68-416c-b5b6-986324d3285c.PNG" width="100%" height="100%"></td>
            <td><img src="https://user-images.githubusercontent.com/86700191/164159717-52e1837b-d2e8-4c84-9bc6-4841f1e0276e.PNG" width="100%" height="100%"></td>
        </tr>
        </table><br>

  - 부정 라벨의 말뭉치 입력 (결과는 매변 달라짐)<br><br>
        <table border = "0">
        <tr>
            <td><img src="https://user-images.githubusercontent.com/86700191/163935994-46312708-80ef-4b5a-85d3-dbd105de1475.PNG" width="100%" height="100%"></td>
            <td><img src="https://user-images.githubusercontent.com/86700191/163935997-96e7bccf-f055-4ab5-b884-7275067a8d87.PNG" width="100%" height="100%"></td>
        </tr>
        </table>

##  - 유의점
  - 1D-Convolution Layer (Conv1D) : GPT2에 사용되는 `Conv1D`는 `transformers/pytorch_utils.py`에 클래스로 작성되어있다. Pytorch의 `torch.nn.Conv1d`와는 input, output의 인수입력의 순서가 반대라는 점을 유의 해야한다.
`torch.nn.Conv1d`는 input, ouput의 순서, `Conv1D`는 output, input의 순서로 작성된다. <br>
BERT는 Linear Layer(fully-connected layer) 쓰는 반면, GPT2는 1D-Convolution Layer를 사용하는데 기능적으로는 Linear Layer와 차이가 없다. 단, weight가 transpose되어 계산되는 점이 차이점이다.
<br><br>
  - Output (generator_ids) : 테스크에서 테스트용으로 새로운 말뭉치를 입력 시 토큰화+인코딩을 하여 모델에 입력된다. 그리고 multinomial sampling (다항 분포)를 통해 generator_ids를 출력으로 내놓는다. 
generator_ids[0]에 모델이 예측한 말뭉치 이후의 문장의 토큰ID 시퀀스이기 때문에 이것을 디코딩해야 우리가 알아볼 수 있는 언어(문장)로 변환시킬 수 있다.


## - 사용한 언어 모델, 데이터
- [KoGPT2](https://github.com/SKT-AI/KoGPT2) : 사전 학습 모델
- [NSMC](https://github.com/e9t/nsmc) : 파인튜닝 데이터

## - 참고 사이트
- [GPT2의 흐름에 따른 Tensor 변화](https://jalammar.github.io/illustrated-gpt2/) : GPT 구성과 함께 보는 것을 추천
- [1D-Conv vs Linear](https://wandb.ai/wandb_fc/pytorch-image-models/reports/Are-fully-connected-and-convolution-layers-equivalent-If-so-how---Vmlldzo4NDgwNjY) : 유의점의 1D-Convolution Layer과 함께 보는 것을 추천
