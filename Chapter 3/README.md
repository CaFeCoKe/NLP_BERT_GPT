# Chapter 3. Language model (언어모델)
- Language model (언어모델) : 단어 시퀀스에 확률을 부여하는 모델이다. 문장에서 i번째로 등장하는 단어를 w로 표시한다면 n개의 단어로 구성된 문장이 해당 언어에서
등장할 확률, 즉 n개의 단어가 동시에 나타날 결합확률(joint probability)을 다음 수식으로 나타낼 수 있다.<br><br>
![language](https://user-images.githubusercontent.com/86700191/161233050-3b15fdb9-5dfa-43a6-8509-745b679f432c.png)

    결합 확률는 조건부 확률(conditional probability)로도 나타낼 수 있다.<br><br>
    ![language01](https://user-images.githubusercontent.com/86700191/161262302-38174ffe-2305-4cae-83c3-2df2aca5d865.png)
![img](https://user-images.githubusercontent.com/86700191/161262306-a66b2d3d-0c11-4c9f-8074-32e45349d331.png)
<br><br>
    요약하면 전체 단어 시퀀스가 나타날 확률 = 이전 단어들이 주어졌을 때 다음단어가 등장할 확훟의 연쇄 가 된다. 이 떄문에 언어모델은 이전 단어들이 주어졌을 때 다음 단어가 나타날 확률을 부여하는 모델이라고도 할 수 있다.<br><br>

    - 순방향 언어 모델 (forward language model) : 이전 단어들이 주어졌을 때 다음단어 맞히기 과정으로 문장 앞부터 뒤로 순서대로 계산하는 모델이다.<br><br>
  ![language02](https://user-images.githubusercontent.com/86700191/161266363-952870c7-2bd7-48db-b8af-a77db3e660ae.png)
  <br><br>
    - 역방향 언어 모델 (backward language model) : 이전 단어들이 주어졌을 때 다음단어 맞히기 과정으로 문장 뒤부터 앞로 순서대로 계산하는 모델이다.<br><br>
  ![language03](https://user-images.githubusercontent.com/86700191/161266369-a39d54e2-d0e9-4ad9-9bac-b321fdbac6e4.png)
  <br><br>
    - 마스크 언어 모델 (masked language model) : 학습 대상 문장에 빈칸을 만들어 빈칸에 올 단어가 무엇일지 분류하는 모델이다.<br><br>
  ![language04](https://user-images.githubusercontent.com/86700191/161266371-0cd7028c-9ebc-4c3c-8711-1d0ff36c84fd.png)
  <br><br>
    - 스킵-그램 모델 (skip-gram model) : 어떤 단어 앞뒤에 특정 범위를 정해두고 그 단어 주변에 어떤 단어들이 분포해 있는지를 락습하는 모델이다.<br><br>
  ![language05](https://user-images.githubusercontent.com/86700191/161266372-c865357b-64a8-4499-b564-f5aee58aa2d4.png)
  <br><br>