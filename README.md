Please refer to the following link for more information
https://github.com/microchip-pic-avr-examples/pic24fj64gu205-curiosity-nano-usb-clc-adc

Use the cable wire to connect to the debug side, then an user interface will show that Curiosity Nano is found. 

File - New Project - Microchip Embedded - application projects
Device - PIC24FJ64GU205 - Tool: PIC24FJ64GU205 Curiosity Nano-SN (If the cable successfully connected)
Compiler Toolchains - XC-DSC (v3.00)
Enter a project name and choose MCC (it stands for MPLAB Code Configurator, graphical programming environment integrated within the MPLAB X IDE, designed to simplify and accelerate the development process for Microchip's PIC microcontrollers and dsPIC digital signal controllers.)
Click on Pin Manager window and click finish to download all necessary tools

Right Click on the source file and select property to check if the environment settings are right
If no, go to tools - options - embedded - build tools - scan for build tools
    XC8: is for 8-bit PIC microcontrollers.
    XC16: is for 16-bit PIC microcontrollers and dsPIC Digital Signal Controllers (DSCs).
    XC32: is for 32-bit PIC32 microcontrollers
    XC-DSC: is for Digital Signal Controllers (DSCs) from Microchip, such as the dsPIC series
    
PIC24FJ64GU205 is a 16-bit microcontroller!!! Choose XC16 if you are programmed in C++
If not installed yet, please browse to official website to download XC16
https://www.microchip.com/en-us/search?searchQuery=xc16&category=ALL&fq=start%3D0%26rows%3D10
Then get back to the build tools interface and click on scan for build tools

The `initADC()` function in the code is used to initialize the Analog-to-Digital Converter (ADC) of the PIC microcontroller. It prepares the microcontroller to read analog signals from its pins and convert those signals into digital values that the microcontroller can process.

Right click the tool bar and select to show the build production

Here's a breakdown of what each part of the `initADC()` function is doing:

1. **Set Analog Pin Mode:**
   ```c
   ANSELBbits.ANSB2 = 1;
   ```
   This line sets pin RB2 to analog mode. ANSEL registers control whether pins are in digital or analog mode. When a bit is set, the corresponding pin is switched to analog mode.

2. **Set Pin as Input:**
   ```c
   TRISBbits.TRISB2 = 1;
   ```
   This line configures the data direction of pin RB2 as an input. TRIS registers control the direction of I/O pins. Setting a bit in a TRIS register configures the corresponding pin as an input.

3. **Configure ADC Precision:**
   ```c
   ADCON1bits.AD12B = 0;
   ```
   This line sets the ADC to 10-bit mode (versus 12-bit mode), which affects the resolution of the conversion.

4. **Select Voltage References:**
   ```c
   ADCON2 = 0;
   ```
   This line configures the voltage reference for the ADC conversions. Setting it to `0` typically means that the default voltage references (AVdd and AVss) will be used.

5. **Set ADC Conversion Clock:**
   ```c
   ADCON3 = 0x1F3F;
   ```
   This sets up the ADC conversion clock and the sample time. The sample time is how long the ADC module will "look" at the analog voltage before doing the conversion.

6. **Select ADC Input Channel:**
   ```c
   ADCHSbits.CH0SA = 4;
   ```
   This line selects the analog channel that the ADC will read. It's setting channel 0 to sample from AN4, which is presumed to be connected to the gyro's analog output.

7. **Turn On ADC:**
   ```c
   ADCON1bits.ADON = 1;
   ```
   This line actually turns on the ADC module, making it operational.

When `initADC()` is called, it runs through these steps to ensure that the ADC is correctly set up to read analog voltages from the specified pins. After running this function, the PIC's ADC is ready to convert analog signals into digital values using the `readADC()` function, which starts the conversion process, waits for it to complete, and then reads the result.
