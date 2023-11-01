![Untitled (2)](https://github.com/m1nddoong/capstone-design-2/assets/110027583/775288da-74af-4ad8-afb5-e0b566920f97)![Untitled](https://github.com/m1nddoong/capstone-design-2/assets/110027583/cad4fc5b-b7dd-46f3-8b6e-51ef870adcb2)# capstone-design-2
- 인바디 이미지 Weight, Muscle, Fat 객체 탐지

[Roboflow]
- https://app.roboflow.com/

<br>

>[참고 문헌] 
>- 깃헙 코랩 연동하기 : https://velog.io/@shong676/Colab%EA%B3%BC-GitHub-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0
>- [Object Detection] 누구나 쉽게 따라할 수 있는 YOLOv5 모델 학습하기 (커스텀 데이터) : https://mvje.tistory.com/111
>- YOLOv5 학습 커스텀데이터셋 : https://github.com/ldj7672/Deep-Learning-Tutorials/blob/main/YOLOv5/YOLOv5_%ED%95%99%EC%8A%B5_%EC%BB%A4%EC%8A%A4%ED%85%80%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%85%8B.ipynb
>- YOLOv5 Tutorial
>- [프로젝트를 위한 딥러닝] roboflow를 활용한 annotation: https://www.youtube.com/watch?v=75JFJUcZ3Yw
>

---

[1주차 완료 - 11/1]
1. 데이터 전처리
- roboflow 로 인바디 용지 데이터 라벨링(체중 : weight, 골격근량 : muscle, 체지방량 : fat)
- 데이터 증강(grayscale 등) : 80장 -> 230장
  
2. YOLOv5 모델 학습
- 전처리한 데이터를 가지고 YOLOv5 학습 및 테스트
- 객체 탐지 어느정도 구현

3. 필요한 점
- 새로운 입력 이미지가 들어왔을 떄, 우리가 학습한 YOLOv5 모델을 가지고 객체 탐지를 한 결과(라벨링 정보)값을 저장하는 과정 필요
- 이미지 데이터 처리 및 case 화 필요
---

[2주차 해야할 것]
- 탐지된 객체를 잘라서 해당 라벨의 수치(체중, 골격근량, 체지방량)를 추출하기
- 추출한 데이터를 저장하여 특정 기준에 따른 C,D,I 형으로 분류하는 작업 - case 문 작성
- ...

---


# 이미지 데이터 처리 및 case화 [by euichan]

담당자: 의찬 김, 민선익
상태: 진행 중

# 1. roboflow에서 라벨링된 데이터 처리

먼저 우리가 데이터로 가져온 인바디 이미지들은 각기 다른 크기를 가짐.

체중, 골격근량, 체지방량에 따른 라벨링 작업을 roboflow에서 처리완료.

roboflow에는 이미지에서 라벨링작업을 한 x좌표와 y좌표를 얻을 수 있다고 나옴.


![Untitled](https://github.com/m1nddoong/capstone-design-2/assets/110027583/62a4e5d4-0abe-4111-b3e2-5a0a38b3287b)


다음과 같이 이미지를 불러와 라벨링된 부분을 잘라내고

![Untitled (1)](https://github.com/m1nddoong/capstone-design-2/assets/110027583/7a435193-99ee-43f8-97dd-f51be6bed3a8)


그 이미지를 OCR을 통해 text 화 시키는 작업이 필요.

## 의문점

이미지의 크기가 각각 다르고 라벨링의 위치도 다를텐데 이미지 별로 라벨링의 x좌표와 y좌표를 일일이 수정해야하나?

## 해결방법

roboflow는 라벨링의 절대적인 좌표가 아닌 상대적인 좌표를 제공한다고 함.

따라서 이미지별로 각각의 좌표를 설정할 필요가 없이 

상대적인 좌표를 이용해서 이미지의 가로 세로 길이를 곱하여 절대적인 좌표로 변형시킨 후, 이미지를 자르는 작업이 가능함.

![Untitled (2)](https://github.com/m1nddoong/capstone-design-2/assets/110027583/bca388e9-0970-47dd-a114-93c5e7f50bd0)


따라서 이미지를 자른 후, 잘려진 각각의 라벨링 이미지를 가져와서 OCR을 적용해서 수치를 가져올 수 있다고 함.

## 데이터 저장

가져온 수치들 (weight ,muscle, fat)을 저장해야하는데 파이썬에서 리스트나 딕셔너리가 사용이 가능함.

pandas의 dataframe도 사용이 가능하다고 하는데 더 알아봐야 할 것 같음.

## 데이터를 case화

사용자에게 case별로 조언 및 운동 지도를 하기 위해서 우리는 case화 시켜야함.

그래프의 알파벳화 (C,D,I형) 이 애매모호하다는 결론하에

체중대비 골격근량, 체중대비 체지방량을 토대로 정해진 기준점과 비교하여 case화 할 예정.

예를 들어 기준점이 체중대비 골격근량이 50% 이상,이하 2가지일 경우

70kg인 사람의 골격근량이 35kg 이상이라면 , 골격근량이 어느정도 충분히 발달한 몸이라고 판단하고 골격근량이 35kg 이하라면, 골격근량이 부족하다는 판단 및 그에따른 솔루션,조언 제공 

(case는 구체적으로 알아보고 정할 예정 - 대략 3가지의 case)

→ 작업환경 : 구글 colab

# 해야할 일 정리

1. 먼저 roboflow에서 라벨링이 완료된 데이터들을 저장하기.
2. google colab 에서 위의 정리해놓은 코드를 참고하여 코드 작성.

→ 이미지 불러오기, 이미지 자르기 , OCR을 통한 텍스트 추출, 저장 , case화 시키기.
  
