# NLP_BERT_GPT
[Do it! BERT와 GPT로 배우는 자연어 처리](http://www.easyspub.co.kr/20_Menu/BookView/B001/481/PUB) 를 기반으로 자연어 처리를 공부합니다.

 - 기본 베이스 코드 : https://ratsgo.github.io/nlpbook/docs/tutorial_links
 - 코드에 사용되는 패키지 : https://github.com/ratsgo/ratsnlp
 - 사용하는 기본 라이브러리
   - [Pytorch](https://pytorch.org/docs/stable/torch.html)
   - [Pytorch-lightning](https://pytorch-lightning.readthedocs.io/en/latest/api_references.html)
   - [Transformers](https://huggingface.co/docs/transformers/index)

 
- 유의점 (2022 / 04 / 15 추가)<br><br>

   문제점 : ImportError<br><br>
![error](https://user-images.githubusercontent.com/86700191/163578418-40cbbee6-2eba-4192-b2c2-67c77f4fda5b.PNG)
<br><br>
이유 : ratsnlp 패키지의 `requirements.txt`로 설치되는 PyTorch-Lightning 버전 노후화 (ver.1.3.4 사용)<br><br>
![requirement](https://user-images.githubusercontent.com/86700191/163578709-68fb1b38-bb38-4e0d-a12f-e7dde3a80d4c.PNG)
<br><br>
현재 PyTorch-Lightning의 최신버전은 1.6.1이다. 여기서 버전 1.3.4는 `_init_.py`에 [metrics](https://github.com/PyTorchLightning/metrics) 를 import하며 그 이후로
`torchmetrics/utilities/data.py`의 `get_num_classes` 함수를 가져오는 코드가 포함 되어있다. 해당 부분이 문제가 된다. ratsnlp 패키지는 따로 metrics 버전을 지정하지 않아 PyTorch-Lightning에서 자동으로 최신버전으로 설치된다.
2022 / 04 / 14 에 metrics의 버전이 0.7.0에서 0.8.0으로 패치가 되면서 
해당 함수가 삭제가 되었다. 따라서 ImportError가 뜨게 된다.<br><br>
![error_reason](https://user-images.githubusercontent.com/86700191/163580686-71c217f2-d30a-46df-8e7b-90aa49e14359.PNG)
<br><br>
해결방법 1. PyTorch-Lightning의 버전을 업그레이드 시킨다. (2022 / 04 /15부터 commit한 Chapter 7 부터 적용)
    ```consol
    !pip install ratsnlp
    !pip install --upgrade pytorch-lightning
    ```

    PyTorch-Lightning의 버전중 1.5.0 부터 `_init_.py`에 metrics를 import하지 않는다. 따라서 버전 1.5.0 이상으로 업그레이드시 위의 문제점으로 인한 에러는 뜨지 않게 된다.<br><br>
![error_lightning](https://user-images.githubusercontent.com/86700191/163581290-1387d3da-599a-45fc-afd6-5b2be8c17ead.PNG)
![remove_metrics](https://user-images.githubusercontent.com/86700191/163581272-e00025b7-f932-40f5-9593-8a1bbb2c447c.PNG)
<br><br>
해결방법 2. ratsnlp 패키지를 설치 후 자동으로 설치된 metrics를 삭제후 0.7.0 버전으로 재설치 한다.
    ```consol
    !pip install ratsnlp
    !pip uninstall torchmetrics
    !pip install torchmetrics==0.7.0
    ```