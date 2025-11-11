/********************************************************************************/
/*This program demonstrates the interfacing of LCD to PIC18F4550 microcontroller*/
/********************************************************************************/

/*
LCD DATA port----PORT D
signal port------PORT E
    rs-------RE0
    rw-------RE1
    en-------RE2
*/
#include <p18f4550.h>

//LCD data pins connected to PORTD and control pins connected to PORTE
#define LCD_DATA    PORTD               //LCD data port
#define ctrl        PORTE               //LCD signal port
#define en          PORTEbits.RE2      // enable signal
#define rw          PORTEbits.RE1      // read/write signal
#define rs          PORTEbits.RE0     // register select signal
#define BUSY        PORTDbits.RD7

//LCD function definitions
void LCD_Busy(void);
void LCD_cmd(unsigned char cmd);
void init_LCD(void);
void LCD_write(unsigned char data);
void LCD_write_string(static char *str);

/*The following lines of code perform interrupt vector relocation to work with the USB bootloader. These must be
used with every application program to run as a USB application.*/
extern void _startup (void);
#pragma code _RESET_INTERRUPT_VECTOR = 0x1000

void _reset (void)
{
        _asm goto _startup _endasm
}

#pragma code
#pragma code _HIGH_INTERRUPT_VECTOR = 0x1008
void high_ISR (void)
{
}

#pragma code
#pragma code _LOW_INTERRUPT_VECTOR = 0x1018
void low_ISR (void)
{
}
#pragma code
//Function to generate delay
void myMsDelay (unsigned int time)
{
        unsigned int i, j;
        for (i = 0; i < time; i++)
                for (j = 0; j < 710; j++);/*Calibrated for a 1 ms delay in MPLAB*/
}


// Function to initialise the LCD
void init_LCD(void)
{
    LCD_cmd(0x38);      // initialization of 16X2 LCD in 8bit mode
    myMsDelay(15);

    LCD_cmd(0x01);      // clear LCD
    myMsDelay(15);

    LCD_cmd(0x0C);      // cursor off
    myMsDelay(15);

    LCD_cmd(0x80);      // ---8 go to first line and --0 is for 0th position
    myMsDelay(15);

            // ---8 go to first line and --0 is for 0th position

    return;
}
//Function to pass command to the LCD
void LCD_cmd(unsigned char cmd)
{
    LCD_DATA = cmd;
    rs = 0;
    rw = 0;
    en = 1;
    myMsDelay(15);
    en = 0;
    myMsDelay(15);
    return;
}

//Function to write data to the LCD
void LCD_write(unsigned char data)
{
    LCD_DATA = data;
    rs = 1;
    rw = 0;
    en = 1;
    myMsDelay(15);
    en = 0;
    myMsDelay(15);
    return ;
}
//Function to split the string into individual characters and call the LCD_write function
void LCD_write_string(static char *str)   //store address value of the string in pointer *str
{
    int i = 0;
    while (str[i] != 0)
    {
        LCD_write(str[i]);      // sending data on LCD byte by byte
        myMsDelay(15);
                i++;
    }
    return;
}

void main(void)
{     
     char var1[] = "WELCOME";
  	 ADCON1 = 0x0F;        //Configuring the PORTE pins as digital I/O 
     TRISD = 0x00;         //Configuring PORTD as output
     TRISE = 0x00;         //Configuring PORTE as output
	
    
     init_LCD();           // initialization of LCD
     myMsDelay(50);       // delay of 50 mili seconds
     LCD_write_string(var1);
     while (1);
}
/*
Program : To Interface LED's to Port A, B, C, D, E
*/
#include <p18f4550.h>
/*The following lines of code perform interrupt vector relocation to work with the USB bootloader. These must be used with every application program to run as a USB application.*/
extern void _startup (void);
#pragma code _RESET_INTERRUPT_VECTOR = 0x1000

