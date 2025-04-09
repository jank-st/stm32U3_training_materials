----!
Presentation
----!

# Standby Pullup Retention
For this hands on, we will see how to set up pullup/pulldown retention in Standby mode. For this exercise, we will use the NUCLEO-U083RC. Here are the steps we are going to do in this hands on:

- Enter in Standby​
- How to handle exit from Standby ​
- Monitor activity on LED​
- Keep PU/PD retention during Standby mode​
- Play with CubeMonitorPWR

## Prerequisites
- Software:
  - **[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)** from version 6.12.0
  - **[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)** from version 1.15.1
  - **[STM32CubeMonPWR](https://www.st.com/en/development-tools/stm32cubemonpwr.html)** from version 1.2.1
  - **[STM32U0 Cube library](https://www.st.com/en/embedded-software/stm32cubeu0.html)** from version 1.1.0

- Hardware:
  - **USB-C** cable
  - **[NUCLEO-U083RC](https://www.st.com/en/evaluation-tools/nucleo-u083rc.html)** board
  - **[STLINK-V3PWR](https://www.st.com/en/development-tools/stlink-v3pwr.html#documentation)**

- Documentation:
  - STM32U0 **[Reference Manual](https://www.st.com/resource/en/user_manual/um3261-stm32u0-series-safety-manual-stmicroelectronics.pdf)**
  - STM32U0 **[Data Sheet](https://www.st.com/resource/en/datasheet/stm32u083cc.pdf)**
  - STLINK-V3PWR **[Reference Manual](https://www.st.com/resource/en/user_manual/um3097-source-measurement-unit-smu-and-debuggerprogrammer-for-stm32-microcontrollers-stmicroelectronics.pdf)**
