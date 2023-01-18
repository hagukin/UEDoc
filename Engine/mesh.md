
### Static Mesh (UStaticMesh)  
  
물리 연산 toggle
```c++
BallMesh-> SetSimulatePhysics(true);
```

### Skeletal Mesh
Bone에 대한 정보를 가지고 있는 Mesh를 의미한다.  
Bone은 hierarchy 형태로 존재하며, 폴리곤들은 이 본들의 영향을 받아 움직인다.  
 
하나의 skeletal mesh에는 하나의 Physics Asset이 사용될 수 있는데, 이는 mesh가 시각적인 부분을 담당한다면 물리적인 부분을 담당하는 부분을 분리하는 느낌이라고 이해하면 된다.  
https://docs.unrealengine.com/4.27/ko/InteractiveExperiences/Physics/PhysicsAssetEditor/  

