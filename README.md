![Mobile Arcade](assets/MobileArcade.jpg){:height="480px"}



### Table of Contents
* [Concept](#concept)
* [System Design](#system-design)
  * [Physical Enclosure](#physical-enclosure)
  * [Arcade Emulator](#arcade-emulator)
  * [Mbed](#mbed)
    * [Drive System](#drive-system)
    * [Lighting](#lighting)
  * [Power](#power)
* [Instructions](#instructions)
* [Results](#results)



## Concept

> "Develop a mobile arcade cabinet that can be controlled over Bluetooth to enable ultimate portability and usability, while maintaining retro charm."

The Mobile Arcade was designed to incorporate a retro gaming experience with a quirky mobile chassis. The original idea was centered around a table top arcade experience with additional entertainment features, including vibrant and responsive lighting. In order to better suit and entertain the target audience (children aged 9 through 14), mobility was incorporated as well. With this in mind, the following design requirements were set:
1. Fully functional, single player, arcade system (ability to play NES and Atari games)
2. Visually pleasing enclosure with a retro feel
3. Interactive lighting
4. Basic Bluetooth-controlled mobility



## System Design

The design of the mobile arcade was divided into distinct subsystems: the physical enclosure, the arcade emulator, and the low-level drive system and lighting control. Each of these systems are outlined here.

![Block Diagram](assets/BlockDiagram.png)

* Raspberry Pi: Main processor
  * Handles arcade game emulator and UI
  * Interfaces with joystick and buttons
* Mbed LPC1768: Secondary processor
  * Handles lighting (LED strips)
  * Handles drive system (remotely commanded via the Bluetooth bridge)
* Dual-channel Motor Driver: Controls 2 motors in a tank-drive configuration
* Power: Li-Po battery and 5V regulator supply power to all components



### Physical Enclosure

The enclosure was designed using Dassault Systems’ Solid Works. Each portion of the seven component design was fitted together in software to ensure accurate dimensioning. The enclosure was then fabricated using 3/32" clear acrylic sheets, laser-cut at the Invention Studio.

![CAD design](assets/ArcadeCAD.png)

The overall shape of the enclosure resembles that of a standard arcade cabinet, with a few notable exceptions. The design is much simpler than standard cabinets, reducing the number of distinct components that need to be fabricated. Additionally, the cabinet incorporates mounting holes near the front specifically designed to accommodate geared drive motors. Along with the rear-mounted skid, this produces a "tank drive" configuration which allows the enclosure to maneuver deftly around its environment.



![Before cabinet assembly](assets/ArcadeCabinetPaint.jpg){:height="480px"}



![Trial fit](assets/TrialFit.jpg){:height="355px"}
![Interior view](assets/InteriorView.jpg){:height="355px"}



### Arcade Emulator

**TODO** Raspberry Pi stuff



### Mbed

In order to neatly connect the Mbed to the Bluetooth bridge, motor driver, and the LED strips, a single-layer PCB was designed in Eagle and fabricated at the Mechanical Engineering electronics lab. 90º headers were used so that the connections occupied minimal space.

The Eagle files for the PCB can be found [here](https://github.com/1961C/Mobile-Arcade/tree/master/eagle).

All code for the Mbed can be found [here](https://os.mbed.com/users/abraha2d/code/MobileArcade/).



![Mbed PCB design](assets/MbedPCBLayout.png){:height="480px"}



#### Drive System

The drive system consists of two motors in a tank-drive configuration, with a rear skid for stability. Wheels were added to both sides of the motors (2 visible outside, 2 hidden inside). Not only does this improve stability and ensure traction, it also adds a level of redundancy to the drive system.

A custom Mbed library was used to control the motor driver. The basic library (located [here](https://os.mbed.com/users/simon/code/Motor/)) was extended to add a short brake feature. The extended motor driver library can be found [here](https://os.mbed.com/users/abraha2d/code/Motor/).



![Wheel setup](assets/ArcadeWheels.jpg){:height="480px"}



#### Lighting

[Dotstar LED strips](https://www.adafruit.com/product/2239) were used to implement the interactive lighting features of the Mobile Arcade. These were chosen over NeoPixels due to the standard SPI interface and relaxed timing requirements of the integrated APA102 chip, allowing for relatively easy interface with the Mbed. Since no official library was available for interfacing with the APA102, a simple library was created that fulfilled our needs.

[Custom APA102 Mbed library](https://os.mbed.com/users/abraha2d/code/APA102/)

Code was written to accept input from the Raspberry Pi over USB serial to synchronize lighting effects to certain events in the arcade emulator. For example, on emulation startup, a startup animation is shown on the LEDs. Other effects include a similar shutdown animation, as well as lighting theme changes when games are started/stopped.


### Power

The Mobile Arcade is powered using a wiring harness connected to a large lithium-ion battery pack. A 5V 3A regulator, connected the harness, is used to provide power for the Raspberry Pi, Mbed LPC1768, motors, and LED strips. The LCD is able to plug directly into the harness without further regulation. Fuses are integrated into the harness to protect sensitive components.



![Wiring harness](assets/WireHarness.jpg){:height="480px"}



## Instructions

### Hardware setup

* Wiring harness
  * **TODO** Details
* Mbed PCB wiring
  * Connect 5V regulator output to power input
  * Connect DotStar LED strips to LED strip outputs
  * Connect motor leads to motor outputs
  * Insert Mbed, Bluetooth bridge, and motor driver in appropriate slots
  * Connect Mbed to Raspberry Pi with a USB cable
* Raspberry Pi Arcade Bonnet wiring
  * **TODO** Details

### Mbed setup

* Upload Mbed code (located [here](https://os.mbed.com/users/abraha2d/code/MobileArcade/))

### Raspberry Pi setup

* Follow RetroPie setup (located [here]())
  * **TODO** Add any specific notes
* Replace config files
  * **TODO** Which config files?



## Results

[Demo](https://youtu.be/UGc3tqysLSs)
