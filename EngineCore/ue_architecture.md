필독:
https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/
  
![image](https://user-images.githubusercontent.com/63915665/170287876-0db00cd8-0d29-41d1-aad9-8eb9a9a76a6f.png)
  
![image](https://user-images.githubusercontent.com/63915665/170291503-e32df753-bae5-4a5c-a7cc-c13844c047eb.png)
  
  
### AGameMode (GameMode)
게임모드 오브젝트로, 가장 코어가 되는 게임 로직을 처리하는 것을 담당한다.  
모든 게임은 하나 이상의 게임 모드 오브젝트를 가져야 한다.  
참고: https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Framework/GameMode/
  
  
### AGameStateBase (GameState)
게임스테이트 오브젝트. 게임모드보다 더 자주 변경해야 하는 정보들(게임모드의 경우 데이터 변경이 일반적으로 잦지 않다), 특히 클라이언트와 서버가 계속 동기화해야 하는 정보들의 경우 여기 저장된다. 
  
  
### APlayerController (Player Controller)
플레이어의 컨트롤 입력을 받아 Pawn을 조종하는 오브젝트.  
프로젝트 생성 시 Stock으로 하나 만들어져있다.  
APlayerController가 있어야 아래 기능들을 사용할 수 있다.  
  
**AHUD**  
기본적인 디버깅 HUD를 제공한다.  
**APlayerCameraManager**  
플레이어 카메라를 관리한다.  
**UPlayerInput**  
플레이어 인풋을 관리한다.  
  
