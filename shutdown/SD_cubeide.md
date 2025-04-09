----!
Presentation
----!
# Application code - Features

Here are the different steps of the application:

- When the User push-button is pressed a falling edge is detected on the EXTI line and an interrupt is generated.
- The system set the RTC & enters SHUTDOWN.
- The system will resume after 2 seconds.
- After wake-up from SHUTDOWN mode, program execution restarts from the beginning.


LED4 is used to monitor the system state as follows:

 - **LED4 toggling**: system is restarting and *out-of-shutdown* has been detected
 - **LED4 is ON**: system in RUN mode
 - **LED4 OFF**: system in SHUTDOWN mode

# Application code - *Initialization variable*

Add variable to know if system was resumed from shutdown.

in *USER CODE PV* section, add:

```c
static uint32_t out_of_shutdown;
```

in the *USER CODE 1* section, add:

```c
out_of_shutdown = 0;
```

# Application code - *Main application*

Add the following code in the *USER CODE 2* section:

```c
/* Enable Power Clock */
__HAL_RCC_PWR_CLK_ENABLE();
HAL_PWR_EnableBkUpAccess();

/* Check if the system was resumed from shutdown mode,
     resort to RTC-TAMP back-up register BKP15R to verify
     whether or not shutdown entry flag was set by software
     before entering shutdown mode.  */
if (READ_REG(TAMP->BKP1R) == 1)
{
    WRITE_REG( TAMP->BKP1R, 0x0 );  /* reset back-up register */
    out_of_shutdown = 1;            /* out of shutdown detected */
    /* Toggle LED4 */
    HAL_Delay(200);
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(200);
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(200);
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(200);
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(200);
}

/* Turn on LED4 */
HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
```

# Application code - *Interrupt management*

Add the following code in the *USER CODE 4* section:

```c
/**
  * @brief EXTI line detection callbacks
  * @param GPIO_Pin: Specifies the pins connected EXTI line
  * @retval None
  */
void HAL_GPIO_EXTI_Falling_Callback(uint16_t GPIO_Pin)
{
    /* Set RTC-TAMP back-up register BKP15R to indicate
       later on that system has entered shutdown mode  */
    WRITE_REG( TAMP->BKP1R, 0x1 );

	/* Set RTC to wake up system after 2s */
	HAL_RTCEx_SetWakeUpTimer_IT(&hrtc, 0xFFF, RTC_WAKEUPCLOCK_RTCCLK_DIV16, 0);

    /* Enable Ultra low power RTC */
    HAL_RTCEx_SetLowPowerCalib(&hrtc, RTC_LPCAL_SET);

    /* Enter shutdown mode */
    HAL_PWR_EnterSHUTDOWNMode();
}
```
