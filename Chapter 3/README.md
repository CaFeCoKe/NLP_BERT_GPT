# Chapter 3. Language model (언어모델)
- Language model (언어모델) : 단어 시퀀스에 확률을 부여하는 모델이다. 문장에서 i번째로 등장하는 단어를 w로 표시한다면 n개의 단어로 구성된 문장이 해당 언어에서
등장할 확률, 즉 n개의 단어가 동시에 나타날 결합확률(joint probability)을 다음 수식으로 나타낼 수 있다.<br><br>
![language](https://user-images.githubusercontent.com/86700191/161233050-3b15fdb9-5dfa-43a6-8509-745b679f432c.png)

    결합 확률는 조건부 확률(conditional probability)로도 나타낼 수 있다.<br><br>
    ![language01](https://user-images.githubusercontent.com/86700191/161262302-38174ffe-2305-4cae-83c3-2df2aca5d865.png)
<br><br>
    ![img](https://user-images.githubusercontent.com/86700191/161262306-a66b2d3d-0c11-4c9f-8074-32e45349d331.png)
<br><br>
    요약하면 전체 단어 시퀀스가 나타날 확률 = 이전 단어들이 주어졌을 때 다음단어가 등장할 확률의 연쇄가 된다. 이 떄문에 언어모델은 이전 단어들이 주어졌을 때 다음 단어가 나타날 확률을 부여하는 모델이라고도 할 수 있다.<br><br>

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

- Transformer (트랜스포머)<br><br>
  - Positional Encoding (포지셔널 인코딩) : RNN이 자연어 처리에서 유용했던 이유는 단어의 위치에 따라 단어를 순차적으로 입력받아 처리하기 때문에 각 단어의 위치 정보(position information)를 가질 수 있다는 점이다.
  하지만 트랜스포머는 단어 입력을 순차적으로 받는 방식이 아니므로 단어의 위치 정보가 없다. 따라서, 각 단어의 임베딩 벡터에 위치 정보들을 더하여 모델의 입력으로 사용하는데, 이를 포지셔널 인코딩(positional encoding)이라 한다.<br>
  포지셔널 인코딩의 값은 다음의 수식으로 결정 된다.<br>
  ![pe_math](https://user-images.githubusercontent.com/86700191/176399160-76919971-9498-421e-a401-1f83ec43f760.PNG) <br>
  트랜스포머는 사인 함수와 코사인 함수의 값을 임베딩 벡터에 더해주므로서 단어의 순서 정보를 더한다.<br><br>
  ![transformer7](https://user-images.githubusercontent.com/86700191/176399141-748532cb-1a95-48bf-ace4-83c908de644c.png) <br><br>
  이미지를 보면 pos는 입력 문장에서의 임베딩 벡터의 위치를 나타내며, i는 임베딩 벡터 내의 차원의 인덱스를 의미한다. 위의 식에 따르면 임베딩 벡터 내의 각 차원의 인덱스가 짝수인 경우에는 사인 함수의 값을 사용하고 홀수인 경우에는 코사인 함수의 값을 사용한다는 점을 알 수 있다.<br>
  따라서, 각 단어의 입력을 알아보기 쉽게 나열하면 다음과 같은 그림으로 설명할 수 있다. <br><br>
  ![transformer6_final](https://user-images.githubusercontent.com/86700191/176399151-9edadd44-7e72-45d5-bd8e-bacf5669c49c.png)
<br><br>

  - Sequence-to-Sequence (시퀀스-투-시퀀스) : 시퀀스란 단어 같은 무언가의 나열을 의미한다. 시퀀스-투-시퀀스는 특정 속성을 지닌 시퀀스를 다른 속성의 시퀀스로 변환하는 작업이다.
시퀀스-투-시퀀스 과제를 수행하는 모델은 인코더(encoder)와 디코더(decoder)의 2개 파트로 구성된다. 인코더는 소스 시퀀스의 정보를 압축하는 과정인 인코딩을 하여 만들어진 컨텍스트 벡터(context vector)를 디코더로 보내는 역할을 한다.
디코더는 타깃 시퀀스를 생성하는 과정인 디코딩을 하여 출력을 하게 된다. <br><br>
  ![seq2seq](https://user-images.githubusercontent.com/86700191/176364424-a7d03f32-8c8a-423d-a38c-618ba8cd96bd.png)
<br><br>
디코더에서는 인코더의 마지막 셀의 은닉상태인 컨텍스트 벡터를 첫번째 은닉 상태의 값으로 사용한다. 디코더의 첫번째 셀은 앞서 나온 컨텍스트 벡터(은닉 상태)의 값과 현재 입력 값으로부터 출력값을 예측하고 다음 시점의 입력값으로 넘겨주면서 은닉 상태를 넘겨주는 과정을 마지막 셀까지 반복한다.
(아래 예시는 LSTM으로 구성된 디코더)<br><br>
![seq2seq_decodet](https://user-images.githubusercontent.com/86700191/176366487-57f2c02e-35b4-4812-892d-0232240c6e31.png)
  <br><br>
    - 트랜스포머의 인코더-디코더
    ![transformer](https://user-images.githubusercontent.com/86700191/161271509-4fbb86d6-236a-45ff-9398-f61bc3f58963.png)
<br><br>
    - 모델 학습과 인퍼런스 : 인코더와 디코더의 입력이 주어졌을 때, 정답에 해당하는 단어의 확률값을 높이는 방식으로 학습한다.<br><br>
    ![transformer01](https://user-images.githubusercontent.com/86700191/161276568-20305e00-59ed-4177-9ad3-de0531d79fba.png)
    <br><br>
    여기에서 특이한 점이 하나 있다. 학습 중의 디코더 입력과 학습 후 모델을 실제로 사용할 때(인퍼런스)의 디코더 입력이 다르다는 점이다. 위 그림은 인퍼런스의 과정이다. <br>
학습 중의 디코더 입력은 직전 디코더의 출력결과인 정답 타깃 시퀀스로 이루어지지만, 인퍼런스 때의 디코더 입력은 직전 디코더 출력결과를 추가한 타깃 시뭔스로 이루어져 있다.
즉, 위 그림의 첫번째 과정에서 정답인 'I' 가 나왔다면 두번째 과정에서의 디코더 입력으로 'I'가 아닌 '&lt;s&gt; I'가 들어가게 된다.
<br><br>

  - Attention (어텐션) : 어텐션의 기본 아이디어는 디코더에서 출력 단어를 예측하는 매 시점(time step)마다, 인코더에서의 전체 입력 문장을 다시 한 번 참고한다는 것이다. 어텐션이 나온 배경은 RNN 기반 Seq2Seq 모델의 단점때문에 나오게 되었다.
이 단점은 크게 두가지로 하나의 고정된 크기의 벡터에 모든 정보를 압축하려고 하니까 정보 손실이 발생한다는 점과 RNN의 고질적인 문제인 기울기 소실(vanishing gradient) 문제가 존재한다는 점이다.<br><br>
    - Attention Function (어텐션 함수)<br><br>
    ![attention_func](https://user-images.githubusercontent.com/86700191/176368778-4907eb62-fcc2-4a38-8e11-d84d895a401d.png) <br><br>
    어텐션 함수를 수식으로 표현하면 `Attention(Q, K, V) = Attention Value`이다. 어텐션 함수는 '쿼리(Query)'에 대해서 모든 '키(Key)'와의 유사도를 각각 구하고 이것을 키와 맵핑되어있는 각각의 '값(Value)'에 반영한 다음 모두 더해 리턴한다. 이 리턴된 값을 어텐션 값(Attention Value)이라 한다.
    ```
       Q = Query : t 시점의 디코더 셀에서의 은닉 상태
       K = Keys : 모든 시점의 인코더 셀의 은닉 상태들
       V = Values : 모든 시점의 인코더 셀의 은닉 상태들
    ``` 

<br><br>

  - Self Attention (셀프 어텐션) : 어텐션은 시퀀스 중 중요한 요소에 집중하고 그렇지 않은 요소는 무시하여 태스크 수행 성능을 끌어 올리는 기법이다. 셀프 어텐션은
  입력 시퀀스 중 태스크 수행에 의미 있는 요소들 위주로 정보를 추출한다.<br><br>
    - CNN(합성곱 신경망)과의 비교 : CNN은 합성곱 필터를 사용하여 시퀀스의 지역적인 특징을 잡아내는 모델이다. 특정 단어를 기준으로 주변 문맥이 의미 형성에 중요한 역할을 한다.
따라서 합성곱 필터가 단어를 하나씩 넘기면서 읽어 낸다. 하지만 필터 크기를 넘어서는 문맥을 읽어내기 어렵다는 단점이 있다.<br><br>
![attention](https://user-images.githubusercontent.com/86700191/161284112-e2f30a51-bb75-4ef9-aa69-8fec079c8712.png)
<br><br>
    - RNN(순환 신경망)과의 비교 : RNN은 시퀀스 정보를 압축하는 것에 강점이 있는 모델이다. 하지만 시퀀스 길이가 길어질수록 정보 압축에 문제가 발생하여
초기에 입력된 단어는 잊어버리거나 특정 단어 정보를 과도하게 반영하여 전체 정보를 왜곡할 수가 있다. <br><br>
![attention01](https://user-images.githubusercontent.com/86700191/161286680-5c77fd04-8c1b-4600-966b-639645eee1d1.png)
<br><br>위와 같은 예시에서는 가장 늦게 들어오는 '많더라'에 대한 단어의 의미가 많이 반영 될수 밖에 없다. <br><br>
    - 셀프 어텐션의 계산법 : 셀프 어텐션은 쿼리(query), 키(key), 값(value) 3가지 요소가 서로 영향을 주고받는 구조이다. 트랜스포머 블록에는 문장 내 각 단어가 벡터형태로 입력된다.
해당 벡터에 쿼리, 키, 값을 만들어 주는 가중치 행렬을 행렬 곱으로 곱하여 쿼리벡터, 키 벡터, 값 벡터로 만든다. 다음 그림은 '카페'라는 쿼리 단어와의 문장 단어 관련도를 나타 낸 것이다.<br><br>
![attention02](https://user-images.githubusercontent.com/86700191/161295611-79e0cf3a-8f7b-48fb-a635-0a314f53f466.png)
<br><br>
이러한 결과에 셀프 어텐션 모듈은 값 벡터를 가중합(weighted sum)하는 방식으로 계산을 마무리 한다. '카페'벡터는 다음과 같이 나타낼 수 있다.<br><br>
![attention03](https://user-images.githubusercontent.com/86700191/161295613-1ca1fccf-276c-42f3-afc8-9ffae14d6895.png)
    - 인코더와 디코더에서의 셀프 어텐션<br><br>
    ![attention04](https://user-images.githubusercontent.com/86700191/161415215-da3dbcde-d05d-4126-8a0c-84a46f813f3c.png)
<br><br>

  - GPT 모델 : GPT의 모델 구조는 트랜스포머에서 인코더를 제외하고 디코더만 사용한다. 따라서 디코더 블록 내에 인코더에서 넘어오는 정보를 받는 멀티 헤드 어텐션도 사용하지 않는다.<br><br>
  ![GPT01](https://user-images.githubusercontent.com/86700191/161427371-ef1a2c55-c167-42bd-bb2e-5f448ecd3da7.png)
  <br><br>
  '거기'를 맞춰야 하는 상황에서 GPT 모델은 '어제'. '카페', '갔었어' 3개의 단어만 참고한다. 나머지 정답 단어 이후의 모든 단어는 참고를 할 수 없게끔 처리해준다. 
  이것을 마스킹(masking)이라고 하며, 값(value) 벡터들을 가중합 할 때, 참고할 수 없는 단어들이 0이 되도록 한다. 또한 모델 전체적으로 정답인 '거기'에 해당하는 확률은 높이고, 나머지 단어의 확률은 낮아지도록 업데이트 되게 된다.<br><br>
  ![GPT02](https://user-images.githubusercontent.com/86700191/161427372-1a773d35-6e39-4b17-95d3-96e46d40fa28.png)
<br><br>
  
  - BERT 모델 : BERT의 모델 구조는 GPT와 달리 트랜스포머에서 디코더를 제외하고 인코더만 사용한다. 따라서 인코더의 출력이 디코더의 멀티 헤드 어텐션으로 들어가지 않고 선형변환과 소프트맥스를 거쳐 출력이 된다.<br><br>
  ![BERT01](https://user-images.githubusercontent.com/86700191/161427374-6b4ad63a-4bb9-4ee9-b08d-69045fc7304b.png)
  <br><br>
  입력 단어 시퀀스가 '어제 카페 있었어 [MASK] 사람 많더라' 라고 가정해 보자면 마스크 토큰인 [MASK]에 대응 하는 단어를 찾아야 한다. 이 과정에서 GPT와는 달리 앞뒤 문맥을 모두 참고할 수 있다. 앞뒤 정보에 정답이 있는 것은 아니기 때문이다.
  또한 모델 전체적으로 정답인 '거기'에 해당하는 확률은 높이고, 나머지 단어의 확률은 낮아지도록 업데이트 되게 된다.<br><br>
  ![BERT02](https://user-images.githubusercontent.com/86700191/161427377-99af0bf0-b551-47f4-af65-08d3b1e69b39.png)
