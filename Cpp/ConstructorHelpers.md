---

출처: http://egloos.zum.com/sweeper/v/3208657  
[UE4] ConstructorHelper::FObjectFinder/FClassFinder


1. ConstructorHelper

이름에서 알 수 있듯이 ConstructorHelper는 UObject의 Constructor(생성자)에서만 사용 가능하다.
(즉, CDO 제작에서만 사용된다는 얘기) - CDO란? (https://bbagwang.com/unreal-engine/ue4-%EC%97%90%EC%84%9C%EC%9D%98-cdo/)
아래 FObjectFinder와 FClassFinder의 정의 코드 중 Line:16에서 생성자에서 호출되었는지 체크하는 것을 확인할 수 있다.

그리고, 아래 코드에서 보겠지만, ConstructorHelper::FObjectFinder 혹은 FClassFinder 객체에 모두 static 키워드를 주었다.
리소스는 여러 언리얼 오브젝트의 인스턴스들이 공유해서 사용하는 자원이므로, 인스턴스마다 불필요하게 애셋을 로드할 필요가 없기 때문이다. 

물론 같은 것을 로드하지 않으면 의미가 없을 수도 있지만 말이다.
하지만, 일반적으로 위에 적은 이유들로 static 키워드를 붙이는 것이 관행이라 할 수 있다.

참고로, 언리얼 프로젝트에서 모든 Asset은 경로(Path) 기반으로 관리된다.
Asset의 경로 정보는 컨텐츠 브라우저에서 Asset을 우클릭한 다음 "레퍼런스 복사"를 누르면, 경로 정보가 클립보드에 복사되어, 코드에서 바로 붙여넣기하여 사용할 수 있게 된다.


2. ConstructorHelpers::FObjectFinder

ConstructorHelpers::FObjectFinder는 Asset의 내용물을 가져올 때 사용한다.
하나의 언리얼 오브젝트는 UClass와 CDO로 나뉘어지는데, FObjectFinder는 CDO 객체를 찾는다 생각하면 된다.

```c++
/** Runtime/CoreUObject/Public/UObject/ConstructorHelpers.h */
 
struct COREUOBJECT_API ConstructorHelpers
{
public:
    template<class T>
    struct FObjectFinder
    {
        T* Object;
        FObjectFinder(const TCHAR* ObjectToFind)
        {
            CheckIfIsInConstructor(ObjectToFind);
            FString PathName(ObjectToFind);
            StripObjectClass(PathName,true);
 
            Object = ConstructorHelpersInternal::FindOrLoadObject<T>(PathName);
            ValidateObject(Object, PathName, ObjectToFind);
        }
        bool Succeeded() const
        {
            return !!Object;
        }
    };
};
```

3. FObjectFinder 예제

다음 예제는 SkeletalMeshComponent에 특정 SkeletalMesh 애셋을 찾은 다음, SetSkeletal 까지 호출하는 코드 흐름을 보여준다.

```c++
///////////////////////////////////////////////////////////////////////////////////////////////
// Header
///////////////////////////////////////////////////////////////////////////////////////////////
 
UCLASS(BlueprintType, Blueprintable)
class ARENABATTLE_API AWeapon : public AActor
{
    GENERATED_BODY()
 
public:
    // CDO constructor에서 생성시키는 녀석은 Blueprint에서 수정할 수 없어야 한다
    UPROPERTY(BlueprintReadOnly, VisibleAnywhere, Category="WeaponComponent")
    class USkeletalMeshComponent* WeaponComponent = nullptr;
};
 
///////////////////////////////////////////////////////////////////////////////////////////////
// CPP
///////////////////////////////////////////////////////////////////////////////////////////////
 
// Sets default values
AWeapon::AWeapon()
{
    // Create USkeletalMeshComponent as RootComponent
    WeaponComponent = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("ABWeaponComponent"));
    check(WeaponComponent);
    RootComponent = WeaponComponent;
 
    // Find SkeletalMesh
    // ConstructorHelpers는 생성자 함수에서만 사용할 수 있다.
    //  ConstructorHelpers::FObjectFinder
    //  ConstructorHelpers::FClassFinder
    static ConstructorHelpers::FObjectFinder<USkeletalMesh> SK_BlackKnight(
        TEXT("SkeletalMesh'/Game/......./SK_Blade_BlackKnight.SK_Blade_BlackKnight'")
    );
    // Set SkeletalMesh to SkeletalMeshComponent
    WeaponComponent->SetSkeletalMesh(SK_BlackKnight.Object);    
}
```

4. ConstructorHelpers::FClassFinder

ConstructorHelpers::FClassFinder는 Asset의 타입 정보를 가져올 때 사용한다.
하나의 언리얼 오브젝트는 UClass와 CDO로 나뉘어지는데, FClassFinder는 UClass 객체를 찾는다 생각하면 된다.

```c++
/** Runtime/CoreUObject/Public/UObject/ConstructorHelpers.h */
 
struct COREUOBJECT_API ConstructorHelpers
{
public:
    template<class T>
    struct FClassFinder
    {
        TSubclassOf<T> Class;
        FClassFinder(const TCHAR* ClassToFind)
        {
            CheckIfIsInConstructor(ClassToFind);
            FString PathName(ClassToFind);
            StripObjectClass(PathName, true);

            Class = ConstructorHelpersInternal::FindOrLoadClass(PathName, T::StaticClass());
            ValidateObject(*Class, PathName, *PathName);
        }
        bool Succeeded()
        {
            return !!*Class;
        }
    };
};
```

5. FClassFinder 예제

다음 예제는 미리 정의된 클래스(블루프린트 클래스)를 찾아내어, BotPawnClass에 지정해주는 코드 흐름을 보여준다.

```c++
///////////////////////////////////////////////////////////////////////////////////////////////
// Header
///////////////////////////////////////////////////////////////////////////////////////////////
TSubclassOf<class APawn> BotPawnClass;
 

///////////////////////////////////////////////////////////////////////////////////////////////
// CPP (어느 생성자 함수 안)
///////////////////////////////////////////////////////////////////////////////////////////////
static ConstructorHelpers::FClassFinder<APawn> BotPawnOb(TEXT("/Game/Blueprints/Pawns/BotPawn"));
BotPawnClass = BotPawnOb.Class;
```
