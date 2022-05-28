처음 새 프로젝트를 만들면 완전히 빈 솔루션이 아닌, 몇 개의 파일들이 들어있는 것을 확인할 수 있다.  
  
  
#### <프로젝트명>.Build.cs
게임이 어떤 모듈에 dependent한지 기록한다. 언리얼 엔진 자체가 사용하는 모듈들도 적혀있다.  
나중에 Steam subsystem 등을 사용할 때 이 파일을 건드릴 일이 있을 수 있다.  
참고: https://docs.unrealengine.com/4.27/ko/ProductionPipelines/DevelopmentSetup/CompilingProjects/
  
  
#### <프로젝트명>.Target.cs
에디터 외부에서 빌드할 경우 어떤 모듈들을 같이 포함해서 빌드해야 하는지를 정해준다.
  
  
#### <프로젝트명>Editor.Target.cs
에디터에서 빌드할 경우 어떤 모듈들을 같이 포함해서 빌드해야 하는지를 정해준다.  
대체로 위와 동일하다. 단 Standalone game에는 없는 기능을 에디터 상에서만 추가하고 싶을 경우 사용할 수 있다.
  
  
#### <프로젝트명>.cpp, .h
Boilerplate code. 게임 모듈을 declare해주는 용도이다.  
모든 프로젝트는 최소 하나 이상의 모듈을 가져야 하는데, 대체적으로 그 모듈이 이 모듈이 된다.
  
  
#### <프로젝트명>GameModeBase.cpp, .h
사실상 여기에서 유일하게 코드다운 역할을 하는 파일로, 각 게임은 최소한 하나 이상의 GameMode 오브젝트를 필요로 하기 때문에 초기에 생성되어있는 파일이다.
  