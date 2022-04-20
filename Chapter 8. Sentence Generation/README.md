# Chapter 8. Sentence Generation

## - 알고리즘 순서도<br><br>


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
  - 1D-Convolution Layer (Conv1D)

  - Output (generator_ids)


## - 사용한 언어 모델, 데이터
- [KoGPT2](https://github.com/SKT-AI/KoGPT2) : 사전 학습 모델
- [NSMC](https://github.com/e9t/nsmc) : 파인튜닝 데이터