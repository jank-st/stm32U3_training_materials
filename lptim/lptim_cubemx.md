----!
Presentation
----!

# LSE crystal
- Configure Low Speed Clock `Crystal/Ceramic Resonator`

![image](./img/LSE.png)


# RealTime Clock unit
To clock LCD by external low speed crystal, the LSE must be activated within RTC configuration.
<p> </p>

- Select **RTC** instance
  
- Tick `Activate Clock Source`


![image](./img/RTC.png)

# LPTIM1 unit
- Mode `Counts internal clock events`

- enable `Channel_1_Active` - assigned to PC1 pin
  
- Select CH1 IO usage as `output`

Kernel clock will be selected LSE 32 768 Hz and requested PWM signal is 100 Hz

- period `327`

- Capture Compare Selection `Compare on CH1 IO`
  
- Pulse value `164`
  
![image](./img/lptim.png)

# Clock Configuration
- Set **MSIS/MSIK** to `96/2 MHz` as `System Clock`
  
- Select **LSE** as source for `LPTIM1`
    
![image](./img/clock.png)

# Project Manager
Project is now ready for generation!

- Select **CubeIDE Toolchain**

- Write project name and `Generate Code`
  