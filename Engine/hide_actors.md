참고영상: https://www.youtube.com/watch?v=kpGFi3ElN3k  

액터가 Hide 되었다는 것은 (=hidden) 해당 액터를 렌더링하지 않는다는 것을 의미한다.  
즉 텍스쳐 뿐만 아니라 그림자 등 모든 렌더링을 처리하지 않는다.  
이때 액터의 나머지 컴포넌트들 (ex. collision)은 작동중이라는 점이 중요하다.  

SetActorHiddenInGame(bool) 또는 에디터 - 액터 - Rendering에서 Hide 체크로 변경이 가능하다.  

---  

참고: 다음과 같이 컴포넌트 별로 별도로 hide 시킬 수 있다. 아래 코드 상황은 Volume의 두 컴포넌트를 hide하는 상황이다.  
![image](https://user-images.githubusercontent.com/63915665/175561528-a2caea15-ba30-496b-8c00-1e6f0738577d.png)
