# Chapter 4. Document Classification
 사전학습 모델으로 [KcBERT](https://github.com/Beomi/KcBERT) 를 사용하고, [NSMC(네이버 영화 리뷰 말뭉치)](https://github.com/e9t/nsmc) 으로 파인튜닝(Fine-tuning)을 하여 
입력된 문장이 영화 리뷰라 생각하고 긍정/부정의 성격을 분석한다.

## - 알고리즘 순서도
![BERT_Algorithm](https://user-images.githubusercontent.com/86700191/162433360-76eea65f-9982-48fa-8658-59b8813a5868.png)

## - BERT(Bidirectional Encoder Representations from Transformers) 구성<br><br>
![BERT](https://user-images.githubusercontent.com/86700191/162212775-9cf0242b-c437-4bae-954d-1e095255b34e.png)

## - 결과
- 학습 과정 결과<br><br>
![train](https://user-images.githubusercontent.com/86700191/162215657-693a74bd-6ea8-4bc2-a429-ea70eb0121e8.PNG)
<br><br>
- 입력한 문장 극성 판단 결과<br><br>
![inference2](https://user-images.githubusercontent.com/86700191/162215663-42d212e2-ee24-4f1c-9256-907de44af960.PNG)