![image](https://user-images.githubusercontent.com/63915665/204085115-9ce502bf-eae9-4b54-8ef0-694c574b5699.png)
1) const 인 레퍼런스 변수는 **반드시** 인풋 파라미터 변수여야 하고, const가 아닌 레퍼런스 변수는 **반드시** 아웃풋 파라미터 변수여야 한다. (addOneToNum(int& x) 꼴)  
만약 인풋 파라미터 변수를 함수 내에서 수정하게 되는 일이 발생해 const를 붙일 수 없다면, UPARAM(ref)를 사용하는 것으로 const를 대체할 수 있다.  
2) 모든 액터나 컴포넌트는 레퍼런스 형태로 전달할 수 없다, 포인터를 사용해야 한다.  
3) 모든 액터나 컴포넌트는은 Input parameter로만 사용되어야 한다.  
4) 반대로 structure나 arrays는 포인터 형태로 전달할 수 없다, 레퍼런스를 사용해야 한다. 가능하면 자료구조의 전달에는 최대한 레퍼런스를 사용하자.  

---  

![image](https://user-images.githubusercontent.com/63915665/204085422-4648158a-9b76-4d3e-b541-5f0873788259.png)
UFUNCTION 매크로로 블루프린트에서의 함수의 작동방식을 지정할 수 있다.  
BlueprintCallable, BlueprintImplementableEvent는 직관적이므로 생략
BlueprintNativeEvent의 경우, 만약 블루프린트에서 해당 함수가 구현되어있지 않은 경우에만 C++에서 "함수명_Implementation"을 찾아 호출한다.  
구현되어있으면 블루프린트 구현을 사용한다.  

참고 - 멀티플레이어 게임일 경우 UFUNCTION 매크로의 다른 기능들도 살펴보자.  



