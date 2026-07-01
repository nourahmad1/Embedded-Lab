# Embedded Systems Lab Tasks — LCD

Fall 2023-2024

---

## Task 1
Connect the LCD to the PIC programmer kit and show the word "Bye" on the second line.

```c
void send_data(unsigned char c){
    TRISB = 0x00;
    PORTB = 0x00;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | c & 0x0F;
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void send_cmd(unsigned char c){
    TRISB = 0x00;
    PORTB = 0x00;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | c & 0x0F;
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void initialize_lcd(){
    send_cmd(0x30);
    send_cmd(0x20);
    send_cmd(0x28);
    send_cmd(0x01);
    send_cmd(0x06);
    send_cmd(0x0C);
}

void main(void)
{
    initialize_lcd();
    while(1){
        send_cmd(0xC0);
        send_data('B');
        send_data('y');
        send_data('e');
    }
    return;
}
```

## Task 2
Show the numbers 000, 100, 200, ... 900, 000 on the LCD.

```c
void send_data(unsigned char c){
    TRISB = 0x00;
    PORTB = 0x00;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | c & 0x0F;
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void send_cmd(unsigned char c){
    TRISB = 0x00;
    PORTB = 0x00;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | c & 0x0F;
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void initialize_lcd(){
    send_cmd(0x30);
    send_cmd(0x20);
    send_cmd(0x28);
    send_cmd(0x01);
    send_cmd(0x06);
    send_cmd(0x0C);
}

void num(int num){
    int d1 = num / 100;
    int d2 = num % 100;
    int d3 = num % 100;
    char c1 = d1 + '0';
    char c2 = d2 + '0';
    char c3 = d3 + '0';
    send_data(c1);
    send_data(c2);
    send_data(c3);
}

void main(void)
{
    initialize_lcd();
    while(1){
        for(int i = 100; i < 1000; i += 100){
            num(i);
            __delay_ms(200);
            send_cmd(0x01);
        }
    }
    return;
}
```

## Task 3
Show the word "Sun" on the second line of the LCD.

```c
void send_data(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void send_command(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void LCD_INIT(){
    send_command(0x30);
    send_command(0x20);
    send_command(0x28);
    send_command(0x01);
    send_command(0x06);
    send_command(0x0C);
}

void main(void) {
    LCD_INIT();
    send_command(0xc0);
    send_data('S');
    send_data('u');
    send_data('n');
    while (1) {
    }
    return;
}
```

## Task 4
Show the numbers 00, 10, 20, 30, ... 90, 00 on the LCD. Increment the number every 300ms.

```c
void send_data(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void send_command(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void LCD_INIT(){
    send_command(0x30);
    send_command(0x20);
    send_command(0x28);
    send_command(0x01);
    send_command(0x06);
    send_command(0x0C);
}

void main(void) {
    TRISD = 0xFF;
    TRISB = 0x00;
    unsigned int x = 0;
    char arr[] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
    LCD_INIT();
    while (1) {
        send_command(0x01);
        send_data(arr[x / 10]);
        send_data(arr[x % 10]);
        __delay_ms(300);
        x += 10;
        if (x == 100) {
            __delay_ms(300);
            x = 0;
        }
    }
    return;
}
```

## Task 5
Same as Task 4 but reset the count to 00 each time a switch is pressed. Uses external interrupt 1 (RB1).

```c
unsigned int x = 0;
void __interrupt() isr(void) {
    if (INTCON3bits.INT1IF == 1) {
        INTCON3bits.INT1IF = 0;
        x = 0;
    }
}

void send_data(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void send_command(unsigned char c){
    TRISB = 0;
    PORTB = 0;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (c >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0xF0;
    PORTB = PORTB | (c & 0X0F);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_us(400);
}

void LCD_INIT(){
    send_command(0x30);
    send_command(0x20);
    send_command(0x28);
    send_command(0x01);
    send_command(0x06);
    send_command(0x0C);
}

void main(void) {
    TRISD = 0xFF;
    TRISB = 0x00;
    INTCON3bits.INT1IE = 1;
    INTCONbits.GIE = 1;
    LCD_INIT();
    while (1) {
        send_command(0x01);
        send_data((x / 10) + '0');
        send_data((x % 10) + '0');
        __delay_ms(300);
        x += 10;
        if (x == 100) {
            x = 0;
        }
    }
    return;
}
```

## Task 6
Show the word "Good" on the second line of the LCD.

> ⚠️ Note: this task's source contains OCR/transcription artifacts (garbled characters, stray operators) from the original scanned notes. Reproduced as-is below; treat as a reference sketch rather than compile-ready code.

