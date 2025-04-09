----!
Presentation
----!
# Application code - main.c
## #define Led Retention
Add the following code in the `Private define` section:

>/* USER CODE BEGIN PD */
>
>/* USER CODE END PD */

```c
#define LEDRETAINED
```

## User Code
Here are the different steps of the application:

- Check if the system was in Standby and then Clear the Standby flag
- Check if the system was resumed with Wakeup pin 2 and then clear its flag. In this case, the LED4 will blink
- if *LEDRETAINED* is defined, configure the pullup retention
- Enable ultra low power mode
- Enable WakeUp Pin PWR_WAKEUP_PIN2 connected to PC.13
- Enter in Standby mode

LED4 is used to monitor the system state as follows:

- **LED4 is ON for 1 sec**: system is restarting
- **LED4 toggling**: system was wake up by WKUP_PIN2
- **LED4 OFF**: system in STANDBY mode without LED retention

Add the following code in the `USER CODE 2` section:

>/* USER CODE BEGIN 2 */
>
>/* USER CODE END 2 */


```c
  /* Turn ON LED for 1 second */
  HAL_Delay(1000);

  /* Check and Clear the Standby flag */
  if(__HAL_PWR_GET_FLAG(PWR_FLAG_SB) != RESET)
  {
  __HAL_PWR_CLEAR_FLAG(PWR_FLAG_SB);
  }

  #ifdef LEDRETAINED
  HAL_PWREx_DisablePullUpPullDownConfig();
  #endif

  /* Check and handle if the system was resumed with Wakeup pin 2 */
  if(__HAL_PWR_GET_FLAG(PWR_FLAG_WUF2) == SET)
  {
    /* Clear Wakeup pin flag */
    __HAL_PWR_CLEAR_FLAG(PWR_FLAG_WUF2);
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

  /* Enable ultra low power mode */
  HAL_PWREx_EnableUltraLowPowerMode();

  #ifdef LEDRETAINED
  HAL_PWREx_EnableGPIOPullUp(PWR_GPIO_A, PWR_GPIO_BIT_5);
  HAL_PWREx_EnablePullUpPullDownConfig();
  #endif

  /* Enable WakeUp Pin PWR_WAKEUP_PIN2 connected to PC.13 */
  HAL_PWREx_EnableGPIOPullUp(PWR_GPIO_C, PWR_GPIO_BIT_13);
  HAL_PWREx_EnablePullUpPullDownConfig();
  HAL_PWR_EnableWakeUpPin(PWR_WAKEUP_PIN2_LOW);
  __HAL_PWR_CLEAR_FLAG(PWR_FLAG_WUF2);

  /* Enter the system to STANDBY mode */
  HAL_PWR_EnterSTANDBYMode();
```

# Run the application
Now it is time to build and run the application on the NUCLEO-U083RC.

Build the project by clicking on the *hammer* icon : ![gif](./img/hammer.png)
Then, Run the application on the NUCLEO-U083RC by clicking on the *play* icon : ![gif](./img/play.png)

![gif](./img/cubeide1.gif)
