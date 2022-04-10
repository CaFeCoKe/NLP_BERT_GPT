# Chapter 5. Sentence pair Classification

## - 알고리즘 순서도

## - BERT(Bidirectional Encoder Representations from Transformers) 구성<br><br>
![BERT1](https://user-images.githubusercontent.com/86700191/162573508-b39e3bd1-cbbd-4b2d-abf7-f6b6554b4762.png)

## - 결과
- 학습 과정 결과<br><br>
![학습결과](https://user-images.githubusercontent.com/86700191/162573511-5f257988-1636-45a0-a0ee-a789616bd141.PNG)
<br><br>
- 입력한 문장 관계 판단 결과<br><br>
![결과2](https://user-images.githubusercontent.com/86700191/162573514-cbbcf0df-1255-4975-b82b-7299d0680418.PNG)
![결과](https://user-images.githubusercontent.com/86700191/162573513-6e02659f-9535-4755-b390-374a3453a6ef.PNG)

## - 사용한 언어 모델, 데이터
- [KcBERT](https://github.com/Beomi/KcBERT) : 사전 학습 모델
- KLUE-NLI [(홈페이지)](https://klue-benchmark.com/tasks/68/overview/description) / [(깃허브)](https://github.com/KLUE-benchmark/KLUE) : 파인튜닝 데이터