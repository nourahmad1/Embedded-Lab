# Embedded Systems Lab Tasks — Motors

Fall 2023-2024

---

## Task 1 — DC Motor
Rotate the DC motor with low speed (duty cycle = 40%) for 4 seconds then stop it for 2 seconds then rotate it with higher speed (duty cycle = 70%) for 3 seconds then stop the motor.

```c
void main(void) {
    TRISB = 0;
    PORTBbits.RB1 = 0;
    for (int i = 0; i < 40; i++)
    {
        PORTBbits.RB2 = 1;
        __delay_ms(40);
        PORTBbits.RB2 = 0;
        __delay_ms(60);
    }
    for (int i = 0; i < 20; i++)
    {
        PORTBbits.RB2 = 1;
        __delay_ms(0);
        PORTBbits.RB2 = 0;
        __delay_ms(100);
    }
    for (int i = 0; i < 30; i++)
    {
        PORTBbits.RB2 = 1;
        __delay_ms(70);
        PORTBbits.RB2 = 0;
        __delay_ms(30);
    }
    while (1) {
        PORTBbits.RB2 = 1;
        __delay_ms(0);
        PORTBbits.RB2 = 0;
        __delay_ms(100);
    }
    return;
}
```

## Task 2 — Stepper Motor
Rotate the stepper motor 1/8 rotation using full steps, stop for 2 seconds, then rotate it for another 1/8 rotation with the highest possible speed. (Each rotation is 2048 full steps or 4096 half steps.)

```c
void main(void) {
    TRISB = 0;
    while (1) {
        for (int i = 0; i < 64; i++)
        {
            RB3 = 1; RB4 = RB5 = RB6 = 0;
            __delay_ms(10);
            RB4 = 1; RB3 = RB5 = RB6 = 0;
            __delay_ms(10);
            RB5 = 1; RB3 = RB4 = RB6 = 0;
            __delay_ms(10);
            RB6 = 1; RB3 = RB5 = RB4 = 0;
            __delay_ms(10);
        }
        __delay_ms(2000);
        for (int i = 0; i < 64; i++)
        {
            RB3 = 1; RB4 = RB5 = RB6 = 0;
            __delay_ms(1);
            RB4 = 1; RB3 = RB5 = RB6 = 0;
            __delay_ms(1);
            RB5 = 1; RB3 = RB4 = RB6 = 0;
            __delay_ms(1);
            RB6 = 1; RB3 = RB5 = RB4 = 0;
            __delay_ms(1);
        }
    }
    while (1) {}
    return;
}
```

## Task 3 — Servo Motor
Move the arm of the servo motor to 0 degrees for 2 seconds then to 60 for 2 seconds then to 180 for 2 seconds and then back to 0.

```c
void main(void) {
    TRISB = 0;
    for (int i = 0; i < 100; i++)
    {
        PORTBbits.RB0 = 1;
        __delay_us(500);
        PORTBbits.RB0 = 0;
        __delay_us(19500);
    }
    for (int i = 0; i < 100; i++)
    {
        PORTBbits.RB0 = 1;
        __delay_us(830);
        PORTBbits.RB0 = 0;
        __delay_us(19170);
    }
    for (int i = 0; i < 100; i++)
    {
        PORTBbits.RB0 = 1;
        __delay_us(2500);
        PORTBbits.RB0 = 0;
        __delay_us(17500);
    }
    while (1)
    {
        PORTBbits.RB0 = 1;
        __delay_us(500);
        PORTBbits.RB0 = 0;
        __delay_us(19500);
    }
    return;
}
```

## Task 4 — DC Motor
Rotate the DC motor with high speed (duty cycle = 80%) for 4 seconds then stop it for 2 seconds then rotate it with lower speed (duty cycle = 40%) for 3 seconds then stop the motor.

```c
void main(void) {
    TRISB = 0;
    PORTBbits.RB1 = 0;
    for (int i = 0; i < 40; i++)
    {
        PORTBbits.RB2 = 1;
        __delay_ms(80);
        PORTBbits.RB2 = 0;
        __delay_ms(20);
    }
    __delay_ms(2000);
    PORTBbits.RB1 = 0;
    for (int i = 0; i < 30; i++)
    {
        PORTBbits.RB2 = 1;
        __delay_ms(40);
        PORTBbits.RB2 = 0;
        __delay_ms(60);
    }
    while (1)
    {
        PORTBbits.RB1 = 0;
        PORTBbits.RB2 = 0;
    }
    return;
}
```

