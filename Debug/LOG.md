![image](https://user-images.githubusercontent.com/63915665/224335018-01c6e2a4-ba3e-4d8b-82ae-26ca6568ffc0.png)  
언리얼에는 로그에 카테고리를 지정해 로그 메세지의 구별을 더 용이하게 만들 수 있다.  
DEFINE_LOG_CATEGORY_xxx 매크로를 사용해 로그 카테고리를 지정할 수 있다.  
![image](https://user-images.githubusercontent.com/63915665/224335488-0ede00f2-9ec1-412a-9f83-f382ae543e50.png)  
또 로그 카테고리와는 별도로 어떤 특정 로그의 사안의 중요도(Verbosity)를 지정할 수 있는데, 이 중요도에 따라 덜 중요한 로그에 의해 메세지가 묻히는 것을 방지하기 위해 해당 중요도 이하의 로그들은 필터링된다.  
또 추가로, FATAL 중요도의 경우 로그 출력임에도 코드 자체를 정지시키므로 주의해서 사용하자.  
![image](https://user-images.githubusercontent.com/63915665/224336566-74bf3416-c6c0-4006-999e-16be3e2862fd.png)  
로그 카테고리에 로그 verbosity를 매칭할 수 있다.  
이때 런타임 verbosity와 컴파일 verbosity를 분류해서 지정할 수 있다.  
컴파일 verbosity는 생각보다 중요한데, 왜냐하면 컴파일 verbosity에 의해 필터링된 로그들은 애초에 executable로 컴파일 되는 과정에서 소스코드에서부터 잘려 나간다. 즉 그만큼 (소량일 지언정) 추가적인 CPU 확보가 가능한 것이다.  

로그에 당연히 아규먼트 사용도 가능하다.  
![image](https://user-images.githubusercontent.com/63915665/224337100-8acb5e8b-9783-48d7-9d05-6fc29e3fdf77.png)  
![image](https://user-images.githubusercontent.com/63915665/224337318-aae2d85b-381b-448b-9163-be3f4b03d1c2.png)  
스크린에 직접 디버그 메세지를 띄우는 간단한 방법은 다음과 같다.  



