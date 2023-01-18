## Physics Asset (=Physics body)
하나의 Skeletal mesh와 짝을 이루어 사용되며, skeletal mesh가 시각적인 모델을 나타낸다면 physics asset은 물리적 성질을 나타낸다.  
Rigid body와 Constraint Set의 두 부분으로 분리되어 있다.  
https://docs.unrealengine.com/4.27/ko/InteractiveExperiences/Physics/PhysicsAssetEditor/  


### 참고
GRIP의 차량 Physics Asset에서는 Center of Mass Offset을 0,0,0으로 사용하는데, 이 값이 조금이라도 틀어지면 차량에 원치않는 물리 현상들이 발생하기 때문이다. 물리연산이 중요한 게임에서 Physics Asset을 다룰 때는  아주 조심해야한다는 것을 명심하자.  



