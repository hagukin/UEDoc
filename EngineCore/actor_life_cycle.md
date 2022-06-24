![image](https://user-images.githubusercontent.com/63915665/175551660-449a4fc6-6ad7-44ab-99c5-5abff96afd9d.png)  
액터는 위 사진과 같은 과정을 거치며 생성, 초기화, 업데이트(tick), 그리고 파괴 등을 처리한다.  
  
![image](https://user-images.githubusercontent.com/63915665/175551933-403ebe99-1ab8-4aa1-b32f-62bc26d84cb5.png)  
![image](https://user-images.githubusercontent.com/63915665/175552076-ca8be591-4f7f-4641-a16a-a3e54c83c2e5.png)  

  
---  
  
  
각각의 과정들에서 어떻게 접근하는 게 이상적인지를 살펴보자.  
![image](https://user-images.githubusercontent.com/63915665/175552473-1b65284e-7227-4df4-b78e-002b5e653621.png)  

우선 액터를 생성 및 초기화를 하는 경우,  
  
1) 간단한 초기화는 되도록 헤더 파일 내에서 기본값을 지정해주는 방식으로 처리한다.  
2) 그렇게 하기 어려운 작업의 경우 클래스 생성자 내에서 처리한다.  
3) 컴포넌트 생성의 경우 클래스 생성자 내에서 CreateDefaultSubobject를 사용한다. 단 오브젝트를 게임플레이 내에서 동적으로 생성하는 경우 다른 방식을 사용하는데, 이는 추후 다루겠다. TODO
4) 아키타입 블루프린트나 레벨 인스턴스들의 경우 오브젝트가 생성된 이후에도 데이터/컴포넌트 데이터가 변경될 수 있고(확실치 않지만 맨 위 사진의 PostActorConstruction에서 처리되는 듯 하다. 엔진 소스코드 확인 필요), 이 경우 어떤 특정한 값으로 초기화해주고 싶은 경우 오브젝트 생성 이후의 시점에서 초기화를 해주어야 한다. 때문에 이 경우에는 다음 세가지 virtual 함수들 중 하나를 선택해서 사용해 초기화해야 한다.  
    * PreInitializeComponents
    * PostInitializeComponents
    * BeginPlay
   대부분의 경우 PostInitializeComponents를 사용하는 게 권장된다. BeginPlay는 게임이 시작된 이후 호출되므로 가급적 무거운 연산을 넣지 않는 게 권장된다.  


---  

![image](https://user-images.githubusercontent.com/63915665/175555610-0d40667c-dd2b-4853-8d07-f657789c8444.png)  

액터를 매 프레임마다 업데이트 하는 경우,  
액터는 Tick(), 컴포넌트는 TickComponent()를 호출하는 것으로 업데이트를 처리한다.  
이 때 액터 및 컴포넌트가 Tick을 하는지를 지정해줘야 하는데, 이는 PrimaryActorTick.bCanEverTick = true; 또는 PrimaryComponentTick.bCanEverTick = false; 와 같은 형태로 지정할 수 있다.  
모든 오브젝트를 Tick하게 만들지 않은 이유는 당연히 CPU Cycle의 낭비를 막기 위해서이다.  
  
---  
![image](https://user-images.githubusercontent.com/63915665/175556735-29543476-6d9f-4157-90eb-ddf6671060d3.png)  

액터의 소멸/파괴의 경우,  
EndPlay() 함수가 액터 및 그 컴포넌트들에서 호출되는 것으로 처리된다.  
일반적인 경우 액터의 파괴 시 특수한 작업을 하고 싶다면 EndPlay() 내부에 작성하면 된다.  
  
액터의 파괴 과정의 도중에 BeginDestroy() 및 FinishDestroy() 함수가 호출되며, 특수한 경우 여기에 무언가를 작성해야 하는 경우도 있다.  
(BeginDestroy: Called before destroying the object. This is called immediately upon deciding to destroy the object, to allow the object to begin an asynchronous cleanup process.)  
그러나 대부분의 경우 언리얼 엔진에서 많은 부분들을 처리해주므로 실제로 소멸자에 무언가 많은 코드를 작성하는 일은 드물다.  
특히 UPROPERTY 매크로가 붙어있는 언리얼 reflection system에 포함된 오브젝트들은 알아서 소멸된다.  

---  

참고:  
위에 언급한 여러 virtual function들을 오버라이딩할 경우에는 항상 Super::을 통해 원본 함수를 호출하는 것을 잊지 말자.  
*헤더  
![image](https://user-images.githubusercontent.com/63915665/175557119-1a8f2a05-8a9b-4ccc-b136-55c09be80b58.png)  
*cpp  
![image](https://user-images.githubusercontent.com/63915665/175556984-27b3bad2-3083-4bca-a326-d4c3f79d7632.png)  