## Task 5 — Stepper Motor
Rotate the stepper motor 1/8 rotation using full steps. (Each rotation is 2048 full steps or 4096 half steps.)

```c
void main(void) {
    TRISB = 0;
    for (int i = 0; i < 64; i++)
    {
        PORTB = 0x08;
        __delay_ms(10);
        PORTB = 0x10;
        __delay_ms(10);
        PORTB = 0x20;
        __delay_ms(10);
        PORTB = 0x40;
        __delay_ms(10);
    }
    while (1) {}
    return;
}
```

## Task 6 — Servo Motor
Move the arm of the servo motor to 90 degrees, wait for 2 seconds, then move it back to 0.

```c
void main(void) {
    TRISB = 0;
    PORTBbits.RB0 = 1;
    __delay_ms(1);
    __delay_us(500);
    PORTBbits.RB0 = 0;
    __delay_ms(18);
    __delay_us(500);
    __delay_ms(2000);
    PORTBbits.RB0 = 1;
    __delay_us(500);
    PORTBbits.RB0 = 0;
    __delay_ms(19);
    __delay_us(500);
    while (1) {}
    return;
}
```

## Task 7 — DC Motor
Rotate the DC motor with low speed (duty cycle = 30%) for 3 seconds then stop it for 2 seconds then rotate it with higher speed (duty cycle = 70%) for 3 seconds then stop the motor.

```c
void mydelay(unsigned int m);

void main(void) {
    TRISB = 0;
    PORTBbits.RB1 = 0;
    for (int i = 0; i < 30; i++) {
        PORTBbits.RB2 = 1;
        mydelay(30);
        PORTBbits.RB2 = 0;
        mydelay(70);
    }
    PORTBbits.RB2 = 0;
    __delay_ms(300);
    for (int i = 0; i < 30; i++) {
        PORTBbits.RB2 = 1;
        mydelay(70);
        PORTBbits.RB2 = 0;
        mydelay(30);
    }
    while (1) {
        PORTBbits.RB2 = 0;
        PORTBbits.RB1 = 0;
    }
    return;
}

void mydelay(unsigned int m)
{
    for (int i = 0; i < m; i++) {
        __delay_ms(1);
    }
}
```

## Task 8 — Stepper Motor
Rotate the stepper motor 1/6 rotation using full steps. (Each rotation is 4096 steps.)

```c
void mydelay(unsigned int m);

void main(void) {
    TRISB = 0;
    for (int i = 0; i < 85; i++) {
        RB3 = 1; RB4 = RB5 = RB6 = 0;
        __delay_ms(10);
        RB4 = 1; RB3 = RB5 = RB6 = 0;
        __delay_ms(10);
        RB5 = 1; RB3 = RB4 = RB6 = 0;
        __delay_ms(10);
        RB6 = 1; RB3 = RB5 = RB4 = 0;
        __delay_ms(10);
        mydelay(70);
    }
    while (1) {}
    return;
}

void mydelay(unsigned int m) {
    for (int i = 0; i < m; i++) {
        __delay_ms(1);
    }
}
```

## Task 9 — Servo Motor
Move the arm of the servo motor to 135 degrees, wait for 2 seconds, then move it back to 0.

```c
void mydelay(unsigned int m);

void main(void) {
    TRISB = 0;
    PORTB = 0X01;
    __delay_us(500);
    PORTB = 0;
    __delay_us(19500);
    __delay_ms(3000);
    for (int i = 0; i < 100; i++) {
        PORTB = 0X01;
        __delay_us(2000);
        PORTB = 0;
        __delay_us(18000);
    }
    while (1) {
        PORTB = 0X01;
        __delay_us(500);
        PORTB = 0;
        __delay_us(19500);
    }
    return;
}
```

---

*Done by: Marah Salahat — Good Luck*
