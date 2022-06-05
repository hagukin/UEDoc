## UPROPERTY
https://docs.unrealengine.com/5.0/en-US/unreal-engine-uproperties/  
  
언리얼에서 제공하는 Reflection system의 일부. Reflection model이란 코드가 런타임 동안 스스로를 점검할 수 있는 기능을 말함.   
엔진 내의 details panel, serialization, blueprint-c++ communication 등 여러 기능의 백그라운드에서 사용됨.  
프로퍼티는 본질적으로 smart pointer임. 언리얼의 GC가 tracking 할 수 있게 해줌.  

---
  
![image](https://user-images.githubusercontent.com/63915665/172052185-7621855d-4bc7-4ff3-8bcb-8e88fd11cc02.png)
  
데이터를 에디터에서 수정하거나,  
블루프린트 스크립트에서 사용하거나,  
직렬화하거나,  
멀티플레이어 게임에서 동기화되길 원하거나,  
심지어는 단순히 UObject 및 그 상속클래스의 상속 클래스 포인터 형식일 경우  
모두 해당 데이터들은 UPROPERTY여야 한다.  
  
---
  
UPROPERTY를 정의하기 위해서는 몇 가지 특성을 지정해주어야 한다.  
  
1. visibility or editability  
archetypes와 instance 중 어디서 수정 가능한지를 지정.  
![image](https://user-images.githubusercontent.com/63915665/172052517-3010c4e4-68dc-4c77-bda9-4d60f138e53d.png)  
![image](https://user-images.githubusercontent.com/63915665/172052584-c482f0c7-b670-40b6-bd4b-01a29f82e9af.png)  

참고 - StaticMesh 같은 일부 프로퍼티의 경우 VisibleAnywhere와 EditAnywhere가 사실상 동일하게 작동한다.  


2. accessibility from blueprint script  
![image](https://user-images.githubusercontent.com/63915665/172052897-5bef97ba-39ca-44b4-bf76-1e9432c6c79d.png)
최대한 블루프린트로부터의 접근을 차단하는게(ReadOnly) 나중에 도움이 됨. 코드만 보더라도 어떤 데이터가 블루프린트에서도 수정될 가능성이 있는지 없는지를 알 수 있기 때문.  


3. category to which the property belongs (자유롭게 설정 가능)  
  
4. transient  
![image](https://user-images.githubusercontent.com/63915665/172053072-58f62c49-0cb2-4c09-b42a-d8d090930d0a.png)  
  
https://forums.unrealengine.com/t/where-to-use-a-transient-variable/17494/12
```
A:
Transient properties are always initialized to zero and are not serialized to disk. 
The time to use one is if the object at runtime will set the variable. 
For instance, let’s suppose you had a character that has MaxHealth as a value setup by the designer, which you treat as const at runtime. 
At runtime, you’d copy that value into a transient called CurrentHealth. 
CurrentHealth would go up or down and can be compared to MaxHealth.

> Transient properties는 항상 0으로 초기화된다. 
때문에 어떤 값이 런타임 동안 초기값이 지정된다면 Transient를 사용하면 좋다.

B:
This makes no sense to me. 
Firstly he says to use Transient to disable serialization. 
However then gives an example using CurrentHealth, which goes up/down through game play.
When the player stops playing, wouldn’t you want to serialize CurrentHealth so it can be restored latter when they continue playing from where they left off. 
You wouldn’t load the game with the player back at MaxHealth.

A:
Save game serialization is different and is handled manually, 
UE4 doesn’t provide a way to serialize runtime state of whole actors out of the box.

Transient disables serialization of a property when the containing object (in this example a character) is serialized to/from disk, 
which generally means when saving/loading the character blueprint in the editor, 
or loading it at game startup. 
A CurrentHealth property has no meaning in those contexts, which is why it would be made transient.

> 즉 Transient는 게임 세이브 직렬화 과정과는 다른 시점에서의 직렬화를 막는 역할이다. 이 부분은 100% 이해하지 못했다. TODO
```

```
A: 
Hello,

Resurrecting this thread because I’m curious about this: 
Why would someone use a UPROPERTY(Transient) UObject Ptr;* as opposed to just UObject Ptr*. 
It seems like UPROPERTY is used to mark things up and provide the ability for reflection.
So you’re able to do things like “DisplayAll” on that property. 
However, are there other advantages to using UPROPERTY in this case? 
Does any of the serialization differ in this case?

Thanks.

B:
Transient just disables serialization. 
The other functionality associated with UPROPERTYs would still remain, 
and be absent with a raw pointer - 
access through the reflection system, potential access from blueprints, automatic initialization, 
and perhaps most important of all, automatic referencing which prevents the UObject from being garbage collected.

> Transient 태그를 붙여도 직렬화를 제외한 UPROPERTY()의 나머지 모든 기능을 사용할 수 있다. 
특히 GC가 제거해준다는 점이 중요하다. 
```
Transient를 붙여주는 걸로 해당 프로퍼티를 언리얼 엔진의 직렬화 과정에서 제외할 수 있다.  
  
이렇게 제외하는 게 엔진 내적으로 어떤 영향을 주는지를 100% 이해하지 못했다. 관련된 세부적인 설명이 나와있는 자료를 아직 찾지 못했다. 현재 추정하기로는 게임 전체 퍼포먼스가 향상되는 대신(직렬화 시간이 줄기 때문) 에디터에서 블루프린트를 편집할 때 아키타입의 디폴트값을 지정하지 못하게 될 것이라고 생각된다. 즉 블루프린트에서 x라는 프로퍼티를 100으로 설정해주고 그 블루프린트를 레벨에 드래그 앤 드랍해도 x는 그냥 0일 것이다. 혹은 블루프린트 상에서 x라는 값 자체가 편집 불가능해질 지도 모르겠다.  


---




