# FIRMWARE-2025.09.19-D_1
### 1. LED 제어 프로젝트

- MCU 내부 클럭을 사용할 것이므로 RCC 에서 HSE, LSE를 Disable 한다.
- RCC(Reset and Clock Control)
<br>
<br>
<img width="1696" height="866" alt="image" src="https://github.com/user-attachments/assets/9b4961cb-ab28-4f72-a697-9edd09f61135" />
<br>
<br>

- Clock Configuration에서 외부 Clk 비 활성화 확인.
<br>
<br>
<img width="1687" height="865" alt="image" src="https://github.com/user-attachments/assets/7c3cd669-778d-40d9-a8cc-f1bc787fb752" />
<br>
<br>

### Clk 는 2가지 종류
- HSE(High Speed External Clock)
- LSE(Low Speed External Clock)
- 내부 기능의 용도에 따라 2 가지로 외부 Clk가 나누어져있다.
<br>
<br>

### GPIO 설정
- LED 제어가 목적이므로 GPIO를 설정한다.
- GPIO(General Purpose Input Output)
- Nucleo-64 개발보드의 LED(LD2)를 사용할 것이므로 별도로 추가적인 LED 설정이 필요 없다. 기본 설정으로 LD2이 활성화 되어있다.
  <img width="1692" height="875" alt="image" src="https://github.com/user-attachments/assets/d98ede98-592b-41e0-89cf-02bc6db2fb77" />
<br>
<br>

- 회로
 <img width="1032" height="533" alt="image" src="https://github.com/user-attachments/assets/4a993df6-d2a8-4531-800e-15a32d29dd25" />
<br>
<br>

- 보드 실물
<p align="center">
<img width="424" height="399" alt="image" src="https://github.com/user-attachments/assets/9e833788-4972-4f7f-b289-ba79801e665f" />
</p>
<br>
<br>

- 핀이 설정이 안되어 있으면 GUI 에서 해당 핀을 클릭하여 설정 할 수 있다.
<p align="center">
  <img width="683" height="691" alt="image" src="https://github.com/user-attachments/assets/be417c62-b2a4-4e2a-80c3-f176c85ed6c1" />
</p>

- GPIO 모드는 크게 Input, Output 모드로 나누어져 있다.
- Input Mode: GPIO 핀으로 입력 High, Low 를 받음
- Output Mode: GPIO 핀으로 출력 High, Low 를 보냄
- 여기서 High, Low Voltage Level 은일반적으로 MCU 공급 전압과 동일하다. 자세한 사항은 MCU Datasheet의 I/O Electricical 특성 참조.
<br>
<br>
<p align="center">
<img width="789" height="489" alt="Voltage" src="https://github.com/user-attachments/assets/68eb8f70-68d4-4ad5-9705-d07270a48741" />
</p>
<br>
<br>
<p align="center">
<img width="905" height="462" alt="image" src="https://github.com/user-attachments/assets/2e870d56-489f-4acb-8510-f1b98d09ed95" />
</p>
<br>
<br>

- GPIO Configuration 설정
<p align="center">
 <img width="550" height="616" alt="image" src="https://github.com/user-attachments/assets/903d0ad0-eead-4051-816f-7ce6611f6e3a" />
 </p>
<br>
<br>

- GPIO 설정에서 Push-Pull, Open-Drain, PullUp, PullDown에 대한 개념 설명은 생략 하도록 하겠다.
<br>
<br>

- Ctrl+S로 저장하면 자동으로 코드 생성 여부를 묻는 알림창이 뜬다. OK를 누르면
<p align="center">
<img width="494" height="147" alt="image" src="https://github.com/user-attachments/assets/deaa6966-6561-4d61-bec1-79efbd08c22c" />
 </p>
<br>
<br>

- 아래와 같이 코드가 생성된다. (필자는 Theme를 변경하여 기본 Theme와 상이하다.)
<p align="center">
<img width="1915" height="1029" alt="image" src="https://github.com/user-attachments/assets/d9287fc5-7252-4ba5-a5a9-5c171dd13ef3" />
 </p>
<br>
<br>

- 코드가 생성되면서 각 핀에 대한 기본 설정이 되어있는데, 이를 코드로써 확인해보자.
- CubeIDE에서 GUI로 설정하였던 내용들이 코드로써 작성 되어있다.
<p align="center">
  <img width="358" height="189" alt="image" src="https://github.com/user-attachments/assets/fc956176-5987-44fa-b3d0-df13fc7700e7" />
   </p>
<br>
<br>


- HAL 라이브러리를 사용하여 핀을 제어해보자.
- HAL(Hadware Abstraction Layer) 로써 STM사 MCU에서 제공하는 라이브러리이이다.
- LED 제어를 위해 While 문 내부에 코드를 일부 쓰고 Ctrl+Space를 누르면 쉽게 코드를 찾을 수 있다.
<p align="center">
<img width="528" height="299" alt="image" src="https://github.com/user-attachments/assets/8baef6ca-0bc6-49a7-a101-44a70cb75318" />
 </p>
<br>
<br>

- HAL_GPIO_WritePin(GPIOx, GPIO_Pin, PinState) 작성 한다.
 <p align="center">
<img width="362" height="142" alt="image" src="https://github.com/user-attachments/assets/863429df-25d2-4ba8-bfbf-14b81aa18432" />
 </p>
<br>
<br>

- 해당 함수의 구조를 보기 위해 
- 코드에 우클릭을 눌러 Open Declaration을 눌러 들어간다.
 <p align="center">
 <img width="439" height="266" alt="image" src="https://github.com/user-attachments/assets/092eea54-b080-4976-aae2-f172db019b98" />
 </p>
 <br>
<br>

```c

void HAL_GPIO_WritePin(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin, GPIO_PinState PinState)
{
  /* Check the parameters */
  assert_param(IS_GPIO_PIN(GPIO_Pin));
  assert_param(IS_GPIO_PIN_ACTION(PinState));

  if (PinState != GPIO_PIN_RESET)
  {
    GPIOx->BSRR = GPIO_Pin;
  }
  else
  {
    GPIOx->BSRR = (uint32_t)GPIO_Pin << 16u;
  }
}
```
 
- 코드를 하나씩 살펴보자.
 
- Void로 반환값이 없는 함수로(함수이름:HAL_GPIO_WritePin) 선언이 되어있다.
<p align="center">
<img width="611" height="230" alt="image" src="https://github.com/user-attachments/assets/0463eb8f-3f65-40a2-8c1a-4c1125db3447" />
</p>

<br>
<br>
- GPIO_TypeDef *GPIOx : GPIO_TypeDef 타입 포인터를 인자로 받는다.

```

GPIO_TypeDef: typedef로 정의된 구조체 타입(GPIO 레지스터 묶음).

*: 포인터 선언자. “~에 대한 포인터”라는 뜻.

GPIOx: 변수(매개변수) 이름.

-> GPIO_TypeDef 형을 가리키는 포인터인 매개변수 GPIOx를 인자로 받는다.

```
<br>
<br>

- uint16_t GPIO_Pin
```
uint16_t : (부호 없는 16비트 정수, 0~65535)를 타입으로 갖는 매개변수 이름

GPIO_Pin : 





 

 

 

   





  

  


