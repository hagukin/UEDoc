# Trigger
* Trigger란?  
언리얼에서 Collision events들은 trigger라는 액터를 이용해 감지할 수 있다. 베이스는 ATriggerBase라는 액터로, 하위 클래스로 ATriggerCapsule, ATriggerSphere, ATriggerBox가 있다.  
![image](https://user-images.githubusercontent.com/63915665/176695712-8e85e454-5fc1-4a83-9253-7738075fcd70.png)  

---  

# Collision
## Overlap (겹침)
* AActor::NotifyActorBeginOverlap  
Event when this actor overlaps another actor, for example a player walking into a trigger. For events when objects have a blocking collision, for example a player hitting a wall, see 'Hit' events. @note Components on both this and the other Actor must have bGenerateOverlapEvents set to true to generate overlap events.  
주의점은 이 함수가 Trigger 뿐 아니라 모든 Actor에게 존재한다는 점이다.  
```c++
// 예시: 투사체에 맞았는지 확인
void AActor::NotifyActorBeginOverlap(AActor* OtherActor)
{
    AProjectile* Projectile = Cast<AProjectile>(OtherActor); 
    if (Projectile)
    {
        // 데미지 연산
        // 타입캐스팅 후 확인을 해주지 않는다면 아무 액터나 스쳐도 데미지를 입을 것이다.
    }
}
```
* AActor::NotifyActorEndOverlap  
마찬가지로 모든 액터에게 있다.  

## Bump (충돌)
* AActor::NotifyHit  
```c++
virtual void NotifyHit
(
    class UPrimitiveComponent * MyComp,
    AActor * Other,
    class UPrimitiveComponent * OtherComp,
    bool bSelfMoved,
    FVector HitLocation,
    FVector HitNormal,
    FVector NormalImpulse,
    const FHitResult & Hit
)
```
Event when this actor bumps into a blocking object, or blocks another actor that bumps into it. This could happen due to things like Character movement, using Set Location with 'sweep' enabled, or physics simulation. For events when objects overlap (e.g. walking into a trigger) see the 'Overlap' event.  
**For collisions during physics simulation to generate hit events, 'Simulation Generates Hit Events' must be enabled.**  
When receiving a hit from another object's movement (bSelfMoved is false), the directions of 'Hit.Normal' and 'Hit.ImpactNormal' will be adjusted to indicate force from the other object against this object.  
=> 충돌을 받을 때와 충돌을 할 때 (가할 때)를 구분해서 활용할 수 있다.  

예제: 매 프레임 BallBearing이 무언가와 충돌하고 있는지를 InContact라는 bool에 저장하려 한다.  
![image](https://user-images.githubusercontent.com/63915665/176699325-6601c7fe-17ef-4551-949c-cdaed2004a15.png)
![image](https://user-images.githubusercontent.com/63915665/176699400-d0fd33e9-9336-4bd9-9496-883741cad883.png)  


---  

# 참고사항들
1. 당연한 말이지만, 물리엔진은 대부분의 경우 직접 구현하기보단 엔진의 최적화된 기능들을 사용하는 게 좋다.  
