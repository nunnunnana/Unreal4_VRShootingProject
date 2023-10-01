# Unreal4_VRShootingProject

### 언리얼로 제작한 VR 슈팅 프로젝트 입니다.

---

<img src="https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/345f7523-8d6e-477c-a01d-b2c7c3f56b63.png" width="800" height="500"/>

<img src="https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/b5a7d633-7697-44e7-955e-e633c795893d.png" width="800" height="500"/>

### [시연 영상](https://youtu.be/QfFVwr08LmE)

---

# 조작법
왼쪽 조이스틱 : 이동 
왼쪽, 오른쪽 그립 : 잡기
왼쪽, 오른쪽 트리거 : 사격

## 주요기능

### 이동 및 그랩
- 이동
  - Pawn 클래스는 VR 템플릿에 있는 MotionControllerPawn 액터 활용
  - 프로젝트 세팅 Input에서 키, 축 매핑 추가
  - AddMovementInput 노드를 사용해 이동 구현
- 그랩
  - PickupActorInterface 인터페이스 생성하고 PickUp, Drop 함수 추가
  - 상호작용할 액터에 인터페이스 이벤트 구현
  - 액터를 그랩했을 때 PickUp 이벤트 호출, 릴리즈 했을 때 Drop 이벤트 호출

![오리아나 궁극기](https://github.com/nunnunnana/Unreal4LOLProject/assets/99165741/5b7ce62a-9adb-4aa7-9c5e-b49d6a9d7a88)

- 블루프린트 코드

VR_Project_Pawn
>https://blueprintue.com/blueprint/jxch0yzb/

VR_Project_Weapon_Knife
>https://blueprintue.com/blueprint/b1o_9dyw/


### 사격 및 양손 그랩
- 사격
  - 인터페이스에 Tirgger 함수 추가
  - 상호작용할 액터에 Trigger 인터페이스 이벤트 구현
  - Trigger Press 이벤트가 호출되면 타이머 델리게이트 설정 후 Shoot 이벤트 실행
  - Trigger Release 이벤트가 호출되면 타이머 델리게이트 초기화
  - Shoot 이벤트가 호출되면 LineTrace 노드를 통해 총구 방향에서 range 값만큼 시작점과 도착점 설정 후 도착점에 충격을 가함
- 양손 그랩
  - 손잡이부분에 Collision 생성
  - 처음 액터를 그랩할 때 First Hand로 설정하고 손잡이 부분을 그랩할 때 Second Hand로 설정
  - Second Hand만 Detach하기 위해 인터페이스에 함수 추가

![오리아나 궁극기](https://github.com/nunnunnana/Unreal4LOLProject/assets/99165741/5b7ce62a-9adb-4aa7-9c5e-b49d6a9d7a88)

- 블루프린트 코드

VR_Project_Weapon_SMG11
>https://blueprintue.com/blueprint/7na6xdho/

VR_Project_Weapon_AK_VAL
>https://blueprintue.com/blueprint/r67rta_u/

>월드 상호작용

- 

>위젯 상호작용

- 

- 블루프린트 코드