void _reset (void)
{
	_asm goto _startup _endasm
}

#pragma code
#pragma code _HIGH_INTERRUPT_VECTOR = 0x1008
void high_ISR (void)
{
}

#pragma code
#pragma code _LOW_INTERRUPT_VECTOR = 0x1018
void low_ISR (void)
{
}
#pragma code
/*End of interrupt vector relocation*/
/*Start of main program*/
void myMsDelay (unsigned int time)
{
	unsigned int i, j;
	for (i = 0; i < time; i++)
		for (j = 0; j < 710; j++);/*Calibrated for a 1 ms delay in MPLAB*/
}

void main()
{
	TRISA = 0x00;
	TRISB = 0x00;
	TRISC = 0x00;
	TRISD = 0x00;
	TRISE = 0x00;
	INTCON2bits.RBPU=0; 
	ADCON1 = 0x0F;
	while(1)
	{
		LATA = 0x55;
		LATB = 0x55;
		LATC = 0x55;
		LATD = 0x55;
		LATE = 0x55;
		myMsDelay(300);
		LATA = 0xAA;
		LATB = 0xAA;
		LATC = 0xAA;
		LATD = 0xAA;
		LATE = 0xAA;
		myMsDelay(300);
	}
}

				
/** I N C L U D E S ********/

#include<p18f4550.h>




/** P R I V A T E  P R O T O T Y P E S ***************************************/

void myMsDelay (unsigned int time);

/** V E C T O R  R E M A P P I N G *******************************************/


extern void _startup (void);  // See c018i.c 
#pragma code _RESET_INTERRUPT_VECTOR = 0x1000
void _reset (void)
{
    _asm goto _startup _endasm
}
#pragma code

#pragma code _HIGH_INTERRUPT_VECTOR = 0x1008
void _high_ISR (void)
{
    //_asm goto High_ISR _endasm
}

#pragma code _LOW_INTERRUPT_VECTOR = 0x1018
void _low_ISR (void)
{
   // _asm goto Low_ISR _endasm
}

#pragma code

/** D E C L A R A T I O N S **************************************************/

#pragma code

void main()
{ 
	TRISCbits.TRISC2 = 0 ;              // Set PORTC, 2 as output
    TRISCbits.TRISC6 = 0 ;
	TRISCbits.TRISC7 = 0 ;
	PR2 = 0x4A;                         // set PWM period to Maximum value 
    CCPR1L = 0x12;                      // Initalise PWM duty cycle to 00 
    CCP1CON = 0x3C;                     // Configure CCP1CON as explained above.
 	T2CON = 0x07;
	PORTCbits.RC6 = 1;
    PORTCbits.RC7 = 0;
  while(1)
	{
		PR2 = 0x00;
		myMsDelay(1000);
		PR2 = 0x3F;
		myMsDelay(1000);
		PR2 = 0xBF;
		myMsDelay(1000);
		PR2 = 0xFF;
		myMsDelay(1000);
 	}   
 
}


void myMsDelay (unsigned int time)
{
	unsigned int i, j;
	for (i = 0; i < time; i++)
		for (j = 0; j < 710; j++);/*Calibrated for a 1 ms delay in MPLAB*/
}
/********************************************************************/
//This program demonstrates the use of timer   		   //								                                                     */
/******************************************************************/


#include <p18f4550.h>
#include <stdlib.h>


/*The following lines of code perform interrupt vector relocation to work with the USB bootloader. These must be
used with every application program to run as a USB application.*/
void timer_isr(void);

