# Chapter 8. Sentence Generation

## - 알고리즘 순서도<br><br>


## - GPT(Generative Pre-trained Transformer) 구성<br><br>


## - 결과
- 학습 과정 결과<br><br>
![train_result](https://user-images.githubusercontent.com/86700191/163935978-26f236fc-4ab4-4737-99ab-732c6a9a274a.PNG)
<br><br>
-  결과 (입력 : 노란 박스)
    - 잘못된 인수 설정<br><br>
   ![result_wrong](https://user-images.githubusercontent.com/86700191/163935982-2f7d9b2e-6e7f-4cac-a303-a105d290d9ca.PNG)
<br><br>
    - 긍정 라벨의 말뭉치 입력 (결과는 매변 달라짐)<br><br>
    ![result_pos1](https://user-images.githubusercontent.com/86700191/163935983-f46ed78e-9b68-416c-b5b6-986324d3285c.PNG)
    ![result_pos2](https://user-images.githubusercontent.com/86700191/163935988-c523540e-d23a-411f-9078-48802f8841a3.PNG)
<br><br>
    - 긍정 라벨의 말뭉치 입력 (결과는 매변 달라짐)<br><br>
    ![result_neg1](https://user-images.githubusercontent.com/86700191/163935994-46312708-80ef-4b5a-85d3-dbd105de1475.PNG)
    ![result_neg2](https://user-images.githubusercontent.com/86700191/163935997-96e7bccf-f055-4ab5-b884-7275067a8d87.PNG)

## - 사용한 언어 모델, 데이터
- [KoGPT2](https://github.com/SKT-AI/KoGPT2) : 사전 학습 모델
- [NSMC](https://github.com/e9t/nsmc) : 파인튜닝 데이터