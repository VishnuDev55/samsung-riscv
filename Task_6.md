# Code
```
#include <ch32v00x.h>
#include <debug.h>

/* PWM Output Mode Definition */
#define PWM_MODE1 0
#define PWM_MODE2 1

/* PWM Output Mode Selection */
#define PWM_MODE PWM_MODE2

// Low-level PWM configuration
void TIM1_PWMOut_Init(u16 arr, u16 psc, u16 ccp) {
    GPIO_InitTypeDef GPIO_InitStructure = {0};
    TIM_OCInitTypeDef TIM_OCInitStructure = {0};
    TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure = {0};

    // Enable GPIO clock and configure PD2 as alternate function push-pull
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_2;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_10MHz;
    GPIO_Init(GPIOD, &GPIO_InitStructure);

    // Enable TIM1 clock and configure timer
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_TIM1, ENABLE);
    TIM_TimeBaseInitStructure.TIM_Period = arr;
    TIM_TimeBaseInitStructure.TIM_Prescaler = psc;
    TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
    TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
    TIM_TimeBaseInit(TIM1, &TIM_TimeBaseInitStructure);

    // Configure PWM mode
#if (PWM_MODE == PWM_MODE1)
    TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM1;
#elif (PWM_MODE == PWM_MODE2)
    TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM2;
#endif

    TIM_OCInitStructure.TIM_OutputState = TIM_OutputState_Enable;
    TIM_OCInitStructure.TIM_Pulse = ccp;
    TIM_OCInitStructure.TIM_OCPolarity = TIM_OCPolarity_High;
    TIM_OC1Init(TIM1, &TIM_OCInitStructure);

    // Enable TIM1 PWM output
    TIM_CtrlPWMOutputs(TIM1, ENABLE);
    TIM_OC1PreloadConfig(TIM1, TIM_OCPreload_Disable);
    TIM_ARRPreloadConfig(TIM1, ENABLE);
    TIM_Cmd(TIM1, ENABLE);
}

// Configure GPIO for input and output
void GPIO_Config(void) {
    GPIO_InitTypeDef GPIO_InitStructure = {0};

    // Enable GPIO clock
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);

    // Configure PD3 as input with pull-up
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_3;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOD, &GPIO_InitStructure);

    // Configure PD6 as output push-pull
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOD, &GPIO_InitStructure);
}

int main(void) {
    uint8_t GPIOInputStatus = 0;
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_1);
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_Config();

    while (1) {
        GPIOInputStatus = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_3);
        if (GPIOInputStatus == 0) {
            // Turn on LED and set PWM to 10% duty cycle
            GPIO_WriteBit(GPIOD, GPIO_Pin_6, SET);
            TIM1_PWMOut_Init(100, 480 - 1, 10);
        } else {
            // Turn off LED and set PWM to 95% duty cycle
            GPIO_WriteBit(GPIOD, GPIO_Pin_6, RESET);
            TIM1_PWMOut_Init(100, 480 - 1, 95);
        }
        Delay_Ms(100);
    }
}

void NMI_Handler(void) {}

void HardFault_Handler(void) {
    while (1) {}
}
```
You should use this code in VS code Platform IO only otherwise it might not work 

# Working Video


https://github.com/user-attachments/assets/31402b1b-48c4-4b91-a82e-5b49b08f9ab2
