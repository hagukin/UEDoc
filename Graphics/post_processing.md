* Post Processing

<h3>PostProcessingVolume</h3>

Level에 추가해 포스트 프로세싱 효과를 사용할 수 있게 해준다. 포스트 프로세싱 관련 파라미터를 조정하기 위한 Volume이다.  
  
PostProcessingVolume 하나는 하나의 blend layer이다. 즉 다른 blend layer들(ex. 일시정지 메뉴에서 게임 배경 위로 불투명한 UI를 그리는 레이어, 카메라에 vignette 효과를 주는 레이어 등)과 blend되는데,  
각 layer는 weight를 가져 그 레이어가 얼마나 최종 결과에 영향을 줄지를 조정 가능하다. (PostProcessVolume의 BlendWeight)  
  
Blend Radius라는 프로퍼티값은 레벨 상의 볼륨의 위치에 따라 얼마만큼 반경에 이펙트를 줄지를 조절할 수 있게 해준다.  
Distance in Unreal units around the volume at which blending with the volume's settings occurs.  

---   
### Features  
다양한 시각 효과 및 화면 밝기, 전반적인 색상 톤 입히기 등 대부분의 시각 효과 처리를 지원한다.  

* Auto Exposure  
사람의 눈이 밝기를 조절하듯이 언리얼의 PostProcessor는 명암을 조절하는 Auto Exposure라는 기능을 제공한다. 공식 [다큐먼트](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/PostProcessEffects/AutomaticExposure/) 참고 권장.  

