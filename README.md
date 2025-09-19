# FIRMWARE-2025.09.19-D_1

- RCC 에서 HSE, LSE Disable
- RCC(Reset and Clock Control)
- MCU 내부 클럭을 사용하기 위해서이다.

  
<img width="1696" height="866" alt="image" src="https://github.com/user-attachments/assets/9b4961cb-ab28-4f72-a697-9edd09f61135" />


- Clock Configuration에서 외부 Clk 비 활성화 확인.


<img width="1687" height="865" alt="image" src="https://github.com/user-attachments/assets/7c3cd669-778d-40d9-a8cc-f1bc787fb752" />



### Clk 는 2가지 종류
- HSE(High Speed External Clock)
- LSE(Low Speed External Clock)
- 내부 기능의 용도에 따라 2 가지로 외부 Clk가 나누어져있다.



### GPIO 설정
- LED 제어가 목적이므로 GPIO를 설정한다.
- GPIO(General Purpose Input Output)
- Nucleo-64 개발보드의 LED(LD2)를 사용할 것이므로 별도로 추가적인 LED 설정이 필요 없다. 기본 설정으로 LD2이 활성화 되어있다.

  <img width="1692" height="875" alt="image" src="https://github.com/user-attachments/assets/d98ede98-592b-41e0-89cf-02bc6db2fb77" />


- 회로
 <img width="1032" height="533" alt="image" src="https://github.com/user-attachments/assets/4a993df6-d2a8-4531-800e-15a32d29dd25" />


- 보드 실물
<p align="center">
<img width="424" height="399" alt="image" src="https://github.com/user-attachments/assets/9e833788-4972-4f7f-b289-ba79801e665f" />
</p>

- 핀이 설정이 안되어 있으면 GUI 에서 해당 핀을 클릭하여 설정 할 수 있다.
<p align="center">
  <img width="683" height="691" alt="image" src="https://github.com/user-attachments/assets/be417c62-b2a4-4e2a-80c3-f176c85ed6c1" />
</p>

- GPIO 모드는 크게 Input, Output 모드로 나누어져 있다.
- Input Mode: GPIO 핀으로 외부 입력 High, Low 를 받음
- Output Mode: GPIO 핀으로 외부 입력 High, Low 를 보냄
- 여기서 High, Low Voltage Level 은일반적으로 MCU 공급 전압과 동일하다. 자세한 사항은 Datasheet의 I/O Electricical 특성 참조.




  

  


