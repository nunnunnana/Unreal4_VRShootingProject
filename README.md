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
  
![VRShooting이동및그랩](https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/e2f62cfd-1705-422b-a670-b7154d440d53)


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
  
![VRShooting사격](https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/279b4c67-b653-4c7f-a3cc-d1bd4cbfc65a)


- 블루프린트 코드

VR_Project_Weapon_SMG11
>https://blueprintue.com/blueprint/7na6xdho/

VR_Project_Weapon_AK_VAL
>https://blueprintue.com/blueprint/r67rta_u/


### 월드 상호작용
- Door
  - Trigger에 들어오면 Door Open하고 자동으로 게임 시작
- Bot
  - Actor가 파괴되면 BP_Menu 액터에 KillCount 이벤트 호출

![VRShooting월드상호작용](https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/a70d6ea5-e954-4657-ac7c-cac863af5766)


- 블루프린트 코드

BP_Door
>https://blueprintue.com/blueprint/i_16f5mg/

BP_Bot_Actor_DM
>https://blueprintue.com/blueprint/_m87lq1i/


### 위젯 상호작용
- 버튼 상호작용
  - 버튼에 Collision을 생성하고 MotionController의 Finger Sphere가 Overlap되면 Button의 Location과 Finger Sphere의 Location을 비교해 Press_Distance 보다 작아지면 Press 이벤트 실행
  - Inverse Transform Location 노드를 사용해 Button Actor를 기준으로 Finger Sphere를 로컬 좌표계로 변환, Press Distance 만큼의 버튼이 눌리는 정도를 로컬 좌표계로 변환해 버튼의 Z값으로 Location 설정
  - Controller가 End Overlap 되면 Tick Event의 Gate를 Close하고 버튼을 초기 위치로 변경
  - 버튼이 Press 됐을 때 실행할 Button_Action 이벤트는 상속받은 클래스에서 오버라이드하여 사용
- 메뉴
  - BP_Menu에는 상호작용 가능한 버튼 3개와 Timer, Count, Score 텍스트 컴포넌트로 구성
  - Bot_Actor가 파괴 될 때 마다 Kill Count에 +1 모든 봇을 파괴하면 스톱워치를 종료하고 Score 출력
  - Time에 따라 Score 출력 변경

![VRShooting위젯상호작용](https://github.com/nunnunnana/Unreal4_VRShootingProject/assets/99165741/dc54e4f0-621a-40ea-bcf4-d4fa859154f5)


- 블루프린트 코드

BP_Button_Parent
>https://blueprintue.com/blueprint/bg1valos/

BP_Menu
>https://blueprintue.com/blueprint/qvry7efa/

BP_Button_Start
>https://blueprintue.com/blueprint/qreb_nve/

BP_Button_Restart
>https://blueprintue.com/blueprint/c6ps8vpz/

BP_Button_Quit
>https://blueprintue.com/blueprint/jb7_wr1n/
