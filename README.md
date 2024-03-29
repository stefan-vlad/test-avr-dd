<!-- Please do not change this html logo with link -->

<a href="https://www.microchip.com" rel="nofollow"><img src="images/microchip.png" alt="MCHP" width="300"/></a>

# Analog to Digital Convertor (ADC) in five different modes using AVR64DD32 Microcontroller

<br>The repository contains five MPLAB® X projects:

- [1. Event Triggered](#1-event-triggered) This code example shows how to configure the ADC to trigger a conversion on a specific event.
- [2. Free Running](#2-free-running) This code example runs the ADC in Free-Running mode, the next conversion starts automatically after the previous one is completed.
- [3. Sample Accumulator](#3-sample-accumulator) This code example uses the sample accumulation to obtain better results that are not affected by noise.
- [4. Single Conversion](#4-single-conversion) This code example demonstrates how to make a single conversion with the ADC.
- [5. Window Comparator](#5-window-comparator) This code example uses the ADC in Window Comparator mode, where the device can detect if the ADC result is below or above a specific threshold value.

## Related Documentation

More details and code examples on the AVR64DD32 can be found at the following links:

- [AVR64DD32 Product Page](https://www.microchip.com/wwwproducts/en/AVR64DD32)
- [AVR64DD32 Code Examples on GitHub](https://github.com/microchip-pic-avr-examples?q=AVR64DD32)
- [AVR64DD32 Project Examples in START](https://start.atmel.com/#examples/AVR64DD32CuriosityNano)

## Software Used

- [MPLAB® X IDE](http://www.microchip.com/mplab/mplab-x-ide) v6.00 or newer
- [MPLAB® XC8](http://www.microchip.com/mplab/compilers) v2.36 or newer
- [AVR-Dx Series Device Pack](https://packs.download.microchip.com/) v2.0.152 or newer

## Hardware Used

- The AVR64DD32 Curiosity Nano Development Board is used as test platform.
  <br><img src="images/AVR64DD32.PNG" width="500">

## Operation

To program the Curiosity Nano board with this MPLAB® X project, follow the steps provided in the [How to Program Curiosity Nano board](#how-to-program-curiosity-nano-board) chapter.<br><br>

## 1. Event Triggered

The purpose of this project is to provide an example on how to configure the ADC to trigger a conversion on a specific event. The RTC overflow is used in this example to trigger the ADC conversion and the on-board LED will be toggled each time the conversion is triggered.

### 1.1 Setup

The following configurations must be made for this project:

- System clock is configured at 4 MHz
- ADC:
  - 10-bit mode
  - Voltage Reference: internal
  - Clock Source: peripheral clock / 4
  - RESRDY enabled
  - Event Trigger enabled
- RTC:
  - 500 ms overflow
  - Oscillator: 32.768 kHz with a prescaler of 32
- PF2 pin: configured as input; disable the digital input buffer and the pull-up resistor. Pin PF2 will be used as ADC input channel.
- PF5 pin: configured as output with initial value HIGH. This pin will be used by LED and the initial value high represents LED OFF.
- Event Generator: RTC overflow
- Event User: ADC Start Conversion

  | Pin | Configuration  |
  | :-: | :------------: |
  | PF5 | Digital output |
  | PF2 |  Analog input  |

### 1.2 Summary

This project shows how to configure the ADC peripheral to execute conversions every time a certain event happens. In this specific example, the RTC overflow (at 500 ms) is used as event generator. Every time a conversion cycle is triggered, the on-board LED is toggled to signal the end of a conversion.<br><br>
[Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)<br>

## 2. Free Running

This example uses ADC in Free-Running mode. When configuring the ADC in Free-Running mode, the next conversion starts automatically after the previous one is completed. The ADC input pin needs to have the digital input buffer and the pull-up resistor disabled to have the highest possible input impedance.

### 2.1 Setup

The following configurations must be made for this project:

- System clock is configured at 4 MHz
- PF2 pin: configured as input; disable the digital input buffer and the pull-up resistor. Pin PF2 will be used as ADC input channel.
- ADC:

  - Configured in Free-Running mode
  - 10-bit mode
  - Voltage Reference: internal
  - Clock Source: peripheral clock / 4

  | Pin | Configuration |
  | :-: | :-----------: |
  | PF2 | Analog input  |

### 2.2 Summary

This project shows how to configure the ADC peripheral in Free-Running mode where a new conversion starts automatically after the previous one is completed.<br><br>
[Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)<br>

## 3. Sample Accumulator

This example demonstrates how to use the sample accumulation function of the ADC to obtain better results that are not affected by noise. The example accumulates 64 samples. The conversion result is represented by the accumulated value divided by 64.

### 3.1 Setup

The following configurations must be made for this project:

- System clock is configured at 4 MHz
- ADC:
  - 10-bit mode
  - Voltage Reference: internal
  - Clock Source: peripheral clock / 4
  - Sample Accumulator: 64 samples
- PF2 pin: configured as input; input buffer disabled and pull-up resistor disabled

  |     Pin     | Configuration |
  | :---------: | :-----------: |
  | PF2 (AIN18) | Analog input  |

### 3.2 Summary

This project shows how to use the ADC in the Sample Accumulator mode to reduce the noise influence on the result.<br><br>
[Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)<br>

## 4. Single Conversion

This code example demonstrates how to make a single conversion with the ADC.
The ADC input pin needs to have the digital input buffer and the pull-up resistor disabled to have the highest possible input impedance. Pin PF2 (AIN18) is used for ADC input in this example.

### 4.1 Setup

The following configurations must be made for this project:

- System clock is configured at 4 MHz
- ADC:
  - 10-bit mode
  - Voltage Reference: internal
  - Clock Source: peripheral clock / 4
- PF2 pin: configured as input; input buffer disabled and pull-up resistor disabled

  | Pin | Configuration |
  | :-: | :-----------: |
  | PF2 | Analog input  |

### 4.2 Summary

This project shows how to configure the ADC peripheral to execute a single conversion cycle.<br><br>
[Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)<br>

## 5. Window Comparator

This example uses the ADC in Window Comparator mode, where the device can detect if the ADC result is below or above a specific threshold value. This is useful when monitoring a signal that is required to be maintained in a specific range or for signaling low battery/overcharge, etc. The Window Comparator is used in Free-Running mode because a monitored signal requires continuous sampling and the Free-Running mode reduces the CPU load by not requiring manual start for each conversion.

### 5.1 Setup

The following configurations must be made for this project:

- System clock is configured at 4 MHz
- ADC:
  - 10-bit mode
  - Voltage Reference: internal
  - Clock Source: peripheral clock / 4
  - Window Mode and Free-Running
  - Conversion Window Comparator Low Threshold: set to `0x200` which is defined as `WINDOW_CMP_LOW_TH_EXAMPLE`
- PF2 pin: configured as input; input buffer disabled and pull-up resistor disabled
- PF5 pin: configured as output with initial value HIGH (this corresponds to the on-board LED being turned OFF)

  | Pin | Configuration  |
  | :-: | :------------: |
  | PF2 |  Analog input  |
  | PF5 | Digital output |

### 5.2 Summary

This project shows how to configure the ADC peripheral in Window Comparator mode. In this mode, the microcontroller detects if the ADC result is below or above a specific threshold value.<br><br>
[Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)<br>

## How to Program Curiosity Nano board

This chapter shows how to use the MPLAB® X IDE to program an AVR® device with an Example_Project.X. This can be applied for any other projects.

- Connect the board to the PC.

- Open the Example_Project.X project in MPLAB X IDE.

- Set the Example_Project.X project as main project.

  - Right click on the project in the **Projects** tab and click **Set as Main Project**.
    <br><img src="images/Program_Set_as_Main_Project.PNG" width="600">

- Clean and build the Example_Project.X project.

  - Right click on the **Example_Project.X** project and select **Clean and Build**.
    <br><img src="images/Program_Clean_and_Build.PNG" width="600">

- Select the **AVRxxxxx Curiosity Nano** in the Connected Hardware Tool section of the project settings:

  - Right click on the project and click **Properties**
  - Click on the arrow under the Connected Hardware Tool
  - Select the **AVRxxxxx Curiosity Nano** (click on the **SN**), click **Apply** and then click **OK**:
    <br><img src="images/Program_Tool_Selection.PNG" width="600">

- Program the project to the board.
  - Right click on the project and click **Make and Program Device**.
    <br><img src="images/Program_Make_and_Program_Device.PNG" width="600">

<br>

- [Back to 1. Event Triggered](#1-event-triggered)
- [Back to 2. Free Running](#2-free-running)
- [Back to 3. Sample Accumulator](#3-sample-accumulator)
- [Back to 4. Single Conversion](#4-single-conversion)
- [Back to 5. Window Comparator](#5-window-comparator)
- [Back to top](#analog-to-digital-convertor-adc-in-five-different-modes-using-avr64dd32-microcontroller)
