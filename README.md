# capstone-design-2
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
  
3. YOLOv5 모델 학습
- 전처리한 데이터를 가지고 YOLOv5 학습 및 테스트
- 객체 탐지 어느정도 구현

---

[2주차 해야할 것]
- 탐지된 객체를 잘라서 해당 라벨의 수치(체중, 골격근량, 체지방량)를 추출하기
- 추출한 데이터를 저장하여 특정 기준에 따른 C,D,I 형으로 분류하는 작업 - case 문 작성
- ...
  