extern void _startup (void);
#pragma code _RESET_INTERRUPT_VECTOR = 0x1000
void _reset (void)
{
	_asm goto _startup _endasm

}
#pragma code
//The program execution comes to this point when a timer interrupt is generated
#pragma code _HIGH_INTERRUPT_VECTOR = 0x1008
void high_ISR (void)
{
	
	_asm goto timer_isr _endasm    //The program is relocated to execute the interrupt routine timer_iser

}
//
#pragma code
//
#pragma code _LOW_INTERRUPT_VECTOR = 0x1018
 void low_ISR (void)
{

}
#pragma code
// This function is executed as soon as the timer interrupt is generated due to timer overflow
#pragma interrupt timer_isr
void timer_isr(void)
{
	TMR0H = 0XFF;                         // Reloading the timer values after overflow
	TMR0L = 0X00;
	PORTB = ~PORTB;                         //Toggle the PORTB led outputs RB0 - RB3
 	INTCONbits.TMR0IF = 0;	             //Resetting the timer overflow interrupt flag

}





void main()
{	
	ADCON1 = 0x0F;        //Configuring the PORTE pins as digital I/O 
	
	TRISB = 0;                  //Configruing the LED port pins as outputs
	PORTB = 0xFF;                //Setting the initial value of the LED's after reset	
	T0CON = 0x00;				//Set the timer to 16-bit mode,internal instruction cycle clock,1:256 prescaler
  	TMR0H = 0xFF;                // Reset Timer0 to 0x48E5 TO MAKE DELAY OF 1 SECOND
  	TMR0L = 0x00;
   	INTCONbits.TMR0IF = 0;      // Clear Timer0 overflow flag
	INTCONbits.TMR0IE = 1;		// TMR0 interrupt enabled
 	T0CONbits.TMR0ON = 1;		// Start timer0
	INTCONbits.GIE = 1;			// Global interrupt enabled

	while(1);                      //Program execution stays here untill the timer overflow interrupt is generated
	
}
/********************************************************************/
//This program demonstrates the use of timer   		   //								                                                     */
/******************************************************************/


#include <p18f4550.h>
#include <stdlib.h>


/*The following lines of code perform interrupt vector relocation to work with the USB bootloader. These must be
used with every application program to run as a USB application.*/
void timer_isr(void);

extern void _startup (void);
#pragma code _RESET_INTERRUPT_VECTOR = 0x1000
void _reset (void)
{
	_asm goto _startup _endasm

}
#pragma code
//The program execution comes to this point when a timer interrupt is generated
#pragma code _HIGH_INTERRUPT_VECTOR = 0x1008
void high_ISR (void)
{
	
	_asm goto timer_isr _endasm    //The program is relocated to execute the interrupt routine timer_iser

}
//
#pragma code
//
#pragma code _LOW_INTERRUPT_VECTOR = 0x1018
 void low_ISR (void)
{

}
#pragma code
// This function is executed as soon as the timer interrupt is generated due to timer overflow
#pragma interrupt timer_isr
void timer_isr(void)
{
	TMR0H = 0XFF;                         // Reloading the timer values after overflow
	TMR0L = 0X00;
	PORTB = ~PORTB;                         //Toggle the PORTB led outputs RB0 - RB3
 	INTCONbits.TMR0IF = 0;	             //Resetting the timer overflow interrupt flag

}





void main()
{	
	ADCON1 = 0x0F;        //Configuring the PORTE pins as digital I/O 
	
	TRISB = 0;                  //Configruing the LED port pins as outputs
	PORTB = 0xFF;                //Setting the initial value of the LED's after reset	
	T0CON = 0x00;				//Set the timer to 16-bit mode,internal instruction cycle clock,1:256 prescaler
  	TMR0H = 0xFF;                // Reset Timer0 to 0x48E5 TO MAKE DELAY OF 1 SECOND
  	TMR0L = 0x00;
   	INTCONbits.TMR0IF = 0;      // Clear Timer0 overflow flag
	INTCONbits.TMR0IE = 1;		// TMR0 interrupt enabled
 	T0CONbits.TMR0ON = 1;		// Start timer0
	INTCONbits.GIE = 1;			// Global interrupt enabled

	while(1);                      //Program execution stays here untill the timer overflow interrupt is generated
	
}
