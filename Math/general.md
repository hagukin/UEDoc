FMath 레퍼런스 - https://docs.unrealengine.com/4.27/ko/RenderingAndGraphics/Materials/ExpressionReference/Math/  


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

* Pow
Pow를 이용해 굳이 expensive한 function 사용 대신 비슷한 효과들을 연출할 수 있다.  
어떤 HUD를 pop하게(크기가 커지면서 나타나게) 만들려고 한다고 할 때, 다음과 같은 형태로 구현이 가능하다.  
![image](https://user-images.githubusercontent.com/63915665/181255539-8fa100f6-6c48-4e18-b79e-b825b921bd03.png)  

언리얼의 FMath::Pow는 양수만 인풋으로 받을 수 있는데, 간단한 수정을 통해 양수 음수 모두 사용가능하게 만들 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/181255791-bfef4901-6e77-4f03-b4b5-24f39d437e7f.png)  

* Interpolation
![image](https://user-images.githubusercontent.com/63915665/181256619-90f78ed7-7ea0-4c42-b32b-925ba043e6db.png)  
![image](https://user-images.githubusercontent.com/63915665/181256651-2e6dc713-2b7f-46b6-8793-b011bee2bdde.png)  
![image](https://user-images.githubusercontent.com/63915665/181256740-c41d9c61-5322-4938-838b-9feffb44ddc2.png)  

Bilinear Filtering에도 사용됨  
![image](https://user-images.githubusercontent.com/63915665/181257774-641a9e37-41cb-45b3-b0f0-c6193ea5c117.png)  
참고 - Frac은 소숫점 부분을 반환함. Frac(1.2) = 0.2; Frac(-0.2)=0.8;  
![image](https://user-images.githubusercontent.com/63915665/181257999-69461f0d-7bec-4499-8a44-6026d6dd74f8.png)  
원리는 아주 단순함. 두번 Linear interpolation을 한다고 해서 bilinear filtering임.  


