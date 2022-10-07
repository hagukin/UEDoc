언리얼에서 어떤 오브젝트의 물리적 위치는 상대적 위치를 통해 나타내어진다.  
(월드 좌표 역시 월드라는 상대적 기준에 대한 위치를 표현한 것에 불과하다)  
skeletal mesh에 위치한 hand도, hand에 위치한 gun이라는 오브젝트도 다 마찬가지로 상대적 기준에 대한 좌표로 나타내어진다.  

언리얼에서는 이를 FTransform이라는 형태로 제공한다.  
![image](https://user-images.githubusercontent.com/63915665/194558209-278af702-0bcf-4800-9ad2-8085fe22c552.png)  
위 사진을 보면 오브젝트들이 hierarchy 구조로 저장되어있음을 볼 수 있는데, 이때 어떤 한 오브젝트의 Transform Rotation Scaling을 변경하면 그 하위의 모든 컴포넌트들이 동시에 움직인다.  

이러한 상대적인 coordinate spaces를 활용하는 한가지 예시를 살펴보자.  
레이싱 게임에서 어떤 두 차량의 collision을 확인하거나, 어떤 차가 다른 차보다 앞서있는지를 확인하는 좋은 방법은 뭘까?  
물론 그냥 월드좌표값을 이용해 비교할 수도 있겠지만, vehicle space라는 별도의 좌표계에서 어떤 두 차의 x좌표값만 비교해주면 알 수 있게 만들 수도 있다.  
내 블로그 글 참고: https://gamesmith.tistory.com/176?category=1032694  
구체적으로 말해, 차량 A와 차량 B가 있을 때 원점에서 차량 A까지의 이동을 나타내는 행렬(Transpose matrix) E를 구했다고 해보자.  
즉 0 * E = A이다.  
이때 차량 B의 A에 대한 상대적 위치, 즉 차량 B의 위치를 A의 위치가 원점일 때의 좌표계에서의 값으로 나타내려면 다음과 같이 구할 수 있다.  
B' = E^-1 * B  

---  
언리얼에서는 다음과 같이 표현 가능하다.  
![image](https://user-images.githubusercontent.com/63915665/194563961-177bc3f8-8fb5-4dcf-bbf4-ab0374ff7e2c.png)  
FTransform의 주 사용처는 바로 이러한 좌표계의 변환이다.  
  
![image](https://user-images.githubusercontent.com/63915665/194564245-bc7b22f3-5420-4170-8dc6-4312dcc786de.png)  
각각 transpose matrix를 곱하거나 그 역행렬을 곱해주는 과정이 함수 내부적으로 구현되어 있다. 즉 양쪽 좌표계에서 왔다갔다 할 수 있다.  
  
![image](https://user-images.githubusercontent.com/63915665/194564909-0b1434bb-0915-4b97-a6d8-2299b2a71d69.png)  
언리얼에서 GetTransform 함수들은 항상 월드좌표계 기준으로 transform을 반환한다. 언리얼에서 Transform은 대체적으로 월드좌표계에서의 transform을 나타내며, 실제로 렌더링을 비롯한 내부적인 연산을 처리하는 데에는 월드좌표계 transform을 사용하기 때문에 언리얼 엔진은 매 틱마다 오브젝트들의 월드좌표를 계산한다.  
![image](https://user-images.githubusercontent.com/63915665/194564642-10b27cad-ae2e-4841-8106-4d77b241ec9a.png)  
주의: 사진과 같이 hierarchy에 속한 경우, 에디터에서 보여지는 것은 상대좌표이다.  

정리:  
![image](https://user-images.githubusercontent.com/63915665/194565230-75047b62-5140-44bd-8bbd-7ef6e5061465.png)  
