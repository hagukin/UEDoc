* UE에서는 각과 라디안을 사용하는 경우가 나뉘어있다!  
![image](https://user-images.githubusercontent.com/63915665/181250293-f02e1f0d-824d-4830-9db1-8b755bd66c05.png)  
때문에 각도 관련 함수 사용 시 항상 레퍼런스 체크할 것.  

상호변경 함수  
![image](https://user-images.githubusercontent.com/63915665/181250352-a861ed86-cf30-48a6-a2d2-2e27d79c887c.png)  

* Perlin이나 Voronoi보다 가볍게 Sin함수를 이용해 Noise를 생성할 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/181252691-67f02bbb-eba9-4dd0-9ac6-54fd770a0c01.png)  
그냥 다른 형태의 사인함수들을 더해주는 방식으로 구현된다.  

* Abs, Sign
![image](https://user-images.githubusercontent.com/63915665/181253555-95826602-2a3c-4a96-8396-9c1618311183.png)  

간혹 1,-1만을 반환하는 (즉 0일 경우 무시하는) 특수한 경우의 Sign함수가 필요할 때가 있다. 이를 UnitSign이라고 한다.  
![image](https://user-images.githubusercontent.com/63915665/181254106-53277c26-e109-4c5c-96fa-f8e1f911e348.png)  
어떤 라디안 값을 0~2pi 사이의 같은 방향의 값으로 반환하는 함수를 만들 때 필요하다.  
![image](https://user-images.githubusercontent.com/63915665/181254202-51d7c067-3274-4a96-9f7d-8b2ed0ed0920.png)  
mod 0을 해버리면 값이 그대로 나오기 때문임.  
(참고: ![image](https://user-images.githubusercontent.com/63915665/181254480-fc01be36-24bd-423a-a7e0-6a9af7306d72.png)  )

