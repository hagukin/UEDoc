언리얼 엔진은 고유의 Array 자료구조형을 제공한다. 언리얼 엔진에서 제공되는 TArray만을 사용하는 것이 강력히 권장된다.  
https://docs.unrealengine.com/4.26/ko/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TArrays/  
  
TArray는 Dynamic한 Array로 크기가 고정되어있지 않다.  
![image](https://user-images.githubusercontent.com/63915665/174286810-9fe05dfe-be92-48f9-8305-1565eb7cca50.png)  
  
.Add()와 .Emplace()의 차이에 대해서는 위 다큐먼트 링크 참고.  
일반적으로 .Emplace()가 선호되고, trivial type의 경우 .Add()가 선호된다.  
  
.Empty()와 .Reset()의 경우, .Empty는 Array에 할당된 메모리까지 다 해제시켜주는 반면 .Reset은 내용물은 비워주되 Array에 할당된 메모리는 남김으로써 다시 새로운 요소들을 배열에 추가할 때 드는 시간 소요를 줄일 수 있다.  
(물론 기존 capacity 이상으로 요소를 넣게 되면 추가로 메모리 할당이 이뤄지는 건 마찬가지다.)  
  
![image](https://user-images.githubusercontent.com/63915665/174287202-d15c89a4-7244-41e6-a5b3-91273b6104da.png)  
![image](https://user-images.githubusercontent.com/63915665/174287300-039204ef-715e-4896-b5e4-27b0859d5899.png)  
![image](https://user-images.githubusercontent.com/63915665/174287328-609a0fda-461d-4b0d-b321-d00ffc8515cf.png)  
![image](https://user-images.githubusercontent.com/63915665/174287753-40885cdb-c368-42e0-ae32-c13e67391960.png)  
![image](https://user-images.githubusercontent.com/63915665/174287804-5f7f09d9-1f0f-42aa-9fd1-4f7071b81b85.png)  
  
Sorting의 경우 lambda function을 사용하는 것을 볼 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/174288098-1b211902-a1bb-4635-9126-53263e0be983.png)  
[&], 즉 앰퍼샌드 하나만 있는 것은 스코프 내의 모든 변수를 참조로 받는 것을 의미한다.  
[=]는 반대로 모든 변수를 copy by value하는 것을 의미한다.  
복잡한 자료형(e.g.fString)을 sorting할 때는 const reference를 사용하는 게 권장된다.  
