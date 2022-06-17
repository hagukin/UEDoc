어떤 블루프린트 오브젝트에 접근할 때는 cpp 말고 다른 블루프린트를 사용하는 게 권장된다.  
즉, 만약 내가 player.cpp로 코드를 작성해 그걸 블루프린트화 했고, 그 블루프린트를 게임의 플레이어로 삼고 싶다면  
MyCustomGameMode.cpp (GameModeBase를 상속)를 블루프린트화 시켜 블루프린트 에디터 내부에서 BP_player을 BP_MyCustomGameMode의 Default pawn class로 설정하면 된다.  
  
그 후 이렇게 만든 게임모드를 쓰기 위해  
Window - World Settings - Game Mode - GameMode Override에 BP_MyCustomGameMode를 선택해주면 된다.  
  
---
  
