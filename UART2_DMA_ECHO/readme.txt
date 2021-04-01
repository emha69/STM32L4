This example is using DMA for echoing of received serial data with the idle detection
on UART2 which can be accessed thru VCOM on STM NUCLEO-L476G. The maximum size
of the incoming message can be adjusted in main.h by setting the RXTX_BUF_SIZE value.

Example is adopted from the https://programming.vip/docs/stm32-hal-library-learning-serial-idle-interrupt.html
(original source https://blog.csdn.net/qq_17351161/article/details/90415407)

Steps:

1. Enable idle, transfer complete and error interrupt in MX_USART2_UART_Init() 
2. Add USER_UART_IRQHandler() call into USART2_IRQHandler()
2. Start initial DMA reception of up to RXTX_BUF_SIZE bytes with HAL_UART_Receive_DMA()
3. In USER_UART_IRQHandler() check interrupt source and handle

Note, that transfer complete interrupt is triggered upon initialization before anything is received. The
received bytes are trasmitted after idle interrupt is triggered or max bytes received. Then after transmission 
complete is triggered, the rxtx_buffer is cleared and a new DMA reception cycle is started. The maximum rxtx_buffer 
size in this example can be 65535 bytes.
