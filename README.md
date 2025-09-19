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

- 코드를 하나씩 살펴보자.
- Void로 반환값이 없는 함수로(함수이름:HAL_GPIO_WritePin) 선언이 되어있다.
<p align="center">
<img width="611" height="230" alt="image" src="https://github.com/user-attachments/assets/0463eb8f-3f65-40a2-8c1a-4c1125db3447" />
</p>

<br>
<br>
- GPIO_TypeDef *GPIOx : GPIO_TypeDef 타입 포인터를 인자로 받는다.

```c

GPIO_TypeDef: typedef로 정의된 구조체 타입(GPIO 레지스터 묶음).

*: 포인터 선언자. “~에 대한 포인터”라는 뜻.

GPIOx: 변수(매개변수) 이름.

-> GPIO_TypeDef 형을 가리키는 포인터인 매개변수 GPIOx를 인자로 받는다.

```
<br>
<br>

- uint16_t GPIO_Pin
```c
uint16_t : (부호 없는 16비트 정수, 0~65535)를 타입으로 갖는

GPIO_Pin : 변수/매개변수 이름
```
<br>
<br>

- GPIO_PinState PinState
```c
GPIO_PinState : enum(열거형) 타입
Pinstate : 변수명
```
<br>
<br>

- 다시 전체 코드를 살펴보자.
```c
void HAL_GPIO_WritePin(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin, GPIO_PinState PinState)
{
  /* Check the parameters */
  assert_param(IS_GPIO_PIN(GPIO_Pin));
  assert_param(IS_GPIO_PIN_ACTION(PinState));

  if (PinState != GPIO_PIN_RESET) // PinState가 'RESET'이 아니면( GPIO_PIN_SET이면) 실행 "!= : 같지 않다. "
  {
    GPIOx->BSRR = GPIO_Pin;      // BSRR 하위 16비트에 마스크 기록 → 해당 핀(들) SET " -> :멤버 접근(포인터) 연산자 ptr->member == (*ptr).member" 
  }
  else
  {
    GPIOx->BSRR = (uint32_t)GPIO_Pin << 16u; // 왼쪽으로 시프트하여 BSRR 상위 16비트에 마스크 기록 → 해당 핀들 RESET "<< 16u : 왼쪽으로 16 비트 시프트"
}
  }
}
```
<br>
<br>

- HAL_GPIO_WritePin의 구성을 알아 보았으니 함수를 이용하여 LED를 ON/OFF 시켜보자.
  ```c
    HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET);
	  HAL_Delay(1000);
	  HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);
	  HAL_Delay(1000);
  ```
<br>
<br>

- 본래 HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET); 식으로 작성하여야 하나 main.h 에 LD2가 정의되어 있어 위와 같이 코드를 써도 무관하다. (GUI에서 User Label을 설정 했기 때문에 자동으로 생성)
- main.h 이미지
<p align="center">
<img width="198" height="35" alt="image" src="https://github.com/user-attachments/assets/d2d594ed-a9b8-4941-a533-21f0dd840609" />
</p>
<br>
<br>

- HAL_Delay( )는 ()ms 만큼 딜레이를 주는 함수이다.
- HAL_Delay(1000) : 1s
- HAL_Delay(1)    : 1ms

<br>
<br>

### 2. SW이용 LED 제어 프로젝트
- Nucleo 보드의 B1 스위치를 이용할 것이다. 기본 설정에서 B1이 GPIO_EXTI(외부 인터럽트) 로써 활성화 되어 있다.
<p align="center">
   <img width="682" height="563" alt="image" src="https://github.com/user-attachments/assets/e7e99403-008b-4f8a-9273-bfd66c92150f" />
</p>
<br>
<br>

- 여기서는 Input 모드로 사용 할 것이므로 바꿔준다. B1 스위치에 외부 PullUp 저항이 HW적으로 구성 되어 있어 GPIO 설정에서 PullUp 설정이 불필요하다.(하여도 무관)
<p align="center">
<img width="717" height="675" alt="image" src="https://github.com/user-attachments/assets/109bb69b-d8f8-4e32-8229-ba11787b986b" />
</p>
- B1 스위치 회로
<p align="center">
<img width="496" height="315" alt="image" src="https://github.com/user-attachments/assets/60df6662-7c56-4d50-a7dc-e2dff7a6a36a" />
</p>
<br>
<br>

- GPIO Init(GPIO 초기설정) 코드를 살펴보자.
<p align="center">
<img width="437" height="424" alt="image" src="https://github.com/user-attachments/assets/5470c843-b72f-451c-9eaa-14fa1d227f21" />
</p>
<br>
<br>

```c
static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
  /* USER CODE BEGIN MX_GPIO_Init_1 */

  /* USER CODE END MX_GPIO_Init_1 */

  /* GPIO Ports Clock Enable */
  __HAL_RCC_GPIOC_CLK_ENABLE();
  __HAL_RCC_GPIOD_CLK_ENABLE();
  __HAL_RCC_GPIOA_CLK_ENABLE();
  __HAL_RCC_GPIOB_CLK_ENABLE();

  /*Configure GPIO pin Output Level */
  HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);

  /*Configure GPIO pin : B1_Pin */
  GPIO_InitStruct.Pin = B1_Pin;
  GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  HAL_GPIO_Init(B1_GPIO_Port, &GPIO_InitStruct);

  /*Configure GPIO pin : LD2_Pin */
  GPIO_InitStruct.Pin = LD2_Pin;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(LD2_GPIO_Port, &GPIO_InitStruct);

  /* USER CODE BEGIN MX_GPIO_Init_2 */

  /* USER CODE END MX_GPIO_Init_2 */
}
```
<br>
<br>

- GPIO Writen 함수를 직관적으로 보기위해 1, 0을(GPIO_SET,REST과 동일) ON, OFF로 매크로 선언하여 정의해주고 사용하겠다.
- #define : #define 매크로 선언 매크로 할 것
- ex)#define ON 1 : ON을 쓰면 전처리기에서 1로 치환한다.
<p align="center">
<img width="176" height="93" alt="image" src="https://github.com/user-attachments/assets/cdff545a-702f-4ee9-a5a7-e8d9752d580f" />
</p>
<br>
<br>

- 일정시간 동안 스위치가 눌려야 감지하도록 하는 변수와, LED 상태 제어를 위한 함수를 선언한다.
```c
  /* USER CODE BEGIN 2 */
int debounce_delay = 160;
int led_state = 0;
  /* USER CODE END 2 */
```
<br>
<br>

- B1 스위치의 입력을 받아 LD2를 Toggle 시키는 코드를 작성해보자.  
```c
  while (1)
  {
	  if(HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin)== ON){
	 		  HAL_Delay(debounce_delay);
	 		  if(HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin)== ON){
	 			 led_state = led_state^1;
	 			 HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, led_state);
	 		  }
	  }
```






 










 

 

 

   





  

  


