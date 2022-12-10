언리얼은 엔비디아의 PhysX 물리엔진을 사용한다.  
![image](https://user-images.githubusercontent.com/63915665/206856766-9e2353c6-9d7d-4a7a-8fbe-3463d89421d8.png)  

![image](https://user-images.githubusercontent.com/63915665/206856971-e584fdf7-ce9d-4e95-9f72-75adbb3e9cd1.png)
Force(힘)와 Impulse(충격량)의 차이에 대해서:  
물리 시간에 배운 내용과 동일하다. 즉 둘은 정의하는 게 다르다.  
위 공식에서도 time을 한 번 더 나눈 값이 Force임을 볼 수 있다. (distance = velocity * time)  

일반적으로 게임 개발에서는 force는 지속적으로 변화를 줘야하는 경우 사용되고, impulse는 1 게임 프레임동안 변화를 줘야할 때 사용된다.  

![image](https://user-images.githubusercontent.com/63915665/206857228-2182b9b6-a6f8-4c37-af28-dd7ceac1d6e2.png)  
각속도에 영향을 주는 토크의 경우도 Force와 마찬가지로 두 형태로 분류가 가능한데, Force와 다르게 이들을 뭉뚱그려 그냥 토크라고 표현한다.  
  
![image](https://user-images.githubusercontent.com/63915665/206857299-1ab28b71-3cb7-4039-bcbb-0ff733fcabb9.png)
Force와 Torque의 작용 정도는 각각 mass와 inertia tensor에 영향을 받는다.  

