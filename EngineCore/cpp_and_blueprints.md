블루프린트에서는 cpp 오브젝트로의 접근이 용이하지만, cpp에서는 블루프린트로의 접근이 어렵다.  
설사 접근하더라도 그 블루프린트 내에 어떤 변수와 함수들이 정의되어있는 지는 알 수 없고, 그 블루프린트가 다른 cpp 객체로부터 무엇을 물려받아왔는지만을 알 수 있다.  
(물론 가지고 있을 거라고 가정하고 refer 하는 것은 가능하지만 여전히 직접 뭐가 있는지 확인 후 접근하는 게 아니기에 위험하다.)
때문에 대체적인 경우 cpp에서 블루프린트를 참조하는 것은 권장되지 않는다.  

![image](https://user-images.githubusercontent.com/63915665/178110117-c88da9e5-48f0-44ea-93d5-14b49538c746.png)  
그럼에도 만약 cpp에서 블루프린트를 참고해야 할 경우 다음과 같이 작성할 수 있다.  

언리얼의 이러한 특징 때문에 게임을 만들 때 처음 구조 설계에 굉장히 신중해야 한다. 성능 외적으로 가급적 cpp로 작성을 권장하는 이유 역시 이같은 특징 때문이다.  
