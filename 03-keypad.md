# Embedded Systems Lab Tasks — Keypad

Fall 2023-2024

---

## Task 1
Connect the Keypad and the LEDs to the PIC programmer kit. Each time KEY n is pressed, the LEDs blink n times (blink every 300 ms).

```c
void main(void)
{
    TRISD = 0;
    TRISB = 0xf0;
    while (1)
    {
        PORTBbits.RB0 = 1;
        PORTBbits.RB1 = 0;
        PORTBbits.RB2 = 0;
        if (PORTBbits.RB0 == 1)
        {
            if (PORTBbits.RB4 == 1)
            {
                for (int i = 0; i < 1; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB5 == 1)
            {
                for (int i = 0; i < 4; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB6 == 1)
            {
                for (int i = 0; i < 7; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
        }
        __delay_ms(50);

        PORTBbits.RB0 = 0;
        PORTBbits.RB1 = 1;
        PORTBbits.RB2 = 0;
        if (PORTBbits.RB1 == 1)
        {
            if (PORTBbits.RB4 == 1)
            {
                for (int i = 0; i < 2; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB5 == 1)
            {
                for (int i = 0; i < 5; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB6 == 1)
            {
                for (int i = 0; i < 8; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
        }
        __delay_ms(50);

        PORTBbits.RB0 = 0;
        PORTBbits.RB1 = 0;
        PORTBbits.RB2 = 1;
        if (PORTBbits.RB1 == 1)
        {
            if (PORTBbits.RB4 == 1)
            {
                for (int i = 0; i < 3; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB5 == 1)
            {
                for (int i = 0; i < 6; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
            if (PORTBbits.RB6 == 1)
            {
                for (int i = 0; i < 9; i++)
                {
                    PORTD = 255;
                    __delay_ms(300);
                    PORTD = 0;
                    __delay_ms(300);
                }
            }
        }
        return;
    }
}
```

## Task 2
Connect the Keypad and the LEDs to the PIC programmer. Key 1 turns on the LEDs, Key 4 turns off the LEDs, Key 7 blinks all LEDs every 300 ms.

```c
int i = -1;
void main(void)
{
    TRISB = 0xF0;
    TRISD = 0x00;
    PORTBbits.RB0 = 1;
    PORTBbits.RB1 = 0;
    PORTBbits.RB2 = 0;
    while (1)
    {
        if (PORTBbits.RB4 == 1)
        {
            i = 0;
        }
        if (PORTBbits.RB5 == 1)
        {
            i = 1;
        }
        if (PORTBbits.RB6 == 1)
        {
            i = 2;
        }
        if (i == 0)
        {
            PORTD = 0xFF;
            __delay_ms(300);
        }
        else if (i == 1)
        {
            PORTD = 0x00;
            __delay_ms(300);
        }
        else if (i == 2)
        {
            while (1)
            {
                PORTD = 0xFF;
                __delay_ms(300);
                PORTD = 0x00;
                __delay_ms(300);
            }
        }
        return;
    }
}
```

## Task 3
Connect the Keypad and the LEDs to the PIC programmer. Turn on one LED. Key x shifts/rotates the LEDs x steps.

> No solution provided.
