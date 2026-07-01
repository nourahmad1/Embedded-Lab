# Embedded Systems Lab Tasks — 7-Segment Display

Fall 2023-2024

---

## Task 1
Show the numbers 1, 3, 5, 7, 9, 1, .... Change the number every 1 second.

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    char arr[10] = {0x40, 0xF9, 0x48, 0x30, 0x19, 0x12, 0x10, 0x78, 0x00, 0x10};
    while (1)
    {
        for (int i = 1; i <= 10; i += 2)
        {
            PORTA = 0;
            PORTB = arr[i];
            PORTA = 0x01;
            __delay_ms(1000);
        }
    }
    return;
}
```

## Task 2
Same as Task 1 but connect the switches and reset the display to 1 each time SW0 is pressed.

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    TRISD = 0Xff;
    char arr[10] = {0x40, 0Xf9, 0x48, 0x30, 0x19, 0x12, 0x10, 0x78, 0x00, 0x10};
    while (1)
    {
        for (int i = 1; i <= 10; i += 2)
        {
            if (PORTDbits.RD0 == 1)
                i = 1;
            PORTA = 0;
            PORTB = arr[i];
            PORTA = 0x01;
            __delay_ms(1000);
        }
    }
    return;
}
```

## Task 3
Show the numbers 90, 80, 70, ... 00, 90, 80, ... Change the number every 0.5 second.

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    TRISD = 0xFF;
    char arr[10] = {0x40, 0xF9, 0x24, 0x30, 0x19, 0x12, 0x02, 0x78, 0x00, 0x10};
    while (1)
    {
        for (int i = 9; i > 0; i--)
        {
            for (int j = 0; j < 250; j++)
            {
                PORTA = 0;
                PORTB = arr[i];
                PORTA = 0x01;
                __delay_ms(1);
                PORTA = 0;
                PORTB = arr[0];
                PORTA = 0x02;
                __delay_ms(1);
            }
        }
    }
    return;
}
```

## Task 4
Show the numbers 0, 1, 2, 3 ... 9, 1, 2, ... Switch every 300 ms.

```c
void main(void)
{
    char arr[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    TRISA = 0x00;
    TRISB = 0x00;
    PORTA = 0x00;
    int i = 1;
    while (1)
    {
        PORTB = arr[i];
        PORTA = 0x01;
        __delay_ms(300);
        PORTA = 0x00;
        i++;
        if (i == 10)
            i = 1;
    }
    return;
}
```

## Task 5
Same as Task 1. Switching time is 1 second. Each time SW0 is pressed, the seven segment restarts counting from 0.

```c
void main(void)
{
    char arr[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    TRISA = 0x00;
    TRISB = 0x00;
    TRISD = 0x01;
    int j = 1;
    while (1)
    {
        PORTA = 0x00;
        for (int i = 0; i < 300; i++)
        {
            PORTB = arr[j];
            PORTA = 0x01;
            __delay_ms(0.5);
            PORTA = 0x00;
            if (RD0 == 1)
            {
                i = 0;
                j = 1;
            }
        }
        if (j == 9)
        {
            j = 1;
        }
        else
            j++;
    }
    return;
}
```

## Task 6
Show the numbers 10, 20, 30 ... 90, 10, 20, ... Switch every 600 ms.

```c
void main(void)
{
    char arr[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    TRISA = 0x00;
    TRISB = 0x00;
    PORTA = 0x00;
    unsigned int i, j;
    for (i = 1; i <= 9; i++)
    {
        for (j = 0; j <= 300; j++)
        {
            PORTA = 0x02;
            PORTB = arr[0];
            __delay_ms(1);
            PORTA = 0x01;
            PORTB = arr[i];
            __delay_ms(1);
        }
    }
    return;
}
```

## Task 7
Show the numbers 9, 8, 7, ... 1, 9, 8 (change every 1 sec).

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    char num[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    while (1)
    {
        for (int i = 9; i >= 1; i--)
        {
            PORTA = 0;
            PORTB = num[i];
            PORTA = 0x01;
            __delay_ms(1000);
        }
    }
    return;
}
```

## Task 8
Same as Task 7 but connect the switches. Each time SW0 is pressed, the counting restarts from 9.

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    TRISD = 0XFF;
    char num[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    while (1)
    {
        for (int i = 9; i >= 1; i--)
        {
            PORTA = 0;
            PORTB = num[i];
            PORTA = 0x01;
            for (int K = 1; K <= 10; K++)
            {
                __delay_ms(100);
                if (RD0 == 1)
                {
                    i = 10;
                }
            }
        }
    }
    return;
}
```

## Task 9
Show the numbers 01, 02, 03, ..., 09, 01, 02 (change every 0.5 sec).

```c
void main(void)
{
    TRISA = 0;
    TRISB = 0;
    char num[10] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x98};
    while (1)
    {
        for (int i = 9; i >= 1; i--)
        {
            for (int k = 0; k < 250; k++)
            {
                PORTA = 0;
                PORTB = num[0];
                PORTA = 0x01;
                __delay_ms(1);
                PORTA = 0;
                PORTB = num[i];
                PORTA = 0x02;
                __delay_ms(1);
            }
        }
    }
    return;
}
```
