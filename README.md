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

