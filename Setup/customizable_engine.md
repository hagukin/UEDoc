### Stock engine

통상적으로 에픽게임즈에서 다운받는 언리얼 엔진. 
소스코드를 수정해 recompile할 수 없다.

### Customizable engine

소스코드를 수정해 recompile할 수 있다!  
엔진을 수정해야 할 일이 있을 것 같은 경우 처음부터 Customizable engine을 사용할 것. 중간에 바꾸는 건 사실상 불가능하다. 
현업의 경우 대부분 Customizable engine을 사용하며, 특히 콘솔게임의 경우 해당 시장의 release requirement를 맞추려면 
사실상 stock으로는 불가능함.  
깃헙에서 다운받을 수 있으며 버전 컨트롤이 다소 복잡할 수 있지만 이러한 과정들은 자동화할 수 있음.  

소스코드를 다운받는 과정은 여기서 확인 가능함.  
https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/DownloadingSourceCode/

엔진 다운 및 작업 시 SSD 사용은 사실상 필수적임.  
만약 SSD 공간이 부족할 경우 엔진의 일부 파일만 SSD로 옮겨온 후 Symbolic Link를 사용해 속도 증가를 기대해볼 수 있음.  

비주얼 스튜디오를 사용 도중 업데이트할 경우 UE의 precomiled header들을 invalidate하므로 다 다시 컴파일 해주어야 함.  
고로 업데이트는 가급적 자제할 것. 
UnrealVS extension을 설치할 것. 설치 방법은 다운로드한 엔진 파일 내에 있는 UnrealVS를 실행하면 됨.
Visual Assist 또는 ReSharper C++ extension의 사용도 추천.  

엔진 컴파일의 경우 언리얼에서 제공하는 레퍼런스를 참조하면 됨.  

엔진 버전 컨트롤의 경우 git도 괜찮고 perforce도 괜찮음.  

### Custom하는 과정
ProUE 70 참고  
GRIP을 위해 커스터마이징된 엔진과 원본 언리얼 엔진을 비교하며 WinMerge를 이용해 다른 코드들을 확인하면서 프로젝트에 바로 사용할 수 있도록 똑같이 복붙하는 과정으로, 앞부분은 거의 그냥 설명없이 복붙하는 내용이고 31분 가량부터 변경한 내용들에 대한 설명이 간략하게 나온다.  

<h3>본 문서를 작성하는 데 참고한 자료들</h3>  

더 자세한 내용은 아래 자료들에서 확인 가능
* Udemy Pro Unreal Engine Game Coding - 1. Getting Started
