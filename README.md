
<a id="readme-top"></a>
[![LinkedIn][linkedin-shield]][linkedin-url]

<br />
<div align="center">
  <a href="https://github.com/Ayush-iitbhu24/Embedded_System_Task">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">ELECTRONICS SPECIALIZATION TASK</h3>

  <p align="center">
    In this project, I used an STM32 microcontroller—specifically the Blue Pill (STM32F103C6T6)—as the main processing unit. The system captures the states of four push-buttons and transmits this data as a single byte over UART at a rate of 50 Hz (every 200 ms). The transmitted byte is then used to control the states of four corresponding LEDs. Additionally, a virtual terminal is connected to monitor the UART data in real time, allowing for easy debugging and verification of communication.
    <br />
    <a href="https://github.com/Ayush-iitbhu24/Embedded_System_Task"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/Ayush-iitbhu24/Embedded_System_Task">View Demo</a>
  </p>
</div>


<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#working">Working</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)
This project provided a valuable opportunity to enhance my skills in working with various peripherals of the STM32 microcontroller. It significantly expanded my understanding of microcontroller programming and interfacing. I gained hands-on experience with STM32CubeIDE for developing applications on STM32 devices, as well as simulating circuits using Proteus. Through the project, I learned to handle external interrupts, transmit data using UART, and utilize the STM32 HAL (Hardware Abstraction Layer) library effectively. Additionally, I deepened my knowledge of low-level programming by controlling hardware registers through bit manipulation.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Built With

* [![Proteus][Proteus]][Proteus-url]
* [![STM32CubeIDE][CubeIDE]][CubeIDE-url]


<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

To successfully work on this project, you need to have STM32CubeIDE and Proteus installed on your PC. Additionally, the Blue Pill library for Proteus must be installed manually, as it is not included by default. A basic understanding of Proteus simulation is essential for effectively following the project. Familiarity with the STM32 HAL (Hardware Abstraction Layer) library is also required—particularly for implementing core functionalities such as UART communication, handling external interrupts, and working with timers.

### Prerequisites
To get started with this project, ensure you have the following:

* STM32CubeIDE and Proteus installed on your PC.

* Blue Pill library for Proteus (must be installed manually, as it is not included by default).

* Basic knowledge of Proteus for simulating microcontroller circuits.

* Familiarity with the STM32 HAL (Hardware Abstraction Layer) library for:

  * UART communication

  * Handling external interrupts

  * Using timers
 
  



### Installation

1. Download Proteus at  [Labcenter.com](https://www.labcenter.com/)
 
2. Download STM32Cube IDE from [www.st.com](https://www.st.com/en/development-tools/stm32cubeide.html)
   
3. For installing, refer to this video tutorial [BluePill](https://www.theelectronics.co.in/2021/03/stm32-bluepill-library-simulation-proteus.html)


<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Working
The PINS that have been used, and their description are - 
* PIN A1, A2, A3, and A4 are used for taking interrupts from PUSH-BUTTONS.
* PIN B3, B4, B5, and B6 are used to control LEDs.
* PIN A9 is used for transmitting data to the virtual terminal.
* +3.3V and GND are used to connect the +3.3V terminal and the ground terminal.
These are the pin configurations.


- STM32CubeIDE
  
  * First, the Blue Pill (F103C6T6A) was selected as the MCU for the project. Then, GPIO pins were configured, and PIN A1-A4 were set to be responsive on the falling edge.
    Then, the global interrupts were activated in the NVIC settings.
    PIN B3-B6 were set as GPIO_OUTPUT.
    Then, USART1 was activated, and the mode was set to 'Asynchronous'.
    These were the settings done in the CubeMX part.

    In the main.c file
    - A function was created to return byte data as output when input is given as 4-bit data.
    - Another function was created to convert the earlier byte data into a string, so that it can be printed on the virtual terminal.
    - A function was created to take in the byte data as input and turn on the respective LEDs using the respective bits.
    - Finally, a callback function was created to respond to the external interrupts by changing the bit state.
 
  
      The variables used in the program are -
      - bits (uint8_t) - 4-sized array to store the bit state.
      - data (uint8_t) - 10-sized array to store the message to be displayed on the virtual terminal.
      - bitmask (uint8_t) - An 8-bit mask to read the state of bits in the byte data.
      - byte (uint8_t) - The main byte data that is controlling everything.
      - LED (uint8_t) - A 4-sized array to store the address of the PIN used for controlling LEDs.
 
  
     The function used in this program -
     - void LEDcontrol(uint8_t); - To control LEDs.
     - uint8_t bytePacker(); - To create byte using bits data.
     - void byteToString(uint8_t); - To convert byte data into string data.



- Proteus
   * Blue Pill was used as the MCU. The power terminals were connected in their designated position. Then, PINs A1-A4 were connected to four PUSH-BUTTONS.
     And then, PINs B3-B6 were connected to LEDs, and PIN A9 was connected to RXD of the virtual terminal.
  
Workflow
  * The main workflow of this program is- when any external interrupt is given using PUSH-buttons it changes the 'bits' array.
    And inside the while loop, the bits data is sent to 'bytePacker' to convert the bits data to a byte, and then the byte is sent to
    'byteToString', now the string is displayed on the virtual terminal, the data is transmitted via UART every 200 ms (50Hz), HAL_Delay()
    is used to give a delay a 200 ms between every transmission. This byte is sent to LEDcontrol(), which uses a mask to extract every bit
    and uses it to change the LED's state.
  



<p align="right">(<a href="#readme-top">back to top</a>)</p>


## Contact

Ayush Soni - ayushsoni6745@gmail.com

Project Link: [https://github.com/Ayush-iitbhu24/Embedded_System_Task](https://github.com/Ayush-iitbhu24/Embedded_System_Task)

<p align="right">(<a href="#readme-top">back to top</a>)</p>




[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/ayush-soni-0a2a46312/
[product-screenshot]: images/screenshot.png
[Proteus]: https://img.shields.io/badge/Proteus-.pdsprj-blue?logo=proteus&logoColor=white
[Proteus-url]: https://www.labcenter.com/
[CubeIDE]: https://img.shields.io/badge/STM32CubeIDE-.c%2F.h-red?logo=stmicroelectronics&logoColor=white
[CubeIDE-url]: https://www.st.com/en/development-tools/stm32cubeide.html
