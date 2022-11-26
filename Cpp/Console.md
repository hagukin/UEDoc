플레이테스트 실행 후 ~(Tilda)키로 열 수 있다. 
콘솔은 언리얼 엔진이 제공하는 아주 강력한 기능 중 하나이므로 적극 활용하자.  
(UE 60참조)  

![image](https://user-images.githubusercontent.com/63915665/204085840-2c31c365-58ba-4075-96a2-b996e359e624.png)
C++ 파일에서 콘솔에 사용될 명령어를 작성해줄 수도 있다. 구체적으로 이걸 어떻게 사용하는지는 조금 더 자세히 공부해봐야겠다. 어쨌든 런타임에서 이런 기능을 제공한다는 것은 굉장히 강력한 기능이며, 잘 활용하면 큰 도움이 될 수 있다.  

![image](https://user-images.githubusercontent.com/63915665/204086004-d2c04cf9-0add-44b0-82d2-813b37ea29d3.png)  
![image](https://user-images.githubusercontent.com/63915665/204086019-dea29e13-a8ce-4fc1-8e2f-f8bd94d2f91a.png)  
더 간단하게 콘솔 명령어(함수)를 작성하는 방법으로, UFUNCTION(Exec)을 사용해주는 방법이 있다. 이 매크로는 아무데나 달 수 있는 건 아니고, 특정 클래스 내의 함수에 대해서만 사용이 가능한데, AGameMode 클래스 내의 함수에 사용할 수 있으므로 자신 프로젝트 게임모드 클래스 내부에 작성하는 게 권장된다.  

![image](https://user-images.githubusercontent.com/63915665/204086056-e5a9f1a1-5e14-40a6-a5c2-a8657500eabc.png)  
콘솔 명령어로 global variable도 설정할 수 있다. 대표적으로 ShowFlag.MeshEdges 1을 통해 메쉬의 wireframe이 보이도록 하게 만드는 것이 있다.  

![image](https://user-images.githubusercontent.com/63915665/204086128-b27e1ece-0e8d-475f-8311-95032adb0de7.png)  
직접 global variable도 설정할 수 있는데, 위 예시에서는 int32형으로 OurGame.ExtraMagnetism이라는 이름으로 전역변수 하나를 작성해주었다. 이 global variable은 이제 콘솔에서 접근이 가능하다.  

![image](https://user-images.githubusercontent.com/63915665/204086183-42167a3c-24d5-44c2-8ead-2c67699b90e0.png)  
이를 활용해 해당 global variable에 따라 인게임 자기력이 꺼졌다 켜졌다 하게 만드는 로직을 다음과 같이 구현할 수 있다.  
여기서 살펴보면 OurGame.ExtraMagnetism을 extraForce라는 이름으로 static하게 저장하는 것을 알 수 있는데, static이기 때문에 한번 선언하는 것으로 캐싱되어 런타임 동안 빠르게 사용할 수 있다.  
(주석: 왜 굳이 Tick에서 선언하는지는 잘 모르겠다)  


