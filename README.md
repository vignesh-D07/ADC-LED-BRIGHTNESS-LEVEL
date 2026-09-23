# ADC-LED-BRIGHTNESS-LEVEL
## AIM:Analyse the relationship between potentiometer position, ADC output, and LED brightness by developing a program to control LED intensity using the potentiometer. Compare the ADC values with the observed brightness levels. 
---

## Apparatus Required

| S. No. | Apparatus / Software | Specification |
|:---:|---|---|
| 1 | Microcontroller Development Board | **NXP S32K144 Development Board** |
| 2 | IDE | **S32 Design Studio** |
| 3 | Programming Language | **Embedded C** |
| 4 | SDK | **S32K144 SDK** |
| 5 | LED | On-board LED / External LED |
| 6 | Programmer / Debugger | On-board Debugger / OpenSDA |
| 7 | USB Cable | For programming and power supply |

---
## Procedure
1. Connect the S32K144 Development Board to the computer using a USB cable.
2. Open S32 Design Studio.
3. Create a new project for the S32K144 microcontroller.
4. Select and configure the appropriate S32K144 SDK for the project.
5. Identify the GPIO pin connected to the LED on the S32K144 development board.
6. Configure the selected GPIO pin/Drivers as a Digital Output/input.
7. Initialize the required GPIO peripheral using the GPIO initialization functions provided by the S32K144 SDK.
8. Write the Embedded C program to control the LED using the GPIO Toggle-Pin API.
9. Insert a one-second delay between successive GPIO toggle operations.
10. The program should continuously execute the following sequence.
11. Build the project in S32 Design Studio.
12. Verify that the project is compiled successfully without errors.
13. Connect the debugger/programmer to the S32K144 Development Board.
14. Download the generated program to the S32K144 microcontroller.
15. Run the program on the S32K144 board.

---
## Program
```
#include "sdk_project_config.h"
#include "peripherals_adc_pal_1.h"

uint16_t AdcStatus;

int main(void) {
    CLOCK_DRV_Init(&clockMan1_InitConfig0);
    PINS_DRV_Init(NUM_OF_CONFIGURED_PINS0, g_pin_mux_InitConfigArr0);
    PWM_Init(&pwm_pal_1_instance, &pwm_pal_1_configs);
    ADC_Init(&adc_pal_1_instance, &adc_pal_1_config);
    while (1) {
        ADC_StartGroupConversion(&adc_pal_1_instance, 0U);
        AdcStatus = adc_pal_1_results0[0];
        PWM_UpdateDuty(&pwm_pal_1_instance, 0U, AdcStatus);
        OSIF_TimeDelay(500);
    }
}

```
---
## OUTPUT
<img width="1914" height="1199" alt="image" src="https://github.com/user-attachments/assets/252fd77f-05fd-4245-bb93-39e7b729a959" />

---
## Result

The relationship between the **potentiometer position, ADC output, and LED brightness** was successfully analyzed. As the potentiometer position was varied, the **ADC value changed accordingly**, and the LED brightness was controlled using the corresponding ADC value. The LED brightness increased with an increase in ADC value and decreased with a decrease in ADC value, confirming the relationship between **potentiometer position, ADC output, and PWM-controlled LED intensity**.
