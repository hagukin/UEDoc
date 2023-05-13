
클래스 내에서만 사용되는 internal한 멤버 함수/변수들은 private으로 만들고,
또 UPROPERTY를 굳이 붙여주지 않아도 되는 경우에는 붙이지 않는 게 성능 향상에 도움이 된다.  
  
---
  
모든 클래스 멤버변수의 초기화는 클래스 생성자 대신 헤더파일에서 정의하는 것이 매우 권장된다.  
클래스 같이 아직 생성되지 않은 값들은 nullptr로 초기화해두면 된다.  
(ProUE 27 - 7:50 경)  

그러나 별 상관 없다고 말하는 사람들도 있음  
https://forums.unrealengine.com/t/is-there-a-difference-in-initialzing-variables-in-the-header-vs-constructor/254878  

![image](https://user-images.githubusercontent.com/63915665/174269134-38eb4b64-1313-4ed2-b565-147d3d242d75.png)  
![image](https://user-images.githubusercontent.com/63915665/174267499-75756ae9-f94c-4bac-b5da-5a525e040fbb.png)
  
(실제 초기화)
![image](https://user-images.githubusercontent.com/63915665/174269234-bd96955a-9b01-44a0-8fc3-e1ea4ec8fe28.png)  

---
  
![image](https://user-images.githubusercontent.com/63915665/174268345-fe142169-7732-4d5b-9a80-77f361eae42e.png)  
virtual 한 함수들, 그중에서도 언리얼에서 제공하는 Tick() 같은 함수들은 최대한 액세스를 막는 것이 권장된다.  
때문에 여기서는 protected로 만들었다.  
  
---
  
![image](https://user-images.githubusercontent.com/63915665/174268625-cab5d30d-45f9-4830-b9db-63b6b62c6ba0.png)  
디자이너 등이 수정해야 되는 값들의 경우 리플렉션 시스템에 보이도록 UPROPERTY를 달아놓는다.  
  
---
  

