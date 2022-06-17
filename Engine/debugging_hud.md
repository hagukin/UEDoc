개발 과정에서 최대한 빨리 디버깅용 허드를 만드는 것이 권장된다.  
디버깅용 허드를 위한 간단한 프레임은 ProUE 30. Adding a debugging HUD를 참고할 것.  
  
디버깅용 허드를 개발할 때 private한 멤버들에 접근할 일이 많을 텐데, 이때 하나하나 다 getter를 설정해주기보다는 C++의 friend를 적극 활용하는 것이 권장된다.  
어차피 디버깅용 콘솔은 게임 내적으로 영향을 주지도 않기 때문에 friend를 사용해 간단하게 private한 인자들에 접근하는 것으로 쉽게 구현할 수 있다.  
물론 friend는 접근권한을 완전히 준다는 점에서 매우 위험하기도 하므로 당연히 게임의 다른 부분들에서는 남용해서는 안된다.  
Rob Baker는 몇 년 간의 개발 경험을 통틀어 friend를 사용한 건 디버깅 허드를 작성할 때가 유일했다고 말했을 정도다...  
  
![image](https://user-images.githubusercontent.com/63915665/174283041-9110b477-3003-4775-b205-cc0365f4d3d3.png)  
위 사진처럼 해놓으면 HUD에서 private한 값들을 읽어 텍스트로 렌더링해줄 수 있다. (ex. 실시간으로 속도 변하는 걸 화면에 렌더링)  
  
이렇게 만든 허드 오브젝트는 커스텀된 GameMode 내에서 cpp로 생성해 사용이 가능하다.  
![image](https://user-images.githubusercontent.com/63915665/174283794-ba472932-a2e0-4794-91dd-f70863a7b9b5.png)  
사진을 보면 인스턴스를 생성하는 대신 StaticClass()를 호출중인 것을 알 수 있는데, 이 기능은 static class를 생성해주는 과정이다.   
c++의 static class는 파이썬의 static class 개념을 생각하면 이해가 빠른데, 객체 자체가 static이므로 프로그램이 종료되기 전까지 사라지지 않는다.  
(참고: static class는 friend와 비슷하게 자주 사용되지는 않는다)  
  
