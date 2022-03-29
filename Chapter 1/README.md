# Chapter 1. Transfer Learning (전이 학습)
- Transfer Learning (전이 학습) : 특정 태스크를 학습한 모델을 다른 테스크 수행에 재사용하는 기법<br><br>
![transfer_learning](https://user-images.githubusercontent.com/86700191/160394941-8f05e644-1022-4d4c-a5b8-30fea5d11d9e.png)


- 업스크림 태스크 : 자연어의 문맥(context)을 모델에 내재화하는 것, 업스트림 태스크를 학습하는 과정을 사전학습(pre-train)이라 한다. 대표적인 과제로는 다음 단어 맟히기와 빈칸 채우기가 있다.
  - 다음 단어 맞히기 : GPT 계열 모델의 학습 수행방법이다. 예를 들어 학습 데이터(train data)에 '시작이 반'라는 구(phrase)가 많아 '시작이' 라는 문맥이 주어지면 학습을 통해 이전 문맥을 고려하여 다음에 올 단어로 '반'이 분류되도록 학습이 된다.<br><br>
  ![upstream](https://user-images.githubusercontent.com/86700191/160401510-70432e0c-ef62-414f-bbf9-c700ac185354.png)

  - 빈칸 채우기 : BERT 계열 모델의 학습 수행방법이다. 예를 들어 학습 데이터에 '공부 열심히 해라'라는 문장이 많아 '열심히'가 들어가야 할 자리를 빈칸으로 만들어 문맥이 주어지면 학습을 통해 앞뒤 문맥을 파악하여 '열심히'라는 단어가 분류되도록 학습이 된다.<br><br>
  ![upstream1](https://user-images.githubusercontent.com/86700191/160407567-f97f1ded-8d15-4448-909a-6ee02f25aa21.png)

- 다운스크림 테스크 : 자연어 처리의 구체적인 과제물이다. 사전학습을 마친 모델(업스크림 태스크)을 활용하여 학습을 진행한다. 대표적인 과제는 문서분류, 자연어 추론, 개체명 인식 등이 있다.
  - <dl>학습하는 방식
      <dt>fine-tuning</dt>
      <dd>다운스크림 태스크 데이터 전체를 사용하며, 데이터에 맞게 모델 전체를 업데이트한다.</dd>
      <dt>prompt tuning</dt>
      <dd>다운스크림 태스크 데이터 전체를 사용하며, 데이터에 맞게 모델의 일부를 업데이트한다.</dd>
      <dt>in-context learning</dt>
      <dd>다운스크림 태스크 데이터의 일부를 사용하며, 모델을 업데이트하지 않고, 바로 다운스트림 태스크를 수행한다. 3가지 방식으로 나누어진다.</dd>
      <ul>
        <li type="i">zero-shot learning : 다운스크림 태스크 데이터를 전혀 사용하지 않는다.</li>
        <li type="i">one-shot learning : 다운스크림 태스크 데이터를 1건만 사용하여 어떻게 수행되는지 참고한 뒤 다운스크림 태스크를 수행한다.</li>
        <li type="i">few-shot learning : 다운스크림 태스크 데이터를 일부만 사용하여 어떻게 수행되는지 참고한 뒤 다운스크림 태스크를 수행한다.</li>
      </ul>
  </dl>

  - 문서분류 : 자연어를 입력받아 해당 입력이 어떤 범주(긍정, 중립, 부정)에 속하는지 확률값을 반환한다. 사전학습이 된 마스크 언어 모델위에 작은 모듈을 하나 더 쌓아 문서 전체의 범주를 분류한다.<br><br>
  ![downscream01](https://user-images.githubusercontent.com/86700191/160618194-aae24451-6e73-4205-863f-79a6d9db14e8.png)
  - 자연어 추론 : 문장 2개를 입력받아 두 문장 사이의 관계가 어떤 범주(참, 중립, 거짓)에 속하는지 확률값을 반환한다. 사전학습이 된 마스크 언어 모델위에 작은 모듈을 하나 더 쌓아 두 문장의 관계 범주를 분류한다.<br><br>
  ![downscream02](https://user-images.githubusercontent.com/86700191/160618202-b8fee884-96dc-483a-ba0c-840a5ec4484f.png)
  - 개체명 인식 : 자연어를 입력받아 단어별로 어떤 개체명 범주에 속하는지 확줄값을 반환한다. 사전학습이 된 마스크 언어 모델위에 작은 모듈을 하나 더 쌓아 단어 각각의 개체명 범주를 분류한다<br><br>
  ![downscream03](https://user-images.githubusercontent.com/86700191/160618204-45246f69-a1a1-4208-8a6d-b726396c3dc4.png)
  - 질의응답 : 질문과 지문으로 이루어진 자연어를 입력받아 각 단어 중 정답의 시작과 끝일 확률값을 반환한다. 사전학습이 된 마스크 언어 모델위에 작은 모듈을 하나 더 쌓아 전체 단어 가운데 어떤단어가 시작인지, 끝인지 분류한다.<br><br>
  ![downscream04](https://user-images.githubusercontent.com/86700191/160618205-31120e87-1ebb-4c37-b452-91692d701d72.png)
  - 문장생성 : 자연어를 입력받아 어휘 전체에 대한 확률값(입력 문장 다음에 올 단어로 얼마나 적절한지에 대한 값)을 반환한다. 사전학습이 된 언어 모델을 그대로 사용하여 문맥에 이어지는 적절한 다음 단어를 분류한다.<br><br>
  ![downscream05](https://user-images.githubusercontent.com/86700191/160618208-de3b03df-945b-44e2-92a3-d6ebad26b99a.png)
