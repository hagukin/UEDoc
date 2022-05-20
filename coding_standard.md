* 코딩 스탠다드:  
여러 개발자가 같이 작업할 때 깔끔하고 명시적인 코드를 작성하는 어떤 기준을 미리 잡는 것은 아주 중요하다.  
에픽게임즈에서 제시한 언리얼 코딩 스탠다드가 있으므로 이를 기준으로 삼는 것이 권장됨.  
https://docs.unrealengine.com/5.0/en-US/epic-cplusplus-coding-standardblueprint-debugging-in-unreal-engine/  

1. 코드 상단 Copyright notice 및 author, 그리고 코드에 대한 간략한 설명을 주석으로 추가할 것.  
![image](https://user-images.githubusercontent.com/63915665/169508088-33822391-05bb-4d56-a7ba-c5a0f28422ab.png)

2. 네이밍 컨벤션을 준수할 것. 또 짧고 명시적인 이름을 만들것.  

3. uint32 등의 타입을 사용할 것. int, long 등의 사용을 지양할 것.  

4. 주석은 코드가 왜 그렇게 쓰여있는지를 설명하는 방향으로 쓸 것.

5. Const correctness: 
변경되지 않는 무언가를 인자로 전달할 때 const reference 사용할 것.
(참고: pass by value 인자일 경우 에픽게임즈에서는 const를 붙이는 걸 권장하지만 굳이 필요는 없음)
객체의 메소드가 객체를 변경하지 않을 경우 const를 붙여줄 것.
루프가 컨테이너의 내용물을 변경하지 않는다면 const iteration을 사용할 것.

```c++
void SomeMutatingOperation(FThing& OutResult, const TArray<Int32>& InArray)
{
    // InArray will not be modified here, but OutResult probably will be
}

void FThing::SomeNonMutatingOperation() const
{
    // This code will not modify the FThing it is invoked on
}

TArray<FString> StringArray;
for (const FString& : StringArray)
{
    // The body of this loop will not modify StringArray
}
```
  
6. documentation은 특히 게임 개발에서는 굳이 필요가 없음. 에픽에서는 권장함.

7. C++11, C++14 문법을 ue4가 지원함. 적극적으로 사용할 것.
* override and final
* nullptr
* auto
* range-based for
* lambdas, anonymous functions
* enums (enum class)
* default member initializer (되도록 항상 사용할 것)

8. if - else 등 bracket 스탠다드를 준수할 것.
``` c++
if (TannicAcid < 10)
{
    UE_LOG(LogCategory, Log, TEXT("Low Acid"));
}
else if (TannicAcid < 100)
{
    UE_LOG(LogCategory, Log, TEXT("Medium Acid"));
}
else
{
    UE_LOG(LogCategory, Log, TEXT("High Acid"));
}
```
  
9. 언리얼에서는 namespace를 아예 사용하지 않는 게 좋음. UCLASS 같은 것들과 호환이 안됨.
  
10. precompiled header 사용하지 말 것.
  
11. public, protected, private 적극 사용할 것. OOP 준수.
  
---
에픽게임즈에서 권장하는 기준과 다르지만 사용하면 좋은 기준들

12. auto 키워드 필요 시 사용. 
타입이 모호해져서 얻는 실보다 빠르게 코딩이 가능한 득이 더 큼.
  
13. bool 타입 변수명 앞에 b 한글자 prefix를 붙이지 말 것.
  
14. JavaDoc commenting 스타일을 굳이 따르지 말 것.
  
15. 영어 사용 시 미국식 영어 스타일을 유지할 것.
  
16. 멤버 함수에 전달되는 인자의 경우 이름을 Headless camel-case로 작성하면 편함.
![image](https://user-images.githubusercontent.com/63915665/169511940-9cb21cce-0edc-4250-84ed-9121ee3f4b4c.png)
위 사진 좌측은 에픽게임즈의 기준이며, 우측은 Headless camel-case로 변경한 모습임.  
우측처럼 작성했을 때 뭐가 함수에 전달된 인자이고 뭐가 멤버 변수인지 구분이 명확해짐.

![image](https://user-images.githubusercontent.com/63915665/169512245-4e6756c8-ef83-4804-a959-fb3ecd43f7fd.png)
또 이렇게 작성하면 코드를 읽을 때 어떤 게 클래스의 멤버 변수고 어떤 게 함수 인자인지를 바로 확인할 수 있음.

17. 코딩 스탠다드는 결국 그 코드를 작성하는 팀에게 맞춰져야 함.  
즉 위에 언급되지 않았거나 다른 사항이더라도 충분한 이유가 있다면 사용해도 좋음.  
단 엔진 단에서 코드를 건드릴 경우 에픽의 기준을 준수할 것.  


