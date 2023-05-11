# ARTNDE001_MEC4126_PRAC10
QUES2
void init_timer_2(void)
{
    // Enable GPIOB clock
    RCC->AHBENR |= RCC_AHBENR_GPIOBEN;

    // Setup GPIOB pin 10 as alternate function
    GPIOB->MODER |= GPIO_MODER_MODER10_1;

    // Select alternate function: TIM2_CH3
    GPIOB->AFR[1] |= (2 << 2 * 4);

    // Enable Timer 2 clock
    RCC->APB1ENR |= RCC_APB1ENR_TIM2EN;

    // Set clock source to 15 kHz
    TIM2->PSC = 2;  // Any combination close to 15 kHz is acceptable

    // Setup ARR to reload after 1023 (for 10-bit ADC) counts
    TIM2->ARR = 1023;  // Any value close to 1023 is acceptable

    // Output, PWM mode 1, enable OC3 preload
    TIM2->CCMR2 |= TIM_CCMR2_OC3M_2 | TIM_CCMR2_OC3M_1 | TIM_CCMR2_OC3PE;

    // Enable output
    TIM2->CCER |= TIM_CCER_CC3E;

    // Enable counter for Timer 2
    TIM2->CR1 |= TIM_CR1_CEN;

    // Set CCR3 to 25% of ARR
    TIM2->CCR3 = 1023 / 4;
}

