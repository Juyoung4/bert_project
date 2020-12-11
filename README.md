## BERT 모델 Pipeline ##


1. 데이터 셋 준비

    * **[For pretraing BERT DATASET]** 데이터셋 information확인 및 txt파일 csv파일로 저장<br>
    => **prepare_data/paper_text_to_csv.py** <br>
    => **prepare_data/Dataset_information.ipynb**

    * **[For QA fine tuning BERT DATASET]** csv질의응답 파일을 json형식[Korquad]으로 변경하여 저장 <br>
    => **prepare_dataset/make_json.py**

2. 데이터 셋 전처리

    * **코드** : **data_preprocessing_code\Data_preprocessing.ipynb**
    * **과정** <br>
    [csv dataset 불러오기] -> [Preprocessing] -> [Pretraining Dataset 구축(합치기)] -> [Additional Preprocessing] -> [문단을 문장단위로 자르기(\n)]

    * [1] preprocessing
        - tag 전처리 : <>, &--;, $--$, $--; &--;
        - 한자 제거
        - 영어, 숫자, 연산 기호만 남기기
        - 다중 띄어쓰기 제거
    
    * [2] 문단을 문장단위로 자르기(\n)

    * [3] text file 분할
        - 충분한 자원을 가지고 있다면 진행 X
    
    (+) Additional preprocessing<br>
     - 한글 스펠링 체크 이용
     - **코드** : **data_preprocessing_code\spell_check.ipynb**

3. vocab file 만들기

    - [방법 1] : 한국어+영어+숫자+특수문자 모두 wordpiece이용

    - [방법 2] : 한국어는 형태소 분석기 + 영어는 wordpiece + 숫자/문자는 직접 추가