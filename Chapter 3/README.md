# Chapter 3. Language model (언어모델)
- Language model (언어모델) : 단어 시퀀스에 확률을 부여하는 모델이다. 문장에서 i번째로 등장하는 단어를 w로 표시한다면 n개의 단어로 구성된 문장이 해당 언어에서
등장할 확률, 즉 n개의 단어가 동시에 나타날 결합확률(joint probability)을 다음 수식으로 나타낼 수 있다.<br><br>
![language](https://user-images.githubusercontent.com/86700191/161233050-3b15fdb9-5dfa-43a6-8509-745b679f432c.png)

    결합 확률는 조건부 확률(conditional probability)로도 나타낼 수 있다.<br><br>
    ![language01](https://user-images.githubusercontent.com/86700191/161262302-38174ffe-2305-4cae-83c3-2df2aca5d865.png)
<br>
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

- Transformer (트랜스포머)
  - sequence-to-sequence (시퀀스-투-시퀀스) : 시퀀스란 단어 같은 무언가의 나열을 의미한다. 시퀀스-투-시퀀스는 특정 속성을 지닌 시퀀스를 다른 속성의 시퀀스로 변환하는 작업이다.
시퀀스-투-시퀀스 과제를 수행하는 모델은 인코더(encoder)와 디코더(decoder)의 2개 파트로 구성된다. 인코더는 소스 시퀀스의 정보를 압축하는 과정인 인코딩을 하여 디코더로 보내는 역할을 한다.
디코더는 타깃 시퀀스를 생성하는 과정인 디코딩을 하여 출력을 하게 된다. 트랜스포머도 인코더와 디코더 구조를 따르며 이는 이렇게 세분화 시킬 수 있다.<br><br>
  ![transformer](https://user-images.githubusercontent.com/86700191/161271509-4fbb86d6-236a-45ff-9398-f61bc3f58963.png)
<br><br>
  - 모델 학습과 인퍼런스 : 인코더와 디코더의 입력이 주어졌을 때, 정답에 해당하는 단어의 확률값을 높이는 방식으로 학습한다.<br><br>
  ![transformer01](https://user-images.githubusercontent.com/86700191/161276568-20305e00-59ed-4177-9ad3-de0531d79fba.png)
  <br><br>
  여기에서 특이한 점이 하나 있다. 학습 중의 디코더 입력과 학습 후 모델을 실제로 사용할 때(인퍼런스)의 디코더 입력이 다르다는 점이다. 위 그림은 인퍼런스때의 과정이다. 
학습 중의 디코더 입력은 출력 단어의 전 단어들로 이루어진 정답 타깃 시퀀스로 이루어 지지만, 인퍼런스 때의 디코더 입력은 직전 디코더 출력결과를 추가한 타깃 시뭔스로 이루어져 있다.
즉, 위의 그림의 첫번째 과정에서 정답인 'I' 가 아닌 'you'가 나왔다면 두번째 과정에서의 디코더 입력으로 '&lt;s&gt; you'가 들어가게 된다.
<br><br>
  - self attention (셀프 어텐션) : 
  