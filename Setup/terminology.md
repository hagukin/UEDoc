UE4 공식 도큐먼트의 여러 terminoligy들 중 자주 쓰이는 용어들을 살펴보자.
https://docs.unrealengine.com/5.0/en-US/unreal-engine-terminology/ 참고

* Projects  
커스텀 언리얼 엔진을 사용 시 프로젝트 경로는 Engine 폴더 옆에 놔두는 게 권장된다. (버전 컨트롤이 용이)

* Object  
언리얼에는 기본 오브젝트 타입이 별도로 마련되어 있다. (UObject)
가비지 콜렉션, 메타데이터 지원, 직렬화(seamless loading, saving 위함) 등의 기능을 지원한다.

* Actor  
레벨에 설치 가능한 오브젝트.

* Components  
액터에 부착되어 성질/기능을 부여

* Pawn  
플레이어 또는 AI에 의해 조작되는 액터

* Character  
플레이어가 조작하는 Pawn

* PlayerController  
플레이어 인풋을 인게임 인터랙션으로 변환

* Level  
맵. 일반적으로 1개의 레벨을 로딩하지만 오픈월드의 경우 여러 레벨을 로딩하는 게 가능.

* World  
레벨을 담는 객체. 일반적으로 1개의 게임에는 1개의 월드가 존재.

* GameMode  
게임 로직들을 중앙에서 관리하는 역할. 항상 최소한 1개의 GameMode가 존재함.

* GameStates  
게임 세션 내내 저장해야 하는 데이터들을 저장할 때 사용되며, 게임을 완전히 종료해야 소멸함.
즉 레벨이 변할 때도 유지됨.
