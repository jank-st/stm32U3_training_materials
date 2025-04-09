----!
Presentation
----!

# LSE crystal
- Configured Low Speed Clock `Crystal/Ceramic Resonator`
- Already done in default configuration 

![image](./img/LSE.png)


# RealTime Clock unit
To clock RTC and LPUART by external low speed crystal, the LSE must be activated within RTC configuration.
<p> </p>

Note that **LSESYSEN bit in BDCR** must be enabled as well (missing in RM description), otherwise LSE is not clocked. It's already enabled by default in `HAL_RCC_OscConfig()` function call.

- Select **RTC** instance
  
- Tick `Activate Clock Source`

- Select `Internal WakeUp` for WakeUp option
  
- Set `Wake Up clock to 1Hz` base
  
- Set `counter to 1`. Periodic wake up event occurs every 2 seconds

- Enable `RTC and TAMP interrupts` under NVIC tab

![image](./img/RTC.png)

# Low Power UART
- LPUART1 is connecetd to STlink via PA2/3 pins and acts as Virtual Comport

- Select **LPUART1** instance
  
- Configure `Asynchronous mode`

- Remap TX/RX to `PA2/3` *(hold CTRL + left mouse click)*

- `Baudrate` = 9600​

- `Enable FIFO mode`​
  - TxFIFO Th. = Empty​
  - RXFIFO Th. = Full

- Enable `USART3 + LPUART1 global interrupt` under NVIC tab

![image](./img/LPUART.png)

# Clock Configuration
- Change **MSI** to `1 MHz` as `System Clock`
  
- Select **LSE** as source for `RTC/LCD` to be able active in down to Stop2 mode

- Select **LSE** as source for `LPUART1`
<p> </p>

![image](./img/clock.png)

# Project Manager
Project is now ready for generation!

- Select **CubeIDE Toolchain**

- Write project name and `Generate Code`
  
![image](./img/generate_project.png)
  