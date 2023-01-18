
### Static Mesh (UStaticMesh)  
  
물리 연산 toggle
```c++
BallMesh-> SetSimulatePhysics(true);
```

### Skeletal Mesh
Bone에 대한 정보를 가지고 있는 Mesh를 의미한다.  
Bone은 hierarchy 형태로 존재하며, 폴리곤들은 이 본들의 영향을 받아 움직인다.  
