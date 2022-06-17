소스코드를 에디터 외부에서 수정할 경우 (예를 들어 외부의 .cpp파일을 게임 내에 복붙하려는 경우) 프로젝트 디렉토리로 가 <프로젝트명>.project를 우클릭 하고 Generate Visual Studio project files를 클릭한다.  
이는 비주얼스튜디오 인텔리센스에 변경된 사항들에 맞는 올바른 정보를 전달하는 과정이다.  
이 방법 말고도 엔진경로/GenerateProjectFiles.bat을 실행하는 것으로도 같은 결과를 얻을 수 있다.  
  
이 때 주의해주어야 할 점은 외부에서 가져온 이 코드들의 최종 수정일자가 반드시 최근 일자로 되어있어야 한다는 것이다. 쉽게 말해, 5년 전에 작성한 소스코드를 이제 프로젝트에 넣으려 한다고 가정해보자. 해당 소스코드의 최종 수정 일자가 5년 전으로 되어있다면 언리얼 빌드 시스템이 이 코드들은 리컴파일해야 하는지 알 지 못하므로 프로젝트 안에 코드를 넣더라도 컴파일 과정에 문제가 있을 수 있다.  
(For some students, unzipping the source code doesn't set the last modified dates on the unzipped files to today's date, and instead keeps them at the date they were originally zipped by myself. This isn't good, as the Unreal build system won't know that they need to be recompiled and relinked. So, if this is the case for you, fear not, just right-click on the TouchSourceFiles.ps1 file, and choose Run with Powershell)  

---

