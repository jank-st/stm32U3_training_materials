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

- Select **RTC** instance
  
- Tick `Activate Clock Source`

- Select `Internal WakeUp` for WakeUp option
  
- Set `Wake Up clock to 1Hz` base
  
- Set `counter to 1`. Periodic wake up event occurs every 2 seconds

- Enable `RTC and TAMP interrupts` under NVIC tab

![image](./img/RTC.png)

# Clock Configuration
- Change **MSIS** to `96/2 MHz` as `System Clock`
  
- Select **LSE** as source for `RTC` 
<p> </p>

![image](./img/clock.png)

# Project Manager
Project is now ready for generation!

- Select **CubeIDE Toolchain**

- Write project name and `Generate Code`
  
  