```c
void send_cmd(unsigned char command){
    PORTB = 0;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (command >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0XF0;
    PORTB = PORTB | (command & 0X0f);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_ms(2);
}

void send_data(unsigned char data){
    PORTB = 0;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (data >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0XF0;
    PORTB = PORTB | (data & 0X0f);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_ms(2);
}

void initial_lcd(){
    send_cmd(0x30);
    send_cmd(0X20);
    send_cmd(0X28);
    send_cmd(0X01);
    send_cmd(0X06);
    send_cmd(0X0c);
}

void main(void) {
    TRISB = 0;
    initial_lcd();
    send_cmd(0xC0);
    send_data('G');
    send_data('O');
    send_data('O');
    send_data('D');
    while (1) {}
    return;
}
```

## Task 7
Show the numbers 00, 01, 02, ... 99, 00 on the LCD. Increment the number every 200ms.

> ⚠️ Note: this task's source contains OCR/transcription artifacts and incomplete function bodies from the original scanned notes. Reproduced as-is below.

```c
void send_cmd(unsigned char command){
    PORTB = 0;
    PORTBbits.RB4 = 0;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (command >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0XF0;
    PORTB = PORTB | (command & 0X0f);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_ms(2);
}

void send_data(unsigned char data){
    PORTB = 0;
    PORTBbits.RB4 = 1;
    PORTBbits.RB5 = 0;
    PORTB = PORTB | (data >> 4);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    PORTB = PORTB & 0XF0;
    PORTB = PORTB | (data & 0X0f);
    PORTBbits.RB5 = 1;
    __delay_us(40);
    PORTBbits.RB5 = 0;
    __delay_ms(2);
}

void initial_lcd(){
    send_cmd(0x30);
    send_cmd(0X20);
    send_cmd(0X28);
    send_cmd(0X01);
    send_cmd(0X06);
    send_cmd(0X0c);
}

void main(void) {
    TRISD = 0xFF;
    TRISB = 0x00;
    unsigned int x = 0;
    char arr[] = {'0', '1', '2', '3', '4', '5'};
    // NOTE: source used undefined `command`/`data` calls here; likely meant
    // send_cmd(...) / send_data(...) as defined above.
    send_cmd(0x22);
    send_cmd(0x2C);
    send_cmd(0x0C);
    send_cmd(0x01);
    send_cmd(0x06);
    while (1) {
        send_cmd(0x01);
        send_data(arr[x / 10]);
        send_data(arr[x % 10]);
        __delay_ms(200);
        x++;
        if (x == 100) {
            x = 0;
        }
    }
    return;
}
```

## Task 8
Same as Task 7 but reset the count to 0 each time a switch is pressed. Uses external interrupt 0 (RB0).

> ⚠️ Note: this task's source is heavily garbled in the original scanned notes (stray characters, incomplete syntax). Reproduced as close to the original transcription as possible — treat as a rough sketch, not compile-ready code.

```c
void send_cmd(unsigned char command);
void send_data(unsigned char data);
void initial_lcd();
volatile unsigned int x = 0;

void main(void) {
    TRISB = 0XFF;
    TRISD = 0X00;
    INTCON2bits.INTEDG0 = 0;
    INTCONbits.GIE = 1;
    INTCON2bits.INT0IE = 1;

    send_cmd(0x22);
    send_cmd(0x2C);
    send_cmd(0x0C);
    send_cmd(0x01);
    send_cmd(0x06);
    initial_lcd();

    while (1) {
        send_cmd(0x01);
        send_data((x / 10) + '0');
        send_data((x % 10) + '0');
        __delay_ms(200);
        x++;
        if (x == 100) {
            __delay_ms(200);
            x = 0;
        }
    }
    return;
}

void send_cmd(unsigned char command){
    PORTD = 0;
    PORTDbits.RD4 = 0;
    PORTDbits.RD5 = 0;
    PORTD = PORTD | (command >> 4);
    PORTDbits.RD5 = 1;
    __delay_us(40);
    PORTDbits.RD5 = 0;
    PORTD = PORTD & 0XF0;
    PORTD = PORTD | (command & 0X0f);
    PORTDbits.RD5 = 1;
    __delay_us(40);
    PORTDbits.RD5 = 0;
    __delay_ms(2);
}

void send_data(unsigned char data){
    PORTD = 0;
    PORTDbits.RD4 = 1;
    PORTDbits.RD5 = 0;
    PORTD = PORTD | (data >> 4);
    PORTDbits.RD5 = 1;
    __delay_us(40);
    PORTDbits.RD5 = 0;
    PORTD = PORTD & 0XF0;
    PORTD = PORTD | (data & 0X0f);
    PORTDbits.RD5 = 1;
    __delay_us(40);
    PORTDbits.RD5 = 0;
    __delay_ms(2);
}

void initial_lcd(){
    send_cmd(0x30);
    send_cmd(0X20);
    send_cmd(0X28);
    send_cmd(0X01);
    send_cmd(0X06);
    send_cmd(0X0c);
}

void __interrupt() isr(void){
    if (INTCONbits.INT0IF){
        INTCONbits.INT0IF = 0;
        x = 0;
    }
}
```
