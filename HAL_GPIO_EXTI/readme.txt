This is a HAL based GPIO external interrupt example, based on STM32CubeIDE version 1.6.1.
and for NUCLEO STM32L476G board. Each time the BLUE BUTTON on the board is pushed, the
GREEN LED toggle speed changes from faster to slower and vice versa.

Important steps (see USER sections in the code)

1. Create project configuration with STM32CubeMX

2. Make sure that PC13 pin is configured as GPIO_EXTI_13

3. In System Core -> GPIO configuration make sure that:
   - GPIO Mode is set to "External Interrupt Mode with Falling edge trigger detection"
   - on the NVIC tab make sure that EXTI line[15:10] interrupts are enabled
   
4. Generate IDE project

5. In main.c
  - include "stm32l4xx_hal_exti.h"
  - define EXTI_HandleTypeDef e.g. hpb_exti_13 = {.Line = EXTI_LINE_13};
  - define ISR function prototype e.g. static void BUTTON_EXTI_ISR(void);
  
6. In main.c initialize EXTI interupt by calling
  - HAL_EXTI_GetHandle()
  - HAL_EXTI_RegisterCallback() to register the callback

7. In main.c enable EXTI and set NVIC priority by calling
  - HAL_NVIC_SetPriority()
  - HAL_NVIC_EnableIRQ()
  
8. Implement ISR function

9. In stm32l4xx_it.c 
  - add extern EXTI_HandleTypeDef hpb_exti_13;
  - in function void EXTI15_10_IRQHandler(void) replace generated call HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_13) with HAL_EXTI_IRQHandler(&hpb_exti_13);
  

   
   
   
   
