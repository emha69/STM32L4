This example is using DMA for echoing of received serial data with the idle detection
on UART2 which can be accessed thru VCOM on STM NUCLEO-L476G. The maximum size
of the incoming message can be adjusted in main.h by setting the RXTX_BUF_SIZE value.

Example is adopted from the https://programming.vip/docs/stm32-hal-library-learning-serial-idle-interrupt.html
(original source https://blog.csdn.net/qq_17351161/article/details/90415407)
