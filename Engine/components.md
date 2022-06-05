https://docs.unrealengine.com/5.0/en-US/components-in-unreal-engine/
  
컴포넌트는 액터에게 부착 가능한 오브젝트로, 그 자체로는 존재할 수 없다.  
액터들에게 부착된 컴포넌트들은 생성될 때 개별적 인스턴스로 생성된다.  
(Contrary to the default behavior of sub-objects in general, Components created as sub-objects within an Actor are instanced, meaning each Actor instance of a particular class gets its own unique instances of the Components.)

* 3 basic component types
1. Actor Component (UActorComponent)
abstract behaviour를 관리하는 데 유용하다. 이동이나 인벤토리 관리, 특성 관리 같이 물리적이지 않은 것들을 처리할 때 쓰인다.  
이들은 월드 내에 물리적으로 존재하지 않는다.  
  
2. Scene Component (USceneComponent)
Actor Component를 상속.
월드 내에 물리적으로 존재하지만 시각적 요소를 필요로 하지 않는다 (안보여도 됨)  
예시로는 spring arms, cameras, physics forces, constraints가 있다.  
오디오나 physics objects 들은 포함되지 않는다.
  
3. Primitive Component (UPrimitiveComponent)
Scene Component를 상속.  
시각적 요소를 필요로 한다.  
시각 요소를 렌더링하거나 physics objects와 collision/overlap할 때 쓰인다.  
예시로는 skeletal meshes, box collision volume, particle systems 등이 있다.  
  
