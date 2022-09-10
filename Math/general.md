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
  
부드러운 움직임을 표현할 때는 linear interpolation과 함께 Pow를 사용해주면 된다.  
그냥 interpolate만 해버리면 속도가 0에서 V로 가속도없이 바로 움직여버려 다소 어색할 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/186427235-e53362e3-e7bf-4014-ac32-848581021c53.png)  
![image](https://user-images.githubusercontent.com/63915665/186427305-0fbcf282-4457-40a5-9c21-a89fffc3aa48.png)  
![image](https://user-images.githubusercontent.com/63915665/186427461-0510bc44-3249-420a-a244-51f45e546557.png)  
![image](https://user-images.githubusercontent.com/63915665/186428626-02c3ea32-de63-47ca-96a9-0f8baa2ed1e7.png)
In-out 커브는 sigmoid curve / 시그모이드 함수로도 불리운다.  
![image](https://user-images.githubusercontent.com/63915665/186429131-e6ab36fe-4dc3-43df-b3b6-ca76413d0ec9.png)
p가 커질 경우 더 빠르게 가파라진다.  
  
이를 시간에 따라 부드럽게 움직이게 만들어보자. (Time-based smoothing)  
이는 카메라 이동 등에 적용될 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/186429522-45abfb31-2f39-41b4-9f13-1b60457284ed.png)  
기본적인 원리는 위와 같이 구현가능하다. targetYaw는 이번 프레임의 Yaw이고 oldYaw는 이전 프레임의 Yaw이다. 즉 마우스가 움직여 카메라의 Yaw값이 변화할 때, 1프레임 후 targetYaw로 바로 가는게 아니라 선형보간을 거쳐 그 사이의 지점으로 이동하는 것이다.  
위 코드는 문제가 있는데, 실제 게임 환경은 프레임레이트가 계속 변화하기 때문에, smoothingRatio값을 고정한 위 코드의 경우 문제가 발생한다. 마우스를 현실에서 일정한 속도로 움직이더라도 초당 프레임 처리횟수가 달라지게 되면 더 많거나 더 적게 움직일 수 있기 때문이다.  이를 해결하는 방법은 언리얼에서 제공하는 deltaSeconds를 활용하는 것이다. delta second이란 이전 프레임에서 해당 프레임까지 걸린 시간을 의미한다.  
![image](https://user-images.githubusercontent.com/63915665/186430906-3e0b9e50-1b2f-4c11-a2e6-0d7103cb965b.png)  
![image](https://user-images.githubusercontent.com/63915665/186431596-16088f75-ab99-42fd-acf9-881ab7b15f65.png)  
위 코드처럼 수정하면, 한 프레임을 처리하는데 다른 프레임들보다 오랜 시간이 걸렸다면 그만큼 Pow의 지수값을 높여주는 것으로 더 많이 움직이게 만들어 그 차이를 조정하는 것을 볼 수 있다. authoredFPS를 유지)  

이러한 기법이 실제로 활용되는 한가지 예시를 살펴보자.  
![image](https://user-images.githubusercontent.com/63915665/186432115-a84d0297-3e68-4deb-898b-77a4f3e96cca.png)  
차량 뒤의 부스터 화염 이펙트가 차량의 속도에 비례해 길게 렌더링된다고 해보자. 이때 만약 이 길이를 차량의 속도에 항상 프레임마다 정비례하게 만든다면, 차량 속도가 시시각각 변하는 레이싱 게임의 특성상 불꽃이 들쭉날쭉거릴텐데, 여기에 시간에 따라 선형보간되게 만든다면 차량이 속도가 빨라질때 자연스럽게 불꽃도 부드럽게 길어지고, 반대일 때는 부드럽게 줄어드는 효과를 연출할 수 있다.  
  
* 난수 생성 (Random Number Generation)  
![image](https://user-images.githubusercontent.com/63915665/186432717-617c2c23-ba38-438d-ad57-2a4afb347ac0.png)  
![image](https://user-images.githubusercontent.com/63915665/186432872-02f46713-de44-4691-83c3-9dfec47dfe6a.png)  
언리얼의 FMath는 다양한 RNG함수를 제공한다.  
RandHelper, RandHelper64는 32,64비트 정수 범위의 난수를 생성한다.  
RandCone는 주어진 각도 사이의 랜덤한 방향 벡터를 반환한다.  
RandPointInCircle과 RandPointInBox는 말 그대로의 역할을 한다.  
  
![image](https://user-images.githubusercontent.com/63915665/186433859-eaaef696-28fc-4d8e-8a29-34e92f7fc12e.png)  
FMath::RandInit으로 RNG의 시드를 지정할 수도 있다.  
기본값은 clock value이다.  
이때 주의해야 할 것은 UE의 RNG는 shared resource이기 때문에 시드를 변경하는 것은 게임 전반은 물론이고 엔진 내부적으로도 영향을 미칠 수 있다는 점이다.  
엔진 자체에 FRandomStream이라는 별도의 RNG가 있지만 썩 권장되지 않는다.  
때문에 어떠한 이유로 시드를 지정해 랜덤성에 대한 통제가 필요하다면 직접 제작하는 게 권장된다.  

![image](https://user-images.githubusercontent.com/63915665/186434558-56f0e4ff-de45-4473-933d-917441addcf7.png)  
![image](https://user-images.githubusercontent.com/63915665/186434602-98e76075-c01c-485e-8e78-d91aa4057f06.png)  
![image](https://user-images.githubusercontent.com/63915665/186434620-c01b7e91-52ab-422d-9442-2978ffe6b709.png)  
또한 완전히 랜덤한 RNG 대신 "랜덤하게 느껴지는" RNG를 원하면 이 역시 별도의 구현이 필요하다.  
이처럼 RNG를 수정해야 할 때는 별도의 클래스로 Wrap하는 게 권장된다.  
언리얼의 RNG는 C의 rand에 의존하고 있음을 참고. (C의 rand는 문제점들이 있으나, 근래 개선된 것으로 알려짐. Mersenne Twister 알고리즘 등의 사용도 고려해볼 것, 그러나 거의 대부분의 경우 rand로도 충분할 것이다)  
  
  
* Vector  
![image](https://user-images.githubusercontent.com/63915665/186436567-1c209f4c-1068-421c-b36d-fb5ae1788b4d.png)  
언리얼에서 Vector는 거의 항상 floats를 저장한다. (FVector)  
대체적으로 2, 3, 4 크기짜리의 벡터들을 사용할 것이며, 이 세 가지로도 대부분의 것들을 만드는데 부족함이 없을 것이다.  
언리얼은 Left handed coordinate system을 사용하며, Vector는 이 3차원 공간에서 위치나 direction을 나타낼 때 사용된다.  
(당연히 수학에서의 벡터처럼 길이와 방향에 대한 정보를 모두 포함할 수도 있다)  
  
![image](https://user-images.githubusercontent.com/63915665/186436723-9080939d-a6c9-45d4-8e7b-d8dd2e3711bd.png)
참고: 언리얼에서의 vector.Size()는 STL에서의 size와 다르다. 이에 혼동하지 않도록 하자.  
  

* Dot product, Cross product
내적과 외적은 크게 어려울 게 없고, 그냥 구현해서 쓰면 된다.  
![image](https://user-images.githubusercontent.com/63915665/189484057-ccf0f211-cf40-47da-8af0-c3c3d6528662.png)  
![image](https://user-images.githubusercontent.com/63915665/189484085-3b0ba02d-60b5-4bde-8e32-3b401d488862.png)  

(참고: direction은 항상 normalized 된 벡터로 나타내는 관습이 있다)  
  
  
* Quaternions  
![image](https://user-images.githubusercontent.com/63915665/189484274-469b2b7e-0220-468b-9f73-33513f22efb1.png)  
속도도 빠르고 부드럽게 Slerp(Spherical linear interpolation)을 할 수 있다.  
그러나 다소 비직관적이고, Slerp할 일 자체가 아주 많지는 않기 때문에 Rotator가 더 자주 쓰이는 경향이 있다.  
  
  
* Rotators  
Roll, Pitch, Yaw 세 축의 회전으로 orientation을 나타내며, 라디안이 아닌 각(360)을 사용한다.  
![image](https://user-images.githubusercontent.com/63915665/189484460-8066b0ab-e11d-4d7f-a328-133400af1055.png)  
빠르게 Quaternion과 상호 변환이 가능하다.  
![image](https://user-images.githubusercontent.com/63915665/189484495-92a35eef-32e8-4752-8e99-988a2b75612b.png)
360도 이상 혹은 -360도 이하로도 각을 설정할 수 있다.  
Quaternion으로 변환할 경우 이 정보들은 사라진다. (즉 여러 바퀴 돈 상태는 표현할 수 없다)  
Quaternion을 Rotator로 다시 변환하면 각은 -180~180 사이로 표현된다.  
Rotator.Normalize()를 이용해 수동으로 각 범위를 맞춰줄 수도 있다.  
![image](https://user-images.githubusercontent.com/63915665/189484685-fe1fd8ee-1ab8-42fb-ae7d-e7fd235b83ea.png)  
  
두 Rotator를 Lerp할 경우 최단 경로를 따라 Lerp한다. 즉 -170과 170 사이를 Lerp하면 340도 도는 게 아닌, 20도만 회전한다.  
또 각을 먼저 Normalize하고 Lerp하므로 180도 이상 회전시킬 수 없다.  
물론 수동으로 긴 경로를 따라 lerp하게 하거나, 큰 각을 가진 Rotator 사이에서 여러 바퀴 회전하게 Lerp할 수도 있다.  
lerp를 smooth하게 처리해주는 RInterpTo 함수도 존재한다.  
![image](https://user-images.githubusercontent.com/63915665/189484812-742f2131-01ed-435f-9ab8-009f07e492f9.png)
  
Rotator는 Vector로 변환이 가능하다. Rotator가 가리키는 방향을 가리키는 Normalized 된 벡터(1.0, 0.0, 0.0)를 해당 방향으로 바라보게 한 벡터를 반환한다고 생각하면 된다.  
![image](https://user-images.githubusercontent.com/63915665/189484908-e33f0ff9-bfa9-4668-8279-9d68539cdd38.png)  
  
Rotator와 Quaternion 모두 특정 Vector를 회전시키는 데 쓸 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/189484935-c814c110-e3cd-41a5-92fc-290793560d09.png)  







































